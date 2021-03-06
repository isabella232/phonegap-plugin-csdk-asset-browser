<!--
#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#  KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#
-->

phonegap-plugin-csdk-asset-browser
------------------------

[![Stories in Ready](https://badge.waffle.io/CreativeSDK/phonegap-plugin-csdk-asset-browser.png?label=ready&title=Ready)](http://waffle.io/CreativeSDK/phonegap-plugin-csdk-asset-browser)

The Creative SDK provides a convenient UI for accessing all of a user’s creative assets stored in the Creative Cloud, including files, photos, libraries, and mobile creations.

This plugin makes it possible for you to use the Creative SDK Asset Browser in your PhoneGap apps on Android and iOS. Read on to learn how!

### Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Setup guide](#setup-guide)
- [Sample code](#sample-code)
- [API guide](#api-guide)

# Prerequisites

**Required:** You must first install the [Client Auth plugin](https://github.com/CreativeSDK/phonegap-plugin-csdk-client-auth) for this plugin to work.

**Required:** This guide will assume that you have installed all software and completed all of the steps in the [Client Auth guide](https://github.com/CreativeSDK/phonegap-plugin-csdk-client-auth).


# Installation

## Adding the plugin

Use the command below to add the plugin to your app.

### Adding released version

```
phonegap plugin add --save phonegap-plugin-csdk-asset-browser
```

### Adding development version

```
phonegap plugin add --save https://github.com/CreativeSDK/phonegap-plugin-csdk-asset-browser
```

## Downloading the Creative SDK

**iOS**

_**Note:** For some developers, the iOS version of the SDK is currently running into some server issues (getting a `400` on launch of the component). We are looking into the issue and will provide an update as soon as possible._

To get the iOS SDK, go to the [Downloads page](https://creativesdk.adobe.com/downloads.html), click the download link for `STATIC FRAMEWORKS (DEPRECATED)`, and extract it to the `src/ios` folder of this plugin. Extracting the ZIP will create an `AdobeCreativeSDKFrameworks` folder.

The ZIP files contain all the frameworks in the Creative SDK, but for this plugin we will only be using the `AdobeCreativeSDKImage.framework`.


**Android**

No action is required for Android. The Creative SDK for Android is delivered as a remote Maven repository, and the required framework will be downloaded automatically by the plugin.


# Setup guide

1. `cd` into your existing PhoneGap app (must already include [Client Auth](https://github.com/CreativeSDK/phonegap-plugin-csdk-client-auth))
1. Add this plugin (see "Adding the plugin" above)
1. **iOS only:** download and add the Creative SDK to this plugin's `src/ios` directory (see "Downloading the Creative SDK" above)
1. Build and run for your platform


# Sample code

## `www/index.html`

Add a button within the `body`. The PhoneGap "Hello World" example includes a `div` with an ID of `app`, so for this example, we are including it in there.

```
// ...

<div class="app">

	// ...

    <button id="launch-browser">Launch asset browser</button>
</div>

// ...

```

## `www/js/index.js`

_**Note:** Most of the code below comes from the PhoneGap "Hello World" example, and we are providing it here for context._

This plugin provides access to a global `CSDKAssetBrowser` object.

The `CSDKAssetBrowser` object exposes a `.downloadFiles()` function, and some enums to use when setting up your options.

See comments **#1-2** below for relevant code:

```
var app = {
    initialize: function() {
        this.bindEvents();
    },
    bindEvents: function() {
        // ...

        /* 1) Add a click handler for your button */
        document.getElementById('launch-browser').addEventListener('click', this.launchBrowser, false);
    },
    onDeviceReady: function() {
        app.receivedEvent('deviceready');
    },
    receivedEvent: function(id) {
        // ...
    },

    /* 2) Make a helper function to launch the Asset Browser */
    launchBrowser: function() {

    	/* 2.a) Prep work for calling `.edit()` */
        function success(newUrl) {
            console.log("Success!", newUrl);
        }

        function error(error) {
            console.log("Error!", error);
        }

        var options = {};

        /* 2.b) Launch the Asset Browser */
        CSDKAssetBrowser.downloadFiles(success, error, options);
    }
};
```


# API guide

[See the full API guide](docs/api.md).
