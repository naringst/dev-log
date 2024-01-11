```python
{
    "compilerOptions":{
				'rootDir':'./src', // typescript 파일이 있는 곳의 루트 디렉토리
				'outDir': './build/js' //js 파일이 생성되는 곳 지정
			}
}
```

이후 tsc -w 하면 설정 적용 되었는지 확인 가능.

```python
여기에 "target" : 'ES6"
```

rootDir 밖에 파일을 생성하면?

- 같은 레벨에서 똑같이 컴파일 해줌.
    
- 하지만 이걸 막고 싶다면?
    
    - “include” : [ “./src/**/*.ts”]
    - 이렇게 설정하면 여기 안에서만 ts 파일을 찾는다.
- emit → ts를 js로 바꾸는 것.
    
- error있을 때 emit안하는 설정
