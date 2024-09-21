---
title: 'Youtube 동영상 컨트롤 커스텀하기'
categories: [Javascript]
tags: [javascript]
---

{:toc .large-only}

## Youtube 동영상 불러오기

유투브 동영상을 가져오려면 iframe을 이용해야 한다.

유투브에서 `공유 -> 퍼가기`를 통해 html 코드를 얻거나,

<a href="https://developers.google.com/youtube/youtube_player_demo">https://developers.google.com/youtube/youtube_player_demo</a> 에서 옵션을 체크하여 코드를 얻을 수 있다.

## Youtube 동영상 컨트롤하기

크게 두 가지 방법이 있을 것 같다.

유투브에서 제공하는 api로 player 객체를 만들어서 사용하거나, iframe에 postMessage를 보내서 컨트롤 하는 방법이 있다.

### player 객체 만들기

```html
<script src="https://www.youtube.com/iframe_api"></script>
<script>
  var player
  var stopButton = document.getElementById('stop')

  function onYouTubeIframeAPIReady() {
    player = new YT.Player('player', {
      height: '360',
      width: '640',
      videoId: 'M7lc1UVf-VE'
    })
  }

  stopButton.addEventListener('click', () => {
    player.stopVideo()
  })
</script>
```

Player 인스턴스를 생성하여 메서드를 호출하면 된다.

### postMessage 사용하기

```js
if (iframe.contentWindow) {
  iframe.contentWindow.postMessage(
    JSON.stringify({
      event: 'command',
      func: func,
      args: args || []
    }),
    '*'
  )
}
```

`iframe.contentWindow`에 postMessage를 보내준다.

`func`에는 아래 기능을 전달한다.

- playVideo
- pauseVideo
- stopVideo
- mute
- unMute

생각해보니 위의 api를 이용하는 방식도 api 코드 까보면 결국 postMessage 일 것 같다.. 쩝

## 참고사이트

[YouTube 플레이어 데모](https://developers.google.com/youtube/youtube_player_demo)<br/>
[iframe 삽입에 대한 YouTube Player API 참조 문서](https://developers.google.com/youtube/iframe_api_reference#Getting_Started)<br/>
[react-youtube-iframe](https://github.com/nsrau/react-youtube-iframe/blob/main/src/index.tsx)
