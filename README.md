
# 📚 Guia de Comandos Git (Básico ao Avançado)

Este material é um guia prático de comandos Git voltado para quem já
utiliza Git no dia a dia, mas precisa relembrar rapidamente comandos,
fluxos e boas práticas.

Contém: 
- Explicações diretas e objetivas
- Exemplos reais de uso

Ideal para: 
- Devs que já trabalham com Git
- Revisão rápida no dia a dia

------------------------------------------------------------------------

## 1. Inicializa o git para fazer o versionamento no repositório

Exemplo:
``` bash
  git init
```

## 2. Remove inicialização incorreta do ```git init``` na pasta incorreta

Exemplo:
``` bash
  rm -rf .git
```

## 3. Adiciona um repositório remoto criado (vazio) em uma pasta criada localmente de um novo projeto

Exemplo:
``` bash
  git remote add origin link_do_github_aqui.git
```

> Fluxo de utilização desse comando:
> 1. Crie a pasta do projeto
> 2. Desenvolva o projeto dentro dela
> 3. Crie o repositório remoto sem README
> 4. Na pasta do projeto, execute o comando para vincular o repositório remoto ao local.

## 4. Visualizar histórico

4.1 Exibe de forma verbosa todos os logs

Exemplo:
``` bash
  git log
```

4.2 Exibe todos os logs de forma resumida em uma linha

Exemplo:
``` bash
  git log --oneline
```

4.3 Exibe de forma verbosa os 3 últimos logs

Exemplo:
``` bash
  git log -3
```

4.4 Exibe de forma verbosa o log de um arquivo específico

Exemplo:
``` bash
  git log -- src/main/java/service/ArquivoService.java
```

4.5 Exibe de forma verbosa o log de um diretório específico

Exemplo:
``` bash
  git log -- node_modules/
```

4.6 Exibe de forma gráfica os logs, as IDEs tb fazem isso sem esse comando

Exemplo:
``` bash
  git log --graph
```

4.7 Exibe o histórico com a diferença das duas últimas alterações

Exemplo:
``` bash
  git log -p -2
```

4.8 Exibe resumo do histórico

Exemplo:
``` bash
  git log --stat
```
> Exibir resumo do histórico
> (hash completa, autor, data, comentário e quantidade de alterações (+/-)

Exemplo:
``` bash
  git log --pretty=format:"%h - %an, %ar : %s"
```
> Fluxo de utilização desse comando:
> 1. %h: Abreviação do hash;
> 2. %an: Nome do autor;
> 3. %ar: Data;
> 4. %s: Comentário

Exemplo:
``` bash
  git log --diff-filter=M -- src/main/java/service/ArquivoService.java
```
> Fluxo de utilização desse comando(Exibir histórico modificação de um arquivo):
> - "M" pode ser substituido por:
> - Adicionado (A), Copiado (C), Apagado (D),
> - Modificado (M), Renomeado (R), entre outros.

Exemplo:
``` bash  
  git log --author=usuario
```
> Exibir histório de um determinado autor

## 5. Remove o arquivo do stage

5.1 Exemplo:
``` bash
git reset ARQUIVO.JAVA
```

5.2 Exemplo:
``` bash
git rm --cached nome_do_arquivo.java
```

## 6. Realiza o commit com a mensagem

Exemplo:
``` bash
  git commit -m 'mensagem'
```

## 7. Adicionando um arquivo esquecido ao commit anterior sem alterar a mensagem

Exemplo:
``` bash
  git commit --amend --no-edit
```

## 8. Alterar mensagem de commit

Exemplo:
``` bash
  git commit --amend -m 'Estou corrigindo a mensagem do ultimo commit'
```

## 9. Lista as branches

Exemplo:
``` bash
  git branch -a
```
> Lista branches locais e remotas

Exemplo:
``` bash
  git branch -r
```
> Lista somente branches remotas

## 10. Mostra branches locais + último commit de cada branch.

Exemplo:
``` bash
  git branch -v
```

## 11. Lista os repositórios remotos

Exemplo:
``` bash
  git remote
```
> Listar  remota

Exemplo:
``` bash
  git remote -v
```
> Mostra os remotes + URLs

## 12. Configura tracking da branch

Exemplo:
``` bash
  git push --set-upstream origin NOME-BRANCH
```
> Depois disso você pode usar: git push

Exemplo:
``` bash
  git push -u origin NOME-BRANCH
```
> Depois disso você pode usar: git push

## 13. Melhor prática quando quer revisar antes:

Exemplo:
``` bash
  git fetch
  git log origin/main
  git merge origin/main
```
> **git fetch**: comando que busca branches e/ou tags (coletivamente, "refs") de um ou mais outros repositórios, juntamente com os objetos necessários para completar seus históricos. Muito usado quando estamos trabalhando em um repositório que é constantemente atualizado.

## 14. ```git rebase``` reaplica seus commits em cima de outra base

Exemplo:
``` bash
  git rebase branch_aqui
```
> Exemplo de uso:
> git checkout feature
> git rebase main

## 15. Descartar alterações do arquivo

Exemplo:
``` bash
  git checkout -- .
```
> Descarta de todos os arquivos - ANTIGO

Exemplo:
``` bash
  git restore .
```
> Descarta de todos os arquivos - MODERNO

Exemplo:
``` bash
git checkout -- nomeArquivo.java
git restore nomeArquivo.java
```
> Descarta de arquivos específicos (utilize um ou outro)

## 16. Git rebase: Reaplica os commits da branch atual em cima de outra branch, criando um histórico linear. Muito usado para atualizar uma branch de feature com as mudanças da branch principal

16.1 Exemplo de uso do git rebase:
``` bash
  git checkout feature-login
  git rebase main
```
``` markdown
O Git pega os commits da feature-login, move o ponteiro para o topo da 
main e reaplica os commits da feature como se tivessem sido feitos 
depois da main.

Antes do rebase:
main
A---B---C

feature
     \---D---E
     

Depois do rebase:
main
A---B---C

feature
         \---D'---E'
         
Os commits são recriados (D' e E') e recebem novos hashes.

Regra importante
Evite usar rebase em commits que já foram enviados para o repositório 
remoto, pois ele altera o histórico.
```

16.2 Exemplo de uso do ```git rebase -i```
``` markdown
  Permite editar, reorganizar, juntar ou remover commits antes de 
  reaplicá-los na nova base. Muito usado para limpar histórico antes 
  de fazer push ou abrir um Pull Request.
```

Exemplo:
``` bash
  git rebase -i HEAD~3
```

``` markdown
  Abre um editor com os 3 últimos commits.
  Exemplo do editor:
  
  pick a1b2c3 Cria entidade Usuario
  pick d4e5f6 Cria endpoint de login
  pick g7h8i9 Corrige bug no login
  
  
  Comandos possíveis:
  pick   → mantém o commit
  reword → altera a mensagem do commit
  edit   → pausa o rebase para editar o commit
  squash → junta o commit com o anterior
  drop   → remove o commit
  
  
  Exemplo juntando commits:
  pick a1b2c3 Cria entidade Usuario
  pick d4e5f6 Cria endpoint de login
  squash g7h8i9 Corrige bug no login
  
  Resultado:
  1 commit:
  Cria endpoint de login (com correção incluída)
  
  
  Continuar o rebase após edição:
```

Exemplo:
``` bash
  git add .
  git commit --amend
  git rebase --continue
```

## 17. Caso você tenha usado o git rebase e ocorrido um conflito que você já resolveu com um commit, use este comando para forçar a atualização remota da branch. Cuidado ao usar este comando quando duas pessoas estão trabalhando na mesma branch

Exemplo:
``` bash
  git push origin feature/a --force
```

## 18. Seleciona um commit específico de outra branch e aplica suas alterações na branch atual. Útil para trazer commits validados da develop ou stage para a branch de produção (main), ou para pegar um commit específico de um colega utilizando o hash do commit

Exemplo:
``` bash
  git cherry-pick hash_commit_aqui
```

## 19. Compara commits, branches ou arquivos

Exemplo:
``` bash
  git diff A_aqui B_aqui
```

## 20. Mostra detalhes de um commit

Exemplo:
``` bash
  git show hash_commit_aqui
```

## 21. Remover arquivo/diretório

2.1 Remove o arquivo (quando você quer deletar o arquivo)

Exemplo:
``` bash
git rm UsuarioService.java
git commit -m "Remove classe não utilizada"
```
> Fluxo de utilização desse comando:
> 1. Remove o arquivo da pasta do projeto
> 2. Adiciona a remoção no stage automaticamente
> 3. Precisa fazer commit para confirmar

2.2 Remove o diretório (quando você quer deletar o diretório)

Exemplo:
``` bash
  git rm diretorio_utils
  git commit -m "Remove pasta utils"
```
> Fluxo de utilização desse comando:
> 1. Remove o diretório do projeto
> 2. Adiciona a remoção no stage automaticamente
> 3. Precisa fazer commit para confirmar

2.3 Remove o arquivo/diretório (quando você quer ignorar no versionamento)

Exemplo:
``` bash
  git rm --cached dados.txt
  git commit -m "Remove dados.txt do versionamento"
```
> Fluxo de utilização desse comando:
> 1. Remove o arquivo do versionamento do git, mas mantém o arquivo no computador
> 2. Adiciona a remoção do arquivo no stage automaticamente
> 3. Precisa fazer commit para confirmar
> 4. ATENÇÃO: Após isso, adicione o arquivo no .gitignore para evitar que ele seja versionado novamente

## 22. Deletar uma branch
22.1 Deletar branch após o merge

Exemplo:
``` bash
  git branch -d nome_da_branch
```

22.2 Força deletar branch sem o merge

Exemplo:
``` bash
  git branch -D nome_da_branch
```

## 23. Arquivar alterações

23.1 Arquiva as alterações não commitadas

Exemplo: 
``` bash
  git stash
```

23.2 Lista as alterações arquivados

Exemplo: 
``` bash
  git stash list
```

23.3 Aplica as alterações arquivadas

Exemplo: 
``` bash
  git stash apply
```

23.4 Desarquiva as alterações

Exemplo: 
``` bash
  git stash pop
```

23.5 Apagar as alterações arquivadas

Exemplo: 
``` bash
  git stash drop
```

## 24. Criar e entrar na branch

24.1 Cria e entra - ANTIGO

Exemplo:
``` bash
  git checkout -b feature/nome-branch
```

24.2 Cria e entra - MODERNO

Exemplo:
``` bash
  git switch -c feature/nome-branch
```

24.3 Entra - ANTIGO

Exemplo:
``` bash
  git checkout feature/nome-branch
```

24.4 Entra - MODERNO

Exemplo:
``` bash
  git switch feature/nome-branch
```

## 25. Desfazer commit local
> Obs.: Posso trocar HEAD~2 pelo hash do commit, mas isso é ruim, só é bom desfazer commit que são recentes
> Possui 4 opções:

25.1 
``` bash
git reset --hard HEAD~2
git reset --mixed HEAD~2
git reset --soft HEAD~1
git revert hash-do-commit
```

## 26. Desfazer commit remoto

``` bash
git log -2
git revert hash-do-commit
git push nome-branch
```

## 27. Ignorar arquivo ou pasta

``` bash
echo arquivo.txt >> .gitignore
echo node_modules_nome_pasta/ >> .gitignore
```

## 28. Renomear repositório remoto

``` bash
git remote set-url origin NOVA_URL_DO_REPOSITORIO
```

## 29. Vincular repositório local com repositório remoto

``` bash
git remote add origin git@github.com:deise/curso-git.git
```

## 30. Clonar apenas uma branch específica

``` bash
git clone git@github.com:deisesalless/nome_do_repositorio_ssh.git --branch nome_branch_especifica --single-branch
```

------------------------------------------------------------------------

# 🚀 Observação final

Esse guia é focado em produtividade no dia a dia.\
Não substitui documentação oficial, mas evita perder tempo lembrando
comandos básicos/intermediários.
