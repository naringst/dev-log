
# extends
자바스크립트에서도 사용할 수 있으며 부모 클래스에 있는 프로퍼티나 메소드를 상속해서 사용할 수 있게 만들어준다.

# implements
새로운 클래스의 타입 체크를 위해 사용되며, 그 클래스의 모양을 정의할 때 사용한다.
부모 클래스의 프로퍼티와 메소드를 상속받아서 사용하는게 아니다.

```typescript
class Car {
	mileage = 0 ;
	price = 100;
	color = 'white';

	drive() {
		return 'drive!'
	}

	brake() {
		return 'brake!'
	}
}


class Ford extends Car {

}

//에러
%% class Ford implements Car { 

}
 %%

//이 에러를 해결하려면 Car에 해당하는 타입을 다 넣어주면 된다.
//Car부분에 지금은 Class를 줬지만, interface를 줄 수도 있다.
class Ford implements Car { 
	mileage = 0 ;
	price = 100;
	color = 'white';

	drive() {
		return 'drive!'
	}

	brake() {
		return 'brake!'
	}
}



const myFordCar = new Ford();
```