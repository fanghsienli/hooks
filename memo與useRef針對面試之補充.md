面試時有答出memo與useCallback的用法

但`useMemo`答得不清楚特此補充

`useMemo`用來記憶昂貴的計算

```typescript
import{useState,useRef,useMemo} from "react"
export default function App() {
    const [count, setCount] = useState<number>(100)
    const [count2, setCount2] = useState<number>(100)
    const execTimes = useRef<number>(0)

    function computeExpensiveValue(count:number):number{
        execTimes.current++
        console.log(`[computeExpensiveValue] execute ${execTimes.current} times`)
        const array = new Array(count).fill(count);
        return array.reduce((currentTotal, item) => currentTotal + item, 0)
    }

    function handleSetCount(){
        console.log(`[handleSetCount] execute`)
        setCount(preCount => preCount * 2);
    }

    function handleSetCount2(){
        console.log(`[handleSetCount2] execute`)
        setCount2(preCount => preCount * 2);
    }

    //const computeValue = computeExpensiveValue(count)
    const computeValue = useMemo<number>(() => computeExpensiveValue(count), [count])

    return (
        <div>
            <div>computeValue: {computeValue}</div>
            <div onClick={handleSetCount}>add count: {count}</div>
            <div onClick={handleSetCount2}>add count2: {count2}</div>
        </div>
    )
}
```

但不要濫用

例如以下情景並不需要使用

```javascript
function Bla() {
    //const baz = useMemo(() => [1, 2, 3], [])
    const { current: baz } = useRef([1, 2, 3])
    return <Foo baz={baz} />
}
```

可使用`useRef`

即補充面試時`useRef`其他用途的地方