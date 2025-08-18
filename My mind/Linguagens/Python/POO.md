
---
### Métodos

| Métodos              | Chamando quando        | Exemplo de uso                      | Quando usar                                     |
| -------------------- | ---------------------- | ----------------------------------- | ----------------------------------------------- |
| __init__             | Objeto é criado        | p = Pessoa("Ana", 30)               | Sempre que quiser inicializar atributos         |
| __str__              | print(obj) ou str(obj) | print(p) → `"Nome: Ana, Idade: 30"` | Mostrar texto legível para humanos<br>          |
| __repr__             | repr(obj)              | Pessoa(nome='Ana', idade=30)        | Mostrar formato útil para debug/desenvolvedores |
| __eq__               | obj1 == obj2           | p1 == p2                            | Comparar conteúdo de objetos                    |
| __ne__               | obj1 != obj2           | p1 != p2                            | Comparar desigualdade                           |
| __le__               | obj1 <= obj2           | p1 <= p2                            | Ordenações personalizadas                       |
| __gt__               | obj1 > obj2            | p1 > p2                             | Comparações personalizadas                      |
| __ge__               | obj1 >= obj2           | p1 >= p2                            | Comparações personalizadas                      |
| __add__              | obj1 + obj2            | p1 + p2                             | Quando quer definir uma “adição” própria        |
| __sub__              | obj1 - obj2            | p1 - p2                             | Definir subtração                               |
| __mul__              | obj1 * obj2            | p1 * p2                             | Definir multiplicação                           |
| __truediv__          | obj1 / obj2            | p1 / p2                             | Definir divisão                                 |
| __len__              | len(obj)               | len(turma)                          | Definir tamanho do objeto                       |
| __getitem__          | obj[idx]               | obj[0]                              | Acesso como lista/dicionário                    |
| __setitem__          | obj[idx] = valor       | obj[0] = "João"                     | Modificar item                                  |
| __delitem__          | del obj[idx]           | del obj[0]                          | Remover item                                    |
| __contains__         | valor in obj           | "Ana" in turma                      | Busca rápida                                    |
| __call__             | obj()                  | p()                                 | Tornar objeto “função”                          |
| __enter__ / __exit__ | with obj:              | with Pessoa("Ana", 30):             | Contexto (abrir/fechar recursos)                |
| __iter__             | for x in obj           | for aluno in turma                  | Iterar sobre o objeto                           |
| __next__             | next(obj)              | next(iterator)                      | Iteradores personalizados                       |
### Exemplos práticos

class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

    def __str__(self):
        return f"{self.nome} ({self.idade} anos)"

    def __repr__(self):
        return f"Pessoa(nome={self.nome!r}, idade={self.idade})"

    def __eq__(self, other):
        return self.nome == other.nome and self.idade == other.idade

    def __add__(self, other):
        return self.idade + other.idade

    def __len__(self):
        return len(self.nome)

    def __call__(self):
        print(f"Olá, meu nome é {self.nome}!")

### Exemplos testando
p1 = Pessoa("Ana", 30)
p2 = Pessoa("João", 25)
p3 = Pessoa("Ana", 30)

print(p1)           # __str__
print(repr(p1))     # __repr__
print(p1 == p3)     # __eq__
print(p1 + p2)      # __add__
print(len(p1))      # __len__
p1()                # __call__

---------
### Decoradores

@property         = Transforma um método em um atributo, você chama ele sem parênteses.
@[nome].setter    = Um set personalizado, com menos código + @property (já incluso no método).
@[nome].deleter   = Um set personalizado, com menos código + @property (já incluso no método).
@classmethod      = Usado para modificar atributos da própria classe. (Não use 'self', use 'cls')
@staticmethod     = Uma função que não usa atributos da instância nem da classe (função auxiliar)

---------

### Herança

class Funcionario(Pessoa):
    def __init__(self, nome, idade, salario):
        super().__init__(nome, idade)  # chama o construtor da classe mãe
        self.salario = salario

------
### Polimorfismo

Várias classes diferentes podem ter métodos com o mesmo nome, mas comportamentos diferentes.

----------
### Encapsulamento

class Pessoa:
    def __init__(self):
        self.publico = "Acesso livre"
        self._protegido = "Sugere uso interno"
        self.__privado = "Escondido (name mangling)"

----
### Abstração

from abc import ABC, abstractmethod

class Forma(ABC):   --A class ABC terá o mesmo método
    @abstractmethod
    def area(self):
        pass

----------
### Dataclasses

from dataclasses import dataclass

@dataclass
class Pessoa:
    nome: str
    idade: int
Isso já cria __init__, __repr__, __eq__ e outros automaticamente.

----------

