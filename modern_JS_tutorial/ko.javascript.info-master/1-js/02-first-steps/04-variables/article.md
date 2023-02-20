# 변수와 상수

대다수의 자바스크립트 애플리케이션은 사용자나 서버로부터 입력받은 정보를 처리하는 방식으로 동작합니다. 아래와 같이 말이죠.
1. 온라인 쇼핑몰 -- 판매 중인 상품이나 장바구니 등의 정보
2. 채팅 애플리케이션 -- 사용자 정보, 메시지 등의 정보

변수는 이러한 정보를 저장하는 용도로 사용됩니다.

## 변수

[변수(variable)](https://en.wikipedia.org/wiki/Variable_(computer_science))는 데이터를 저장할 때 쓰이는 '이름이 붙은 저장소' 입니다. 온라인 쇼핑몰 애플리케이션을 구축하는 경우 상품이나 방문객 등의 정보를 저장할 때 변수를 사용하죠.

자바스크립트에선 `let` 키워드를 사용해 변수를 생성합니다.

아래 문(statement)은 'message'라는 이름을 가진 변수를 생성(*선언*)합니다.

```js
let message;
```

이제 할당 연산자 `=`를 사용해 변수 안에 데이터를 저장해 봅시다.

```js
let message;

*!*
message = 'Hello'; // 문자열을 저장합니다.
*/!*
```

문자열이 변수와 연결된 메모리 영역에 저장되었기 때문에, 변수명을 이용해 문자열에 접근할 수 있게 되었습니다.

```js run
let message;
message = 'Hello!';

*!*
alert(message); // 변수에 저장된 값을 보여줍니다.
*/!*
```

아래와 같이 변수 선언과 값 할당을 한 줄에 작성할 수도 있습니다.

```js run
let message = 'Hello!'; // 변수를 정의하고 값을 할당합니다.

alert(message); // Hello!
```

한 줄에 여러 변수를 선언하는 것도 가능합니다.

```js no-beautify
let user = 'John', age = 25, message = 'Hello';
```

이렇게 작성하면 코드가 좀 더 짧아 보이긴 하지만 권장하는 방법은 아닙니다. 가독성을 위해 한 줄에는 하나의 변수를 작성해주세요.

한 줄에 한 개의 변수를 작성하면 코드가 길어 보이지만 읽기엔 편합니다.

```js
let user = 'John';
let age = 25;
let message = 'Hello';
```

어떤 사람들은 이런 방식으로도 변수를 정의합니다.
```js no-beautify
let user = 'John',
  age = 25,
  message = 'Hello';
```

'쉼표가 먼저 오는' 방식으로 작성하는 사람도 있습니다.

```js no-beautify
let user = 'John'
  , age = 25
  , message = 'Hello';
```

위에서 소개한 방식들에 기술적인 차이가 있지는 않습니다. 개인의 취향과 미적 감각에 따라 원하는 방식으로 코드를 작성하세요.

````smart header="`let` 대신 `var`"
만들어진 지 오래된 스크립트에서 `let` 대신 `var`라는 키워드를 발견하는 경우가 있습니다.

```js
*!*var*/!* message = 'Hello';
```

`var`는 `let`과 *거의* 동일하게 동작합니다. `var`도 `let`처럼 변수를 선언하는 데 쓰이죠. 다만 `var`는 '오래된' 방식입니다.

`let`과 `var`의 미묘한 차이점에 대해선 추후 <info:var> 에서 자세히 다루도록 하겠습니다. 지금 시점에선 이 차이점이 중요하지 않기 때문에 넘어가도록 합시다.
````

## 현실 속의 비유

'상자' 안에 데이터를 저장하는데, 이 상자에는 특별한 이름표가 붙어 있다고 상상해 봅시다. 이렇게 하면 '변수'를 좀 더 쉽게 이해할 수 있습니다.

예를 들어, 변수 `message`는 `message`라는 이름표가 붙어있는 상자에 `"Hello!"`라는 값을 저장한 것이라고 생각할 수 있습니다.

![](variable.svg)

상자 속엔 어떤 값이든지 넣을 수 있습니다.

원하는 만큼 값을 변경할 수도 있습니다.
```js run
let message;

message = 'Hello!';

message = 'World!'; // 값이 변경되었습니다.

alert(message);
```

값이 변경되면, 이전 데이터는 변수에서 제거됩니다.

![](variable-change.svg)

변수 두 개를 선언하고, 한 변수의 데이터를 다른 변수에 복사할 수도 있습니다.

```js run
let Hello = 'Hello world!';

let message;

*!*
// Hello의 'Hello world' 값을 message에 복사합니다.
message = Hello;
*/!*

// 이제 두 변수는 같은 데이터를 가집니다.
alert(Hello); // Hello world!
alert(message); // Hello world!
```

````warn header="변수를 두 번 선언하면 에러가 발생합니다."
변수는 한 번만 선언해야 합니다.

같은 변수를 여러 번 선언하면 에러가 발생합니다.

```js run
let message = "This";

// 'let'을 반복하면 에러가 발생합니다.
let message = "That"; // SyntaxError: 'message' has already been declared
```
따라서 변수는 딱 한 번만 선언하고, 선언한 변수를 참조할 때는 `let` 없이 변수명만 사용해 참조해야 합니다.
````

```smart header="함수형 언어"
[함수형(functional)](https://en.wikipedia.org/wiki/Functional_programming) 프로그래밍 언어는 변숫값 변경을 금지합니다. [스칼라(Scala)](http://www.scala-lang.org/)와 [얼랭(Erlang)](http://www.erlang.org/)은 대표적인 함수형 언어입니다.

이들 언어에서는 '상자 속에' 값이 일단 저장되면, 그 값을 영원히 유지합니다. 다른 값을 저장하고 싶다면 새로운 상자를 만들어야(새 변수를 선언해야)만 합니다. 이전 변수를 재사용할 수 없습니다.

처음 봤을 땐 좀 이상해 보일 수 있지만, 함수형 언어는 중대한 개발에 상당히 적합한 언어입니다. 이런 제약이 장점으로 작용하는 병렬 계산(parallel computation)과 같은 영역도 있죠. 당장은 사용할 계획이 없더라도 이런 언어를 공부하는 것은 시야를 넓히는 데 도움이 되므로, 학습을 권유 드립니다.
```

## 변수 명명 규칙

자바스크립트에선 변수 명명 시 두 가지 제약 사항이 있습니다.

1. 변수명에는 오직 문자와 숫자, 그리고 기호 `$`와 `_`만 들어갈 수 있습니다.
2. 첫 글자는 숫자가 될 수 없습니다.

다음은 유효한 변수명의 예시입니다.

```js
let userName;
let test123;
```

여러 단어를 조합하여 변수명을 만들 땐 [카멜 표기법(camelCase)](https://en.wikipedia.org/wiki/CamelCase)이 흔히 사용됩니다. 카멜 표기법은 단어를 차례대로 나열하면서 첫 단어를 제외한 각 단어의 첫 글자를 대문자로 작성합니다. `myVeryLongName`같이 말이죠.

달러 기호 `'$'` 와 밑줄 `'_'` 를 변수명에 사용할 수 있다는 점이 조금 특이하네요. 이 특수 기호는 일반 글자처럼 특별한 의미를 지니진 않습니다.

아래는 유효한 변수명에 관한 예시입니다.

```js run untrusted
let $ = 1; // '$'라는 이름의 변수를 선언합니다.
let _ = 2; // '_'라는 이름의 변수를 선언합니다.

alert($ + _); // 3
```

아래는 잘못된 변수명의 예시입니다.

```js no-beautify
let 1a; // 변수명은 숫자로 시작해선 안 됩니다.

let my-name; // 하이픈 '-'은 변수명에 올 수 없습니다.
```

```smart header="대·소문자 구별"
`apple`와 `AppLE`은 서로 다른 변수입니다.
```

````smart header="비 라틴계 언어도 변수명에 사용할 수 있지만 권장하진 않습니다."
키릴 문자, 심지어 상형문자도 변수명에 사용할 수 있습니다. 모든 언어를 변수명에 사용할 수 있죠.

```js
let имя = '...';
let 我 = '...';
```

위 코드에는 기술적인 에러가 없습니다. 변수명도 유효합니다. 하지만 영어를 변수명에 사용하는 것이 국제적인 관습이므로, 변수명은 영어를 사용해서 만들길 권유 드립니다. 다른 나라 사람이 스크립트를 볼 경우 등을 대비해 장기적인 안목을 가지고 코드를 작성합시다.
````

````warn header="예약어"
[예약어(reserved name) 목록](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)에 있는 단어는 변수명으로 사용할 수 없습니다. 이 단어들은 자바스크립트 내부에서 이미 사용 중이기 때문입니다.

예약어 예시: `let`, `class`, `return`, `function`

아래 코드는 문법 에러를 발생시킵니다.

```js run no-beautify
let let = 5; // 'let'을 변수명으로 사용할 수 없으므로 에러!
let return = 5; // 'return'을 변수명으로 사용할 수 없으므로 에러!
```
````

````warn header="`use strict` 없이 할당하기"

변수는 대개 정의되어 있어야 사용할 수 있습니다. 그러나 예전에는 `let` 없이도 단순하게 값을 할당해 변수를 생성하는 것이 가능했습니다. `use strict`를 쓰지 않으면 과거 스크립트와의 호환성을 유지할 수 있기 때문에 여전히 이 방식을 사용할 수 있습니다.

```js run no-strict
// 참고: 이 예제에는 "use strict"가 없습니다.

num = 5; // 변수 'num'이 정의되어있지 않더라도, 단순 할당만으로 변수가 생성됩니다.

alert(num); // 5
```

이렇게 변수를 생성하는 것은 나쁜 관습입니다. 엄격 모드에서 에러를 발생시키기 때문이죠.

```js
"use strict";

*!*
num = 5; // error: num is not defined
*/!*
```
````

## 상수

변화하지 않는 변수를 선언할 땐, `let` 대신 `const`를 사용합니다.

```js
const myBirthday = '18.04.1982';
```

이렇게 `const`로 선언한 변수를 '상수(constant)'라고 부릅니다. 상수는 재할당할 수 없으므로 상수를 변경하려고 하면 에러가 발생합니다.

```js run
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```

변숫값이 절대 변경되지 않을 것이라 확신하면, 값이 변경되는 것을 방지하면서 다른 개발자들에게 이 변수는 상수라는 것을 알리기 위해 `const`를 사용해 변수를 선언하도록 합시다.


### 대문자 상수

기억하기 힘든 값을 변수에 할당해 별칭으로 사용하는 것은 널리 사용되는 관습입니다.

이런 상수는 대문자와 밑줄로 구성된 이름으로 명명합니다.

예시로 웹에서 사용하는 색상 표기법인 16진수 컬러 코드에 대한 상수를 한번 만들어보겠습니다.

```js run
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// 색상을 고르고 싶을 때 별칭을 사용할 수 있게 되었습니다.
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```

대문자로 상수를 만들어 사용하면 다음과 같은 장점이 있습니다.

- `COLOR_ORANGE`는 `"#FF7F00"`보다 기억하기가 훨씬 쉽습니다.
- `COLOR_ORANGE`를 사용하면 `"#FF7F00"`를 사용하는 것보다 오타를 낼 확률이 낮습니다.
- `COLOR_ORANGE`가 `#FF7F00`보다 훨씬 유의미하므로, 코드 가독성이 증가합니다.

그렇다면 언제 일반적인 방식으로 상수를 명명하고, 언제 대문자를 사용해서 명명해야 하는 걸까요? 명확히 짚고 넘어갑시다.

'상수'는 변수의 값이 절대 변하지 않음을 의미합니다. 그중에는 (빨간색을 나타내는 16진수 값처럼) 코드가 실행되기 전에 이미 그 값을 알고 있는 상수도 있고, 런타임 과정에서 *계산되지만* 최초 할당 이후 값이 변하지 않는 상수도 있습니다.

예시:
```js
const pageLoadTime = /* 웹페이지를 로드하는데 걸린 시간 */;
```

`pageLoadTime`의 값은 페이지가 로드되기 전에는 정해지지 않기 때문에 일반적인 방식으로 변수명을 지었습니다. 하지만 이 값은 최초 할당 이후에 변경되지 않으므로 여전히 상수입니다.

정리하자면, 대문자 상수는 '하드 코딩한' 값의 별칭을 만들 때 사용하면 됩니다.

## 바람직한 변수명

변수에 관한 매우 중요한 사실이 한 가지 더 있습니다.

변수명은 간결하고, 명확해야 합니다. 변수가 담고있는 것이 무엇인지 잘 설명할 수 있어야 하죠.

변수의 이름을 짓는 것은 프로그래밍에서 가장 중요하고 복잡한 기술 중 하나입니다. 변수명만 슬쩍 봐도 초보자가 코드를 작성했는지, 노련한 개발자가 작성했는지 알 수 있습니다.

실제 프로젝트에선 맨 처음부터 완전히 독립적인 코드를 작성하기보다 기존 코드의 틀을 변경하고 확장하는데 대부분의 시간을 보냅니다. 작성했던 코드를 얼마 후에 다시 봤을 때, 정보에 알맞은 이름이 적혀있으면 정보를 더 쉽게 찾을 수 있습니다. 다시 말해, 변수가 올바른 이름을 가졌을 때 말이죠.

그러므로 변수를 선언하기 전에 내가 지은 변수의 이름이 괜찮은지 숙고해 주시기 바랍니다.

아래는 변수 명명 시 참고하기 좋은 규칙입니다.

- `userName` 이나 `shoppingCart`처럼 사람이 읽을 수 있는 이름을 사용하세요.
- 무엇을 하고 있는지 명확히 알고 있지 않을 경우 외에는 줄임말이나 `a`, `b`, `c`와 같은 짧은 이름은 피하세요.
- 최대한 서술적이고 간결하게 명명해 주세요. `data`와 `value`는 나쁜 이름의 예시입니다. 이런 이름은 아무것도 설명해주지 않습니다. 코드 문맥상 변수가 가리키는 데이터나 값이 아주 명확할 때에만 이런 이름을 사용합시다.
- 자신만의 규칙이나 소속된 팀의 규칙을 따르세요. 만약 사이트 방문객을 'user'라고 부르기로 했다면, 이와 관련된 변수를 `currentVisitor`나 `newManInTown`이 아닌 `currentUser`나 `newUser`라는 이름으로 지어야 합니다.

간단해 보이나요? 그렇게 보이긴 합니다. 그러나 실전에서 서술적이고 간결한 변수명을 짓는 것은 간단하지 않습니다. 그럼, 화이팅!

```smart header="재사용 아니면 새로 만들기?"
개발자 중에는 새로운 변수를 선언하기보다 기존 변수를 재사용 하는 걸 선호하는 게으른 분들이 있습니다.

재사용된 변수는 과거에 붙여진 스티커를 떼지 않은 채 물건만 바뀐 상자와 같습니다. 상자 안에는 무엇이 들어 있을까요? 내용물에 대한 정보를 알고 있는 사람은 누구인가요? 이를 알기 위해선 상자에 가까이 다가가 확인해야만 합니다.

변수를 재사용하면 변수 선언에 쏟는 노력을 좀 덜 순 있겠지만, 디버깅에 열 배 더 많은 시간을 쏟아야 합니다.

변수를 추가하는 것은 악습이 아닙니다. 좋은 습관입니다.

모던 자바스크립트 압축기(minifier)와 브라우저는 코드 최적화를 잘해줍니다. 변수를 추가한다고 해서 성능 이슈가 생기지 않죠. 값이 다른 경우, 변수를 다르게 선언해 주면 코드 최적화에 도움이 될 수도 있습니다.
```

## 요약

`var`, `let`, `const`를 사용해 변수를 선언할 수 있습니다. 선언된 변수엔 데이터를 저장할 수 있죠.

- `let` -- 모던한 변수 선언 키워드입니다.
- `var` -- 오래된 변수 선언 키워드입니다. 잘 사용하지 않습니다. `let`과의 미묘한 차이점은 <info:var> 챕터에서 다루도록 하겠습니다.
- `const` -- `let`과 비슷하지만, 변수의 값을 변경할 수 없습니다.

변수명은 변수가 담고 있는 것이 무엇인지 쉽게 알 수 있도록 지어져야 합니다.