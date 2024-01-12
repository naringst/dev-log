# 필요성
아래 예시처럼 다른 타입들에 대해 동일한 연산을 해주고 싶을 때, 모든 타입을 union으로 넣어 계산할 수도 있지만, 이를 간편하게 하려면 generic을 사용할 수 있다.
```typescript

function getArrayLength(arr:number[]):number{
	return arr.length;
}

const array1 = [ 1,2,3];
const array2 = ['a','b','c'];
const array3 = [true,false,true]

getArrayLength(array1);
getArrayLength(array2);
getArrayLength(array3);
```

# 사용 방법
###  예시1
```typescript

function getArrayLength<T>(arr:T[]):number{
	return arr.length;
}

const array1 = [ 1,2,3];
const array2 = ['a','b','c'];
const array3 = [true,false,true]

getArrayLength<number>(array1);
getArrayLength<string>(array2);
getArrayLength<boolean>(array3);
```

### 예시2
Vehicle 인터페이스를 사용해서 두 개의 다른 car, bike의 타입을 지정해주고 싶다. 
이때에도 제네릭을 사용할 수 있다.
달라지는 부분에 대해서만 제네릭으로 설정하면 된다.
```typescript
interface Vehicle<T> {
	name : string;
	color : string;
	option : T;
}

const car:Vehicle<{price:number;}> = {
	name : 'Car',
	color : 'red',
	option : {
		price: 1000
	}
} 

const bike:Vehicle<boolean> = {
	name :'bike',
	color:'green',
	option:true;
}
```

## 장점
- 재사용성이 높은 함수와 클래스를 생성할 수 있다.
- any 처럼 타입을 직접 지정하지 않지만, 타입을 체크해 컴파일러가 오류를 찾을 수 있게 된다.


# 함수에 매개변수가 두개라면?
```typescript
const makeArr =<X,Y=string> (x:X,y:Y): [X,Y] => {
	return [x,y];
}

const array1 = makeArr<number,number>(4,5);
const array2 = makeArr<string,string>('a','b')
const array3 = makeArr<string>('a','b')
```

## extends와 제네릭 사용⭐️
makeFullName이라는 함수에 firstName, lastName 파라미터는 항상 입력받고, 나머지는 옵션으로 넣어줄 수도 있고, 아닐 수도 있을 때 extends와 제네릭을 사용하면 된다!

```typescript
const makeFullName = <T extends {firstName : string, lastName : string}>(obj:T) =>{
	return {
		...obj,
		fullName : obj.firstName + ' ' + obj.lastName	
	}
}

makeFullName({firstName : 'Miki', lastName : 'Jeong', location : 'Seoul'})

```

# 리액트에서 제네릭
아래와 같은 상황에서, 컴포넌트 props로 뭐가 올지 모르기에 Generic을 사용합니다.
useState도 Generic 타입을 받습니다.

```typescript

interface Props {
	name : string;
}

const ReactComponent: React.FC<Props> = ({name}) => {
	const [state] = useState<{name:string|null}>({name :""});
	return <div>{name}</div>
}
```


# 질문
- 리액트에서 제네릭 부분 이해 안됨
	- 그냥 리액트에서 이렇게 사용할 수 있다는 것을 의미.