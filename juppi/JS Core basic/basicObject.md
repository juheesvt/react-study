### 객체 : 연관 배열(associative array)

Javascript엔 8가지 자료형이 존재하는데, 그 중 7개는 오직 하나의 데이터만 담을 수 있는 원시형primitive type 이다

객체형은 원시형과 달리 다양한 데이터를 담을 수 있음

객체는 중괄호`{...}`를 이용해 만들 수 있음. 중관호 안에는 `key: value` 쌍으로 구성된 **property**를 여러개 넣을 수 있는데, `key`에는 문자형, `value`엔 모든 자료형이 허용됨 property key는 property name이라고도 부름

✅ **빈 객체를 만드는 방법**

```jsx
let user = new Object(); // '객체 생성자 문법'
let user = {}; // '객체 리터럴' 문법, 주로 사용
```

✅ **리터럴과 프로퍼티**

중괄호`{...}` 안에는 *key:value*로 구성된 프로퍼티가 들어감

```jsx
// 프로퍼티가 3개 존재하는 객체 user 
let user = {
	name: "John",
	age: 30,

	// 여러 단어를 조합해 프로퍼티 이름을 만든 경우엔 따옴표로 묶어줘야함
	"likes birds": ture, 
	// 마지막 프로퍼티 끝은 쉼표로 끝날 수 있음
	//‘trailing(길게 늘어지는)’ 혹은 ‘hanging(매달리는)’ 쉼표
};

// 점 표기법(dot notation)으로 프로퍼티 값 읽기
alert( user.name );
alert( user.age );

// 대괄호 표기법(square bracket notation)으로 복수의 단어로 만든 프로퍼티 이름의 값 읽기
user["likes birds"] = true;
alert(user["likes birds"]); 

let key = "likes birds";

// user["likes birds"] = true; 와 같음
user[key] = true;
```

✅ **변수 `key`는 런타임에 평가되기 때문에 사용자 입력값 변경 등에 따라 값 변경 가능\**

```jsx
let user = {
  name: "John",
  age: 30
};

let key = prompt("사용자의 어떤 정보를 얻고 싶으신가요?", "name");

// 변수로 접근
alert( user[key] ); // John (프롬프트 창에 "name"을 입력한 경우)
```

**❌ 점 표기법은 위와 같은 방식이 불가능 ❌**

```jsx
let user = {
  name: "John",
  age: 30
};

let key = "name";
alert( user.key ) // undefined
```

✅ **계산된 프로퍼티**

객체 생성시, 객체 리터럴 안의 **프로퍼티 키**가 대괄호`[]` 로 둘러싸여있는 경우, 이를 계산된 프로퍼티라고 부름

```jsx
let fruit = prompt("어떤 과일을 구매하시겠습니까?", "apple");

let bag = {
  [fruit]: 5, // 변수 fruit에서 프로퍼티 이름을 동적으로 받아 옴.
};

alert( bag.apple ); // fruit에 "apple"이 할당되었다면, 5가 출력됨
```

➡️  위 예시에서 `[fruit]`는 프로퍼티 이름을 변수 `fruit`에서 가져오겠다는 것을 의미

➡️ 사용자가 프롬프트 대화상자에 `apple`을 입력했다면 `bag`엔 `{apple: 5}`가 할당되었음

💡**대괄호 표기법은 프로퍼티 이름과 값의 제약을 없애주기 때문에 점 표기법보다 강력함. 하지만 작성하기 번거롭다는 단점이 존재 ! 때문에 단순한 이름엔 점 표기법을, 복잡한 상황이 발생하면 대괄호 표기법으로 바꾸는 경우가 많음**

✅ **단축 프로퍼티**

```jsx
function makeUser(name, age) {
  return {
    name, // name: name 과 같음
    age,  // age: age 와 같음
		sex : "여", // 일반 프로퍼티와 단축 프로퍼티 함께 사용 가능
  };
}
```

➡️ *프로퍼티 값 단축 구문(property value shorthand)* 을 사용하면 코드를 짧게 줄일 수 있음

➡️ `name:name` 대신 `name`만 적어주어도 프로퍼티를 설정

💡**프로퍼티 이름에는 특별한 제약이 없음. 예약어 사용 가능 !**

✅ 자바스크립트 객체는 존재하지 않는 프로퍼티에 접근하면 에러가 아닌 `undefined`를 반환함 !

```jsx
let user = {};

// true는 '프로퍼티가 존재하지 않음'을 의미
alert( user.noSuchProperty === undefined ); 

let user = { name: "John", age: 30 };

alert( "age" in user ); // user.age가 존재하므로 true가 출력됩니다.
alert( "blabla" in user ); // user.blabla는 존재하지 않기 때문에 false가 출력됩니다.
```

✅ 객체 정렬 방식

정수 프로퍼티는 자동 정렬, 그 외의 프로퍼티는 객체에 추가한 순서 그대로 정렬됨

```jsx
let codes = {
  "49": "독일",
  "41": "스위스",
  "44": "영국",
  // ..,
  "1": "미국"
};

for (let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```