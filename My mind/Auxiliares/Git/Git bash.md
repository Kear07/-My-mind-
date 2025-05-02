
---
#### Git bash comandos

git help  
git config 
git init                          = Inicia um repositório

git status   

git add .                       //todos arquivod da pasta 
git add                         //arquivo por arquivo 
git clean                       //desconstroi o arquirvo 

git reset arquivo               //volta o arquivo de preparado para modificado 

git commit -a                   //manda direto do modificado para o consolidado 

git commit -m "comentario"      //Comita logo mandando para o estado consolidado  

git restore                     //nome do arquivo volta para o ultimo consolidado. 

 

git clone                       //usando o link do git hub TRAZ O REPOSITORIO REMOTO PARA O LOCAL CRIANDO UMA PASTA. 

 

git remote                      //Mostra as branches  

 

git remote -v                   //Mostra as branches envio e recebimento  

 

git branch -M "nome"            //Muda de master para "nome" 

 

git revert <hash>            //Faz um novo comiit desfazendo o comiit selecionado  hash = 6 primeiros caracteres no git log 

-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-= 

Lunix 

 

ctrl limpa a tela 

 

ls -l //para organizar 

 

ls --help  

 

git remote add oringin https://github.com/Kear07/Indisciplinar.git           --IMPORTANTE DEPOIS DO INIT 

 

git push origin main                            --envia o arquivo ao hub, da classe main 

git pull origin                                 --atualiza o git bash com o github 

git remote                                      --mostra o nome da conexão 

git remote -v                                   --mostra as conexões 

git log                                         --mostra todas os commits 

git log --oneline                               --mostra os commits simplificado 

git pull --rebase origin main                   --atualiza o arquivo 

git branch                                      --mostra quais branch existem 

git branch -a                                   --motra a branch remota 

git branch <NOME>                               --Cria uma com um nome qualquer 

git branch -d <NOME>                            --Exclui a branch 

git branch -D <NOME>                            --Exclui mesmo estando em excecussao 

git checkout classe-criada                      --Muda a branch para classe-criada 

git branch -M "nome"                            //Muda de master para "nome" 

git pull --rebase origin classe-cliente         --Vai baixar as alterações na branch classe-cliente  

git merge classe-cliente -m "comentario"        --atualiza classe, puxando os dados do hub 

git log --oneline                               --Mostra o historico de atts da branch. 

git diff  

git reset                                             --hard CODIGO 