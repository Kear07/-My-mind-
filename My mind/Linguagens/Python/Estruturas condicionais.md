--------------------------
### IF - ELSE

if idade >= 18:
    print("Você tem mais de 18 anos, portanto você é um adulto")
else:
    print("Você não tem de 18 anos, portanto você é não é um adulto")

----------
###  IF - ELIF - ELSE

if idade < 4:
    print("Você é um bebê")
elif idade < 12:
    print("você é uma criança")
elif idade < 18:
    print("você é um adolescente")
else:
    print("Você é um adulto")

------
### Match case
 
match opcao:
    case 1:
        print("Você escolheu 1")
    case 2:
        print("Você escolheu 2")
    case 3:
        print("Você escolheu 3")
    case _:
        print("Você não escolheu nada")

---
