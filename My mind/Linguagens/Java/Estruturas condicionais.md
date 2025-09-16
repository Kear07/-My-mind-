--------------------------
### IF - ELSE IF - ELSE

if ([condição]) {System.out.println();} 
else if ([condição]) {System.out.println();} 
else {System.out.println();}

----
### Switch case

int var = 1

switch (var) {
    case 1:
        // Código para o caso var = 1
        break;
    case 2:
        // Código para o caso var = 2
        break;
    default:
        // Código executado se nenhum dos casos acima for correspondido (similar ao 'else')
}

---------
### Dica de Ouro: 

Para comparar Strings em Java, NUNCA use == 
Use sempre o método .equals()!

if (nome == "Ana")      ❌ ERRADO (compara a posição na memória)
if (nome.equals("Ana")) ✅ CORRETO (compara o conteúdo do texto)



