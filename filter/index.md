---
title:       JavaScript - filter
description: Exemplo do método filter em JavaScript
capitulo:    "javascript-referencia"
ordem:       12
---

Neste artigo iremos aprender comom usar o método __filter()__ em JavaScript.

Na documentação da Mozila sobre o [filter](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/filtro)
diz o seguinte:

> O método filter() cria um novo array com todos os elementos que passaram no teste implementado
> pela função fornecida.

Ainda na documentação, encontramos o seguinte exemplo:

```javascript
function isBigEnough(value) {
    return value >= 10;
}

let filtered = [12, 5, 8, 13, 14].filter(isBigEnough);

console.log(filtered);
// [12, 13, 14]

```

Detenha-se um pouco nele, olhe o exemplo até que você tenha "compilado" ele mentalmente.


## Evoluindo com o filter

Agora vamos partir do exemplo acima e tentar procurar algumas variações.

A primeira alteração que eu fiz foi colocar o array em uma variável.

```javascript
function isBigEnough(value) {
    return value >= 10;
}

let number = [12, 5, 8, 13, 14];

let filtered = number.filter(isBigEnough);

console.log(filtered);
// [12, 13, 14]
```

Agora vamos passar nossa função `isBigEnough` diretamento para `filter`, sem precisar definir a função
(bem no estilo callback).

```javascript
let number = [12, 5, 8, 13, 14];

let filtered = number.filter(function isBigEnough(value) {
    return value >= 10;
});

console.log(filtered);
// [12, 13, 14]
```

Agora vamos transformar a funcão em uma arrow function.


```javascript
let number = [12, 5, 8, 13, 14];

let filtered = number.filter( (value) => {
    return value >= 10;
});

console.log(filtered);
// [12, 13, 14]
```

Agora que tal se criarmos um funcão (mais externa) para encapsular nossa pequena lógica ?

Criei a funcção `filterItems`.

```javascript
let number = [12, 5, 8, 13, 14];

function filterItems () {
    let filtered = number.filter((value) => {
        return value >= 10;
    });
    return filtered;
}

console.log(filterItems());
// [12, 13, 14]
```

Percebo que não preciso da variável `filtered`. Faço o `return` diretamente.

```javascript
let number = [12, 5, 8, 13, 14];

function filterItems() {
    return number.filter((value) => {
        return value >= 10;
    });
}

console.log(filterItems());
// [12, 13, 14]

```

Interessante seria se pudéssemos passar o array como parâmetro.

```javascript
let number = [12, 5, 8, 13, 14];

function filterItems(arr) {
    return arr.filter((value) => {
        return value >= 10;
    });
}

console.log(filterItems(number));
// [12, 13, 14]

```

Bem massa ficou nossa função, o que você achou até aqui ?

Mas agora nos daremos um passo para trás.

Vamos retirar nosso callback de dentro da função.

```javascript
let number = [12, 5, 8, 13, 14];

function isBigEnough(value) {
    return value >= 10;
}

function filterItems(arr) {
    return arr.filter(isBigEnough);
}

console.log(filterItems(number));
```

Agora podemos passar ele como parâmetro.


```javascript
let number = [12, 5, 8, 13, 14];

function isBigEnough(value) {
    return value >= 10;
}

function filterItems(arr, callback) {
    return arr.filter(callback);
}

console.log(filterItems(number, isBigEnough));
```

Então, notamos que a função `filterItems` tem apenas uma linha e que ela não tem muita serventia.

Em outras palavras, não precisamos da função, podemos fazer isso diretamente.

```javascript
let number = [12, 5, 8, 13, 14];

function isBigEnough(value) {
    return value >= 10;
}

console.log(number.filter(isBigEnough));
// [12, 13, 14]
```

Eu acho que essa é a melhor versão. E você o que acha ?

Ele é quase uma leitura natural: "número filtrado caso seja o maior"


