# Use Cases and Requirements

The primary goal of this API is to be able to create a UI to start remote playback even when using custom controls and disable default remote playback UI in case of remote playback is handled another way (eg. Presentation API or a button outside of the default controls). Thus, the use cases and requirements' inputs are the proprietary API and the browser UIs, the MVP being to be able to match them all.

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


## Browser UIs

Both Safari for iOS and Chrome Android have UIs specific to remote playback. Safari will show an icon in order to send a video to an AirPlay device nearby. Chrome will show a similar icon but for Chrome Cast devices.

Safari iOS:
- The user will see an AirPlay button on the audio/video controls if there is an AirPlay device available in the local network.
- When the AirPlay button is pressed, the user will be able to select a device from a picker (inc. local).
- While playing remotely, the user can play/pause and seek using the default controls.
- While playing remotely, the video element changes look and no longer shows the playback locally.
- While playing remotely, the AirPlay button will allow the user to picke another device (inc. local).

Chrome Android:
- Some screenshots: http://avayvod.github.io/chrome-android-remote-playback.pdf
- The user will see a Cast button on the video controls if there is a Cast device available in the local network.
- When the cast button is pressed, the user will be able to select a Cast device from a picker.
- While casting, the video element shows a different Cast button and no longer shows the video playback locally.
- While casting, the user can play/pause and seek using the default controls.
- While casting, the Cast button changes style.
- While casting, the Cast button will show a different UI that allows setting the volume on the Cast device and stop casting.

Firefox Android:
- TODO

## Use cases

Based on the different UIs and APIs, we can define the following use cases:
- A website should be able to know if there is a remote device available and if this changes.
- A website should be able to know when a remote playback session is connected, disconnected.
- A website should be able to control a remote playback:
  - A website should be able start a remote playback session.
  - A website should be able to apply any usual media control to a remote playback session.
- A website should be able to de-active the default browser UI button for remote playback.

The following use cases might be added in the future or considered in the first set of use cases but there is no strong signal that they are needed as of yet:
- A website should be able to know when a remote playback session is connecting (ie. in the process of being connected but not connected yet).
- A website should be able to stop a remote playback session.
