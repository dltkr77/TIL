# 포폴.데브

일시: 2019.11.16(토)

[포폴.데브 튜토리얼](https://pofol.dev/tutorials/)

## Terminal

- `.` 현재 디렉토리
- `..` 상위 디렉토리

- `brew uninstall …` : 패키지 삭제 용이함 

## HTML

* [HTML Cheat Sheet (New HTML5 Tags Included)](https://www.hostinger.com/tutorials/html-cheat-sheet)

## CSS

- 스타일 (font-size)는 부모 요소 (parent)의 스타일에 영향을 받게 된다. 이 경우 부모 요소가 아닌 절대 루트 요소에 기준을 맞추는 단위로 rem을 사용한다 

- 검색의 생활화. 쓰는 시간보다 읽는 시간이 더 길다 

- [CSS 선택자 연습 게임](https://flukeout.github.io/ ) 등을 주기적으로 연습하는것이 필요

  - 오늘 해봤을 때 찾은 내가 자주 사용하지 않는 선택자 

  ```markdown
  General Sibling Selector 
  
  Select elements that follows another element 
  
  A ~ B 
  
  You can select all siblings of an element that follow it. This is like the Adjacent Selector (A + B) except it gets all of the following elements instead of one. 
  Examples 
  
  A ~ B selects all B that follow a A 
  ```

## 배포

- [Netlify](https://www.netlify.com/)
- 코드가 수정되면, Production deploys 에서 다시 드래그앤드롭으로 배포한다 

## Javascript

### 값

* 숫자

* 식

  ```
  1 + 1
  5 * 10
  1 < 2
  ```

* 글자(문자열)
  
    ```
    `역따옴표 문자열`
    '따옴표 문자열'
    "쌍따옴표 문자열"
    ```
    
    * ` `` `은 줄 바꿈을 지원한다
    
* 참/거짓
  
    * 부등호, ===, !== (반대)

### 변수 / 상수

* `const` 변하지 않는 값, 상수
* `let` 변하는 값, 변수

### 함수(기능)

* 호출

  ```
  name()
  ```

  예제로 컨펌 창을 열고 닫는 코드

  ```
  confirm(): ok
  confirm(): false
  ```

* 내장함수 외에 직접 함수를 만들 수도 있다

  ```
  const bark = () => {
    alert('멍멍')
  }
  ```

* 입력 받기

  ```
  const hello = (name) => {
    alert(`Hello,` + name)
  }
  
  hello(`hy`)
  ```

* 반환

  ```
  const double = (number) => {
    return number * 2
  }
  
  double(4)
  ```

* DOM 선택

   document 한 페이지의 모든 문서 내용은 document로 호출할 수 있다

  ```
  document.querySelector('#first’)
  ```

  document.querySelector('#first’): #first인 엘리먼트를 가지고 온다

  ```
  document.querySelectorAll('.odd’)
  ```

  .odd 클래스를 가지고 있는 모든 노드를 다 불러온다

 조건문, 반복문 등…. 자바스크립트의 기본 문법은 모두 배우게 된 것~!0!

## Gatsby

* 설치

  ```
  npx gatsby new my-portfolio https://github.com/pofoldev/pofol-dev-starter
  ```

* 실행

  ```
  npx gatsby develop
  ```

  내 컴퓨터에서 gatsby로 만들어진 사이트를 띄워준다. `http://localhost:8000/` 에서 확인할 수 있다.

*  자바스크립트에서 함수를 이용하기 위해는 함수가 정의되어있어야한다. 기본적으로 자바스크립트에 정의된 함수도 있지만, reacte라는 프레임웍에서 만들어둔 함수를 사용한다

* `<head>`의 역할로 `<helmet>`을 사용함

  ```
  import Helmet from ‘react-helmet'
  
  <Helmet>
  ...
  </Helmet> 
  ```

  기본적으로 사용하는 코드가 많아 사용자에게 노출 시키지 않고 추가할 수 있는 기능이라고 볼 수 있다

## Webfont

화면에 시스템 기본 폰트를 사용하면, 사용자마다 다른 폰트가 보여지게 된다. OS별로 각자 다른 디자인 스타일을 가지고 있다. 그래서, 웹 폰트를 추가해서 사용자의 화면에 의도된 디자인이 적용되도록 만든다.

###  주요 웹폰트 서비스

- https://fonts.google.com/ 한국어도 있음. 주로 무료 
- https://typolink.co.kr/ 주로 한국어. 주로 유료. 개인사용자 10,000회/월 까지 무료 
- https://fonts.adobe.com/fonts 주로 영어 
- https://noonnu.cc/ 한국어 무료 

`font-family`에 있는 따옴표 (혹은 쌍따옴표)는 어느것을 써도 상관은 없다. 작업자의 취향이라고 볼 수 있다. 

 다만 코드는 사람이 읽기에도 좋아야 하기 때문에, 가급적 일관성을 맞춰 사용하는것이 좋다. 사전에 규칙을 정한 후 작업하는것을 추천!

## Layout

* 큰 덩어리를 점점 잘게 쪼개 나가는 방식과 컬럼으로 나누는 방식이 있다
* 최근 디바이스가 다양해지면서 주목받는 방식 
  * 큰 덩어리를 점점 잘게 쪼개고 
  * 이 쪼개는 방식을 용이하게 하는건 `flex`
* **꿀팁** - `키워드 + cheat sheet` 로 검색하면 속성을 사용하는 방법 등을 알려주는 친절한 사이트들이 있다 [Flex Cheat sheet](https://yoksel.github.io/flex-cheatsheet/)
* `box-sizing`: 기본값은`content-box`. `border-box`를 주면 보더의 넓이가 박스 사이즈에 포함된다 
  * 맨 첨 CSS에 `box-sizing`을 `bodrder-box`로 바꾸고 사용하는것을 추천 



아래는 실습 진행하며 기록한 내용

* 모든 jsx 파일은 기본적으로 `import`, `함수`, `함수의 export` 를 가진다

* gatsby에서 지원하는 Link 엘리먼트 사용하기

  1. `import {Link} from 'gatsby'` 선언

  2. Link 사용

     ```jsx
     <Link to ="/work2">
       <img src="/images/2.jpg" alt="image2" />
     </Link>
     ```

     일반 a 태그는 새로운 페이지를 새로 읽어오는데, 개츠비의 link는 자바스크립트로 해당 부분만 불러와준다

* 모든 페이지를 전체 복사해 붙여넣는것은 Bad practice

  * 예를 위 방법으로 작업을 진행한 경우, 공통으로 사용하는 요소들 중에 변경사항이 발생하면 모든 페이지에 들어가 수정해줘야하는 상황이 발생한다.
  * 공통적으로 사용하는 부분은 layout을 만들어 해결한다.

* 현재 상황에서 작업후 배포할 때, html파일이 없어 에러가 발생할것

  * js코드를 html로 바꿔주는 과정이 필요함
  * `npx gatsby build` 명령어 실행

## 후기

* [1차 워크샵 결과물](https://github.com/pofoldev/result-first-workshop)

 일단 내가 뚝딱뚝딱 작업한 결과물과, 쌤이 올려주신 1차 워크샵 결과물을 링크로 남겨둔다. Layout을 분리시키고 `{props.children}` 같은 코드로 반복되는 부분을 분리시켜두었었는데, 자세한 내용은 좀더 들여봐야지!