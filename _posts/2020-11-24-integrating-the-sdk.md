---
title: Integrating the SDK
description: 5
---

<p>You can download the codelab project from: <a href="https://github.com/huaweicodelabs/VideoKit/tree/master/PlayVideosWithVideoKit" target="_blank">https://github.com/huaweicodelabs/VideoKit/tree/master/PlayVideosWithVideoKit</a></p>

<h2><strong>Creating a Project</strong></h2>
<p><strong>Step 1</strong>: Start Android Studio.</p>
<p><strong>Step 2</strong>: Choose <strong>File</strong> &gt; <strong>Open</strong>, go to the directory where the sample project is decompressed, and click <strong>OK</strong>.<br><img style="width: 376.00px" src="https://raw.githubusercontent.com/bekiryavuzkoc/testRepo/gh-pages/assets/videokitcodelab.png" onclick="imageclick(src)"></p>
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
			classpath </span><span class="str">'com.huawei.agconnect:agcp:1.4.1.300'</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
	</li>
</ul>
<p><strong>2. Configure the dependency package in the app's build.gradle file.</strong></p>
<ul>
	<li>Add a dependency package to the <strong>dependencies</strong> section in the <strong>build.gradle</strong> file.<pre><div id="copy-button4" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">dependencies </span><span class="pun">{</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
		implementation </span><span class="str">'com.huawei.hms:image-vision:1.0.3.301'</span><span class="pln">
		implementation </span><span class="str">'com.huawei.hms:image-vision-fallback:1.0.3.301'</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
	</li>
	<li>Configure <strong>minSdkVersion</strong>.<pre><div id="copy-button5" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">android </span><span class="pun">{</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
		defaultConfig </span><span class="pun">{</span><span class="pln">
			</span><span class="pun">...</span><span class="pln">
			minSdkVersion </span><span class="lit">26</span><span class="pln">
			</span><span class="pun">...</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span></code></pre>
	</li>
	<li>Add the following information under <strong>apply plugin: 'com.android.application'</strong> in the file header:<pre><div id="copy-button6" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">apply plugin</span><span class="pun">:</span><span class="pln"> </span><span class="str">'com.huawei.agconnect'</span><span class="pln">
	</span></code></pre>
	</li>
</ul>
<p><strong>3. Configure obfuscation scripts.</strong></p>
<ul>
	<li>Configure the following information in the <strong>app/proguard-rules.pro</strong> file:<pre><div id="copy-button7" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pun">-</span><span class="pln">ignorewarnings
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
	<li>If you are using AndResGuard, add it to the allowlist in the obfuscation script file.<pre><div id="copy-button8" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="str">"R.string.hms*"</span><span class="pun">,</span><span class="pln">
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
</span></code></pre>
<p><strong>Step 4</strong>: In the Android Studio window, choose <strong>File</strong> &gt; <strong>Sync Project with Gradle Files</strong> to synchronize the project.</p>
<p><strong>Step 5</strong>: Complete the essentials in the code; locate and open the MainActivity.kt</p>
<p><strong>1. Locate following line to create ImageVision instance</strong></p>
<pre><div id="copy-button10" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	// TODO: Create an ImageVision Instance<span class="pln">
</span></code></pre>
<p><strong>2. Create the ImageVision instance</strong></p>
<pre><div id="copy-button11" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	imageVisionAPI = ImageVision.getInstance(baseContext)<span class="pln">
</span></code></pre>
<p><strong>3. Locate following line to initialize the ImageVision service</strong></p>
<pre><div id="copy-button12" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	// TODO Initialize the ImageVision service.<span class="pln">
</span></code></pre>
<p><strong>4. Initialize the ImageVision service. Return code 0 means initialization succeeded </strong></p>
<pre><div id="copy-button13" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	imageVisionAPI.setVisionCallBack(object : VisionCallBack {
		override fun onSuccess(successCode: Int) {
			val initCode = imageVisionAPI.init(baseContext, authJson)
			// initCode must be 0 if the initialization is successful.
			if (initCode == 0)
				Log.d(TAG, "getImageVisionAPI rendered image successfully")
		}

		override fun onFailure(errorCode: Int) {
			Log.e(TAG, "getImageVisionAPI failure, errorCode = $errorCode")
			Toast.makeText(this@MainActivity, "initFailed", Toast.LENGTH_SHORT).show()
		}
	})
	<span class="pln">
</span></code></pre>
<p>Description of <strong>authJson</strong> parameters:<br></p>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
	<tr><td colspan="1" rowspan="1"><p>Parameter</p>
	</td><td colspan="1" rowspan="1"><p>Type:</p>
	</td><td colspan="1" rowspan="1"><p>Mandatory or Not</p>
	</td><td colspan="1" rowspan="1"><p>Description</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>projectId</p>
	</td><td colspan="1" rowspan="1"><p>String</p>
	</td><td colspan="1" rowspan="1"><p>Yes</p>
	</td><td colspan="1" rowspan="1"><p>Project ID you obtained when registering with HUAWEI Developers.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>appId</p>
	</td><td colspan="1" rowspan="1"><p>String</p>
	</td><td colspan="1" rowspan="1"><p>Yes</p>
	</td><td colspan="1" rowspan="1"><p>Project ID you obtained during registration.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>authApiKey</p>
	</td><td colspan="1" rowspan="1"><p>String</p>
	</td><td colspan="1" rowspan="1"><p>Yes</p>
	</td><td colspan="1" rowspan="1"><p>API key used for authentication, which is provided by HUAWEI Developers.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>clientSecret</p>
	</td><td colspan="1" rowspan="1"><p>String</p>
	</td><td colspan="1" rowspan="1"><p>Yes</p>
	</td><td colspan="1" rowspan="1"><p>Client secret used for authentication.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>clientId</p>
	</td><td colspan="1" rowspan="1"><p>String</p>
	</td><td colspan="1" rowspan="1"><p>Yes</p>
	</td><td colspan="1" rowspan="1"><p>Client ID.</p>
	</td></tr>
	<tr><td colspan="1" rowspan="1"><p>token</p>
	</td><td colspan="1" rowspan="1"><p>String</p>
	</td><td colspan="1" rowspan="1"><p>No</p>
	</td><td colspan="1" rowspan="1"><p>Session token, which is used to verify an app. It is recommended that the app server obtain the session token from the AppGallery using clientId and ClientSecret.</p>
	</td></tr>
</tbody></table>
<aside class="special">
	<p><strong>Note:</strong> You can find the preceding parameters in the agconnect-services.json file. For details, please refer to the  <a href="https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/config-agc-0000001050199019" target="_blank">Development Guide</a>.</p>
</aside>
<aside class="special">
	<p>For security purposes, the authentication information used in the sample code is fake. You need to enter the actual authentication information during app development.</p>
</aside>
<p><strong>5. Locate following line to load filters. Filters are initialized in MainViewModel </strong></p>
<pre><div id="copy-button14" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	// TODO get filters from ViewModel<span class="pln">
</span></code></pre>
<p><strong>6. Get the filters </strong></p>
<pre><div id="copy-button15" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	viewModel.getAllFilterItems(null)
<span class="pln">
</span></code></pre>
<p><strong>7. Locate following line to prepare the image filtering request. </strong></p>
<pre><div id="copy-button16" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	// TODO prepare request parameters for applying filters <span class="pln">
</span></code></pre>

<p><strong>8. Construct required JSON objects.  </strong></p>
<pre><div id="copy-button17" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	taskJson.put(
		"intensity",
		intensity
	) //Filter strength. Generally, set this parameter to 1.
	taskJson.put("filterType", filterType) // 24 different filterType code
	taskJson.put("compressRate", compress) // Compression ratio.
	jsonObject.put("requestId", "1")
	jsonObject.put("taskJson", taskJson)
	jsonObject.put(
		"authJson",
		authJson
	) // App can use the service only after it is successfully authenticated.

	<span class="pln">
</span></code></pre>

<p><strong>8. Locate following line to start applying filters and getting result.  </strong></p>
<pre><div id="copy-button18" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	// TODO Start applying filters to images and retrieve results then send to UI<span class="pln">
</span></code></pre>

<p><strong>9. Start applying filters and fetch result </strong></p>
<pre><div id="copy-button19" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	coroutineScope.launch {
		var deferred: Deferred<ImageVisionResult?> = async(Dispatchers.IO) {
			imageVisionAPI?.getColorFilter(jsonObject, bitmapFromGallery)
		}
		visionResult = deferred.await() // wait till obtain ImageVisionResult object
		val image = visionResult?.image
		if (image == null)
			Log.e(
				TAG,
				"FilterException: Couldn't render the image. Check the restrictions while rendering an image by Image Vision Service"
			)

		channel.send(image)
		// Sending image bitmap with an async channel to make it receive with another channel
	}
<span class="pln">
</span></code></pre>
<p>Description of <strong>requestJson</strong> and <strong>imageBitmap</strong>parameters is as following;<br></p>

<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
		<tr><td colspan="1" rowspan="1"><p>Parameter</p>
		</td><td colspan="1" rowspan="1"><p>Type</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory or Not</p>
		</td><td colspan="1" rowspan="1"><p>Description</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>requestJson</p>
		</td><td colspan="1" rowspan="1"><p>JSONObject</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory</p>
		</td><td colspan="1" rowspan="1"><p>JSON string containing image processing request parameters.</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>imageBitmap</p>
		</td><td colspan="1" rowspan="1"><p>Bitmap</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory</p>
		</td><td colspan="1" rowspan="1"><p>Image to be processed. The aspect ratio is between 1:3 and 3:1, and the width and height pixels are less than or equal to 8000.</p>
		</td></tr>
	</tbody>
</table>

<p>Description of <strong>requestJson</strong> parameters;<br></p>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
		<tr><td colspan="1" rowspan="1"><p>Parameter</p>
		</td><td colspan="1" rowspan="1"><p>Type</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory or Not</p>
		</td><td colspan="1" rowspan="1"><p>Description</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>requestId</p>
		</td><td colspan="1" rowspan="1"><p>String</p>
		</td><td colspan="1" rowspan="1"><p>Optional</p>
		</td><td colspan="1" rowspan="1"><p>Request ID provided by the Image Vision service.</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>taskJson</p>
		</td><td colspan="1" rowspan="1"><p>JSONObject</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory</p>
		</td><td colspan="1" rowspan="1"><p>JSON string containing detailed service request information.</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>authJson</p>
		</td><td colspan="1" rowspan="1"><p>JSONObject</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory</p>
		</td><td colspan="1" rowspan="1"><p>JSON string containing authentication parameters.</p>
		</td></tr>
	</tbody>
</table>

<p>Description of <strong>responseJson</strong> parameters:</p>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
		<tr><td colspan="1" rowspan="1"><p>Parameter</p>
		</td><td colspan="1" rowspan="1"><p>Type</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory or Not</p>
		</td><td colspan="1" rowspan="1"><p>Description</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>index</p>
		</td><td colspan="1" rowspan="1"><p>int</p>
		</td><td colspan="1" rowspan="1"><p>Optional</p>
		</td><td colspan="1" rowspan="1"><p>Image index for color mapping. The value ranges from 0 to 24. Value 0 indicates the original image.</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>intensity</p>
		</td><td colspan="1" rowspan="1"><p>float</p>
		</td><td colspan="1" rowspan="1"><p>Optional</p>
		</td><td colspan="1" rowspan="1"><p>Filter strength. Generally, set this parameter to 1.</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>compressRate</p>
		</td><td colspan="1" rowspan="1"><p>float</p>
		</td><td colspan="1" rowspan="1"><p>Optional</p>
		</td><td colspan="1" rowspan="1"><p>Compression rate. Compression is not performed by default. The value range is (0-1].</p>
		</td></tr>
	</tbody>
</table>
<p>List of available filters and <strong>filterType</strong> mapping:</p>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
		<tr><td colspan="1" rowspan="1"><p>1</p>
		</td><td colspan="1" rowspan="1"><p>2</p>
		</td><td colspan="1" rowspan="1"><p>3</p>
		</td><td colspan="1" rowspan="1"><p>4</p>
		</td><td colspan="1" rowspan="1"><p>5</p>
		</td><td colspan="1" rowspan="1"><p>6</p>
		</td><td colspan="1" rowspan="1"><p>7</p>
		</td><td colspan="1" rowspan="1"><p>8</p>
		</td><td colspan="1" rowspan="1"><p>9</p>
		</td><td colspan="1" rowspan="1"><p>10</p>
		</td><td colspan="1" rowspan="1"><p>11</p>
		</td><td colspan="1" rowspan="1"><p>12</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>Black-and-white</p>
		</td><td colspan="1" rowspan="1"><p>Brown tone</p>
		</td><td colspan="1" rowspan="1"><p>Lazy</p>
		</td><td colspan="1" rowspan="1"><p>Freesia</p>
		</td><td colspan="1" rowspan="1"><p>Fuji</p>
		</td><td colspan="1" rowspan="1"><p>Peach pink</p>
		</td><td colspan="1" rowspan="1"><p>Sea salt</p>
		</td><td colspan="1" rowspan="1"><p>Mint</p>
		</td><td colspan="1" rowspan="1"><p>Reed</p>
		</td><td colspan="1" rowspan="1"><p>Vintage</p>
		</td><td colspan="1" rowspan="1"><p>Marshmallow</p>
		</td><td colspan="1" rowspan="1"><p>Moss</p>
		</td></tr>
	</tbody>
</table>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
		<tr><td colspan="1" rowspan="1"><p>13</p>
		</td><td colspan="1" rowspan="1"><p>14</p>
		</td><td colspan="1" rowspan="1"><p>15</p>
		</td><td colspan="1" rowspan="1"><p>16</p>
		</td><td colspan="1" rowspan="1"><p>17</p>
		</td><td colspan="1" rowspan="1"><p>18</p>
		</td><td colspan="1" rowspan="1"><p>19</p>
		</td><td colspan="1" rowspan="1"><p>20</p>
		</td><td colspan="1" rowspan="1"><p>21</p>
		</td><td colspan="1" rowspan="1"><p>22</p>
		</td><td colspan="1" rowspan="1"><p>23</p>
		</td><td colspan="1" rowspan="1"><p>24</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>Sunlight</p>
		</td><td colspan="1" rowspan="1"><p>Time</p>
		</td><td colspan="1" rowspan="1"><p>Haze blue</p>
		</td><td colspan="1" rowspan="1"><p>Sunflower</p>
		</td><td colspan="1" rowspan="1"><p>Hard</p>
		</td><td colspan="1" rowspan="1"><p>Bronze yellow</p>
		</td><td colspan="1" rowspan="1"><p>Monochromic tone</p>
		</td><td colspan="1" rowspan="1"><p>Yellow-green tone</p>
		</td><td colspan="1" rowspan="1"><p>Yellow tone</p>
		</td><td colspan="1" rowspan="1"><p>Green tone</p>
		</td><td colspan="1" rowspan="1"><p>Cyan tone</p>
		</td><td colspan="1" rowspan="1"><p>Violet tone</p>
		</td></tr>
	</tbody>
</table>
<p>Description of  <strong>visionResult</strong> parameters is as following:</p>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
		<tr><td colspan="1" rowspan="1"><p>Parameter</p>
		</td><td colspan="1" rowspan="1"><p>Type</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory or Not</p>
		</td><td colspan="1" rowspan="1"><p>Description</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>resultCode</p>
		</td><td colspan="1" rowspan="1"><p>int</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory</p>
		</td><td colspan="1" rowspan="1"><p>Result code.</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>responseJson</p>
		</td><td colspan="1" rowspan="1"><p>JsonObject</p>
		</td><td colspan="1" rowspan="1"><p>Optional</p>
		</td><td colspan="1" rowspan="1"><p>JSON string containing the returned result.</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>compressRate</p>
		</td><td colspan="1" rowspan="1"><p>Bitmap</p>
		</td><td colspan="1" rowspan="1"><p>Optional</p>
		</td><td colspan="1" rowspan="1"><p>Processed image. For an API that directly returns images, this parameter is used by the API to transfer the processed image.</p>
		</td></tr>
	</tbody>
</table>

<p>Description of  <strong>responseJson</strong> parameters is as following:</p>
<table style="width: 100%;table-layout: fixed;">
	<tbody><tr></tr>
		<tr><td colspan="1" rowspan="1"><p>Parameter</p>
		</td><td colspan="1" rowspan="1"><p>Type</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory or Not</p>
		</td><td colspan="1" rowspan="1"><p>Description</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>requestId</p>
		</td><td colspan="1" rowspan="1"><p>String</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory</p>
		</td><td colspan="1" rowspan="1"><p>Request ID provided by the Image Vision service. This parameter is available only if it is carried in the service request.</p>
		</td></tr>
		<tr><td colspan="1" rowspan="1"><p>serviceId</p>
		</td><td colspan="1" rowspan="1"><p>String</p>
		</td><td colspan="1" rowspan="1"><p>Mandatory</p>
		</td><td colspan="1" rowspan="1"><p>ID of the service being called.</p>
		</td></tr>
	</tbody>
</table>

<p><strong>9. Locate following line to safely stop the ImageVision service.  </strong></p>
<pre><div id="copy-button20" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	// TODO Stop ImageVision service<span class="pln">
</span></code></pre>

<p><strong>10. Stop ImageService</strong></p>
<pre><div id="copy-button21" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	if (imageVisionAPI != null)
		imageVisionAPI.stop()
	<span class="pln">
</span></code></pre>

<h2><strong>Test and Verification</strong></h2>
<p>Upon completing the essential parts of the code, connect your mobile device to the PC and enable the USB debugging mode. In the Android Studio window, click   <img style="width: 19.00px" src="/assets/run_image.png" onclick="imageclick(src)">    icon to run the project you have created in Android Studio to generate an APK. Then install the APK on the mobile device.</p>

<ol type="1">
	<li>Open the app upon installing it to your device</li>
	<li>Use the <img style="width: 19.00px" src="/assets/gallery_icon.jpg" onclick="imageclick(src)"> icon to access to your gallery and pick an image. Grant necessary permissions in case system asks for it</li>
	<li>Wait for filter and preview initialization</li>
	<li>Apply a filter to the image</li>
</ol>
<img style="width: 220.00px" src="/assets/Hms_image_kit1.jpg" onclick="imageclick(src)">
<img style="width: 220.00px" src="/assets/hms_image_kit2.jpg" onclick="imageclick(src)">
<img style="width: 220.00px" src="/assets/hms_image_kit3.jpg" onclick="imageclick(src)">

<h2><strong>Advanced Information</strong></h2>
<ol type="1">
	<li>If the image cannot be displayed during the test, you are advised to turn off hardware acceleration.</li>
	<p>To turn off hardware acceleration, configure the AndroidManifest.xml file as follows:</p>

	<li>Add a dependency package to the <strong>dependencies</strong> section in the <strong>build.gradle</strong> file.<pre><div id="copy-button22" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code><span class="pln">&lt;application </span><span class="pun"></span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
		android: </span><span class="str">hardwareAccelerated</span><span class="pln">
		</span><span class="pun">...</span><span class="pln">
	</span><span class="pun">&lt;/application&gt;</span><span class="pln">
	</span></code></pre>
	</li>


	<li>At this codelab asynchronous operations are applied with with Kotlin coroutines to protect battery life and prevent memory leak by making a performance-oriented image filtering application.</li>
	<p>In this scenario of codelab, a user selects an image from the Gallery. Call Init filter method and then start filtering images one by one which are located in recyclerView. (24 different items included in recyclerview to show all the filter types.)</p>
	<p>All the sub-images were filtered by different filter types. </p>
	<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	  private fun startFilterForSubImages() {
		subBitmapList.clear()
		viewModel.getAllFilterItems(null)
		recylerFilter.scrollToPosition(0)
		channelIsFetching = true
		coroutineScope.launch {
			if (filterList.isNotEmpty()) {
				initFilter() // initialize the vision service
				for (x in 1..filterList.size) {
					startFilter(x.toString(), "1", "1") // start filtering
					var bitmap = channel.receive()
					subBitmapList.put(x, bitmap)
					viewModel.getAllFilterItems(subBitmapList)
				}
				stopFilter() // stop the vision service
				channelIsFetching = false
			}
		}
	  }
	<span class="pln">
	</span></code></pre>

	<pre><div id="copy-button24" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	  private fun startFilter(filterType: String, intensity: String, compress: String) {

		if (initCode == 0) {
			coroutineScope.launch { // CoroutineScope is used for the async     calls
				val jsonObject = JSONObject()

	<span class="pln">
	</span></code></pre>

	<pre><div id="copy-button25" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	  val taskJson = JSONObject()
				try {
					taskJson.put("intensity", intensity) //Filter strength. Generally, set this parameter to 1.
					taskJson.put("filterType", filterType) // 24 different filterType code
					taskJson.put("compressRate", compress) // Compression ratio.
					jsonObject.put("requestId", "1") // Optinal
					jsonObject.put("taskJson", taskJson)
					jsonObject.put("authJson", authJson) // App can use the service only after it is successfully authenticated.

					coroutineScope.launch {

						visionResult = withContext(Dispatchers.IO) {
							imageVisionAPI?.getColorFilter(
								jsonObject,
								bitmapFromGallery
							)
						}
						// Obtain the rendering result from visionResult

						val image = visionResult?.image
						if (image == null)
							Log.e(TAG, "FilterException: Couldn't render the image. Check the restrictions while rendering an image by Image Vision Service")

						channel.send(image)
						// Sending image bitmap with an async channel to make it receive with another channel
					}

				} catch (e: JSONException) {
					Log.e(TAG, "JSONException: " + e.message)
				}
			}
		}
		else {
			Toast.makeText(this@MainActivity, "initFailed", Toast.LENGTH_SHORT).show()
		}
	 }
	</code></pre>

	<p>When user clicks a filter to render the selected image, getColorFilter is invoked and the ImageVision service returns the filtered bitmap. Then it is necessary to implement onSelected method of the activity, which gets the FilterItem object of the clicked item from the adapter.</p>
	<p>startFilter method is used for the image previews and the selected image.</p>

	<pre><div id="copy-button26" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	  // Initialize and start a filter operation when a filter item is selected
	  override fun onSelected(item: BaseInterface) {

		if (!channelIsFetching)
	</code></pre>

	<pre><div id="copy-button27" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>
	   {
		if (bitmapFromGallery == null)
		Toast.makeText(baseContext, getString(R.string.select_photo_from_gallery), Toast.LENGTH_SHORT).show()
		else
		{
			var filterItem = item as FilterItem
			coroutineScope.launch {
			initFilter() // initialize the vision service
			startFilter(filterItem.filterId, "1", "1") // intensity and compress are 1
			   var receivedBitmap = withContext(Dispatchers.IO){channel.receive()} // receive the filtered bitmap result from another channel
			   imgView.setImageBitmap(receivedBitmap)
			   stopFilter() // stop the vision service
			}
		}
	  }
		else
			Toast.makeText(baseContext, getString(R.string.wait_to_complete_filtering), Toast.LENGTH_SHORT).show()
	 }
	</code></pre>

</ol>
