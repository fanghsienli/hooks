`unknown`和`any`差別

`any`可以賦值給任何型別，`unknown`只能賦值給`any`和`unknown`

限縮型別後可通過編譯

限縮型別有兩種方法

1.型別檢測(`typeof`)
```typescript
let isUnknown: unknown;

//Error: Type 'unknown' is not assignable to type 'number'
let value: number = isUnknown;

//限縮型別
if(typeof isUnknown === "number"){
    value = isUnknown
}
```

2.型別斷言(`as`)
```typescript
const value: unknown = "unknown"
const someString: string = value as string
const otherString = someString.toUpperCase() // "UNKNOWN"
```


`never`用在

一個從來不會有返回值的函數(如: 如果函數內含有while(true) {})

一個總是會拋出錯誤的函數(如: function foo() { throw new Error('Not Implemented') }，foo 的返回類型是`never`)

```typescript
function foo(x: string | number): boolean {
    if (typeof x === 'string') {
        return true;
    } else if (typeof x === 'number') {
        return false;
    }

    //如果fail返回不是一個never類型這會報錯
    return fail('Unexhaustive');
}

function fail(message: string): never {
    throw new Error(message);
}
```