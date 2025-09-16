-------------------------
### Tipos de dados

String var           = Tipo texto.
int var              = Tipo inteiro numérico.
double var           = Tipo decimal numérico.
boolean var          = Tipo verdadeiro ou falso.

----------
### Operadores matemáticos

[+]	 Soma.
[-]	 Subtração.
[*]	 Multiplicação.
[/]	 Divisão.
[//] Divisão exata.
[%]	 Resto.

--------------
### Operadores de Comparação 

[==] Igual a.
[!=] Diferente de.
[<]	 Menor que.
[>]	 Maior que.
[<=] Menor ou igual a.
[>=	 Maior ou igual a.

-----------
### Operadores Lógicos

[&&] Operador "E".
[||] Operador "OU".
[!]	 Operador de negação "NÃO".

-----
### Operadores de Atribuição

[=]	 Define/Atribui valor.
[+=] Adiciona e atribui.
[-=] Subtrai e atribui.
[*=] Multiplica e atribui.	
[/=] Divide e atribui.

-----
### Input/Entrada

import java.util.Scanner;                   = Importa a classe.
Scanner input = new Scanner(System.in);     = Cria o objeto input.
System.out.print("Digite seu nome: ");      = Exibe algo no terminal.

String var = input.nextLine();              = Salva na variável de texto.
int var = input.nextInt();                  = Salva na variável de inteiro.
double var = input.nextDouble();            = Salva na variável de quebrado.
boolean var = input.nextBoolean();          = Salva na variável de verdadeiro ou falso. 

input.close();                              = Fecha o input quando não for mais usar.

-------

### Print (exibição)

System.out.println()	                    = Exibe algo e pula uma linha.
System.out.printf()                         = Exibe algo com variáveis.
System.out.printf("Me chamo %s", nome,);    

[%s] = Para textos (String).
[%d] = Para números inteiros (int).
[%f] = Para números com casas decimais (double).
[%c] = Para um único caractere (char).
[%b] = Booleano	para valores true ou false.
[%n] = Pula linha.

---------
### Sequências de Escape

[\n]  = Nova Linha (pula uma linha)
[\t]  = Tabulação (adiciona um espaço de tabulação)
[\r]  = Retorno de Carro (sobrescreve o início da linha)
[\\]	  = Exibe uma barra invertida (\)
[\"]   = Exibe aspas duplas (")