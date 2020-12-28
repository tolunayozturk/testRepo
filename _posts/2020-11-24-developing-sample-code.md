---
title: Create Wiseplayer and Play Video
description: 15
---

<p><strong>1. First, define the location and the radius we want to be notified of when a user enters that area.</strong></p>
<pre>
<code>
// Example location
double latitude = 12.3456;
double longitude = 78.9012;
double radius = 305;
</code>
</pre>

Remember the radius should be at least 200 meters.

<p><strong>2. Define the PendingIntent that will be triggered upon a barrier status change, and register a broadcast receiver to receive the broadcast.</strong></p>
<pre>
<code>
final String barrierReceiverAction = getApplication().getPackageName() + "LOCATION_BARRIER_RECEIVER_ACTION";
Intent intent = new Intent(barrierReceiverAction);
mPendingIntent = PendingIntent.getBroadcast(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);

mBarrierReceiver = new LocationBarrierReceiver();
registerReceiver(mBarrierReceiver, new IntentFilter(barrierReceiverAction));
</code>
</pre>

<p><strong>3. Create and add the barrier </strong></p>
<pre>
<code>
private void addBarrier(Context context, final String label,
                            AwarenessBarrier barrier, PendingIntent pendingIntent) {
        BarrierUpdateRequest.Builder builder = new BarrierUpdateRequest.Builder();
        BarrierUpdateRequest request = builder.addBarrier(label, barrier, pendingIntent).build();
        Awareness.getBarrierClient(context).updateBarriers(request)
                .addOnSuccessListener(aVoid -> {
                    Toast.makeText(context, "add barrier " + label + " success",
                            Toast.LENGTH_SHORT).show();
                    Log.i(TAG, "add barrier success");
                })
                .addOnFailureListener(e -> {
                    Toast.makeText(context, "add barrier " + label + " success",
                            Toast.LENGTH_SHORT).show();
                    Log.e(TAG, "add barrier failed", e);
                });
    }
</code>
</pre>

<pre>
<code>
AwarenessBarrier enterBarrier = LocationBarrier.enter(latitude, longitude, radius);
addBarrier(this, ENTER_BARRIER_LABEL, enterBarrier, mPendingIntent);
</code>
</pre>

Remember that you need to create the barrier only if your app has the neccessary permissions so check the permissions before creating a location barrier.

<pre>
<code>
 @Override
    public void onRequestPermissionsResult(
            int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        if (requestCode == PERMISSION_REQUEST_CODE) {
            boolean isPermissionDenied = false;
            for (int result : grantResults) {
                if (result == PackageManager.PERMISSION_DENIED) {
                    isPermissionDenied = true;
                }
            }

            if (isPermissionDenied) {
                Toast.makeText(this, "PERMISSION DENIED", Toast.LENGTH_SHORT).show();
            } else {
                Toast.makeText(this, "PERMISSION GRANTED", Toast.LENGTH_LONG).show();

                @SuppressLint("MissingPermission") AwarenessBarrier enterBarrier = LocationBarrier.enter(latitude, longitude, radius);
                addBarrier(this, ENTER_BARRIER_LABEL, enterBarrier, mPendingIntent);

                @SuppressLint("MissingPermission") AwarenessBarrier exitBarrier = LocationBarrier.enter(latitude, longitude, radius);
                addBarrier(this, EXIT_BARRIER_LABEL, exitBarrier, mPendingIntent);
            }
        }
    }
</code>
</pre>

<p><strong>4. If a user enters the area we specified, we will be notified via LocationBarrierReceiver class. </strong></p>
<pre>
<code>
class LocationBarrierReceiver extends BroadcastReceiver {
        private final String TAG = LocationBarrierReceiver.class.getSimpleName();

        @Override
        public void onReceive(Context context, Intent intent) {
            BarrierStatus barrierStatus = BarrierStatus.extract(intent);
            String label = barrierStatus.getBarrierLabel();
            switch (barrierStatus.getPresentStatus()) {
                case BarrierStatus.TRUE:
                    Log.i(TAG, label + " status:true" + barrierStatus.getLastBarrierUpdateTime());
                    printLog(label + " status:true");

                    if (label.equals("ENTER_BARRIER_LABEL")) {
                        mChronometer.setBase(SystemClock.elapsedRealtime());
                        mChronometer.start();
                    } else if (label.equals("EXIT_BARRIER_LABEL")) {
                        mChronometer.stop();
                        double elapsedMillis = SystemClock.elapsedRealtime() - mChronometer.getBase();
                        printLog("Length of stay: " + elapsedMillis / 1000 + " seconds");
                    }
                    break;
                case BarrierStatus.FALSE:
                    Log.i(TAG, label + " status:false");
                    printLog(label + " status:false");
                    break;
                case BarrierStatus.UNKNOWN:
                    Log.i(TAG, label + " status:unknown");
                    printLog(label + " status:unknown");
                    break;
            }
        }
    }
</code>
</pre>
