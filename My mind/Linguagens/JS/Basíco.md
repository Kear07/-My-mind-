------
### Declaração de variáveis 

var      = Forma antiga, possui alguns bugs
let      = Forma atual, variável comum
const    = Variável fixa, só se pode alterar o valor se for do tipo array

var d = 10
var e = 20
var f = 30

let a = 10;
let b = 20;
let c = 30;

const g = 10;
const h = 20;
const i = 30;

------
### Seleção de elemento

.getElementById("")               = Seleciona um elemento por id
.getElementsByClassName("")       = Seleciona um elemento por class
.getElementsByTagName("")         = Seleciona um elemento por tag html

-----
### Após seleção de elemento

.style.color              = Define uma cor
.style.padding            = Define um top
.style.margin             = Define uma margin
.style.border             = Define uma borda
...

------
### Operadores Aritméticos

"+"     = Adição
"-"     = Subtração
"*"     = Multiplicação 
"/"     = Divisão
### Operadores de comparação

"=="     = Igual
"!="    = Diferente
">"     = Maior que
"<"     = Menor que 
">="    = Maior ou igual a
"<="    = Menor ou igual a

### Operadores lógicos
&&      = Argumento "e"
||      = Argumento "ou"
!       = Argumento de negação
===     = Usado para comparação estrita, verificando tanto o valor quanto o tipo
!===    = Usado para negação estrita, verificando tanto o valor quanto o tipo

### Operadores de atribuição

=       = Atribuição
+=      = Adição
-=      = subtração 
*=      = Multiplicação
/=      = Divisão
 
### Operador ternário

Condição ? valor se verdadeiro : valor se falso
let resultado = (idade >= 18) ? "Maior de idade" : "Menor de idade";

----
### Exibição no html

.innerHTML
ex:
document.getElementById("id").innerHTML = "Meu primeiro texto em <b>JavaScript</b>";
