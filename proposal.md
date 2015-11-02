This proposal is strongly inspired from the original proposal from Anton Vayvod in https://github.com/avayvod/remotehtmlmedia/blob/master/proposal.md

```js
partial interface HTMLMediaElement {
  readonly attribute RemotePlayback remote;
  
  // Reflects disable-remote-playback attribute.
  // This will disable the button from the default controls.
  attribute disableRemotePlayback;
};

interface RemotePlayback : EventTarget {
  Promise<RemotePlaybackAvailability> getAvailability();
  
  readonly attribute RemotePlaybackState state;
  
  // TODO: should this be named something else?
  // TODO: should the return value be something else?
  Promise<boolean> start();
  
  // TODO: should stop() be added?
  
  attribute EventHandler onstatechange;  
};

// TODO: values do not match Presentation API.
enum RemotePlaybackState {
  // TODO: "connecting"?
  "connected",
  "disconnected"
};

interface RemotePlaybackAvailability : EventTarget {
  readonly attribute value;
  attribute EventHandler onchange;
};
```
