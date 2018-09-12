
# Jquery to Javascript

- :link: [Promesas - async - await ](https://dev.to/ardennl/about-promises-and-async--await-5ebm)

## Promesas

```javascript
// SE REGRESA -resolve- -reject- VASADOS EN EL VALOR QUE SE LE PASO POR PARAMETRO
function isTonyStark(name) {
    // SE CREA LA PROMESA CON ARROWFUNCTION
    return new Promise((resolve, reject) => {
        if (name === 'Tony') {
            resolve(`Welcome ${name}`);
        } else {
            reject(Error('Danger, Will Robinson, danger!'));
        }
    });
}
// CONSUMIR UNA PROMESA
isTonyStark('Tony')
    .then(console.log)
    .catch(err => console.error(err));
```

```javascript
// CONSUMIR VARIAS PROMESAS A LA VEZ.
// EL THEN SE EJECUTAN CUANDO TERMINEN TODAS LAS PROMESAS.
// EL CATCH SE EJECUTA EN EL PRIMER ERROR.
Promise.all([
  promesa1,
  promesa2
])
.then(function() {})
.catch(function() {})

// SE EJECUTA EL THEN DE LA PROMESA QUE TERMINE PRIMERO.
Promise.race([
  promesa1,
  promesa2
])
.then(function() {})
.catch(function() {})
```

## Ajax

### Ajax con jQuery

```javascript
$.ajax({
    type: "POST", // GET, DELETE, PUT
    url: '/ruta/del/API/', // -VARIABLE QUE CONTIENE LA RUTA -RUTA DE LA PAGINA EN DONDE RECIVE LA DATA
    data: {
        'variable_a_pasar': valor_de_la_variable,
    },
    dataType: 'json',
    success: function(data) {
        console.log(data); // EN CASO DE SER EXITOSA LA RESPUESTA
    },
    error: function(data) {
        console.log(err); // EN CASO DE NO SER EXITOSA LA RESPUESTA
    }
});

```
## Ajax con JavaScript
Ejempo con [Random User Generator API -free-](https://randomuser.me/)
```javascript

fetch('https://randomuser.me/api/') // -VARIABLE QUE CONTIENE LA RUTA -RUTA DE LA PAGINA EN DONDE RECIVE LA DATA
    .then(function (response){
        // CUANDO UNA RESPUESTA ES CORRECTA LA RESPUESTA ES CORRECTA
        return response.json()
    })
    .then(function (user) {
        console.log('user', user.results[0].name.first)
    })
    .catch(function () {
        console.log('fallo algo... ')
    });
```
## Funciones asíncronas
Ejemplo mostrado con la API [https://yts.am/api -free-](https://yts.am/api)
```javascript
console.log(fetch('https://yts.am/api/v2/list_movies.json')); // DEVUELVE UNA PROMESA -PENDIENTE-
```
__Ejemplo con arrow function__ en en [link](https://www.imdb.com/feature/genres/) es para saber los generos que estan disponibles. Action, Crime, Drama, Thriller

```javascript
// REGRESA LA PROMESA Y SE PUEDE VER EL STATUS OK
fetch('https://yts.am/api/v2/list_movies.json?genres=sci-fy')
    .then(data => console.log(data));
```
```javascript
// REGRESA LA PROMESA Y SE PASAN LOS DATOS A FORMATO JSON
fetch('https://yts.am/api/v2/list_movies.json?genres=sci-fy')
    .then(data => data.json()) // EN LA RESPUESTA EN __proto__ HAY UN METODO JSON, QUE REGRESA OTRA PROMESA
    .then(data => console.log(data)); // REGRESA UN ARRAY DE OBJETOS QUE SE OBTIENEN EN LA RESPUESTA
```

```javascript
// REGRESA LA PROMESA Y SE PRESENTA UN ERROR
fetch('yts.am/api/v2/list_movies.json?genres=sci-fy')
    .then(data => data.json()) // EN LA RESPUESTA EN __proto__ HAY UN METODO JSON, QUE REGRESA OTRA PROMESA
    .then(data => console.log(data)) // REGRESA UN ARRAY DE OBJETOS QUE SE OBTIENEN EN LA RESPUESTA
    .catch(err => console.error('HAY UN ERROR EN LA CONSULTA DEL API -->', err));
```

El metodo **finaly** Retorna la promesa sin importar si esta es exitosa o es rechazada; puede ser de utilidad para poner a un estado inicial la promesa ejecutada.

- :link: [Finally - MDN web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/finally)

```javascript
fetch('https://yts.am/api/v2/list_movies.json?genres=sci-fy')
    .then(data => data.json()) // EN LA RESPUESTA EN __proto__ HAY UN METODO JSON, QUE REGRESA OTRA PROMESA
    .then(data => console.log(data)) // REGRESA UN ARRAY DE OBJETOS QUE SE OBTIENEN EN LA RESPUESTA
    .catch(err => console.error('HAY UN ERROR EN LA CONSULTA DEL API -->', err))
    .finally(() => console.log('FIN DE LA PROMESA'));
```

## Async / Await
Async/Await estan basadas en promesas. En orden para que **async** se ejecute, **await** se necesita una funcion para que retorne una promesa.

**await** "**SIEMPRE**" se necesita llamar de una funcion "**async**"

```javascript
function wait(ms) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(console.log(`waited for ${ms}ms`));
        }, ms);
    });
}

const go = async () => {
    await wait(600);
    await wait(1200);
    await wait(1800);
}
go();

// SALIDA
// waited for 600ms
// VM431:4 waited for 1200ms
// VM431:4 waited for 1800ms

```
```javascript
// Async/Await ARROW FUNCTION
const getData = async (url) =>  {
    const response = await fetch(url);
    const data = await response.json();
    console.log(data);
}
getData('https://yts.am/api/v2/list_movies.json?genres=action');
```
Ejecutar al momento Async/Await Categorias Action, Crime, Drama, Thriller
```javascript
(async () => {
    const getData = async (url) => {
        const response = await fetch(url);
        const data = await response.json()
        return data;
    }
    const actionList = await getData('https://yts.am/api/v2/list_movies.json?genres=action')
    const crimeList = await getData('https://yts.am/api/v2/list_movies.json?genres=crime')
    const DramaList = await getData('https://yts.am/api/v2/list_movies.json?genres=drama')
    const thrillerList = await getData('https://yts.am/api/v2/list_movies.json?genres=thriller')
    console.log('actionList -->', actionList);
    console.log('crimeList -->', crimeList);
    console.log('DramaList -->', DramaList);
    console.log('thrillerList -->', thrillerList);
})()
```
## Selectores
Por convención una variable que este represente un objeto del DOM lleva el signo $, esto es para tener claro que estamos manipulando un objeto del DOM y no algún tipo de información o dato.

Dentro de JavaScript existen distintas funciones para hacer selectores, entre ellas se encuentra:

+ getElementById: recibe como parámetro el id del objeto del DOM que estás buscando. Te regresa un solo objeto.
+ getElementByTagName: recibe como parámetro el tag que estas buscando y te regresa una colección html de los elementos que tengan ese tag.
+ getElementByClassName: recibe como parámetro la clase y te regresa una colección html de los elementos que tengan esa clase.
+ querySelector: va a buscar el primer elemento que coincida con el selector que le pases como parámetro.
+ querySelectorAll: va a buscar todos los elementos que coincidan con el selector que le pases como parámetro.

### jQuery
```jquery
const $home = $(".home") // ELEMENTO CON LA CLASE HOME
const $home = $("#home") // ELEMENTO CON EL ID HOME
```

### Javascript

```javascript
// RETORNA UN ELEMENTO CON EL ID HOME
document.getElementById("home")

// RETORNA UNA LISTA DE ELEMENTOS CON LA CLASE HOME
document.getElementsByClassname("home")

// RETORNA UNA LISTA DE ELEMENTOS CON EL TAG DIV
document.getElementsByTagName("div")

// DEVUELVE EL PRIMER ELEMENTO QUE COINCIDA CON EL QUERY DE BÚSQUEDA.
document.querySelector("div .home #modal")

// DEVUELVE TODOS LOS ELEMENTOS QUE COINCIDAN CON EL QUERY DE BÚSQUEDA.
document.querySelectorAll("div .home #modal")
```