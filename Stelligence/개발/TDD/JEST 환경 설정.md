설치
```
```bash
yarn add jest jest-dom jest-environment-jsdom ts-jest babel-jest --dev
@types/jest

```

```bash
실제로 추가로 설치 
yarn add @testing-library/user-event @testing-library/react-hooks @testing-library/react @testing-library/jest-dom @testing-library/dom --dev
```


eslinrc.json에 추가
```

//eslintrc.json
{
  "env": {
    // ...
    "jest": true
  }
  // ...
}

```

- package.json 설정
```jsx
"test": "jest --watch --passWithNoTests",
    "test:ci": "jest --ci --passWithNoTests"
```

필요하다면 tsconfig 설정
```jsx
//tsconfig.json

{
  "compilerOptions": {
    "baseUrl": "./src",
    "paths": {
      "@/*": ["./*"],
      "@pages/*": ["pages/*"],
      "@components/*": ["components/*"],
      "@utils/*": ["utils/*"],
      "@hooks/*": ["hooks/*"],
      "@types/*": ["types/*"]
    },
      //...
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}
```

jest 설정
- jest.setup.js
- import '@testing-library/jest-dom';

- jest.config.js
```
const nextJest = require('next/jest');
const createJestConfig = nextJest({
 dir: './',
});

const customJestConfig = {
 setupFilesAfterEnv: ['./jest.setup.js'],
 testEnvironment: 'jest-environment-jsdom',
 preset: 'ts-jest',
};

module.exports = createJestConfig(customJestConfig);
```
/
```
const nextJest = require('next/jest');

  

const createJestConfig = nextJest({

// Provide the path to your Next.js app to load next.config.js and .env files in your test environment

dir: './',

});

  

// Add any custom config to be passed to Jest

const customJestConfig = {

setupFilesAfterEnv: ['<rootDir>/jest.setup.js'],

// if using TypeScript with a baseUrl set to the root directory then you need the below for alias' to work

moduleDirectories: ['node_modules', '<rootDir>/'],

  

// Handle module aliases

moduleNameMapper: {

'^@/pages/(.*)$': '<rootDir>/pages/$1',

},

testEnvironment: 'jest-environment-jsdom',

};

  

// createJestConfig is exported this way to ensure that next/jest can load the Next.js config which is async

module.exports = createJestConfig(customJestConfig);
```

## eslint 설정
yarn add -D eslint-plugin-testing-library eslint-plugin-jest-dom

### .eslintrc.json

`"plugins": ["testing-library", "jest-dom"], "extends": {  "plugin:testing-library/react",  "plugin:jest-dom/recommended" }`


추가
tsconfig.,json에 
{
  "include": [
    "next-env.d.ts",
    "**/*.ts",
    "**/*.tsx",
    ".next/types/**/*.ts",
    "postcss.config.js",
    "jest.config.js",
    "jest.setup.js"
  ],
  "exclude": ["node_modules"]
}

# 참고
https://velog.io/@leehyunho2001/Next.js-TypeScript-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-Jest%EC%99%80-testing-library-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0