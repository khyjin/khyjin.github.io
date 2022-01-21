---
title:  "WaveSurfer"
excerpt: "wavesurfer"

categories:
  - JavaScript-lib
tags:
  - [라이브러리]

toc: true
toc_sticky: true

date: 2022-01-21
last_modified_at: 2022-01-21
layout: single
---

- Wavesurfer : 오픈소스 자바스크립트 라이브러리로 오디오 파일의 파형을 그려주는 기능을 한다.

### 설치 및 시작

- 설치방법
    
    방법1) Github 저장소를 다운 받아 html 파일에서 wavesurfer.min.js 파일을 불러온다.
    
    <aside>
    💡 Github 주소 : `[https://github.com/katspaugh/wavesurfer.js](https://github.com/katspaugh/wavesurfer.js)`
    
    </aside>
    
    방법2) CDN(Content Delivery Network) 로 설치
    
    ```javascript
    <script src="https://cdnjs.cloudflare.com/ajax/libs/wavesurfer.js/4.0.1/wavesurfer.min.js"></script>
    ```
    

※처음 CDN 설치시 wavesurfer를 제일 상단으로 올려줄 것

※버전 확인할 것

- 시작방법
1. html에 파형을 그려줄 위치에 `div`를 만들고 id를 부여한다 

```html
<div id="waveform"></div>
```

1. 자바스크립트에서 `WaveSurfer` 객체를 새로 생성한다. `WaveSurfer.create` 함수에 몇 가지 옵션을 전달하여 생성하며, `container` 옵션은 어떤 오브젝트에 파형을 렌더링 할 지 결정하는 옵션으로 필수로 입력해야 한다. 

```javascript
var wavesurfer = WaveSurfer.create({
    // id="waveform" 인 오브젝트에 파형 생성
    // 필수 옵션
    container: '#waveform',
    // 선택 옵션들 
    waveColor: 'violet',
    progressColor: 'purple'
});
```

1. `wavesurfer.load()` 함수에 오디오 오브젝트를 전달하여 실행 시킨다. 

```javascript
wavesurfer.load('audio.wav');
```

### 옵션

파형을 생성하는 `create` 메소드에 여러가지 옵션들을 전달하여 커스터마이징 할 수 있다.

| 옵션 | 타입 | 기본값 | 설명 |
| --- | --- | --- | --- |
| container | mixed | none | 웨이브 폼이 그려질 오브젝트의 CSS선택자 또는 HTML 요소를 전달한다. 유일한 필수 옵션 |
| barHeight | number | 1 | 웨이브 폼 막대들의 높이. 1보다 높은 값을 주면 더 길어지고 그 반대는 작아진다. |
| waveColor | String | #999 | 파형 중 아직 재생되지 않은 부분의 색상 |
| progressColor | String | #555 | 파형 중 재생된 부분의 색상 설정 |
| audioContext | object | none | 미리 생성된 AudioContext를 사용하도록 한다 |
| audioRate | float | 1 | 재생 속도. 정상 속도는 1 |
| barWidth | number | none | 웨이브 폼 막대들의 넓이 |
| cursorColor | String | #333 | 커서의 색상 설정 |
| cursorWidth | Integer | 1 | 커서의 넓이 |
| fillParent | boolean | true | 부모 요소의 넓이를 가득 채울지, minPerSec 옵션에 따라 렌더링할 지 선택 |
| height | Integer | 128 | 전체 높이 |
| hideScrollbar | boolean | false | 가로 스크롤바 표시 여부 |
| minPxPerSec | Integer | 50 | 오디오 파일의 1초당 렌더링 될 픽셀 수의 최소값 |
| normalize | boolean | false | true 일 경우 가장 큰 막대길이에 비례하여 막대 높이 설정 |
| responsive | boolean | true | 반응형 웨이브폼 여부 |
| scrollParent | boolean | false | 웨이브폼이 부모 요소보다 큰 경우 스크롤바를 나타낼지, 부모 요소의 길이에 맞춰 렌더링할 것인지를 설정 |

### 메서드

- 로드된 `WaveSurfer` 객체를 통해 사용가능한 메스드

| 메소드 | 설명 |
| --- | --- |
| play([start[,end]]) | 커서가 있는 위치부터 음원 재생. start, end 값이 있는 경우 start부터 end까지 재생 |
| pause() | 일시정지 |
| playPause() | 재생중일 경우 일시정지, 정지중이면 재생 |
| stop() | 정지 |
| isPlaying() | 현재 재생 중일 경우 true, 아닐 경우 false 를 리턴 |
| getCurrentTime() | 음원 중 커서의 위치를 초단위로 리턴 |
| getDuration | 음원의 전체 길이를 초단위로 리턴 |
| on(event, callback) | event를 등록하여, 등록한 event 발생시 callback 함수 실행 |
| cancelAjax() | 오디오 파일 로드 프로세스를 취소한다 |
| destroy() | 이벤트, 요소를 제거하고 웹 오디오 노드 연결을 끊는다. |
| empty() | 길이가 0인 오디오가 로드된 것 처럼 파형을 지운다. |
| getActivePlugins() | 현재 초기화된 플러그인 이름의 맵 반환 |
| getMute() | 음소거 상태로 만듬 |

- 참고용
[자세한 함수 목록 ](https://wavesurfer-js.org/docs/methods.html)

### 이벤트

- on 메소드를 통해 여러 이벤트를 등록시켜 상황에 따른 동작을 설정할 수 있다.
- `wavesurfer.on(’event’, function());`

| 이벤트 | 설명 |
| --- | --- |
| ready | 음원 로딩이 끝난 경우 발생 |
| play | 음원 재생이 시작되는 경우 발생 |
| audioprocess | 음원이 재생 중인 경우 지속적으로 발생 |
| pause | 음원이 일시정지 될 경우 발생 |
| finish | 음원이 끝까지 재생된 경우 발생 |

- 등록 가능한 이벤트 목록
[자세한 이벤트 설명 페이지](https://wavesurfer-js.org/docs/events.html)


```html
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src="https://unpkg.com/wavesurfer.js/dist/wavesurfer.min.js"></script>
    <script src="https://unpkg.com/wavesurfer.js/dist/plugin/wavesurfer.timeline.min.js"></script>
    <script src="./app.js"></script>
</head>

<body>
    <div class="row">
        <div>
            <div id="waveform">
                <!-- Here be waveform -->
            </div>
            <div id="wave-timeline"></div>
        </div>
    </div>

    <div class="row">
        <div class="col-sm-2">
            <button onclick="wavesurfer.play()" class="btn"><i class="far fa-play-circle"></i></button>
            <button onclick="wavesurfer.pause()" class="btn"><i class="far fa-pause-circle"></i></button>
            <button onclick="wavesurfer.toggleMute()" class="btn"><i class="fas fa-volume-off"></i></button>
            <button onclick="wavesurfer.toggleMute()" class="btn"><i class="fas fa-volume-mute"></i></button>
            <p></p>
            <button class="btn play-1x" onclick="wavesurfer.setPlaybackRate(1)">X1</i></button>
            <button class="btn" onclick="wavesurfer.setPlaybackRate(1.25)">X1.25</i></button>
            <button class="btn" onclick="wavesurfer.setPlaybackRate(1.5)">X1.5</button>
            <button class="btn play-2x" onclick="wavesurfer.setPlaybackRate(2)">X2</button>
        </div>
        <div style="text-align: right; padding-right: 2%;">
            <span class="badge badge-info" id="msg"  style="font-size: medium;"></span>
        </div>
    </div>

    <p></p>
    <div class="list-group" id="playlist">
        <a href="insert here audio-link" class="list-group-item">
            <i class="glyphicon glyphicon-play"></i>
            재생목록1</a>

        <a href="audio link" class="list-group-item">
            <i class="glyphicon glyphicon-play"></i>
            재생목록2</a>

        <a href="audio file" class="list-group-item">
            <i class="glyphicon glyphicon-play"></i>
            재생목록3</a>

    </div>
</body>
```

###app.js
```javascript
var wavesurfer = WaveSurfer.create({
    container: '#waveform',
    waveColor: '#D9DCFF',
    progressColor: '#4353FF',
    cursorColor: '#4353FF',
    height : 200,
    scrollParent : true,
    plugins: [
        WaveSurfer.timeline.create({
            container: "#wave-timeline"
        })
      ]
  });

var links = document.getElementsByClassName("list-group-item");
var currentTrack = 0;

var setCurrentSong = function(index){
    links[currentTrack].classList.remove('active');
    currentTrack = index;
    links[currentTrack].classList.add('active');
    wavesurfer.load(links[currentTrack].href);
};

Array.prototype.forEach.call(links, function(link, index) {
    link.addEventListener('click', function(e) {
        e.preventDefault();
        setCurrentSong(index);
    });
});

wavesurfer.on('ready', function() {        
    wavesurfer.play();
});

wavesurfer.on('finish', function() {
    setCurrentSong((currentTrack + 1) % links.length);
});

setCurrentSong(currentTrack);
    
 
    
function parseTime(seconds){
    var min = parseInt((seconds%3600)/60);
    var sec = Math.round(seconds%60);

    if(min < 10) {min = "0"+min;}
    if(sec < 10) {sec = "0"+sec;}
    return min + ":" + sec;
}

wavesurfer.on('audioprocess', function(){
    var totalTime = wavesurfer.getDuration(links[currentTrack]);
    var playTime = wavesurfer.getCurrentTime(links[currentTrack]);

    document.getElementById("msg").innerText = parseTime(playTime) +"/"+ parseTime(totalTime);
});


```
