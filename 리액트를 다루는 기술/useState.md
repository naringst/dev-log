## 기본 구조
const [state, setState] = useState(initialState)

## 특징
- 가장 기본적인 훅
- 함수 컴포넌트에서 상태를 관리해야 할 때 사용

## useState로 counter 구현하기
```
Counter.js

import {useState } from 'react';

const Counter = () => {
	const [value, setValue] = useState(0);

	return(
		<div>
			<p>
				현재 카운터 값은 <b>{value}</b>입니다.
			</p>
		</div>
	);
	
};

export default Counter;
```

- useState가 호출되면 배열을 반환한다. 그 배열의 첫 요소는 상태 값, 두 번째 요소는 상태를 설정하는 함수
- 함수에 파라미터를 넣어서 호출하면 전달받은 파라미터로 값이 바뀌고 컴포넌트가 정상적으로 **리렌더링** 된다.


## 컴포넌트에서 관리해야 할 상태가 여러 개 일때
-> useState를 여러 번 사용




## 공식문서 : https://react.dev/reference/react/useState
- 두 개의 컴포넌트에서 하나의 상태를 공유 할 때
- 두 개의 상위 컴포넌트에서 상태를 만들고, 이를 props로 내려준다.
```javascript
export default function MyApp() {  

const [count, setCount] = useState(0);  

//여기서는 handleClick 자체를 넘겨준다.
function handleClick() {  

setCount(count + 1);  

}  
  

return (  

<div>  

<h1>Counters that update together</h1>  

<MyButton count={count} onClick={handleClick} />  

<MyButton count={count} onClick={handleClick} />  

</div>  

);  

}
```



## setState props로 넘겨주는 방법
React에서 `setState` 함수를 자식 컴포넌트에 props로 넘겨주는 방식은 상태 관리 로직을 부모 컴포넌트에서 자식 컴포넌트로 전달하고자 할 때 사용됩니다. `setState` 자체를 넘겨주는 방식과 함수로 감싸서 넘겨주는 방식 사이에는 중요한 차이점이 있으며, 각각의 사용 사례에 따라 적합한 방식이 달라집니다.

### `setState` 자체를 넘겨주는 경우

- **직접성**: `setState` 함수를 직접 넘겨주면, 자식 컴포넌트는 부모 컴포넌트의 상태를 직접 조작할 수 있습니다. 이 방식은 자식 컴포넌트에게 더 많은 통제력을 부여하며, 부모 컴포넌트의 상태 변경 로직을 자식 컴포넌트가 직접 결정하게 합니다.
- **유연성**: 자식 컴포넌트는 넘겨받은 `setState` 함수를 사용하여 상태를 다양한 방식으로 변경할 수 있습니다. 예를 들어, 상태에 추가, 삭제, 수정 등 다양한 연산을 적용할 수 있습니다.
- **주의 필요**: 이 방식은 자식 컴포넌트가 부모 컴포넌트의 상태를 예기치 않게 변경할 수 있기 때문에 주의가 필요합니다. 상태 관리가 복잡해질 수 있으며, 컴포넌트 간의 결합도가 높아질 수 있습니다.

### 함수로 감싸서 넘겨주는 경우

- **제한적 접근**: 함수로 `setState`를 감싸서 넘겨주는 방식은 자식 컴포넌트가 부모 컴포넌트의 상태를 변경하는 방식을 미리 정의합니다. 이는 자식 컴포넌트가 상태 변경 로직을 알 필요 없이, 특정 행동을 실행하기만 하면 됨을 의미합니다.
- **명확성**: 부모 컴포넌트에서 상태 변경 로직을 명확하게 정의하고, 자식 컴포넌트는 그 로직을 실행하기만 하므로, 상태 변경의 원인과 효과가 더 명확해집니다. 이는 유지보수와 코드 이해에 도움이 됩니다.
- **재사용성과 결합도**: 특정 상태 변경 로직을 함수로 감싸서 넘겨주면, 그 로직을 여러 컴포넌트에서 재사용할 수 있습니다. 또한, 컴포넌트 간의 결합도를 낮출 수 있으며, 상태 변경 로직을 쉽게 변경하거나 확장할 수 있습니다.

### 일반적인 형태

두 방식 중 어느 것이 더 일반적이라고 말하기는 어렵습니다. 상황에 따라 적절한 방식을 선택해야 합니다. 그러나, 코드의 명확성, 재사용성, 유지보수의 용이성을 중시한다면, **함수로 감싸서 넘겨주는 방식**이 더 권장됩니다. 이 방식은 상태 변경 로직을 부모 컴포넌트에서 캡슐화하고, 자식 컴포넌트는 단순히 그 로직을 실행하는 역할을 하도록 함으로써, 좀 더 선언적이고 관리하기 쉬운 코드를 작성할 수 있도록 돕습니다.



## 문제
### 상태를 업데이트 했는데, 로그에 업데이트 되지 않고 뜬다.

`set`함수를 호출해도 **실행 코드의 상태는 변경되지 않습니다** .

```
function handleClick() {  console.log(count);  // 0  setCount(count + 1); // Request a re-render with 1  console.log(count);  // Still 0!  setTimeout(() => {    console.log(count); // Also 0!  }, 5000);}
```

[이는 상태가 스냅샷처럼 동작하기](https://react.dev/learn/state-as-a-snapshot) 때문입니다 . `count`상태를 업데이트하면 새 상태 값으로 또 다른 렌더링이 요청되지만 이미 실행 중인 이벤트 핸들러의 JavaScript 변수에는 영향을 미치지 않습니다 .

다음 상태를 사용해야 하는 경우 함수에 전달하기 전에 변수에 저장할 수 있습니다 `set`.

```
const nextCount = count + 1;setCount(nextCount);console.log(count);     // 0console.log(nextCount); // 1
```

### 상태를 업데이트 했는데 화면 업데이트가 안된다.
비교 를 통해 결정된 대로 **다음 상태가 이전 상태와 같으면** React는 업데이트를 무시합니다 [`Object.is`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is). 이는 일반적으로 상태의 객체나 배열을 직접 변경할 때 발생합니다.

```
obj.x = 10;  // 🚩 Wrong: mutating existing objectsetObj(obj); // 🚩 Doesn't do anything
```

기존 객체를 변경 `obj`하고 다시 전달했기 `setObj`때문에 React가 업데이트를 무시했습니다. [이 문제를 해결하려면 상태에 있는 객체와 배열 을](https://react.dev/reference/react/useState#updating-objects-and-arrays-in-state) [_변경_ _하는_ 대신](https://react.dev/reference/react/useState#updating-objects-and-arrays-in-state) 항상 교체해야 합니다 .

```
// ✅ Correct: creating a new objectsetObj({  ...obj,  x: 10});
```


### useState를 통해 컴포넌트가 리렌더링 되는 조건?
React에서 `useState`를 사용하여 컴포넌트 상태를 관리할 때, 컴포넌트가 리렌더링 되는 시점은 다음과 같은 경우에 발생합니다:

1. **상태 변경**: `useState`에 의해 관리되는 상태가 변경될 때마다 해당 컴포넌트는 리렌더링 됩니다. `setState` 함수를 호출하여 상태를 업데이트하면, React는 새로운 상태를 가지고 컴포넌트 함수를 다시 실행하여 UI를 업데이트합니다. 이는 상태의 변화가 UI에 반영되어야 할 때 중요합니다.

2. **Props 변경**: 부모 컴포넌트로부터 받은 props가 변경되면, 해당 변경 사항이 자식 컴포넌트에 전달되고, 자식 컴포넌트는 이에 따라 리렌더링 됩니다. 만약 부모 컴포넌트에서 자식 컴포넌트로 `setState` 함수를 props로 전달하고, 이 함수가 호출되어 부모 컴포넌트의 상태가 변경된다면, 해당 상태를 props로 받는 자식 컴포넌트도 리렌더링 될 수 있습니다.

3. **부모 컴포넌트 리렌더링**: 부모 컴포넌트가 리렌더링 되면, 그 하위의 자식 컴포넌트들도 기본적으로 리렌더링 됩니다. 다만, React는 Virtual DOM을 사용하여 실제 변경이 필요한 부분만 DOM에 반영하기 때문에, 자식 컴포넌트의 props나 상태가 변경되지 않았다면 실제 DOM에는 영향을 주지 않습니다. 그러나, 자식 컴포넌트의 리렌더링을 최적화하기 위해서는 `React.memo`나 `shouldComponentUpdate` 같은 기법을 사용할 수 있습니다.

`setState` 함수를 하위 컴포넌트에 props로 전달하는 경우, 이 함수가 호출될 때마다 상태 변경 로직이 실행되고, 이로 인해 상태가 업데이트되면 컴포넌트는 자동으로 리렌더링 됩니다. 이는 부모 컴포넌트의 상태를 변경하고, 그 결과로 부모 컴포넌트 뿐만 아니라 상태 변경이 props를 통해 영향을 받는 모든 하위 컴포넌트들도 함께 리렌더링 되는 과정을 포함할 수 있습니다.

따라서, `useState`와 함께 컴포넌트 상태 관리를 할 때는 상태 변경이 필요한 시점과 이로 인한 리렌더링의 영향을 잘 이해하고 관리하는 것이 중요합니다.


### 하위 컴포넌트에서 setState 함수를 호출해서 리렌더링 되는 과정
하위 컴포넌트에서 `setState` 함수를 호출할 때 발생하는 렌더링 과정은 다음과 같이 진행됩니다:

1. **`setState` 호출**: 하위 컴포넌트에서 부모 컴포넌트로부터 받은 `setState` 함수를 호출합니다. 이 함수는 부모 컴포넌트의 상태를 변경하는 로직을 실행합니다.

2. **상태 변경**: React는 `setState` 호출을 통해 요청된 상태 변경을 큐에 넣습니다. React는 이벤트 처리나 비동기 호출 같은 작업이 완료되고, 제어가 이벤트 루프로 돌아갈 때까지 실제로 상태를 변경하지 않을 수도 있습니다. 이는 여러 `setState` 호출을 배치하여 효율적으로 처리하기 위함입니다.

3. **리렌더링 시작**: 상태 변경이 확정되면, React는 해당 컴포넌트를 비롯하여 상태 변경으로 인해 영향을 받는 모든 컴포넌트의 리렌더링을 시작합니다. 리렌더링 과정에서는 컴포넌트 함수나 클래스 컴포넌트의 `render` 메소드가 다시 호출됩니다.

4. **가상 DOM 비교**: 새로운 상태를 반영하여 생성된 가상 DOM과 이전 렌더링에서 생성된 가상 DOM을 비교합니다. React는 이 비교 과정을 통해 실제 DOM에 반영해야 할 변경 사항을 결정합니다.

5. **DOM 업데이트**: 변경 사항이 확인되면, React는 실제 DOM을 최소한의 연산으로 업데이트합니다. 이는 컴포넌트의 실제 UI 변경으로 이어집니다.

6. **컴포넌트 업데이트 완료**: 모든 DOM 업데이트가 완료되면, 컴포넌트의 리렌더링 과정이 완료됩니다. 클래스 컴포넌트의 경우, `componentDidUpdate` 같은 생명주기 메소드가 호출될 수 있으며, 함수 컴포넌트에서는 `useEffect` 훅의 클린업 함수와 의존성 배열에 따른 실행이 이어질 수 있습니다.

이 과정은 React의 선언적 UI 패러다임을 기반으로 합니다. 개발자는 상태가 어떻게 변화해야 하는지를 선언하고, React는 가장 효율적인 방식으로 UI를 해당 상태에 맞게 업데이트합니다. 이렇게 함으로써, 상태 관리 로직과 UI 업데이트 사이의 복잡성을 대폭 줄일 수 있습니다.



## 하위 컴포넌트가 setState를 받는 방식(직접, 함수로 감싸서)에 따른 차이 ?
그러면 하위 컴포넌트가 props로 setState를 받을 때 직접 받는게 아니라 함수로 한번 감싸서 받아도 똑같아? (예를 들면 handleClick = () => setState(state+1) )


네, 원칙적으로는 하위 컴포넌트가 `setState`를 직접 받든, 함수로 한 번 감싸서 받든 상태 변경의 결과와 리렌더링의 과정에 있어서는 큰 차이가 없습니다. 중요한 것은 상태 변경이 일어나고 이 변경이 리액트 컴포넌트 트리에 어떻게 반영되는지입니다.

하위 컴포넌트에서 함수로 감싸서 `setState`를 받는 경우 (예: `handleClick = () => setState(state+1)`), 이 함수는 부모 컴포넌트의 상태 변경 로직을 추상화하고 있습니다. 이 방식의 장점은:

1. **추상화**: 하위 컴포넌트는 상태 변경 로직의 세부 사항을 몰라도 됩니다. 즉, 하위 컴포넌트는 단순히 버튼 클릭 등의 이벤트에 반응하여 부모 컴포넌트에 정의된 함수를 호출하기만 하면 됩니다.

2. **재사용성**: 같은 상태 변경 로직을 여러 컴포넌트에서 재사용할 수 있습니다. 예를 들어, 여러 버튼이나 입력 필드에서 같은 상태 변경 함수를 사용할 수 있습니다.

3. **캡슐화와 유지보수**: 상태 변경 로직을 부모 컴포넌트에 캡슐화함으로써, 이 로직을 변경할 필요가 있을 때 하위 컴포넌트를 수정하지 않고도 부모 컴포넌트에서만 변경을 관리할 수 있습니다. 이는 유지보수성을 향상시킵니다.

함수로 감싸서 `setState`를 넘겨받을 때와 직접 `setState`를 넘겨받을 때의 주요 차이는, 함수로 감싸서 넘겨받는 경우에는 그 함수가 호출될 때만 상태가 변경된다는 점입니다. 이 방식은 상태 변경 로직을 더 명확하게 관리할 수 있게 해주며, 상태 변경의 의도를 더 명확하게 표현할 수 있습니다.

결국, `setState`를 직접 넘기는 방식이든, 함수로 감싸서 넘기는 방식이든, 상태 변경이 발생하면 해당 변경 사항에 의존하는 모든 컴포넌트의 리렌더링이 트리거됩니다. 선택하는 방식은 주로 코드의 명확성, 재사용성, 유지보수성 등의 고려 사항에 따라 달라질 수 있습니다.


## 상태의 객체 및 배열 업데이트

객체와 배열을 상태로 만들 수 있습니다. React에서 상태는 읽기 전용으로 간주되므로 **기존 객체를** **_변경하기_** **보다는 상태를** **_교체_** **해야 합니다** . 예를 들어 상태에 있는 객체가 있는 경우 `form`해당 객체를 변경하지 마세요.


```
// 🚩 Don't mutate an object in state like this:form.firstName = 'Taylor';
```

대신 새 객체를 생성하여 전체 객체를 교체하세요.

```
// ✅ Replace state with a new objectsetForm({  ...form,  firstName: 'Taylor'});
```

상태는 객체를 포함한 모든 종류의 JavaScript 값을 보유할 수 있습니다. 하지만 React 상태에 있는 객체를 직접 변경해서는 안 됩니다. 대신, 객체를 업데이트하려면 새 객체를 생성하거나 기존 객체의 복사본을 만든 다음 해당 복사본을 사용하도록 상태를 설정해야 합니다.
-> dom에서는 요소가 같으면 업데이트 하지 않음.

### 이렇게 해야 하는이유?
React에서 `setState`를 사용하여 객체 상태를 업데이트할 때 스프레드 연산자(`...`)를 사용하는 것은 불변성(Immutability)을 유지하기 위함입니다. 불변성을 유지하는 것은 React의 상태 관리 및 성능 최적화에 중요한 역할을 합니다. 여기에는 여러 이유가 있습니다:

### 1. 변경 감지
React는 상태나 props가 변경되었는지 감지하기 위해 얕은 비교(shallow comparison)를 수행합니다. 객체의 불변성을 유지하면, 객체의 참조가 변경될 때만 React가 변화를 감지하고 컴포넌트를 리렌더링하게 됩니다. 만약 객체를 직접 수정한다면, 객체의 참조가 변하지 않아 React가 변화를 감지하지 못하고 결과적으로 UI가 업데이트되지 않을 수 있습니다.

### 2. 순수 컴포넌트 최적화
`React.PureComponent`나 `React.memo`는 props나 상태의 얕은 비교를 통해 컴포넌트가 리렌더링할 필요가 있는지 결정합니다. 불변성을 유지하면 이러한 최적화 기법이 제대로 작동하여 불필요한 리렌더링을 방지할 수 있습니다.

### 3. 예측 가능한 상태 관리
불변성을 유지하면 상태 변화를 추적하기 쉬워집니다. 상태 변경이 발생할 때마다 새로운 객체를 생성하기 때문에, 어느 지점에서 상태가 변경되었는지 더 쉽게 파악할 수 있으며, 이전 상태를 변경하지 않고도 이전 상태를 유지할 수 있습니다. 이는 디버깅과 상태 관리를 더욱 쉽게 만듭니다.

### 스프레드 연산자 사용 예시

스프레드 연산자를 사용하지 않고 객체 상태를 직접 변경하는 경우:

```javascript
this.setState({
  myObject: {
    ...this.state.myObject,
    key: newValue
  }
});
```

위 코드에서 `...this.state.myObject`는 현재 상태의 `myObject`를 새 객체로 복사하고, `key: newValue`를 통해 필요한 값만 업데이트합니다. 이 방법으로 `myObject`의 불변성을 유지하면서 상태를 업데이트할 수 있습니다.

반면에, 객체를 직접 수정하는 방식은 React에서 권장하지 않는 패턴입니다. 예를 들어, `this.state.myObject.key = newValue`와 같이 상태를 직접 변경하고 `this.setState()`를 호출해도 React는 이전 상태와 새 상태가 같은 객체를 참조하고 있다고 판단하여 UI를 업데이트하지 않습니다.

결론적으로, 스프레드 연산자를 사용하여 상태 객체를 복사하고 업데이트하는 방식은 React에서 상태의 불변성을 유지하고, 애플리케이션의 성능을 최적화하며, 상태 변화를 예측 가능하게 만드는 데 필수적입니다.




## 중첩된 개체 업데이트[](https://react.dev/learn/updating-objects-in-state#updating-a-nested-object "중첩된 개체 업데이트 링크")

다음과 같은 중첩된 객체 구조를 고려해보세요.

```
const [person, setPerson] = useState({  name: 'Niki de Saint Phalle',  artwork: {    title: 'Blue Nana',    city: 'Hamburg',    image: 'https://i.imgur.com/Sd1AgUOm.jpg',  }});
```

업데이트하고 싶다면 `person.artwork.city`돌연변이를 사용하여 수행하는 방법이 명확합니다.

```
person.artwork.city = 'New Delhi';
```

하지만 React에서는 상태를 불변으로 취급합니다! 을 변경하려면 먼저 새 객체(이전 객체의 데이터로 미리 채워져 있음)를 생성한 다음 새 객체를 가리키는 새 객체를 생성 `city`해야 합니다 .`artwork``person``artwork`

```
const nextArtwork = { ...person.artwork, city: 'New Delhi' };const nextPerson = { ...person, artwork: nextArtwork };setPerson(nextPerson);
```

또는 단일 함수 호출로 작성됩니다.

```
setPerson({  ...person, // Copy other fields  artwork: { // but replace the artwork    ...person.artwork, // with the same one    city: 'New Delhi' // but in New Delhi!  }});
```