Display readable json
```
<pre>{JSON.stringify(myObject, null, 2)}</pre>
```
Delayed js debugger
```
setTimeout(() => { debugger; }, 5000)
```
Create an array of n following number, starting at 0
```
Array.apply(null, {length: N}).map(Number.call, Number)
=> [0, 1, 2, ..., n-1]
```
