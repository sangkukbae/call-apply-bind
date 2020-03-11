# [Call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)-[Apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)-[Bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)

**Basic rules worth remembering:**
1. `this` always refers to an object.
2. `this` refers to an object which calls the function it contains.
3. In the global context `this` refers to either window object or is undefined if the `strict mode` is used.

## :page_facing_up: 목차
* [Implicit Binding](#implicit-binding)
* [Explicit Binding](#explicit-binding)
* [new Binding](#new-binding)
* [Lexical Binding](#lexical-binding)
* [window Binding](#window-binding)



## Implicit Binding

```javascript
const user = {
  name: 'Tyler',
  age: 27,
  greet() {
    alert(`Hello, my name is ${this.name}`)
  },
  mother: {
    name: 'Stacey',
    greet() {
      alert(`Hello, my name is ${this.name}`)
    }
  }
}
user.greet() // Hello, my name is Tyler
user.mother.greet() // Hello, my name is Stacey
```

## Explicit Binding

**Call**
```javascript
function greet () {
  alert(`Hello, my name is ${this.name}`)
}
const user = {
  name: 'Tyler',
  age: 27,
}
greet.call(user) // Hello, my name is Tyler
```

```javascript
function greet (l1, l2, l3) {
  alert(
    `Hello, my name is ${this.name} and I know ${l1}, ${l2}, and ${l3}`
  )
}
const user = {
  name: 'Tyler',
  age: 27,
}
const languages = ['JavaScript', 'Ruby', 'Python']
greet.call(user, languages[0], languages[1], languages[2]) // Hello, my name is Tyler and I know JavaScript, Ruby, and Python
```

**Apply**
```javascript
const languages = ['JavaScript', 'Ruby', 'Python']
greet.apply(user, languages) // Hello, my name is Tyler and I know JavaScript, Ruby, and Python
```

**Bind**
```javascript 
const newFn = greet.bind(user, languages[0], languages[1], languages[2])
newFn() // alerts "Hello, my name is Tyler and I know JavaScript, Ruby, and Python"
```

## new Binding
```javascript
function User (name, age) {
  /*
    Under the hood, JavaScript creates a new object called `this`
    which delegates to the User's prototype on failed lookups. If a
    function is called with the new keyword, then it's this new object
    that interpretor created that the this keyword is referencing.
  */

  this.name = name
  this.age = age
}
onst me = new User('Tyler', 27)
```

## Lexical Binding
```javascript
const user = {
  name: 'Tyler',
  age: 27,
  languages: ['JavaScript', 'Ruby', 'Python'],
  greet() {
    const hello = `Hello, my name is ${this.name} and I know`

    const langs = this.languages.reduce(function (str, lang, i) {
      if (i === this.languages.length - 1) {
        return `${str} and ${lang}.`
      }

      return `${str} ${lang},`
    }.bind(this), "")

    alert(hello + langs)
  }
}
user.greet() // alerts "Hello, my name is Tyler and I know JavaScript, Ruby, and Python"
```
**Arrow Functions**
```javascript 
const user = {
  name: 'Tyler',
  age: 27,
  languages: ['JavaScript', 'Ruby', 'Python'],
  greet() {
    const hello = `Hello, my name is ${this.name} and I know`

    const langs = this.languages.reduce((str, lang, i) => {
      if (i === this.languages.length - 1) {
        return `${str} and ${lang}.`
      }

      return `${str} ${lang},`
    }, "")

    alert(hello + langs)
  }
}
user.greet() // alerts "Hello, my name is Tyler and I know JavaScript, Ruby, and Python"
```

## window Binding
```javascript
window.age = 27

function sayAge () {
  console.log(`My age is ${this.age}`)
}
```
**use strict**
```javascript
'use strict'

window.age = 27

function sayAge () {
  console.log(`My age is ${this.age}`)
}

sayAge() // TypeError: Cannot read property 'age' of undefined
```
:memo: **참고 자료**   
[https://tylermcginnis.com/this-keyword-call-apply-bind-javascript/](https://tylermcginnis.com/this-keyword-call-apply-bind-javascript/)   
[https://www.taniarascia.com/this-bind-call-apply-javascript/](https://www.taniarascia.com/this-bind-call-apply-javascript/) :heavy_check_mark:   
[https://www.freecodecamp.org/news/how-to-use-the-apply-call-and-bind-methods-in-javascript-80a8e6096a90/](https://www.freecodecamp.org/news/how-to-use-the-apply-call-and-bind-methods-in-javascript-80a8e6096a90/)   
[https://www.codementor.io/@niladrisekhardutta/how-to-call-apply-and-bind-in-javascript-8i1jca6jp](https://www.codementor.io/@niladrisekhardutta/how-to-call-apply-and-bind-in-javascript-8i1jca6jp)   
[https://www.codingame.com/playgrounds/9799/learn-solve-call-apply-and-bind-methods-in-javascript](https://www.codingame.com/playgrounds/9799/learn-solve-call-apply-and-bind-methods-in-javascript)   
[https://medium.com/@omergoldberg/javascript-call-apply-and-bind-e5c27301f7bb](https://medium.com/@omergoldberg/javascript-call-apply-and-bind-e5c27301f7bb)   
[https://youtu.be/zE9iro4r918](https://youtu.be/zE9iro4r918)   
[https://www.youtube.com/watch?v=AYVYxezrMWA](https://www.youtube.com/watch?v=AYVYxezrMWA)   
