# Tpyescript


## 시작하기 전에
```powershell
# 초기 설정
$npm init -y
$npm install typescript -D   # -g 로 로컬 전역 설치해도 무관
$npx tsc --init

# 사용 방법
$npc ydv                     # 컴파일 (TS → JS)
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
- null & underfined : string/number에 사용 불가 (예외 처리 가능하긴함)
- object
```ts
const a = {
  key: 'value'
  index: 1
}
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
- any : 정말 문자열이 다양하게 입력되는게 아니라면, 가급적 사용하지 않는게...
```ts
function leakingAny(obj: any){
  const a:number = obj.num; //a가 any로 정해지는 것을 방지함
  const b = a + 1;
  return b;
}
```
- unknown :
- never :
- vlid :