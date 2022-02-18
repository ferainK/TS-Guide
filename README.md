# Tpyescript


## 시작하기 전에
```powershell
# 초기 설정
$npm init -y
$npm install typescript -D   # -g 로 로컬 전역 설치해도 무관
$npx tsc --init

# 사용 방법
$npc tsc                     # 컴파일 (TS → JS)
$node xxxx.js                # 디버그 (JS)
```

## 1. 문자열
```ts
let a = 'mark'        //string (자동)

let a: string | null         //string (명시)
```
- boolean
- number
```ts
a = 0x39ad1  //16진수
a = 0o12813  //8진수
a = 0b01010  //2진수
a = NaN
a = 1_000_000
```
- string
```ts
 `Hello, ${name}. Your age is ${age + 1}.`
```
- symbol : 고유하고 수정 불가능한 값 (접근 권한에 많이 사용됨)
```ts
const sym = Symbol();
const obj ={
  [sym]: 'value';
}

obj[sym];   //그냥 값이 아니라 Symbol타입을 넣어야지만, 값을 불러올 수 있겠지.
```
- null & undefined : string/number에 사용 불가 (예외 처리 가능하긴함)
```ts
//strictNullChecks 옵션 : 계산결과 string or number에 null/undefined가 계산된다면, 에러 문구 표시
```
- object
```ts
const a = {
  key: 'value'
  index: 1
}

//매개변수 제한 방법 (Interface or Type)
interface PersonInterface{
  name: string;
  age: number;
}

function user(a: PersonInterface): string{
  return `이름은 ${a.name}이고 나이는 ${a.age} 입니다.`
}

//이름(PersonInterface)이 다르더라도 구조(name, age)가 같다면, 서로 대입 가능하다.
```
- array
```ts
let list: (number)[] = [1, 2, 3];
let list: (number | string)[] = [1, 2, 3, "4"];
```
- tuple : 정해진 문자열, 정해진 lenth
```ts
let x: [string, number];
x = ['Lee', 39];
```
- any : 정말 문자열이 다양하게 입력되는게 아니라면, 가급적 사용하지 않는게... (unknown을 쓰자)
```ts
//noImplicitAny 옵션 : TS가 추론하여 any로 결정된 경우, 에러 문구 표시 
//                    (정말 any라면 사용자가 any라고 명기하게끔)

function leakingAny(obj: any){
  const a:number = obj.num; //a가 any로 정해지는 것을 방지함
  const b = a + 1;
  return b;
}
```
- unknown : any와는 다르게 타입을 한정한 상태에서만, 문자열 변경 가능
```ts
declare const maybe: unknown;

if (typeof maybe === "string"){
  const aString: string = maybe; //가능
  const aNumber: number = maybe; //불가능
}
```
- never : 잘못된 타입을 입력하는 것을 막고자 할때 사용
```ts
function error(message: string): never{ //리턴타입이 never
  throw newError(message);
}

function fail() {
  return error("failed");
}

declare const a: string | number;
if (typeof a !== 'string'){
  a;    //a는 자동으로 number로 지정됨 (a는 string or number인데, if 에서 string을 제외했으니)
}

```
- void : 리턴값이 없다.
```ts
// noImplicitReturns 옵션 : 함수의 리턴이 없으면 에러 발생 시킴
// strictFunctionTypes 옵션 : 잘못된 함수 할당 시 에러 발생 시킴 
```
- 타입 별칭 (type) 
```ts
//길게 입력해야할 것을 간략하게 작성
type StringOrNumber = string | number;
type PersonTuple = [string, number];
type EatType = (good: string) => void;

//interface : 목적이 명확한 경우
//type : 단순히 이름만 지정할 때
```

## 2. 컴파일 설정
- 자동저장 : "CompileOnSave" : "true"
- tsconfig 파일 확장 : "extend" : "경로"
- ★ 컴파일 대상 설정 (file > exclude > include)
```json
  {
    "file" : {
      "..." : "...",
      "items": {
        "type" : "경로"
      }
    }
  }
```
- 