Сегодня мы поговорим о такой вещи, как функции высшего порядка.
```js
function copyArrayAndDoSmth(arr, instructions) {
 let output = [];

 for(let i = 0; i < arr.length; i++) {
  output.push(instructions(arr[i]));
 } 

 return output;
}

function numSquared(num){
 return num * num;
}

function divideBy2(num){
 return num / 2;
}

const result = copyArrayAndDoSmth([1, 2, 3], numSquared);
const result2 = copyArrayAndDoSmth([10, 20, 30], divideBy2);
```

Итого мы с вами посмотрели функции высшего порядка и создали пример, который принимает функцию и использует внутри себя, функция высшего порядка.

Ещё раз, она могла бы не принимать функцию, могла бы создать ее внутри, и вернуть ее наружу, это тоже была бы функция высшего порядка. То есть, по сути, либо-либо, и то, и другое будет называться функцией высшего порядка.

Мы просмотрели также колбэки. Колбэки, функции, которые мы напрямую не вызываем, а просто передаем их в качестве параметров в какие-то другие функции или методы.