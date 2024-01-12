
# 전체 구성

```typescript
{
	//컴파일러 옵션 지정
	"compilerOptions" : {},
	//컴파일할 개별 파일 목록(확장자 이름 필수)
	"files": [
		"node_modules/library/index.ts"
	],
	//컴파일러를 이용해서 변환할 폴더 경로를 지정
	"include": [
		"src/**/*",
		"tests/**/*"
	],
	//컴파일러를 이용해서 변환하지 않을 폴더 경로를 지정
	"exclude": [
		"node_modules",
		"dist"
	],
	//상속해서 사용할 다른 TS 구성파일 지정
	//다른곳에 지정해둔 파일 가져와서 쓰기
	"extends": "main_config.json"
}
```

# compilerOptions
## lib
- 컴파일 할 때 사용할 라이브러리들을 여기에 넣음.
- ESNext
- lib.dom.d.ts에 console이 Console타입이라고 지정돼있다. 이를 가져오려면 ESNext를 써줘야함.

## moduleResolution
- Node or Classic 사용 가능
- 스크립트 컴파일러가 노드를 찾는 방식을 명기하는 것.
- 그 중에서 relative인지 non-relative인지 구분을 한다.
- 요즘에는 Node만 사용.(거의)

## baseUrl



## paths
- 이게 next에서 @로 표현되는 그것
- baseUrl 기준으로 paths : {"@src/*" : ["src/*" ]}로 바꿔 사용 가능.
```typescript
import {bar} from "../../../../bar";
=> import {bar} from "@src/bar"

export const foo =() => {
	console.log(bar())
}
```


## isolatedModules
- 이걸 true로 하면 모든 파일을 module로 만들기로 강제한다.

## removeComments
- true로 하면 커멘트를 컴파일 시에 다 없애준다.

## allowJs
- js파일도 사용할 수 있게 한다.

## checkJs
- js 파일의 오류가 보고된다.

## forceConsistentCasingInFileNames
- 파일 이름을 대소문자 판별하게 하는 옵션

## declaration
- true로 하면 TS파일을 JS 파일로 컴파일 하는 과정에서 JS파일과 함께 d.ts선언 파일이 생성된다.
- 이 선언 파일에서 타입들만 따로 관리 가능

## strict
- 엄격하게 타입 체크![[스크린샷 2024-01-12 오후 3.08.05.png]]