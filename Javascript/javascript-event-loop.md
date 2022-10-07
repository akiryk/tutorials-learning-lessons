# Event Loop
Useful quiz from [FEM course](https://www.typescript-training.com/course/making-typescript-stick/02-warm-up/#question-2)

What is the order of logs? 

```js
function getData() {
  console.log("elephant")
  const p = new Promise((resolve) => {
    console.log("giraffe")
    resolve("lion")
    console.log("zebra")
  })
  console.log("koala")
  return p
}
async function main() {
  console.log("cat")
  const result = await getData()
  console.log(result)
}

console.log("dog")

main().then(() => {
  console.log("moose")
})
```

Here's another one:
```js
function getData() {
  return new Promise(resolve => {
    resolve('bear');
    console.log("ralphy")
  })
}

function getOtherData() {
  return new Promise(resolve => {
    console.log('snake');
    setTimeout(() => {
      console.log("hamster")
      resolve("alligator");
      console.log("chicken")
    }, 0);
  })
}


async function main () {
  const train = await getOtherData();
  console.log(train)
  const park = await getData();
  console.log(park);
  return train;
}

main().then(res => {
  console.log(res);
});
```

Answer to question above:

```js
The answer to the above is
// TOP: dog, cat, elephant, giraffe, zebra, koala, lion, moose
// BOTTOM: snake, hamster, chicken, alligator, ralphy, bear, alligator
```
Why? Because when you come to a promise that resolves right away, it runs right away -- so we get giraffe and zebra right after elephant. But the   `thenable` part waits until there's a `then`, so we get lion later, after Koala.
