------------------------------
### Classes e Objetos

Classe: O "molde". Vamos criar um Funcionario.java. Ele define o que todo funcionário terá.
Objeto: A instância da classe. Será o "João" ou a "Maria", criados a partir do molde Funcionario.

public class Funcionario {
    // Atributos (Características)
    String nome;
    String cargo;
    double salario;

    // Métodos (Ações)
    void trabalhar() {
        System.out.println(nome + " está trabalhando...");
    }
}

public class Main {
    public static void main(String[] args) {
        // new Funcionario() -> Cria o objeto na memória
        Funcionario func1 = new Funcionario();

        // Definindo os valores dos atributos
        func1.nome = "João Silva";
        func1.cargo = "Desenvolvedor";
        func1.salario = 5000.0;

        // Usando o objeto
        System.out.println("Funcionário: " + func1.nome); // Saída: Funcionário: João Silva
        func1.trabalhar(); // Saída: João Silva está trabalhando...
    }
}

------------
### Construtores

public class Funcionario {
    String nome;
    String cargo;
    double salario;

    // Construtor: Obriga a definir nome e cargo na criação
    public Funcionario(String nome, String cargo) {
        this.nome = nome;
        this.cargo = cargo;
        this.salario = 1500.0; // Salário base padrão
    }

    void trabalhar() {
        System.out.println(nome + " está trabalhando...");
    }
}

public class Main {
    public static void main(String[] args) {
        // Agora, os dados são passados na criação do objeto
        Funcionario func1 = new Funcionario("Maria Souza", "Analista de RH");
        
        System.out.println(func1.nome + " - " + func1.cargo); // Saída: Maria Souza - Analista de RH
    }
}

-------
### Encapsulamento

O acesso direto será bloqueado (private) e o controle será feito por métodos públicos (get e set).

public class Funcionario {
    private String nome;
    private String cargo;
    private double salario;

    public Funcionario(String nome, String cargo) {
        this.nome = nome;
        this.cargo = cargo;
        this.salario = 1500.0;
    }

    // Getter para nome (Permite ler)
    public String getNome() {
        return this.nome;
    }

    // Setter para salário (Permite alterar com uma regra)
    public void setSalario(double novoSalario) {
        if (novoSalario > this.salario) {
            this.salario = novoSalario;
        } else {
            System.out.println("O novo salário não pode ser menor que o atual.");
        }
    }
    
    public double getSalario() {
        return this.salario;
    }
}

public class Main {
    public static void main(String[] args) {
        Funcionario func1 = new Funcionario("Carlos Lima", "Gerente");

        // func1.salario = 1000; // ❌ ERRO! Não pode acessar diretamente.

        // Jeito correto de interagir
        func1.setSalario(8000.0);
        System.out.println("Salário do " + func1.getNome() + ": R$" + func1.getSalario()); // Saída: Salário do Carlos Lima: R$8000.0
    }
}

--------
### Herança

Vamos criar uma classe específica, Gerente, que herda tudo de Funcionario e adiciona suas próprias características.

// Gerente "é um" Funcionario, então ele herda (extends)
public class Gerente extends Funcionario {
    private int numeroDeSubordinados;

    // Construtor do Gerente
    public Gerente(String nome, String cargo, int numeroDeSubordinados) {
        // super() -> Chama o construtor da classe mãe (Funcionario)
        super(nome, cargo);
        this.numeroDeSubordinados = numeroDeSubordinados;
    }

    // Método específico do Gerente
    public void aprovarDespesa() {
        System.out.println("Despesa aprovada pelo gerente " + getNome());
    }
}

public class Main {
    public static void main(String[] args) {
        Gerente gerente1 = new Gerente("Ana Paula", "Gerente de Projetos", 5);
        
        // Métodos e atributos herdados de Funcionario
        System.out.println("Salário: " + gerente1.getSalario());
        
        // Método próprio do Gerente
        gerente1.aprovarDespesa(); // Saída: Despesa aprovada pelo gerente Ana Paula
    }
}

----------------------------
### Polimorfismo

Vamos criar um método calcularBonus() que funciona de forma diferente para cada pessoa.

public class Funcionario {
    // ... (atributos e construtor anteriores) ...
    
    // Método de bônus padrão
    public double calcularBonus() {
        return this.getSalario() * 0.10; // Bônus de 10% para funcionários
    }
}


public class Gerente extends Funcionario {
    // ... (atributos e construtor anteriores) ...

    @Override // Sobrescrevendo o método para ter um comportamento diferente
    public double calcularBonus() {
        return this.getSalario() * 0.25; // Bônus de 25% para gerentes
    }
}

public class Main {
    public static void main(String[] args) {
        Funcionario func = new Funcionario("João Silva", "Desenvolvedor");
        func.setSalario(5000);

        Gerente gerente = new Gerente("Ana Paula", "Gerente de Projetos", 5);
        gerente.setSalario(10000);

        // O mesmo método se comporta de formas diferentes
        System.out.println("Bônus do Funcionário: " + func.calcularBonus());   // Saída: 500.0
        System.out.println("Bônus do Gerente: " + gerente.calcularBonus()); // Saída: 2500.0
    }
}

---------
### Abstração

Vamos transformar Funcionario em uma classe abstrata. Agora ela é um "contrato" que não pode ser instanciado, apenas herdado, e obriga as classes filhas a implementarem certos métodos.

// abstract -> Agora é um modelo, não pode ser criado um "new Funcionario()"
public abstract class Funcionario {
    private String nome;
    private double salario;
    
    public Funcionario(String nome) {
        this.nome = nome;
    }
    
    // Método abstrato: sem corpo, obrigando as filhas a implementar
    public abstract double calcularBonus();

    // getters e setters ...
    public String getNome() { return nome; }
    public double getSalario() { return salario; }
    public void setSalario(double salario) { this.salario = salario; }
}

// Arquivo: Gerente.java (agora é obrigado a implementar calcularBonus)
public class Gerente extends Funcionario {
    public Gerente(String nome) { super(nome); }

    @Override
    public double calcularBonus() {
        return getSalario() * 0.25;
    }
}

// Arquivo: Desenvolvedor.java (outra classe filha obrigada a implementar)
public class Desenvolvedor extends Funcionario {
    public Desenvolvedor(String nome) { super(nome); }

    @Override
    public double calcularBonus() {
        return getSalario() * 0.15;
    }
}