
---
### While comum

x = 0
while x != 10:
    x += 1
    print(f"x é = {x}")

-------------
### While True

x = 0        
while True:
    x += 2
    if x == 100:
        print(f"X é = {x}")
        break 

---
### For in range normal

for x in range(4):  
    print(f"x vale: {x}")

----
### For in range completo

for i in range(1, 11, 2):  # Começa em 1, vai até 10, pulando de 2 em 2
    print(i)

----
### For para listas

frutas = ["maçã", "banana", "uva"]
for f in frutas:
    print(f"A fruta da vez é {f}")

----
### For para dicionário

pessoa = {"nome": "Ana", "idade": 25, "cidade": "São Paulo"}

for chave, valor in pessoa.items():
    print(f"{chave}: {valor}")

----
### Resumo

for                   = Percorre listas, strings, dicionários e muito mais
range()               = Gera sequências de números
enumerate()           = Fornece índice e valor
break                 = Interrompe o loop
continue              = Pula uma iteração
else                  = Executa ao final do for