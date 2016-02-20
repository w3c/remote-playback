# Use Cases and Requirements

The primary goal of this API is to enable websites to customize the default UI for playing HTML media remotely, e.g. to implement custom media controls or disable the default UI in the case when presenting content remotely is implemented differently (i.e. via Presentation API). Thus he use cases and requirements are defined by the existing browsers' behaviors and also some related proprietary APIs (see below).


## Proprietary APIs

Safari for iOS has some proprietary APIs in order to allow remote playback on AirPlay.
- Safari 7 release notes: https://developer.apple.com/library/prerelease/mac/releasenotes/General/WhatsNewInSafari/Articles/Safari_7_0.html#//apple_ref/doc/uid/TP40014305-CH5-SW7
- Safari 9 release notes: https://developer.apple.com/library/prerelease/mac/releasenotes/General/WhatsNewInSafari/Articles/Safari_9.html

The Safari API can be described as:
- ```x-webkit-wirelessvideoplaybackdisabled``` property, it lets the website disable AirPlay video playback, it superseeds ```x-webkit-airplay```.
- ```webkitplaybacktargetavailabilitychanged``` event, it lets the website know if an AirPlay device beomes available or there no none available anymore.
- ```webkitShowPlaybackTargetPicker()``` function, it allows website to show an AirPlay device picker, allowing them to creat a button which will show that UI.
- ```webkitCurrentPlaybackTargetIsWireless```property, it exposes whether the media element is currently being played on an AirPlay device.
- ```webkitcurrentpalybacktargetiswireless``` event, it lets the website know whet the previous property changes.


## Existing remote media playback behavior in browsers

Safari, Edge on Windows 10, as well as Android versions of Firefox and Chrome allow users to play some website's media remotely. Safari will show an icon in order to send a video to an AirPlay device nearby. Chrome and Firefox will show a similar icon but for Cast devices. Edge provides a menu item.

Safari:
- Description link: https://support.apple.com/en-gb/HT201343
- The user will see an AirPlay button on the audio/video controls if there is an AirPlay device available in the local network.
- When the AirPlay button is pressed, the user will be able to select a device from a picker (inc. local).
- While playing remotely, the user can play/pause and seek using the default controls.
- While playing remotely, the media element changes look and no longer renders the video locally.
- While playing remotely, the AirPlay button will allow the user to pick another device (inc. local).
- The selected screen (local or remote) is a global system setting that affects all relevant apps

Chrome for Android:
- Description link: http://googlesystem.blogspot.be/2014/04/cast-videos-in-chrome-for-android.html
- The user will see a Cast button on the video controls if there is a Cast device available in the local network.
- When the cast button is pressed, the user will be able to select a Cast device from a picker.
- While casting, the Cast button changes to the connected state and the media element no longer renders the video locally.
- While casting, the user can play/pause and seek using the default controls.
- While casting, tapping the Cast button will show a different dialog that allows setting the volume on the Cast device and stop casting.

Firefox Android:
- Description link: https://support.mozilla.org/en-US/kb/use-firefox-android-send-videos-chromecast
- The user will see the Cast button in the omnibox if there's a castable video on the page
- The rest of the behavior matches the one Chrome provides

Edge on Windows 10:
- Description link: https://blogs.windows.com/windowsexperience/2015/10/29/announcing-windows-10-insider-preview-build-10576/
- The user will initialize media casting from the ... menu

## Use cases

Based on the Safari's API and supported behaviors in various browsers, we can define the following use cases:
- A website should be able to know if there is a remote device available and if this changes.
- A website should be able to know when a remote playback session is connected, disconnected.
- A website should be able to control a remote playback:
  - A website should be able start a remote playback session.
  - A website should be able to apply any usual media control to a remote playback session.
- A website should be able to disable the remote playback (e.g. the default browser UI or the feature completely if the UI is not necessary for initiating the remote playback).

The following use cases might be added in the future or considered in the first set of use cases but there is no strong signal that they are needed as of yet:
- A website should be able to know when a remote playback session is connecting (ie. in the process of being connected but not connected yet).
- A website should be able to stop a remote playback session.
