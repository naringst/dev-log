
```

interface People{

name :string

age :number

}

```

  

## 차이점

### 확장
- interface : extends를 이용해 확장

- type : intersection을 이용해 확장

### 선언 병합

- interface : 아래에서 다시 선언해서 선언 병합

```

interface Animal {

name : string;

}

  

interface Animal {

honey : boolean;

}

  

const bear1 : Animal {

name : 'honey bear',

honey : true

}

```
- type : 선언 병합 불가

  

## 공통점
### implements 사용 가능
```typescript

interface IArticle {

category: string;

content: string;

}

  

class Article implements IArticle {

public category = "";

public content = "";

}

```


### union

- Union 유형을 사용하면 개발자가 타입 A 또는 타입 B가 될 수 있는 새로운 Type을 만들 수 있다.

- | 연산자를 사용하여 Type과 Interface를 모두 사용해 새로운 Union 유형을 생성한다. 그러나 선언은 항상 type이어야 한다.

```typescript

interface Animal {

name: string;

}

interface Bear {

honey: boolean;

}

  

type NewType = Animal | Bear;

```