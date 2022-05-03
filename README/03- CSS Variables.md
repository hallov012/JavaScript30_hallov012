## 03 - CSS Variables

### :cherries: 전체 코드

```css
:root {
  --base: #4b25f5;
  --spacing: 10px;
  --blur: 10px;
}

img {
  padding: var(--spacing);
  background: var(--base);
  filter: blur(var(--blur));
}

.hl {
  color: var(--base);
}
```

```javascript
const inputs = document.querySelectorAll('.controls input')

function handleUpdate() {
  console.log(this.value)
  const suffix = this.dataset.sizing || ''
  // suffix 단위를 받아오는 것 , sizing은 spacing과 blur에만 달려있음 
  // || : or을 뜻함 => dataset.sizing이 없다면 ''(빈공간)을 받아오겠다
  document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix)
}
inputs.forEach(input => input.addEventListener('change', handleUpdate))
inputs.forEach(input => input.addEventListener('mousemove', handleUpdate))
```



### JS 연산자

https://curryyou.tistory.com/193

> * `||` (논리합)
>
>   * 둘 중 하나만 True이면 True로 평가되므로 왼쪽 피연산자가 True이면 바로 True를 반환
>   * 왼쪽이 맞다면 바로 왼쪽을 반환하고, 왼쪽이 False라면 오른쪽을 반환
>
>   ![스크린샷 2022-05-04 오전 2.11.34](03- CSS Variables.assets/스크린샷 2022-05-04 오전 2.11.34.png)
>
> * `&&` (논리곱)
>
>   * 둘 다 True여야만 True가 반환된다. 
>   * 왼쪽이 False라면 고민도 없이 바로 왼쪽을 반환, True라면 오른쪽 값을 반환
>
>   ![스크린샷 2022-05-04 오전 2.11.54](03- CSS Variables.assets/스크린샷 2022-05-04 오전 2.11.54.png)



### documentElement

> * 요소 개체로, 문서의 documentElement를 반환
>
> * HTML 문서의 반환 된 객체는 <HTML> 요소임
>
>   ```javascript
>   document.documentElement // => HTML
>   document.documentElement.style // => CSS
>   ```
>
>   ![스크린샷 2022-05-04 오전 2.19.33](03- CSS Variables.assets/스크린샷 2022-05-04 오전 2.19.33.png)



### setAttribue & setProperty 

https://url.kr/e384i6

> * `setAttribue` : 속성, HTML안에 쓰임
>
> * `setProperty` : 프로퍼티, DOM 객체 안에 쓰임 
>
> * ```
>   document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix)
>   ```
>
>   * documentElement 까지는 속성
>   * documentElement 는 프로퍼티
>   * 따라서 `setAttribute`가 아닌 `setProperty`로 새로운 값을 입력해줘야 한다



### :root

https://blog.thereis.xyz/136

> * `:root` : 최상위 엘리먼트
>
>   * HTML에서의 최상위 엘리먼트: HTML
>
>   *  그렇다면 왜 HTML에 직접 속성을 부여하지 않고 :root를 쓰는가?
>
>     * HTML 태그 이름을 선택자로 쓰면 우선순위 1점이지만, 
>
>       :root 가상 선택자는 class로 간주되어 10점이 된다
>
> * `:root`를 이용한 변수 사용하기
>
>   ```css
>   :root {
>     --base: #4b25f5;
>     --spacing: 10px;
>     --blur: 10px;
>   }
>   
>   img {
>     padding: var(--spacing);
>     background: var(--base);
>     filter: blur(var(--blur));
>   }
>   ```
>
>   * 변수로 사용할 이름 앞에 '--'를 입력 한다 (JS의 '$' 같은 느낌)
>   * 이 다음 필요한 곳에 '--변수명'을 입력하면 적용됨

