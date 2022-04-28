## 01-JavaScript Drum Kit (0428)

###  :cherries: 전체 코드

```javascript
  function removeTransition(event) {
    if (event.propertyName != 'transform') return // 아직 transform 상태일 때는 return, 이 코드를 안쓰면 총 6개의 transform massege를 볼 수 있음^^
    event.target.classList.remove('playing')
    console.log(event.propertyName)
  }

  function playSound(event) {
    const audio = document.querySelector(`audio[data-key="${event.keyCode}"]`)
    const key = document.querySelector(`div[data-key="${event.keyCode}"]`)
    if (!audio) return;  //최적화 관련, 지정되지 않은 key를 누를 땐 바로 function을 종료

    key.classList.add('playing')
    audio.currentTime = 0 //소리가 끝나기 전에 키를 눌러도 소리가 출력되도록 설정
    audio.play()
  }

  const keys = Array.from(document.querySelectorAll('.key'))
  keys.forEach(key => key.addEventListener('transitionend', removeTransition))
  document.addEventListener('keydown', playSound)
```



<hr>

### querySelector(₩Tag[class="  "]₩)

```javascript
const audio = document.querySelector(`audio[data-key="${event.keyCode}"]`)
const key = document.querySelector(`div[data-key="${event.keyCode}"]`)
```

> * Tag 안에서 특정 class를 가져오고 싶을 때 ₩tag[class]₩로 처리가 가능 
> * 만약 같은 class로 지정된 여러 항목 중 원하는 값으로 가려오려면 " "안에 원하는 값을 입력



### .currentTime

http://www.w3big.com/ko/tags/av-prop-currenttime.html

> * (초) 오디오 / 비디오 재생의 현재 위치를 설정
> * 만약 0으로 설정하면 재생하던 오디오를 멈추고 제일 처음 지점으로 돌아간다고 볼 수 있음

`audio.currentTime = 0`

> * 해당 코드가 없을 때: 오디오가 출력되고 있을 때 해당 버튼을 다시 눌러도 소리가 출력되지 않음
> * 해당 코드가 있을 때: 오디오 출력이 끝나지 않더라도 바로 또 다른 오디오를 출력 할 수 있음



### Transition

https://it-eldorado.tistory.com/110

> * 엘리먼트의 CSS 속성을 변경할 때 두 가지 상태 사이에서 일어나는 변화를 커스터마이징 할 때 사용
> * 속성 변경이 즉시 영향을 미치게 하는 대신, 그 속성의 변화가 일정 기간에 걸쳐 일어나도록 하는 것

```javascript
function removeTransition(event) {
  if (event.propertyName != 'transform')
  event.target.classList.remove('playing')
}

keys.forEach(key => key.addEventListener('transitionend', removeTransition))
```

> * 변화된 border를 다시 원상태로 돌리기 위해 remove를 해준다
>
> * `if (event.propertyName != 'transform')` ::가장 이해안되는 부분::
>
>   * 해당 코드를 작성하지 않았을 때 console 창
>
>     ![스크린샷 2022-04-29 오전 3.41.01](01-JavaScrit Drum Kit.assets/스크린샷 2022-04-29 오전 3.41.01.png)
>
>   * 작성 했을 때의 console 창
>
>     ![스크린샷 2022-04-29 오전 3.41.44](01-JavaScrit Drum Kit.assets/스크린샷 2022-04-29 오전 3.41.44.png)
>
>   * key에 css가 적용한 taransform, taransition이 실했될  코드를 작성하지 않으면 관련 변화 항목이 모두 출력되는 것으로 보인다
>
>   * 따라서 모든 변화가 완료되어 transform이 출력될 때 'playing'을 remove한다
>
>   * transform이 두번 뜨는 것은 적용되었을 때 한번, 삭제되었을 때 한번으로 총 두번이 뜨는 것으로 보인다
>
>   * 사실 아직 잘 모르겠는 부분이라 좀 더 공부가 필요할 것 같다
>
>   * 위의 코드를 작성하지 않아도 일단 사이트 작동에는 문제가 없음



### Transform

https://it-eldorado.tistory.com/110

> * 엘리먼트에 **회전, 크기 조절, 기울이기, 이동 효과 등을 부여**할 때 사용
> * CSS의 시각적 서식 모델의 좌표 공간을 변형하는 역할을 수행



### Array.From

```javascript
const keys = Array.from(document.querySelectorAll('.key'))
```

> * 솔루션에서는 Array.from을 사용했는데.
>
>   사실 `const keys = document.querySelectorAll('.key')`로도 작동 된다
>
> * 이부분에 대해서는 다음에 다루겠다고 하였으므로 진행하며 나중에 추가할 예정

