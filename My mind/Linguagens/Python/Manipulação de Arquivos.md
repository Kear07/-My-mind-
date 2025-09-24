-------------------
### Sintáxe

with open('arquivo.txt', 'w', encoding='utf-8') as arquivo:
    # executa operações no arquivo aqui
    arquivo.write("Olá, mundo!\n")
    arquivo.write("Esta é uma nova linha.")

----------
### Modos de Abertura

O segundo argumento da função open() define como o arquivo será aberto.

'r'	                     = Abre um arquivo para leitura. Gera erro se não existir.
'w'	                     = Apaga o conteúdo se o arquivo já existir. Cria um novo se não existir.
'a'	                     = Abre para escrita, adicionando o novo conteúdo ao final do arquivo. Cria se não existir.
'r+'	                 = Abre o arquivo para ler e escrever.
'b'	Binário              = Usado em conjunto com outros modos ('rb', 'wb') para arquivos que não são de texto.
't'	Texto Padrão         = Usado para arquivos de texto.

-------
### Métodos de Leitura

Usados dentro do bloco with quando o modo permite leitura ('r', 'r+').

with open('arquivo.txt', 'r', encoding='utf-8') as arquivo:
    
    # Opção 1: Ler o arquivo inteiro
    conteudo_completo = arquivo.read()

    # Opção 2: Ler linha por linha em uma lista
    # arquivo.seek(0) # Volta o cursor para o início do arquivo
    lista_de_linhas = arquivo.readlines()
    
    # Opção 3: Ler uma única linha
    # arquivo.seek(0)
    primeira_linha = arquivo.readline()

    # Opção 4 (recomendada): Iterar sobre as linhas
    # arquivo.seek(0)
    for linha in arquivo:
        print(linha.strip()) # .strip() remove espaços e quebras de linha indesejadas

-------
### Métodos de Escrita

Usados quando o modo permite escrita ('w', 'a', 'r+').


linhas = ["Primeira linha.\n", "Segunda linha.\n", "Terceira linha.\n"]

with open('arquivo.txt', 'w', encoding='utf-8') as arquivo:
    
    # Opção 1: Escrever uma string de cada vez
    arquivo.write("Olá!\n")

    # Opção 2: Escrever todos os itens de uma lista
    arquivo.writelines(linhas_para_escrever)
-------
### Complemento com a biblioteca "os"

Para verificar se um arquivo existe ou para removê-lo, usamos o módulo os.

import os
caminho_arquivo = 'arquivo.txt'


if os.path.exists(caminho_arquivo):
    print(f"O arquivo '{caminho_arquivo}' existe.")
    
    # Remover o arquivo
    # os.remove(caminho_arquivo)
    # print(f"O arquivo '{caminho_arquivo}' foi removido.")
else:
    print(f"O arquivo '{caminho_arquivo}' não existe.")