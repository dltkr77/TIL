# CSS Basic

CSS는 선택자를 사용해 HTML 요소를 선택하는 다양한 방법을 제공한다. 이번에는 CSS 기본 규칙과 CSS가 제공하는 선택자, 스타일 상속과 캐스케이드, 스타일이 동시에 적용되었을 때 처리되는 방법을 살펴본다.

## CSS Style Rule

스타일 규칙은 문서의 요소에 적용되는 스타일을 결정한다. 각 스타일 규칙은 선택자(Selector)와 선언(Declaration)으로 구성된다. 선언은 다시 속성(Property)과 값(Value)로 구분된다.

* 선택자
* 선언
  * 속성
  * 값

## CSS 선택자(Selector)

선택자는 스타일 규칙 집합이 적용되는 요소를 정의한다. 심플 선택자, 결합 선택자, 복합 선택자 혹은 선택자 목록으로 구분할 수 있다.

### 심플 선택자 (Simple Selector)

* 요소 선택자 (Type selector)
  
  ```
  div { ... }
  p   { ... }
  ```
  
* 전체 선택자 (Universal selector)

  ```
  * { ... }
  ```

* 속성 선택자 (Attribute selector) 

  ```
  [target="_blank"]  { ... }
  [id="logo"]        { ... }
  [class="logo-img"] { ... }
  ```

* 클래스 선택자 (Class selector)

  ```
  .logo-img { ... }
  ```

* 아이디 선택자 (ID selector)

  ```
  #logo { ... }
  ```

* 가상 클래스 선택자 (Pseudo class)

  ```
  :link { ... }
  :visited { ... }
  :hover { ... }
  :active { ... }
  ```

* 가상 요소 선택자 (Pseudo-elements)

  엘리먼트를 가상으로 만들어 주는 기능을 한다. 가상 클래스 선택자와는 `:`, `::` 으로 구분된다.

  ```
  ::first-letter { ... }
  ::first-line   { ... }
  ::before       { ... }
  ::after        { ... }
  ```

### 결합 선택자(Compound Selectors)

콤비네이터로 분리되지 않고 둘 이상의 심플 선택자를 사용한다. 멀티 클래스 선택자로도 불린다

```css
.list-item.is-selected {
  background-color: blue;
}
```

### 복합 선택자 (Complex Selectors)

콤비네이터로 분리된 결합 선택자. 복합 선택자는 콤비네이터에 의해 정의된 특정 관계에서 동시 조건을 나타낸다. 콤비네이터의 종류는 아래와 같다.

* ` ` 자손 콤비네이터 (Descendant combinator): e.g. ` ul li` (whitespace)
* `>` 자식 콤비네이터 (Child combinator): e.g. `div > p`
* `+` 인접 형제 콤비네이터 (Next-sibling combinator): e.g. `p + img`
* `>` 후속 형제 콤비네이터 (Subsequent-sibling combinator): e.g. `ul ~ .myclass`

### 선택자 목록 (Selector Lists)

심플, 결합, 복합 선택자를 `,` 콤마로 구분한다. 여러 선택자에 동일한 스타일을 동시에 적용할 수 있다.

```css
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
}
```

## CSS 상속 (Inheritance)

CSS 속성 중 일부는 상속이 된다. 상속에 대한 개념과 상속이 되는 속성, 그렇지 않은 속성을 알아본다.

**상속 되는 속성 (글자색, 디자인에 관련된 것): **

* color
* font-size
* font-family
* letter-spacing
* line-height

**상속되지 않는 속성 (공간에 관련된 것):**

* outline
* margin
* padding
* border

## CSS 캐스케이드

 동일한 요소에 여러가지 스타일 규칙이 적용되는 경우가 있다. 이런 경우 순서와 명시도(specificity) 계산에 따라 어떤 스타일 규칙이 우선하는지 결정한다.

> Cascade 는 여러 스타일 시트를 결합하고 이들 사이의 충돌을 해결하는 프로세스이다 - [Håkon Wium Lie](https://www.wiumlie.no/2006/phd/)

캐스케이드에서 어떤 선택자가 우선권을 가지는지 결정하는 요인은 세가지이다

1. 중요성(Important)
2. 속성의 명시도(계산된 점수)
3. 소스 순서

### 중요성 (Importance)

스타일에 `!important` 를 선언하면 다른 선언보다 우선하게 한다. MDN에 따르면 이 선언은 스타일 시트에서 cascading을 끊어 디버깅을 더 어렵게 하므로 사용하지 않는것을 권고한다.

 실제 사용시에도 `!importnat` 가 적용된 속성을 덮어 쓰려면, 다시 `!importnat` 를 사용하기 떄문에 사용하지 않도록 노력해야한다.

### 명시도 (Specificity)

선택자가 다른것 보다 높은 명시도(highter specificity)를 가지면 다른 것보다 우선한다. 일반적으로 ID 선택자는 클래스 선택자, 속성 선택자 및 pseudo 클래스보다 우선한다.

W3.org 문서의 9. Calculating a selector's specificity 항목에 선택자의 명시도(specificity)를 계산하는 방법을 제공한다.

* selectors의 ID selectors 수를 계산 (= a)
* selector에서 class selectors, attributes selectors 및 pseudo-classes 수를 계산 (= b)
* selectors의 type selectors 및 pseudo-elements 수를 계산 (= c)
* `*` 와  `>`, `+`, `~` 등 콤비네이터(Combinators)는 무시

```
Examples:

*               /* a=0 b=0 c=0 -> specificity =   0 */
ul              /* a=0 b=0 c=1 -> specificity =   1 */
ul li           /* a=0 b=0 c=2 -> specificity =   2 */
ul ol+li        /* a=0 b=0 c=3 -> specificity =   3 */
h1 + *[href]    /* a=0 b=1 c=1 -> specificity =  11 */
ul ol li.red    /* a=0 b=1 c=3 -> specificity =  13 */
li.red.level    /* a=0 b=2 c=1 -> specificity =  21 */
#logo           /* a=1 b=0 c=0 -> specificity = 100 */
#logo:not()     /* a=1 b=0 c=1 -> specificity = 101 */
!important
```

**명시도 계산 팁**

 선택자의 우선권에 대한 척도를 1, 10, 100, 1000 단위로 생각하면 이해하기 편하다.

| 요소 선택자 | 클래스, Psuedo, Attribute 선택자 | ID 선택자  | 인라인 스타일 |
| ----------- | -------------------------------- | ---------- | ------------- |
| 0, 0, 0, 1  | 0, 0, 1, 0                       | 0, 1, 0, 0 | 1, 0, 0, 0    |

### 소스 순서

`!important`가 선언되지 않았거나 명시도가 동일 또는 설정되지 않은 경우, 스타일 시트에 가장 나중에 배치된 스타일이 우선권을 가진다.

## CSS 선언 (Declaration)

선언은 중괄호 안에 표시된다. 속성과 값의 짝으로 표시한다.

* 속성(Property)
* 값(Value)
* 중요 표시(important flag)

각 선언은 세미 콜론`;` 으로 끝난다.

```
선택자(selector) {
	속성(property): 값(value);
}
```



📖 **참고 자료**

* [W3C CSS Syntax Module Level 3](https://www.w3.org/TR/css-syntax-3/)
* [W3C Selectors Level 3](https://www.w3.org/TR/selectors-3/)
* [MDN CSS selectors](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors)
* [MDN 상속](https://developer.mozilla.org/ko/docs/Web/CSS/inheritance)
* [MDN CSS 속성 인덱스](https://developer.mozilla.org/ko/docs/Web/CSS/Reference)
* [MDN 명시도](https://developer.mozilla.org/ko/docs/Web/CSS/Specificity)
* [CSS Diner - 선택자 학습용 게임](http://flukeout.github.io/)
* [CSS usage on the web platform - 자주 사용하는 속성들](https://developer.microsoft.com/en-us/microsoft-edge/platform/usage/)
* [The average web page - 자주 사용하는 HTML 태그들](https://www.advancedwebranking.com/html/)
* [반드시 기억해야 하는 CSS 선택자 30개](https://code.tutsplus.com/ko/tutorials/the-30-css-selectors-you-must-memorize--net-16048)
* [CSS를 배우는 방법](https://webactually.com/2019/02/css%eb%a5%bc-%eb%b0%b0%ec%9a%b0%eb%8a%94-%eb%b0%a9%eb%b2%95/)

