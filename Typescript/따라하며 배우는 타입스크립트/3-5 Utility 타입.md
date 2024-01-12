
# Partial
파셔 타입은 특정 타입의 부분 집합을 만족하는 타입을 정의할 수 있습니다.

```typescript

interface Address {
	email : string;
	address : string;
}

const me: Partial<Address>= {};
const you: Partial<Address>= {email : 'ellie@abc.com' };
const all: Address = { email : 'ellie@abc.com', address : 'john'};
```

# pick
특정 타입에서 몇 개의 속성을 정해 사용

```typescript
interface Todo {
	title : string;
	description : string;
	completed: boolean;
}

//이렇게 부분집합으로 쓸 수도 있고,
const todo : Partial<todo> = {
	title : "Clean Room",
	completed : false
}

//이렇게 Pick을 통해 지정도 가능
type TodoPreview = Pick<Todo, "title"|"completed"> //이렇게 pick

const todo : TodoPreview = {
	title : "Clean Room",
	completed : false
}


```

# Omit

```typescript
interface Todo {
	title : string;
	description : string;
	completed: boolean;
	createdAt : number;
}

type TodoPreview = Omit<Todo, "description"> 


const todo : Partial<todo> = {
	title : "Clean Room",
	completed : false,
	createdeAt : 123234
}

```

# Exclude
일반 union 유형을 전달한 다음 두 번째 인수에서 제거할 멤버를 지정
```typescript
type myUnionType = '나리' | '지원' | '다희'


let lemon : myUnionType = '나리'

let noNariPlease: Exclue<myUnionType, '나리'> = '지원'

```

# Required
원래 유형이 일부 속성을 선택 사항으로 정의한 경우에도 객체에 Required 속성이 있는지 확인해야 하는 경우가 있다.
-> ?로 사용한 프로퍼티도 모두 갖고 있어야 하도록 지정하는 방법
```typescript
type User = {
	firstName : string,
	lastName? : string
}

let firstUser = {
	firstName : 'John',	
}

let secondUser: Required<User> = {
	firstName : 'John',	 
	//lastName 없다는 오류 발생
}
```

# Record <Keys, Type>
속성 키가 Keys이고 속성 값이 Type인 객체 type을 구성합니다.
이 유틸리티는 type의 속성을 다른 type에 매핑하는 데 사용할 수 있습니다.
여기서는 miffy가 keys 타입이고, {}가 Type 부분의 type

```typescript

interface CatInfo = {
	age: number,
	breed: string
}

type CatName = 'miffy' | 'boris' | 'mordred'

const cats : Record<CatName, CatInfo> = {
	miffy : {age:10, breed: "Persian"},
	boris : {age:5, breed: "Maine Coon"},
	mordred:{age:16, breed: "British Shorhair"}
};

cats.boris; 

```

# ReturnType <>

함수 T의 반환 타입으로 구성된 타입

```typescript
type T0 = ReturnType<() => string>
type T1 = ReturnType<(s:string) => void>

function fn(str:string) {
	return str;
}

const a: ReturnType<typeof fn> = 'Hello';

```


# 질문
- union타입 쓰는거랑 partial쓰는거랑  generic extends의 차이?
	- 간단할 대에는 union, 복잡해지면 partial, generic extends를 쓴다.
	- generic extends는 generic을 쓸 때 쓰니까 .. 
- 다른 질문인데 A는 type이 id, title, isDirty 이고, B는 id, title, children, isFile이면 어떻게 지정하는 게 좋은지?
	- FileType {
		- id 
		- title   
		 - isDirty ? 
		 - ? 
		 - ? 
	- }
	- 클라이언트, 서버 상태를 같게 하는 게 가장 좋다. 프로퍼티 이름과 타입을 같게 해준 뒤 사용한다. 
	- 클라이언트/ 서버 타입을 나눠서 
	- Common { 
	-  id, title
	- }
	- Client {
	- }
	- Server {
	- } 
	- 백엔드에서 저장하는 이름도 맞추기
	- 다를 경우에는 