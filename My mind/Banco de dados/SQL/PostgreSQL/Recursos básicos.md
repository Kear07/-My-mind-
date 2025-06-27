
---
### Funções básicas

current_date                                     = Exibe a data atual 
current_time                                     = Exibe o horário atual 
now()                                            = Exibe data e horário atual

show datestyle                                   = Exibe o modelo de data atual
set datestyle = 'ISO, DMY'                       = Altera o modelo de data 
set datestyle = 'ISO, MDY'                       = Altera o modelo de data

alter table [table] add [nome tipo]              = Adiciona um coluna
update [table] set [colun] = 10                  = Altera o valor da coluna 
delete from [colun] where [valor] < 10           = Remove o valor de uma colun
alter table [table] drop [colun]                 = Remove uma coluna  

select * from [table]                            = Exibe uma tabela
alter table [table] rename to [table2]           = Renomeia uma tabela
drop table [table]                               = Deleta uma tabela 
truncate table [table]                           = Deleta os dados da tabela 

---------
### Restrições para tabelas

alter table [table] alter column [colun] set not null   = Não aceita nulos
alter table [table] alter column [colun] set unique     = Não aceita repetidos alter table [table] alter column [colun] set unique     = Aceita tudo 

alter table [table] add check (id > 18)                 = Condição if números
alter table [table] add check ('a')                     = Condição if letras

alter table [table] add constraint [colun coned]         = Condição pós criação

---

### Tipos primitivos

varchar              = String 
varchar(x)           = [X] strings
char                 = Um caractere 

smalint              = De -32768 a 32767 
int                  = De -2147483648 a -2147483648 
bigint               = De -9+++19 a 9++19 

decimal(x,y)         = [x] dígitos e [y] depois da vírgula
numeric(x,y)         = [x] dígitos e [y] depois da vírgula

real                 = Até 6 casa decimais; 
double precision     = Até 15 casa decimais; 

smallserial          = Contador de 1 a 32.767
serial               = Contador de 1 a 2147483647
bigserial            = Contador de 1 a 9223372036854775807

date                 = Datas 

---
### Funções básicas para números

select [colun] from [table] order by [colun]         = Põe em ordem crescente
select [colun] from [table] order by [colun] desc    = Põe em ordem decrescente

select distinct([colun]) from [table]                = Remove os duplicados

select round([colun], 2) from [table]                = Arredonda em x decimais
select trunc([colun], 0) from [table]                = Remove x decimais

select abs([colun]) from [table]                     = Exibe o valor absoluto

select |/[colun] from [table]                        = Exibe a raiz quadrada 
select ||/[colun] from [table]                       = Exibe a raiz cúbica

select power(9, 3)                                   = Exibe a potenciação 

select ceil([colun]) from [table]                    = Arredonda pra cima  
select floor([colun]) from [table]                   = Arredonda pra inteiro 

select random()                                      = Gera um número de 0 a 1

---
### Funções básicas para texto

select [text1] || [text2]                      = Concatena textos 
select char_length('Kear');                    = Exibe a quantidade de caracter

select lower([text]);                          = Transforma tudo em maiúsculo 
select upper([text]);                          = Transforma tudo em minúsculo

select substring('Maça', 1, 4)                 = Exibe por posição

select initcap('kear')                         = Inicia com letra maiúscula

select '4211'::int                             = Transforma em inteiro 
select 4211::varchar                           = Transforma em texto 

select reverse('Kear_07')                      = Inverte o texto 
select right('Kear_07', 2);                    = Exibe os últimos caracteres

----
### Manipulação de texto

select 'abc' like 'a%';  
select 'abc' similar to '%(b|d)%'   

O operador % = '%Batata%' = nao importa oque vem antes ou depois
O operador _ = '__Batata' = procure depois de 2 caractetres
O operador | = '(B | b)atata' = procore por B e b



https://halleyoliv.gitlab.io/pgdocptbr/functions.html  --Funções 