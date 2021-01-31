# JS snippets

Display readable json:
```
<pre>{JSON.stringify(myObject, null, 2)}</pre>
```
Delayed js debugger:
```
setTimeout(() => { debugger; }, 5000)
```
Create an array of n following number [0, 1, 2, ..., n-1]:
```
Array.from(Array(10), (_, i) => i)
```
Sleep method:
```
await new Promise(r => setTimeout(r, 2000));
```
Get form inputs values:
```
const inputs = document.forms?.formId?.elements;
const inputs = document.getElementById(formId)?.elements;
Array.from(inputs).reduce((values, input) => acc[input.name] = input.value, {});
```
