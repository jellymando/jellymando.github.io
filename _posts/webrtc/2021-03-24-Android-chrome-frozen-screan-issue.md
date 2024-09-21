---
title: "Android chrome에서 동영상을 중지하면 화면이 멈춤 이슈"
categories: [WEBRTC]
tags: [webrtc]
---

{:toc .large-only}

### 이슈 내용

- Chrome89에서 동영상을 중지하면 종료페이지가 보여야 하나 화면이 멈추는 현상
- 디버깅하면 정상적으로 종료페이지로 이동한 것으로 확인되지만 동영상 화면 남아있음
- 안드로이드에서 열려있는 어플 화면으로 갔다가 다시 크롬 앱을 실행하면 종료 화면 보임
  <br/>

[Frozen screen when clicking 'stop video' on android Chrome](https://github.com/twilio/twilio-video-app-react/issues/355#issuecomment-780368725)
<br/>

Chrome86.0.4240.110 에서도 동일한 이슈가 발생했던 것 같다.

아래 해결방법 중 2번처럼 수정하니 정상 동작하는 것을 확인했다.
<br/>

1. 트랙을 중지하기 전에 video.srcObject 지우기

```js
video.srcObject = null;

stream.getTracks().forEach((track) => track.stop());
```

2. 중지하기 전에 트랙 삭제

```js
stream.getTracks().forEach((track) => {
  stream.removeTrack(track);
  track.stop();
});
```

[MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack)
