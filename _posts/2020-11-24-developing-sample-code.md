---
title: Developing Sample Code
description: 15
---

<p><strong>1. Locate following line to create the Wise Player Factory instance in WisePlayerInit Object.</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    //TODO Initializing of Wise Player Factory
<span class="pln">
</span></code></pre>
<p><strong>2. Create the Wise Player Factory instance</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    val factoryOptions = WisePlayerFactoryOptions.Builder().setDeviceId("xxx").build()
    // In the multi-process scenario, the onCreate method in Application is called multiple times.
    // The app needs to call the WisePlayerFactory.initFactory() API in the onCreate method of the app process (named "app package name") 
    // and WisePlayer process (named "app package name:player").
    WisePlayerFactory.initFactory(context, factoryOptions, object : InitFactoryCallback {
        override fun onSuccess(factory: WisePlayerFactory) {
            wisePlayerFactory = factory
        }
        override fun onFailure(errorCode: Int, msg: String) {
            Log.d("WisePlayerInit", "onFailure: $errorCode - $msg")
        }
    })
<span class="pln">
</span></code></pre>
<p>Description of <strong>Wise Player Factory</strong> is as following:<br></p>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
	<tr><td colspan="1" rowspan="1"><p>Parameter</p>
	</td><td colspan="1" rowspan="1"><p>Type:</p>
	</td><td colspan="1" rowspan="1"><p>Mandatory or Not</p>
	</td><td colspan="1" rowspan="1"><p>Description</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>context</p>
	</td><td colspan="1" rowspan="1"><p>Context</p>
	</td><td colspan="1" rowspan="1"><p>M</p>
	</td><td colspan="1" rowspan="1"><p>Android context object, which is not set to null.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>options</p>
	</td><td colspan="1" rowspan="1"><p>Integer</p>
	</td><td colspan="1" rowspan="1"><p>M</p>
	</td><td colspan="1" rowspan="1"><p>Instance of the WisePlayer factory class initialization option <a href="https://developer.huawei.com/consumer/en/doc/HMSCore-References-V5/wpf-options-0000001050439397-V5" target="_blank">WisePlayerFactoryOptions</a></p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>callback</p>
	</td><td colspan="1" rowspan="1"><p>Object</p>
	</td><td colspan="1" rowspan="1"><p>M</p>
	</td><td colspan="1" rowspan="1"><p>Instance of the <a href="https://developer.huawei.com/consumer/en/doc/HMSCore-References-V5/init-factory-callback-0000001050199187-V5" target="_blank">InitFactoryCallback API</a> for initializing the WisePlayer factory class.</p>
	</td></tr>
</tbody></table>
<p><strong>3. Locate following line and set the EditTexts Urls in MainActivity to play related buttons</strong></p>
<pre><div id="copy-button12" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>   // TODO Set video Url or Urls
<span class="pln">
</span></code></pre>
<p><strong>4.Set the EditTexts Urls </strong></p>
<pre><div id="copy-button13" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code> edtUrl.setText(resources.getString(R.string.single_url))
 edtMultipleUrl.setText(resources.getString(R.string.multiple_url))
 <span class="pln">
</span></code></pre>
<p><strong>5. Locate following line and create Wise Player Instance in WisePlayerInit Object. </strong></p>
<pre><div id="copy-button14" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  // TODO Initializing of Wise Player Instance
<span class="pln">
</span></code></pre>
<p><strong>6. Create Wise Player Instance</strong></p>
<pre><div id="copy-button15" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  return wisePlayerFactory.createWisePlayer()
<span class="pln">
</span></code></pre>
<aside class="special">
	<p><strong>Note: Frame Layout is necessary for SurfaceView to display videos, otherwise only audio will be listened</strong></p>
</aside>
<br><img style="width: 400.00px" src="https://raw.githubusercontent.com/bekiryavuzkoc/testRepo/gh-pages/assets/framelayout.PNG" onclick="imageclick(src)">
<p><strong>7. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button17" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Setting the Listeners
<span class="pln">
</span></code></pre>
<p><strong>8. Set listeners in Play Activity.</strong></p>
<pre><div id="copy-button18" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setReadyListener(this)
  player.setErrorListener(this)
  player.setEventListener(this)
  player.setResolutionUpdatedListener(this)
  player.setLoadingListener(this)
  player.setPlayEndListener(this)
  player.setSeekEndListener(this)
  <span class="pln">
</span></code></pre>
<p><strong>9. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button19" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code> //TODO Callback Listener
<span class="pln">
</span></code></pre>
<p><strong>10. Set the Callback Listener in Play Activity.</strong></p>
<pre><div id="copy-button20" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  surfaceView.holder.addCallback(this)
<span class="pln">
</span></code></pre>
<p><strong>10. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button21" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code> //TODO Callback Listener
<span class="pln">
</span></code></pre>
<p><strong>11. Set the Seekbar Listener in Play Activity.</strong></p>
<pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  seekBar.setOnSeekBarChangeListener(this)
<span class="pln">
</span></code></pre>
<p><strong>12. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Starting the Player
	<span class="pln">
</span></code></pre>
<p><strong>13. Start Wise Player in Play Activity.</strong></p>
<pre><div id="copy-button24" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player?.start()
<span class="pln">
</span></code></pre>
<p><strong>14. Locate following line in Play Activity. </strong></p>
<pre><div id="copy-button25" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Change
<span class="pln">
</span></code></pre>
<p><strong>15. Set surface change to Wise Player.</strong></p>
<pre><div id="copy-button26" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setSurfaceChange()
<span class="pln">
</span></code></pre>
<p><strong>16. Locate following line in Play Activity. </strong></p>
<pre><div id="copy-button27" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Destroy
<span class="pln">
</span></code></pre>
<p><strong>17. Suspend the Wise Player if surface is destroyed.</strong></p>
<pre><div id="copy-button28" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.suspend()
<span class="pln">
</span></code></pre>
<p><strong>18. Locate following line in Play Activity. </strong></p>
<pre><div id="copy-button29" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Create
<span class="pln">
</span></code></pre>
<p><strong>19. Resume Wise Player with the current time when app is sent to foreground.</strong></p>
<pre><div id="copy-button30" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setView(surfaceView)
  player.resume(PlayerConstants.ResumeType.KEEP)
<span class="pln">
</span></code></pre>
<p><strong>20. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button31" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Release Wise Player
<span class="pln">
</span></code></pre>
<p><strong>21. Resume Wise Player with the current time when app is sent to foreground.</strong></p>
<pre><div id="copy-button32" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setErrorListener(null)
  player.setEventListener(null)
  player.setResolutionUpdatedListener(null)
  player.setReadyListener(null)
  player.setLoadingListener(null)
  player.setPlayEndListener(null)
  player.setSeekEndListener(null)
  player.release()
<span class="pln">
</span></code></pre>

<h2><strong>Test and Verification</strong></h2>
<p>Upon completing the essential parts of the code, connect your mobile device to the PC and enable the USB debugging mode. In the Android Studio window, click   <img style="width: 19.00px" src="https://raw.githubusercontent.com/bekiryavuzkoc/testRepo/gh-pages/assets/run_image.png" onclick="imageclick(src)">    icon to run the project you have created in Android Studio to generate an APK. Then install the APK on the mobile device.</p>

<ol type="1">
	<li>Open the app upon installing it to your device</li>
	<li>Fill the Edittext and enter an Url, click the “Play” Button.</li>
	<li>Wait for video to be displayed.</li>
</ol>
<img style="width: 220.00px" src="https://raw.githubusercontent.com/bekiryavuzkoc/testRepo/gh-pages/assets/playvideoswithvideokitone.PNG" onclick="imageclick(src)">             <img style="width: 217.00px" src="https://raw.githubusercontent.com/bekiryavuzkoc/testRepo/gh-pages/assets/playvideoswithvideokittwo.PNG" onclick="imageclick(src)">

<h2><strong>Advanced Information</strong></h2>
<ol type="1">
  <li><h3>Seekbar:</h3></li>
  <p>With the feature of Seekbar, displayed video can be rewound or forwarded.</p>
  
<p><strong>1. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button33" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Seekbar Change
<span class="pln">
</span></code></pre>
<p><strong>2. Implement the Wise Player’s seek method.</strong></p>
<pre><div id="copy-button34" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  seekBar?.progress?.let {player.seek(it)}
<span class="pln">
</span></code></pre>

 <li><h3>Handler and Runnable:</h3></li>
<p>A Handler allows you to send and process Message and Runnable objects associated with a thread's MessageQueue. With the feature of Handler, we can update the UI elements for every 1 seconds.</p>
<p><strong>1. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button35" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Handler and Runnable Implementation
<span class="pln">
</span></code></pre>
<p><strong>2. Implement the Wise Player’s seek method.</strong></p>
<pre><div id="copy-button36" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>        //Player UI
        configureControlView()
        //Text UI Elements 
        configureContentView()
        if (!mStopHandler) {
            mHandler.postDelayed(runnable, DELAY_SECOND)
        }
        <span class="pln">
</span></code></pre>
</ol>
