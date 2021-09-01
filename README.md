# fullstack
나의 풀스택을 만들어보자

개발 환경 설정

1. 타입스크립트와 노드타입 설치
yarn add -D typescript @types/node
yarn global add typescript

2. ts-node 설치
yarn add -D ts-node

3. tsconfig 파일 생성
만약 TypeScript가 로컬에 설치되어 있을 경우, 로컬의 node_modules 폴더에서 tsc를 호출해야 합니다.
./node_modules/.bin/tsc --init
npx tsc --init // npx는 로컬의 node_modules를 통해서 명령어를 실행해 준다.

4. tsconfig 파일 수정
"outDir": "./dist/", 로 바꾸면 해석된 자바스크립트 파일의 위치 ./dist/ 로 설정한다.

5. nodemon 설치
yarn add -D nodemon

6. package.json의 script 수정
"watch" : "tsc -w", // 매번 변화가 있을 때마다 TypeScript 컴파일을 해주는 것 대신에, watch mode로 컴파일을 시작하면 자동으로 TypeScript 파일에 변화가 있을 때마다 다시 컴파일을 해줍니다.
"dev" : "nodemon dist/index.js",
"dev2" : "nodemon --exec ts-node src/index.ts",
"start" : "node dist/index.js",
"start2" : "ts-node src/index.ts"

7. tslint 설치와 설정
global
$ yarn global add tslint

local
$ yarn add tslint --dev

if using global tslint:
$ tslint --init

if using local tslint:
$ npx tslint --init

tslint.json의 내용
{
    "defaultSeverity": "error",
    "extends": [
        "tslint:recommended"
    ],
    "jsRules": {},
    "rules": {
        "eofline": false,
        "quotemark": [
            true,
            "single"
        ]
    },
    "rulesDirectory": []
}

Airbnb style-guide for tslint
yarn add tslint-config-airbnb

구글 스타일로 한번에 설정
이 명령어는 tsconfig.json과 linting 설정을 하는데 필요한 모든 것을 만들어 줍니다. 심지어 package.json 파일까지 생성해 줍니다.
npx gts init
yarn

또한 gts는 간편한 npm script를 package.json에 추가해줍니다. 예를 들어, 프로젝트를 컴파일 하기 위해서는 npm run compile 명령어를 사용하거나, linting 에러를 확인하기 위해서는 npm run check 명령어를 사용하면 됩니다.

에디터에서 tslint를 사용하기 위해서는 tslint.json에 직접 추가해 gts의 tslint 설정을 확장해주어야 합니다.
{
  "defaultSeverity": "error",
  "extends": [
    "./node_modules/gts/tslint.json"
  ],
  "jsRules": {},
  "rules": {},
  "rulesDirectory": []
}