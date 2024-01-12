
# 개념
맵드 타입을 이용하면 중복을 피하기 위해 다른 타입을 바탕으로 새로운 타입을 생성할 수 있다.
Mapped type을 사용하는 것은 type이 다른 type에서 파생되고 동기화 상태를 유지해야 하는 경우에 특히 유용하다.

아래의 예제는 AppConfig타입에 따라 AppPermissions가 영향을 받을 수 있는 관계이다. 이처럼 두 타입에 대한 적절한 업데이트를 동시에 수행하기 위해 Mapped Types를 활용해 관리 가능하다.
```typescript
type AppConfig = {
	username : string;
	email : string;
};

//AppConfig 타입과 암시적인 관계 존재
type AppPermissions = {
	changeUsername : boolean;
	changeEmail : boolean;
}

```


```typescript
type Users = 'John' | 'Han' | 'Kim';

type UserFirstNames = { [ K in Users] : string}'
const userFirstNamInfo : UserFirstNames = {
	'John':'Doe',
	'Han':'Ho',
	'Kim' : 'Jun'
}
```

## 더 실용적인 예제 알아보기
```typescript

type DeviceFormatter<T> = {
	[K in keyof T] : T[K];
	//[K in keyof T]? : T[K]; //이렇게 사용하면 속성중에 어떤 것들이 없어도 가능하다
}

type Device = {
	manufacturer : string;
	price :number;
};

type DeviceFormatter = {
	manufacturer : string;
	price :number
}
const iphone: DeviceFormatter<Device> = {manufacturer : 'apple', price:100}
```


# 질문
- 그래서 어떻게 쓴다는건지 .. 이해가 잘 안됩니다 ㅠㅠ