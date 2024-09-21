---
title: "[error] The play() request was interrupted by a call to pause()"
categories: [webRTC]
tags: [webrtc, error]
---

{:toc .large-only}

```js
<video id="video" preload="none" src="https://example.com/file.mp4"></video>

<script>
  video.play(); // <-- This is asynchronous!
  video.pause();
</script>
```

### Uncaught (in promise) DOMException: The play() request was interrupted by a call to pause().

`video.play()` 가 비동기 메서드기 때문에 비디오가 로드되기 전에 `video.pause()` 를 실행하면 위와 같은 에러가 발생한다.

`video.play()` 에 primise를 걸어 비디오가 로드된 후 pause 되도록 할 수 있다.

```html
<video id="video" preload="none" src="https://example.com/file.mp4"></video>

<script>
  // Show loading animation.
  const playPromise = video.play();

  if (playPromise !== undefined) {
    playPromise
      .then((_) => {
        // Automatic playback started!
        // Show playing UI.
        // We can now safely pause video...
        video.pause();
      })
      .catch((error) => {
        // Auto-play was prevented
        // Show paused UI.
      });
  }
</script>
```

[DOMException: The play() request was interrupted](https://developers.google.com/web/updates/2017/06/play-request-was-interrupted)
