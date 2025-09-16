---------
### Repetição For

for (inicialização; condição; incremento) {
    // Bloco de código a ser repetido
}


for (int x = 1; x <= 5; x++) {
    System.out.println("O número atual é: " + x);
}

----------
### Repetição While

while (condição) {
    // Bloco de código a ser repetido
    // É crucial ter uma linha aqui que altere a variável da condição!
}


while (download <= 10) {
    System.out.println("Baixando... " + download);
    download += 1; 
}

-----------------
### Repetição Do while

do {
    // Bloco de código que executa pelo menos uma vez
} while (condição);

// Excelente para menus, pois executa primeiro, e depois verifica
