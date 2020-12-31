---
title: Integrating the Location Barrier capabilities
description: 15
---

<p><strong>1. First, define the location and the radius to be notified of when a user enters that area.</strong></p>
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
                    Toast.makeText(context, "add barrier " + label + " failed",
                            Toast.LENGTH_SHORT).show();
                    Log.e(TAG, "add barrier failed", e);
                });
    }
</code>
</pre>

Remember to remove a barrier if it already exists and add it again
<pre>
<code>
Awareness.getBarrierClient(this).queryBarriers(BarrierQueryRequest.all())
                .addOnSuccessListener(barrierQueryResponse -> {
                    AwarenessBarrier enterBarrier = LocationBarrier.enter(
                            latitude, longitude, radius);
                    AwarenessBarrier exitBarrier = LocationBarrier.exit(
                            latitude, longitude, radius);

                    if (barrierQueryResponse.getBarrierStatusMap().getBarrierLabels()
                            .contains(ENTER_BARRIER_LABEL)) {
                        removeBarrier(ENTER_BARRIER_LABEL, res -> {
                            if (res) {
                                addBarrier(this, ENTER_BARRIER_LABEL, enterBarrier,
                                        mPendingIntent);
                            }
                        });
                    } else {
                        addBarrier(this, ENTER_BARRIER_LABEL, enterBarrier,
                                mPendingIntent);
                    }

                    if (barrierQueryResponse.getBarrierStatusMap().getBarrierLabels()
                            .contains(EXIT_BARRIER_LABEL)) {
                        removeBarrier(EXIT_BARRIER_LABEL, res -> {
                            if (res) {
                                addBarrier(this, EXIT_BARRIER_LABEL, exitBarrier,
                                        mPendingIntent);
                            }
                        });
                    } else {
                        addBarrier(this, EXIT_BARRIER_LABEL, exitBarrier,
                                mPendingIntent);
                    }
                }).addOnFailureListener(e -> Log.e(TAG, e.getMessage(), e));
</code>
</pre>

Remember that you need to create the barrier only if your app has the neccessary permissions so check the permissions before creating a location barrier.

<pre>
<code>
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.Q) {
            requestPermissions(new String[]{Manifest.permission.ACCESS_FINE_LOCATION,
                            Manifest.permission.ACCESS_BACKGROUND_LOCATION},
                    PERMISSION_REQUEST_CODE);
        } else {
            requestPermissions(new String[]{Manifest.permission.ACCESS_FINE_LOCATION},
                    PERMISSION_REQUEST_CODE);
        }
</code>
</pre>

<pre>
<code>
    @Override
    public void onRequestPermissionsResult(
            int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == PERMISSION_REQUEST_CODE) {
            boolean isPermissionGranted = true;
            for (int result : grantResults) {
                if (result == PackageManager.PERMISSION_DENIED) {
                    isPermissionGranted = false;
                }
            }

            if (!isPermissionGranted) {
                Toast.makeText(this, "Permission(s) denied! " +
                                "You must give necessary permissions for this demo app to run properly.",
                        Toast.LENGTH_LONG).show();
            } else {
                Toast.makeText(this, "Permission(s) granted! ", Toast.LENGTH_SHORT).show();
            }
        }
    }
</code>
</pre>

<p><strong>4. If a user enters the specified area, we will be notified via LocationBarrierReceiver class. </strong></p>
<p>Here when the enter event of Awareness Kit triggers, we start a timer and on exit event trigger, we stop the timer and calculate the length of stay. Then we send this data to Analytics Kit and CloudDB to analyze the data later. </p>
<pre>
<code>
final class LocationBarrierReceiver extends BroadcastReceiver {
        private final String TAG = LocationBarrierReceiver.class.getSimpleName();

        @Override
        public void onReceive(Context context, Intent intent) {
            BarrierStatus barrierStatus = BarrierStatus.extract(intent);
            String label = barrierStatus.getBarrierLabel();
            switch (barrierStatus.getPresentStatus()) {
                case BarrierStatus.TRUE:
                    Log.i(TAG, "[" + label + "]" + " BarrierStatus: TRUE");
                    printLog("[" + label + "]" + " BarrierStatus: TRUE");
                    if (label.equals("ENTER_BARRIER_LABEL")) {
                        mChronometer.setBase(SystemClock.elapsedRealtime());
                        mChronometer.start();
                    } else if (label.equals("EXIT_BARRIER_LABEL")) {
                        mChronometer.stop();
                        double elapsedMillis = SystemClock.elapsedRealtime() -
                                mChronometer.getBase();
                        printLog("Length of stay: " + elapsedMillis / 1000 + " seconds");
                        Log.e(TAG, "Length of stay: " + elapsedMillis);

                        // Send lengthOfStay via a custom event to Analytics
                        Bundle bundle = new Bundle();
                        bundle.putDouble("length_of_stay", elapsedMillis / 1000);
                        mHiAnalytics.onEvent("LENGTH_OF_STAY", bundle);

                        // Send lengthOfStay to CloudDB
                        User user = new User();
                        user.setId(UUID.randomUUID().toString());
                        user.setUserId(userId);
                        user.setLengthOfStay(elapsedMillis / 1000);
                        mCloudDBHelper.upsertUser(user, res -> {
                            if (res) {
                                mCloudDBHelper.queryAverage(avgResult -> {
                                    printLog("Average length of stay: " + avgResult);
                                });
                            }
                        });
                    }
                    break;
                case BarrierStatus.FALSE:
                    Log.i(TAG, "[" + label + "]" + " BarrierStatus: FALSE");
                    printLog("[" + label + "]" + " BarrierStatus: FALSE");
                    break;
                case BarrierStatus.UNKNOWN:
                    Log.i(TAG, "[" + label + "]" + " BarrierStatus: UNKNOWN");
                    printLog("[" + label + "]" + " BarrierStatus: UNKNOWN");
                    break;
            }
        }
    }
</code>
</pre>

