---
title: Integrating the SDK
description: 5
---

<p>You can download the codelab project from: <a href="https://github.com/huaweicodelabs/VideoKit/tree/master/PlayVideosWithVideoKit" target="_blank">https://github.com/huaweicodelabs/VideoKit/tree/master/PlayVideosWithVideoKit</a></p>

<h2><strong>Creating a Project</strong></h2>
<p><strong>Step 1</strong>: Start Android Studio.</p>
<p><strong>Step 2</strong>: Choose <strong>File</strong> &gt; <strong>Open</strong>, go to the directory where the sample project is decompressed, and click <strong>OK</strong>.<br><img style="width: 376.00px" src="https://raw.githubusercontent.com/bekiryavuzkoc/testRepo/gh-pages/assets/videokitcodelab.PNG" onclick="imageclick(src)"></p>
<p><strong>Step 3</strong>: Configure the AppGallery Connect plug-in, Maven repository address, build dependencies, obfuscation scripts, and permissions. (These items have been configured in the sample code. If any of them does not meet your requirements, change it in your own project.)</p>
<p><strong>1. Configure the Maven repository address and AppGallery Connect plug-in in the project's build.gradle file.</strong></p>
<ul>
	<li>Go to <strong>allprojects</strong> &gt; <strong>repositories</strong> and configure the Maven repository address for the HMS Core SDK.<pre><div id="copy-button1" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">allprojects </span><span class="pun">{</span><span class="pln">
		repositories </span><span class="pun">{</span><span class="pln">
			maven </span><span class="pun">{</span><span class="pln"> url </span><span class="str">'https://developer.huawei.com/repo/'</span><span class="pln"> </span><span class="pun">}</span><span class="pln">
			</span><span class="pun">...</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
	</li>
	<li>Go to <strong>buildscript</strong> &gt; <strong>repositories</strong> and configure the Maven repository address for the HMS Core SDK.<pre><div id="copy-button2" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">buildscript </span><span class="pun">{</span><span class="pln">
		repositories </span><span class="pun">{</span><span class="pln">
		   maven </span><span class="pun">{</span><span class="pln">url </span><span class="str">'https://developer.huawei.com/repo/'</span><span class="pun">}</span><span class="pln">
			</span><span class="pun">...</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
	</li>
	<li>Go to <strong>buildscript</strong> &gt; <strong>dependencies</strong> and add build dependencies.<pre><div id="copy-button3" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">buildscript </span><span class="pun">{</span><span class="pln">
		dependencies </span><span class="pun">{</span><span class="pln">
     </span><span class="str">                   //Replace {agconnect_version} with the actual AGC plugin version number.</span><span class="pln">
     </span><span class="str">                   //Example: classpath 'com.huawei.agconnect:agcp: 1.4.1.300'</span><span class="pln">
			classpath </span><span class="str">'com.huawei.agconnect:agcp:{agconnect_version}'</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
	</li>
</ul>
<p><strong>2. Configure the dependency package in the app's build.gradle file.</strong></p>
<ul>
	<li>Add a dependency package to the <strong>dependencies</strong> section in the <strong>build.gradle</strong> file.<pre><div id="copy-button4" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">dependencies </span><span class="pun">{</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
    </span><span class="str">            //Video Kit</span><span class="pln">
		implementation </span><span class="str">'com.huawei.hms:videokit-player:1.0.1.300'</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
  <p>For Video Kit, please refer to <a href="https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/version-change-history-0000001050199403" target="_blank">latest version</a>.</p>
	</li>
	<li>Add the following information under <strong>apply plugin: 'com.android.application'</strong> in the file header:<pre><div id="copy-button6" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">apply plugin</span><span class="pun">:</span><span class="pln"> </span><span class="str">'com.huawei.agconnect'</span><span class="pln">
	</span></code></pre>
	</li>
</ul>
<p><strong>3. Configure obfuscation scripts.</strong></p>
<ul>
	<li>Configure the following information in the <strong>app/proguard-rules.pro</strong> file:<pre><div id="copy-button7" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>           <span class="pun">-</span><span class="pln">ignorewarnings<span class="pln">
		</span><span class="pun">-</span><span class="pln">keepattributes </span><span class="pun">*</span><span class="typ">Annotation</span><span class="pun">*</span><span class="pln">
		</span><span class="pun">-</span><span class="pln">keepattributes </span><span class="typ">Exceptions</span><span class="pln">
		</span><span class="pun">-</span><span class="pln">keepattributes </span><span class="typ">InnerClasses</span><span class="pln">
		</span><span class="pun">-</span><span class="pln">keepattributes </span><span class="typ">Signature</span><span class="pln">
		</span><span class="pun">-</span><span class="pln">keepattributes </span><span class="typ">SourceFile</span><span class="pun">,</span><span class="typ">LineNumberTable</span><span class="pln">
		</span><span class="pun">-</span><span class="pln">keep </span><span class="kwd">class</span><span class="pln"> com</span><span class="pun">.</span><span class="pln">hianalytics</span><span class="pun">.</span><span class="pln">android</span><span class="pun">.**{*;}</span><span class="pln">
		</span><span class="pun">-</span><span class="pln">keep </span><span class="kwd">class</span><span class="pln"> com</span><span class="pun">.</span><span class="pln">huawei</span><span class="pun">.</span><span class="pln">updatesdk</span><span class="pun">.**{*;}</span><span class="pln">
		</span><span class="pun">-</span><span class="pln">keep </span><span class="kwd">class</span><span class="pln"> com</span><span class="pun">.</span><span class="pln">huawei</span><span class="pun">.</span><span class="pln">hms</span><span class="pun">.**{*;}</span><span class="pln">
		</span></code></pre>
	</li>
	<li>If you are using AndResGuard, add it to the allowlist in the obfuscation script file.<pre><div id="copy-button8" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>		       <span class="str">"R.string.hms*"<span class="pun">,</span><span class="pln">
		</span><span class="str">"R.string.connect_server_fail_prompt_toast"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.string.getting_message_fail_prompt_toast"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.string.no_available_network_prompt_toast"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.string.third_app_*"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.string.upsdk_*"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.layout.hms*"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.layout.upsdk_*"</span><span class="pun">,</span><span class="pln"> 
		</span><span class="str">"R.drawable.upsdk*"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.color.upsdk*"</span><span class="pun">,</span><span class="pln"> 
		</span><span class="str">"R.dimen.upsdk*"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.style.upsdk*"</span><span class="pun">,</span><span class="pln">
		</span><span class="str">"R.string.agc*"</span><span class="pln">
		</span></code></pre>
	</li>
</ul>
<p><strong>4. Configure permissions in the AndroidManifest.xml file.</strong></p>
<pre><div id="copy-button9" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.INTERNET"</span><span class="tag">/&gt;</span><span class="pln">
</span><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACCESS_NETWORK_STATE"</span><span class="tag">/&gt;</span><span class="pln">
</span><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"android.permission.ACCESS_WIFI_STATE"</span><span class="tag">/&gt;</span><span class="pln">
</span><span class="tag">&lt;uses-permission</span><span class="pln"> </span><span class="atn">android:name</span><span class="pun">=</span><span class="atv">"com.huawei.permission.SECURITY_DIAGNOSE"</span><span class="tag">/&gt;</span><span class="pln">
</span></code></pre>
<p><strong>Step 4</strong>: In the Android Studio window, choose <strong>File</strong> &gt; <strong>Sync Project with Gradle Files</strong> to synchronize the project.</p>
<p><strong>Step 5</strong>: Complete the essentials in the code; locate and open the MainActivity.kt</p>
<p><strong>1. Locate following line to create the Wise Player Factory instance in WisePlayerInit Object.</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>    //TODO Initializing of Wise Player Factory<span class="pln">
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
    })<span class="pln">
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
<pre><div id="copy-button12" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>   // TODO Set video Url or Urls<span class="pln">
</span></code></pre>
<p><strong>4.Set the EditTexts Urls </strong></p>
<pre><div id="copy-button13" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code> edtUrl.setText(resources.getString(R.string.single_url))
 edtMultipleUrl.setText(resources.getString(R.string.multiple_url))<span class="pln">
</span></code></pre>
<p><strong>5. Locate following line and create Wise Player Instance in WisePlayerInit Object. </strong></p>
<pre><div id="copy-button14" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  // TODO Initializing of Wise Player Instance<span class="pln">
</span></code></pre>
<p><strong>6. Create Wise Player Instance</strong></p>
<pre><div id="copy-button15" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  return wisePlayerFactory.createWisePlayer()<span class="pln">
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
<pre><div id="copy-button20" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  surfaceView.holder.addCallback(this)<span class="pln">
</span></code></pre>
<p><strong>11. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button21" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Starting the Player
	<span class="pln">
</span></code></pre>
<p><strong>12. Start Wise Player in Play Activity.</strong></p>
<pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  this.player.start()<span class="pln">
</span></code></pre>
<p><strong>13. Locate following line in Play Activity. </strong></p>
<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Change
	<span class="pln">
</span></code></pre>
<p><strong>14. Set surface change to Wise Player.</strong></p>
<pre><div id="copy-button24" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setSurfaceChange()<span class="pln">
</span></code></pre>
<p><strong>15. Locate following line in Play Activity. </strong></p>
<pre><div id="copy-button25" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Destroy
	<span class="pln">
</span></code></pre>
<p><strong>16. Suspend the Wise Player if surface is destroyed.</strong></p>
<pre><div id="copy-button26" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.suspend()<span class="pln">
</span></code></pre>
<p><strong>17. Locate following line in Play Activity. </strong></p>
<pre><div id="copy-button27" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Surface Create
	<span class="pln">
</span></code></pre>
<p><strong>18. Resume Wise Player with the current time when app is sent to foreground.</strong></p>
<pre><div id="copy-button28" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setView(surfaceView)
  player.resume(PlayerConstants.ResumeType.KEEP)<span class="pln">
</span></code></pre>
<p><strong>19. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button29" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Release Wise Player
<span class="pln">
</span></code></pre>
<p><strong>20. Resume Wise Player with the current time when app is sent to foreground.</strong></p>
<pre><div id="copy-button30" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  player.setErrorListener(null)
  player.setEventListener(null)
  player.setResolutionUpdatedListener(null)
  player.setReadyListener(null)
  player.setLoadingListener(null)
  player.setPlayEndListener(null)
  player.setSeekEndListener(null)
  player.release()<span class="pln">
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
<pre><div id="copy-button31" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Seekbar Change<span class="pln">
</span></code></pre>
<p><strong>2. Implement the Wise Player’s seek method.</strong></p>
<pre><div id="copy-button32" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  seekBar?.progress?.let {player.seek(it)}<span class="pln">
</span></code></pre>

 <li><h3>Handler and Runnable:</h3></li>
<p>A Handler allows you to send and process Message and Runnable objects associated with a thread's MessageQueue. With the feature of Handler, we can update the UI elements for every 1 seconds.</p>
<p><strong>1. Locate following line in Play Activity.</strong></p>
<pre><div id="copy-button33" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>  //TODO Handler and Runnable Implementation<span class="pln">
</span></code></pre>
<p><strong>2. Implement the Wise Player’s seek method.</strong></p>
<pre><div id="copy-button34" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>        //Player UI
        configureControlView()
        //Text UI Elements 
        configureContentView()
        if (!mStopHandler) {
            mHandler.postDelayed(runnable, DELAY_SECOND)
        }<span class="pln">
</span></code></pre>
</ol>
