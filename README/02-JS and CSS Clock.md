## 02-JS and CSS Clock

### :cherries: 전체 코드

```javascript
<script>
  const secondHand = document.querySelector('.second-hand')
const mindHand = document.querySelector('.min-hand')
const hourHand = document.querySelector('.hour-hand')

function setDate () {
  const now = new Date()

  const seconds = now.getSeconds()
  const secondsDegrees = ((seconds / 60) * 360) + 90
  secondHand.style.transform = `rotate(${secondsDegrees}deg)`

  const mins = now.getMinutes()
  const minsDegrees = ((mins / 60) * 360) + ((seconds / 60) * 6) + 90
  mindHand.style.transform = `rotate(${minsDegrees}deg)` 

  const hour = now.getHours();
  const hourDegrees = ((hour / 12) * 360) + ((mins/60)*30) + 90;
  hourHand.style.transform = `rotate(${hourDegrees}deg)`;
}

setInterval(setDate, 1000)

setDate()
</script>
```

```css
.hand {
  width: 50%;
  height: 6px;
  background: black;
  position: absolute;
  top: 50%;
  transform-origin: 100%;
  transform: rotate(90deg);
  transition: all 0.05s;
  transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
}
```



### Transform 세부 속성 (scale, rotate, skew, origin)

https://url.kr/mj8dhp

> * `transform: sacale()`: 지정 요소 확대/ 축소
>   * `transform: sacaleX()`: x축 확대/ 축소
>   * `transform: sacaleY()`: y축 확대/ 축소
>   * scale 안의 변수는 원하는 비율로 작성 (1 = 100%_원사이즈)
> * `transform: rotate(Ndeg)`: 지정 요소 회전
>   * `transform: rotateX(Ndeg)`: x축 기준 N도 만큼 회전
>   * `transform: rotateY(Ndeg)`: y축 기준 N도 만큼 회전
> * `transform: skew(Ndeg)`: 지정 요소 기울이기
>   * `transform: skewX(Ndeg)`: x축으로 N도 만큼 기울이기
>   * `transform: skewY(Ndeg)`: y축으로 N도 만큼 기울이기
> * `transform-origin: x축 y축`: 지정 요소의 기준점을 변경
>   * 세부 값은 px, 백분율(%), left, center, right 중 하나를 사용할 수 있음



### Transition 세부 속성

https://url.kr/kdfr2q

