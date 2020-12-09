## Table of Contents

 * [Introduction](#introduction)
 * [Installation](#installation)
 * [Configuration ](#configuration )
 * [Supported Environments](#supported-environments)
 * [Sample Code](#Sample-Code)
 * [License](#license)
 
 
## Introduction
    Videokit Codelab code encapsulates APIs of the HUAWEI Video Kit SDK. It provides many sample programs for your reference or usage.
    Before you use this codelab, it's assumed that you already have a HUAWEI developer account and have already created an app to implement the
HMS Video Kit. If you haven't, please refer to https://developer.huawei.com/consumer/en/doc/start/introduction-0000001053446472 and https://developer.huawei.com/consumer/en/doc/development/AppGallery-connect-Guides/agc-introduction.
    
    model:       The package name which refers to a video object.
    ui:          The package name which shows the interface of the app to the user.
    utils:       The Package which helps the video duration and current time values shown in the ui.

## Installation
    Before using Videokit Codelab code, check whether the Android Studio environment has been installed. 
    Download the Videokit Codelab project by zip or clone in Github.
    Wait for the gradle build in your project.
    
## Supported Environments
	•	Android Studio 3.x or later version
	•	Java JDK 1.8 or later version
	•	EMUI 3.0 or later version
	•	HMS Core (APK) 5.0.0.300 or later version

## Configuration 
    To use functions provided by packages in examples, you need to set related parameters in Video Kit Codelab in the WisePlayerInit Object.
    
    deviceId: Unique device ID, which is set by an app. The WisePlayer SDK is used to request content authentication and report O&M data. The app can ensure that the device ID does not involve user privacy information by generating a UUID or using methods such as SHA-based digest or obfuscation.
	
## Sample Code
    Videokit Codelab code uses the Client structure in the project.The following describes methods in the Client structure.

    1). Initiliaze WisePlayerFactory instance.
    You can obtain the initialized WisePlayerFactory instance using the initialize method in the WisePlayerInit object.
    Code location src/main/java/com.dtse.videokitcodelab/WisePlayerInit.kt
    
    2). Create WisePlayer instance
    You can obtain the initialized Wise Player instance using the createPlayer method in the WisePlayerInit object.
    Code location  src/main/java/com.dtse.videokitcodelab/WisePlayerInit.kt
    
    3). Playing Single Video Url
    You can play a video by specfying a video Url.
    Code location src/main/java/com.dtse.videokitcodelab/ui/main/MainActivity.kt
    
    4). Playing Multiple Video Urls
    You can play a video by specfying multiple video Urls.
    Code location src/main/java/com.dtse.videokitcodelab/ui/main/MainActivity.kt
    
    5). Using FrameLayout in the UI
    Videos can only be displayed if the FrameLayout is created in the xml.
    Code location src/main/res/layout/activity_player.xml
    
    6). Using Only Audio Mode
    Only audio can only be listened by the Wise Player's play mode settings.
    Code location src/main/java/com.dtse.videokitcodelab/ui/player/PlayerActivity.kt
    
    7). Video Rewinding and Forwarding Options
    Displaying videos can be rewound or forwarded with the Wise Player's seek feature.
    Code location src/main/java/com.dtse.videokitcodelab/ui/player/PlayerActivity.kt

##  License
    Videokit Codelab is licensed under the [Apache License, version 2.0](http://www.apache.org/licenses/LICENSE-2.0).
