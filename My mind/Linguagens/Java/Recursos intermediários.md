----------
### Arrays (Vetores)

// Declaração e Inicialização

// 1ª Forma: Declarando o tamanho primeiro
String[] nomes = new String[4]; // Cria um "armário" com 4 gavetas vazias para Strings.


// Atribuindo valores a cada posição (índice)
nomes[0] = "Goku";
nomes[1] = "Vegeta";
nomes[2] = "Gohan";
nomes[3] = "Piccolo";

// 2ª Forma: Declarando já com os valores
double[] notas = { 8.5, 9.0, 7.5, 10.0 };


// --- Acessando e Usando os Dados ---

System.out.println("O primeiro lutador é: " + nomes[0]); // Saída: Goku
System.out.println("A terceira nota é: " + notas[2]);    // Saída: 7.5

System.out.println("\nLista de Lutadores:");
for (int i = 0; i < nomes.length; i++) {
    System.out.println("Posição " + i + ": " + nomes[i]);
}

------------


