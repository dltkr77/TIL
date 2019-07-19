# UI 인터랙션

강사: 야무

[발표자료](https://yamoo9.github.io/WTC2019)

## 내용

### Part 1 . CSS Animation

* 자바스크립트 대비 CSS 애니메이션의 성능이 많이 개선되었다
* 장식적인 부분이라 필수적이기 보단 선택적인 내용으로, 모션 제공을 통한 흥미유발의 목적이 크다

#### CSS3 Animation

* Animation의 속성들: [name](https://developer.mozilla.org/ko/docs/Web/CSS/animation-name) / [duration](https://developer.mozilla.org/ko/docs/Web/CSS/animation-duration) / [delay](https://developer.mozilla.org/ko/docs/Web/CSS/animation-delay) / [timing function](https://developer.mozilla.org/ko/docs/Web/CSS/animation-timing-function) / [fill-mode](https://developer.mozilla.org/ko/docs/Web/CSS/animation-fill-mode)  |  [@keyframes](https://developer.mozilla.org/ko/docs/Web/CSS/@keyframes)

* Q. animation과 transition의 차이? - A.transition은 시작과 끝이 있어 장면 전환을 하며, 보다 디테일하게 장면을 쪼개기 위해 animation을 사용한다

  ```css
  @keyframes fade-In {
   /* 시작 (from) */
    0% {
      opacity: 0;
    }
    
    /* 끝 (to) */
    100% {
      opacity: 1;
    }
  }
  
  .app-header {
    opacity: 0;
    animation: 
      fade-in   /* name */
      0.35s     /* duration */ 
      /* 350ms 와 같이 더 디테일한 속도를 제어할 수 있다 */
      0.4s      /* delay */
      ease-out  /* timing function */
      /* 여러 속성을 제공하지만, 속성제공을 안할 경우 베지어 곡선을 편집해야한다 */
      forwards; /* fill mode */
  }
  ```

  * 1초는 굉장히 길다. Normal 속도는 0.4, slow 속도가 0.6초
  * `@keyframe` 으로 정의한 애니메이션은 재사용할 수 있다
  * `0.3s` 는 `.3s` 와 같이 `0` 을 생략할 수 있지만, 명시적으로 `0.3s`  라고 쓰는것을 권장한다

* [cubic-bezier](https://cubic-bezier.com/#.17,.67,.83,.67) 혹은 크롬 브라우저의 개발자 도구에서 큐빅 베지어를 수정할 수 있다

* Effective Management
  
  매번 애니메이션을 만든다는건 상당히 공수가 드는 일이다. 세분화와 모듈화를 통해 성능을 더 좋게 만들 수 있다. 아래와 같이 마지막 지점에서 원래 형태로 돌아오는 코드를 만든다

  ```css
  @keyframes transform-none {
    to {
      transform: none;
      opacity: 1;
    }
  }
  ```

  그 후, 시작 지점의 형태를 선언하고 아래와 같이 재사용한다

  ```css
  .app-header {

    /* 0% */
    opacity: 0;
    transform: translateY(-4rem);

    /* 100% */
    animation: transform-none 0.35s 0.4s ease-out forwards;

  }
  ```

* [Accessibility Concerns]([https://developer.mozilla.org/ko/docs/Web/CSS/animation#%EC%A0%91%EA%B7%BC%EC%84%B1_%EA%B3%A0%EB%A0%A4%EC%82%AC%ED%95%AD](https://developer.mozilla.org/ko/docs/Web/CSS/animation#접근성_고려사항))
  
  * 깜박이는 애니메이션은 주의력 결핍 과잉 행동 장애 (ADHD)와 같은 인지 적 문제가 있는 사람들에게 문제가 될 수 있다. 또한, 특정 종류의 운동은 전정 장애, 간질, 편두통 및 조영제 민감도를 유발할 수 있다.
  * 움직임을 끌 수 있는 기능이 필요하다
  * [Text Sequencing Motion](https://codepen.io/yamoo9/embed/WqLmGa) 예제와 [top & Play Animation for Everyone](https://codepen.io/yamoo9/embed/agPPXj)

### Part 2 . DOM Script

뉘앙스를 이해하자!

* 상태 관련 속성은 변경할 수 있다 Show(Open) / Hide(Close)

HTML Markup & UI

Selecting [DOM](https://developer.mozilla.org/ko/docs/Glossary/DOM) Element : [querySelector()](https://developer.mozilla.org/ko/docs/Web/API/Document/querySelector)

Selecting [DOM](https://developer.mozilla.org/ko/docs/Glossary/DOM) Element : [querySelectorAll()](https://developer.mozilla.org/ko/docs/Web/API/Document/querySelectorAll)

**[Click Event](https://developer.mozilla.org/ko/docs/Web/API/Element/click_event) Handling**

```js
/* DOM API : 사용자가 문서 요소를 클릭하면 동작하도록 하는 방법
 * 문서_객체.addEventListener('이벤트_유형', 실행될_함수)
 */

// 클릭 시, 실행 될 함수
const onClickAction = (event) => {
  console.log('이벤트 유형:', event.type)
}

// 첫번째 메뉴 아이템 버튼 클릭 시, 연결된 함수 실행
menuItemButtons[0].addEventListener('click', onClickAction)
```

* 포커스를 줄 수 있는 요소: `<a>`,`< button>` ...

  * `<div>`를 버튼처럼 만들려면 `role="button", tabindex="0" …` 선언할 것이 무궁무진해진다

* `onClick` 의 여러 단점이 있어 `addEventListener()` 라는 이벤트를 만들 수 있다

  ```js
  el('.ediya-menu__item a').addEventListener('click', ()=>{
  	consloe.log('clicked like button')
  })
  ```

* 집합에서 하나의 객체를 뽑아내는 방법은 두가지가 있다

  ```js
  elList('.ediya-menu__item a')[0]
  elList('.ediya-menu__item a').item(0)
  ```

  두가지 모두 제일 위에 있는 아이템을 가져오지만, 위와 같은 문법을 더 많이 사용한다

* 순환 처리를 위해 each, while, for … forEach 함수를 사용한다. infinity이든 30개든 50개든 아이템을 찾는 수고를 덜 수 있다

  ```js
  menuItemButtons.forEach((item, index)=>{
    console.log(item, index)
  })
  ```

**Programming : Show Detail Modal**

```js
elList('.ediya-menu__item a[role="button"]').forEach(button =>
  button.addEventListener('click', showDetailModal)
)

const showDetailModal = e => {
  const button = e.currentTarget            // 클릭한 버튼(a[role="button"] 요소)
  const modal = button.nextElementSibling   // 버튼에 인접한 다음 요소는 '모달'(div[role="dialog"])
  button.setAttribute('aria-pressed', true) // 버튼 요소를 '누른' 상태로 변경
  modal.removeAttribute('hidden')           // 모달 요소의 hidden 속성 제거
  // 모달 요소에 is-active 클래스 속성 추가
  window.setTimeout(() => modal.classList.add('is-active'), 0)
  // 브라우저 기본 동작 차단
  e.preventDefault()
}
```

* `<a>`에 `href=""` 를 삭제하면 키보드로 포커스가 가지 않음, 그래서 브라우저의 기본 동작을 차단시켰다.

### Part 3 . Front-End Framework

* [React](https://ko.reactjs.org/)
* Node.js
* creat-react-app, creat-react-native-app 등 도구를 활용할 수 있음
* [stackblitz](https://stackblitz.com/) 온라인에서 개발 경험할 수 있음
* `package.json` 프로젝트의 정보를 가지고 있는 파일

**리액트 맛보기**

* 프로젝트 Fork 하기 [내 프로젝트](https://stackblitz.com/edit/react-bndzzz?file=index.js)
* html에서 `class="…"` 로 선언해 주던 방식이 `className="…"` 와 같이 카멜케이스로 작성해줘야한다. JSX 즉 XML 문법
* 컴포넌트를 클래스와 함수 두가지 형태로 제공하고 있다