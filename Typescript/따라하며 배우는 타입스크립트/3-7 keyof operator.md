
# 정의
keyof 연산자는 제공된 타입의 키를 추출해 새로운 Union 유형으로 반환한다.  

```typescript
interface IUser {
	name : string;
	age : number;
	address : string;
}

type UserKeys = keyof IUser
//'name' | 'age' | 'address'라는 타입이 반환됨.

const user = {
	name : 'John'
	age:20
	address:'seoul'
}

//user라는 객체 속성을 받아서 이름으로 만들어준다.
type UserKeys = keyof typeof user

//enum에서 키 추출?
enum UserRole {
	admin, manager
}

type UserRoleKeys = keyof typeof user

```
