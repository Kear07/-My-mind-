------
## Listas (arrays)

let frutas = ["maçã", "banana", "laranja", "uva"];
frutas.push([""]);                           = Adiciona um elemento no final
frutas.pop();                                     = Remove o último elemento
frutas.shift();                                   = Remove o primeiro elemento
frutas.unshift([""]);                        = Adiciona um elemento no início
frutas.splice(1, 2);                              = Remove 2 elementos a partir do índice
console.log(frutas[0]);                           = Acessa o primeiro elemento

---
### Objetos (dicionários , JSON)

let pessoa = {
    nome: "João",
    idade: 30,
    cidade: "São Paulo"
};