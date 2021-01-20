## Table of Contents

 * [Introduction](#introduction)
 * [Installation](#installation)
 * [Configuration ](#configuration )
 * [Supported Environments](#supported-environments)
 * [Sample Code](#Sample-Code)
 * [License](#license)
 
 
## Introduction
HMS Awareness Kit Codelab use the enter and exit events of Awareness Kit to measure length of stay of our users in a specific location and send that data to Analytics Kit and CloudDB. Then use this data to get the average time of our users' stay in that area via queryAverage capability of CloudDB. Before you use this codelab, it's assumed that you already have a HUAWEI developer account and have already created an app to implement the HMS Awareness Kit. If you haven't, please refer to https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/service-introduction-0000001050031140 and https://developer.huawei.com/consumer/en/doc/development/AppGallery-connect-Guides/agc-introduction.

## Installation
Before using HMS Awareness Kit Codelab code, check whether the Android Studio environment has been installed. 
Download the HMS Awareness Kit Codelab project by zip or clone in Github.
Wait for the gradle build in your project.
    
## Supported Environments
	•	Android Studio 3.x or later version
	•	Java JDK 1.8 or later version
	•	HMS Core (APK) 4.0.2.300 or later

## Configuration 
1. Register and sign in to HUAWEI Developers.
2. Create a project and then create an app in the project, enter the project package name.
3. Go to Project Settings > General information, click Set next to Data storage location under Project information, and select a data storage location in the displayed dialog box.
4. Download the agconnect-services.json file and place it to the app's root directory of the project.
5. Add the Maven repository address maven {url 'https://developer.huawei.com/repo/'} and plug-in class path 'com.huawei.agconnect:agcp:1.4.1.300' to the project-level build.gradle file.
6. Add apply plugin: 'com.huawei.agconnect' to the last line of the app-level build.gradle file.
7. Configure the dependencies \
      'com.huawei.hms:awareness:1.0.7.303' \
      'com.huawei.hms:hianalytics:5.0.5.301' \
      'com.huawei.agconnect:agconnect-auth:1.4.2.301' \
      'com.huawei.agconnect:agconnect-database:1.2.3.301' \
      'com.huawei.hms:hwid:5.1.0.301' in the app-level buildle.gradle file.
8. Synchronize the project.
	
## Sample Code
    HMS Awareness Kit Codelab 

1) First, define the location and the radius to be notified of when a user enters that area.
  Remember the radius should be at least 200 meters.
  Code location https://github.com/tolunayozturk/locationbarrier-codelab/blob/97622546ecaf313214843624760f3eec34d59c7e/app/src/main/java/com/tolunayozturk/barrierdemo/MainActivity.java#L46
    
2) Define the PendingIntent that will be triggered upon a barrier status change, and register a broadcast receiver to receive the broadcast.
  Code location https://github.com/tolunayozturk/locationbarrier-codelab/blob/97622546ecaf313214843624760f3eec34d59c7e/app/src/main/java/com/tolunayozturk/barrierdemo/MainActivity.java#L72
    
3) Create and add the barrier
    Code location https://github.com/tolunayozturk/locationbarrier-codelab/blob/97622546ecaf313214843624760f3eec34d59c7e/app/src/main/java/com/tolunayozturk/barrierdemo/MainActivity.java#L121
    
    Remember to remove a barrier if it already exists and add it again
    Code location https://github.com/tolunayozturk/locationbarrier-codelab/blob/97622546ecaf313214843624760f3eec34d59c7e/app/src/main/java/com/tolunayozturk/barrierdemo/MainActivity.java#L80

    Remember that you need to create the barrier only if your app has the neccessary permissions so check the permissions before creating a location barrier.
    Code locatio https://github.com/tolunayozturk/locationbarrier-codelab/blob/97622546ecaf313214843624760f3eec34d59c7e/app/src/main/java/com/tolunayozturk/barrierdemo/LoginActivity.java#L55
    
4) If a user enters the specified area, we will be notified via LocationBarrierReceiver class.
    When the enter event of Awareness Kit triggers, we start a timer and on exit event trigger, we stop the timer and calculate the length of stay. Then we send this data to Analytics Kit and CloudDB to analyze the data later.
    Code location https://github.com/tolunayozturk/locationbarrier-codelab/blob/97622546ecaf313214843624760f3eec34d59c7e/app/src/main/java/com/tolunayozturk/barrierdemo/MainActivity.java#L166
    

##  License
    HMS Video Kit Codelab is licensed under the [Apache License, version 2.0](http://www.apache.org/licenses/LICENSE-2.0).
