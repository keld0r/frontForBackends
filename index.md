title: Frontend 101
author:
  name: Claudio Ulloa
output: index.html
theme: juanbrujo/cleaver-beerjs
style: style.css
controls: true

--

# Frontend for Backends

--

# ¿Que es Javascript?

Javascript es un lenguaje de programacion interpretado, **no tipado*** basado en el estandard ECMAScript.

(El mas usado actualmente ES6).

--
# Tipado y variables.

![What meme](https://media.giphy.com/media/uHox9Jm5TyTPa/giphy.gif)

--

### Tipos primitivos

- Boolean
- Null
- Undefined
- Number
- BigInt
- String
- Symbol

--

### Variables: var, let, const


```js
let ten = 10;
console.log(ten * ten);
// → 100

var name = "Iron Team";
const greeting = "Hello ";
console.log(greeting + name);
// → Hello Iron Team
```
Los nombres de las variables solo pueden contener numeros, letras, signo peso **$** o guión bajo **_** 

Pero **no puede comenzar con un numero**.

```js
var 2018scotia = "Iron Team";  ✘
var scotia2018 = "Iron Team";  ✓
var _scotia2018 = "Iron Team"; ✓
var $scotia2018 = "Iron Team"; ✓

```
--

### Las variables no se asocian a un tipo de dato
En Java es necesario hacer un cast
```js
int i = Integer.parseInt(myString);
```
En Javascript **NO**
```js
let mood = "light";
console.log(mood);
// → light
mood = 123;
console.log(mood);
// → 123
```

--

### Binding y Scope de var, let, const 
```js
let x = 10;
if (true) {
  let y = 20;
  var z = 30;
  let x = 1;
  console.log(x + y + z);
  // → ?
}
console.log(x + z);
// → ?
```

Var se declara de forma global, en cambio let y const se declaran dentro de su scope.
--

### Binding y Scope de var, let, const
```js
let x = 10;
if (true) {
  let y = 20;
  var z = 30;
  let x = 1;
  console.log(x + y + z);
  // → 51
}
console.log(x + z);
// → 40
```
la variable **x** dentro del if, esta en un scope distinto a la que esta afuera, por lo que no se sobreescribe.
--

### Funciones

En javascript existe más de una forma de declarar una función.

```js
function square(x){
  return x * x;
};

const square = function(x) {
  return x * x;
};

const square = (x) => {
  return x * x;
};
```
```js
square(10):
// → 100
```


--
### Hoisting

```js
var tipoAnimal = "Gato";
nombreDelGato("Juanito");
// → Mi gato se llama Juanito
function nombreDelGato(nombre) { 
  console.log("Mi "+tipoAnimal+" se llama " + nombre);
}
```
## Descubra el error
--

Un ejemplo común es decir que en el **Hoisting** las declaraciones de variables y funciones se mueven al inicio del codigo, **peeeeeeeeeero...** lo que en realidad ocurre es que estas declaraciones se guardan en memoria en fase de compilación.

# ¿Dijo compilación?
```js
nombreDelGato("Juanito");
// → Mi undefined se llama Juanito
function nombreDelGato(nombre) {
  console.log("Mi " + tipoAnimal + " se llama " + nombre);
}
var tipoAnimal = "Gato";
```
https://medium.com/@tatymolys/var-let-y-const-donde-cuando-y-por-qu%C3%A9-d4a0ee66883b
--
### Scope Anidado
Como deciamos, una funcion puede guardarse dentro de una variable, por lo que podemos tener algo como una función dentro de otra
```js
const mayonesaCasera = function(factor) {
  const ingredient = function(amount, unit, name) {
    let ingredientAmount = amount * factor;
    if (ingredientAmount > 1) {
      unit += "s";
    }
    console.log(`${ingredientAmount} ${unit} ${name}`);
  };
  ingredient(1, "", "huevo");
  ingredient(0.5, "cucharadita", "sal");
  ingredient(1, "cucharada", "jugo de limón");
  ingredient(0.15, "litro", "aceite");
};
```
--

### Data Structures: Objects and Arrays

Array
```js
let listOfNumbers = [2, 3, 5, 7, 11];
console.log(listOfNumbers[2]);      // → 5
console.log(listOfNumbers[2 - 1]);  // → 3
```
Objeto
```js
let day1 = {
  squirrel: false
};
console.log(day1.squirrel); // → false
console.log(day1.wolf);// → undefined
day1.wolf = false;
console.log(day1.wolf);// → false

```
--
### Destructuring

```js
let {name, weight} = {name: "Eulalio", age: 23, height: 1.75, weight: "80kg"};
console.log(name+" - "+weight);
// → Eulalio - 80kg
```

```js
var foo = ["uno", "dos", "tres"];

var uno  = foo[0];
var dos  = foo[1];
var tres = foo[2];
// lo mismo en 1 linea
var [uno, dos, tres] = foo;
```
--
### Objetos... un poco mas allá
```js
  function speak(line) {
    console.log(`The ${this.type} rabbit says '${line}'`);
  }
  let whiteRabbit = {type: "white", speak};
  let hungryRabbit = {type: "hungry", speak};

  whiteRabbit.speak("I'm white and cute");
  // → The white rabbit says 'I'm white and cute'
  hungryRabbit.speak("I'm starving!");
  // → The hungry rabbit says 'I'm starving!'
```
--

### Clases
```js
class Rabbit {
  constructor(type) {
    this.type = type;
  }
  speak(line) {
    console.log(`The ${this.type} rabbit says '${line}'`);
  }
}

let whiteRabbit = new Rabbit("white");
let hungryRabbit = new Rabbit("hungry");
whiteRabbit.speak("I'm white and cute")
hungryRabbit.speak("I'm starving!")
```

--
# Asynchronous Programming
 Al trabajar con funciones asíncronas tenemos la ventaja de que no necesitamos esperar el resultado de esta, para poder seguir ejecutando el resto del codigo. 
 
 Pero como le dijo el Tio Ben a Peter parker: **"Un gran poder conlleva una gran responsabilidad"**
--

# Asynchronous Programming

```js
function httpGet(theUrl){
    var xmlHttp = new XMLHttpRequest();
    xmlHttp.open( "GET", theUrl, false ); // sincrona
    xmlHttp.send( null );
    return xmlHttp.responseText;
}
console.log(httpGet('https://jsonplaceholder.typicode.com/posts/1'));
```
```js
function httpGet(theUrl){
    var xmlHttp = new XMLHttpRequest();
    xmlHttp.open( "GET", theUrl, true ); // asincrona
    xmlHttp.send( null );
    return xmlHttp.responseText;
}
console.log(httpGet('https://jsonplaceholder.typicode.com/posts/1'));
```
--

# Asynchronous Programming & Promises

![Async](https://www.deadcoderising.com/content/images/2017/09/sync-async.gif)

--

# Asynchronous Programming & Promises

![AsyncProm](https://www.deadcoderising.com/content/images/2017/09/successful_callback.gif)


--
# Asynchronous Programming & Promises

Una Promesa puede tener 3 estados:

- pendiente (pending): estado inicial, no cumplida o rechazada.
- cumplida (fulfilled): significa que la operación se completó satisfactoriamente.
- rechazada (rejected): significa que la operación falló.


--
# Asynchronous Programming & Promises

```js
new Promise(function(resolver, rechazar) { ... } );
```
Esto es equivalente al ejemplo asincrono de las slides anteriores:
```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(function(response) {
    return response.json();
  })
  .then(function(myJson) {
    console.log(myJson);
  })
  .catch(function(reason) {
    console.log('la promesa falló por error en IA4');
  });
```

--

# Asynchronous Programming & Promises

```js
new Promise(function(resolver, rechazar) { ... } );
```
Esto es equivalente al ejemplo asincrono de las slides anteriores:
```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(function(response) {
    return response.json();
  })
  .then(function(myJson) {
    console.log(myJson);
  })
  .catch(function(reason) {
    console.log('la promesa falló por error en IA4');
  });
```
https://codesandbox.io/s/eager-fermat-u7s38 (revisar)

--

# Import & export

```js
function apiCallImages(){
  //...do some stuff
  return result;
}
function apiCallAlbums(){
  //...do sanotherome stuff
  return result;
}
export { apiCallImages, apiCallAlbums };
```
Esto es equivalente al ejemplo asincrono de las slides anteriores:
```js
import { apiCallImages, apiCallAlbums } from "./apiCall";
```



