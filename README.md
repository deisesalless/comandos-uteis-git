
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

``` bash
git init
```

## 2. Remover inicialização incorreta do git init na pasta incorreta

``` bash
rm -rf .git
```

## 3. Adiciona um repositório remoto criado (vazio) em uma pasta criada localmente de um novo projeto

``` bash
git remote add origin link_do_github_aqui.git
```

> O correto é você primeiro criar a pasta do seu projeto e criar o
> projeto de fato, depois você cria o seu repositório sem o readme, dai
> você entra na pasta do seu projeto e dá o comando

------------------------------------------------------------------------

## 4. Visualizar histórico

``` bash
git log
// exibe de forma verbosa todos os logs

git log --oneline
// exibe de forma resumida em uma linha todos os logs

git log -3
// exibe de forma verbosa os 3 últimos logs

git log -- src/main/java/service/ArquivoService.java
// exibe de forma verbosa o log de um arquivo específico

git log -- node_modules/
// exibe de forma verbosa o log de um diretório específico

git log --graph
// exibe de forma gráfica os logs, as IDEs tb fazem isso sem esse comando

git log -p -2
// Exibe o histórico com a diferença das duas últimas alterações

git log --stat
/*
Exibir resumo do histórico 
(hash completa, autor, data, comentário e quantidade de alterações (+/-)
*/

git log --pretty=format:"%h - %an, %ar : %s"
/*
%h: Abreviação do hash;
%an: Nome do autor;
%ar: Data;
%s: Comentário
*/

git log --diff-filter=M -- src/main/java/service/ArquivoService.java
/*
Exibir histórico modificação de um arquivo
"M" pode ser substituido por: 
Adicionado (A), Copiado (C), Apagado (D), 
Modificado (M), Renomeado (R), entre outros.
*/

git log --author=usuario
// Exibir histório de um determinado autor
```

------------------------------------------------------------------------

## 5. Remove o arquivo do stage

``` bash
git reset ARQUIVO.JAVA

// ou

git rm --cached nome_do_arquivo.java
```

------------------------------------------------------------------------

## 6. Adicionando um arquivo esquecido ao commit anterior sem alterar a mensagem

``` bash
git commit --amend --no-edit
```

------------------------------------------------------------------------

## 7. Alterar mensagem de commit

``` bash
git commit --amend -m 'Estou corrigindo a mensagem do ultimo commit'
```

------------------------------------------------------------------------

## 8. Lista as branches

``` bash
git branch -a
// lista branches locais e remotas

git branch -r
// lista somente branches remotas
```

------------------------------------------------------------------------

## 9. Lista os repositórios remotos

``` bash
git remote
// listar  remota

git remote -v
// mostra os remotes + URLs
```

------------------------------------------------------------------------

## 10. Mostra branches locais + último commit de cada branch.

``` bash
git branch -v
```

------------------------------------------------------------------------

## 11. Configurar tracking da branch

``` bash
git push --set-upstream origin NOME-BRANCH
// ou
git push -u origin NOME-BRANCH
```

> Isso configura **tracking da branch**. Depois disso você pode usar:

``` bash
git pull
git push
```

------------------------------------------------------------------------

## 12. Melhor prática quando quer revisar antes:

``` bash
git fetch
git log origin/main
git merge origin/main
```

> git fetch: comando que busca branches e/ou tags (coletivamente,
> "refs") de um ou mais outros repositórios, juntamente com os objetos
> necessários para completar seus históricos. Muito usado quando estamos
> trabalhando em um repositório que é constantemente atualizado.

------------------------------------------------------------------------

## 13. Fetch + Pull separado

``` bash
git fetch 
// (aqui vai retornar tudo que foi modificado e aonde, antes de fazer o pull)

git pull
//(aqui atualiza direto)
```

------------------------------------------------------------------------

## 14. git rebase reaplica seus commits em cima de outra base.

``` bash
git rebase branch_aqui
```

/* Exemplo de uso: git checkout feature/login git rebase main */

------------------------------------------------------------------------

## 15. Descartar alterações do arquivo

``` bash
git checkout -- .
// descarta de todos os arquivos - ANTIGO

git restore .
// descarta de todos os arquivos - MODERNO

// exemplo de arquivos específicos:
git checkout -- nomeArquivo.java
git restore nomeArquivo.java
```

------------------------------------------------------------------------

## 16. Git rebase (explicação completa)

``` bash
git checkout feature-login
git rebase main
```

Antes do rebase: main A---B---C

feature ---D---E

Depois do rebase: main A---B---C

feature ---D'---E'

Os commits são recriados (D' e E') e recebem novos hashes.

Regra importante\
Evite usar rebase em commits que já foram enviados para o repositório
remoto, pois ele altera o histórico.

------------------------------------------------------------------------

## 17. Force push após rebase

``` bash
git push origin feature/a --force
```

------------------------------------------------------------------------

## 18. Cherry-pick

``` bash
git cherry-pick hash_commit_aqui
```

------------------------------------------------------------------------

## 19. Comparar commits, branches ou arquivos

``` bash
git diff A_aqui B_aqui
```

------------------------------------------------------------------------

## 20. Mostrar detalhes de um commit

``` bash
git show hash_commit_aqui
```

------------------------------------------------------------------------

## 21. Remover arquivo/diretório

``` bash
git rm UsuarioService.java
git commit -m "Remove classe não utilizada"
```

``` bash
git rm diretorio_utils
git commit -m "Remove pasta utils"
```

``` bash
git rm --cached dados.txt
git commit -m "Remove dados.txt do versionamento"
```

------------------------------------------------------------------------

## 22. Apagar uma branch

``` bash
git branch -d nome_da_branch
// após o merge

git branch -D nome_da_branch
// força apagar a branch
```

------------------------------------------------------------------------

## 23. Git stash

``` bash
git stash
// arquiva as alterações não commitadas

git stash list
// lista as alterações arquivados

git stash apply
// aplica as alterações arquivadas

git stash pop
// desarquiva as alterações

git stash clear
// apagar as alterações arquivadas
```

------------------------------------------------------------------------

## 24. Criar e entrar na branch

``` bash
git checkout -b feature/nome-branch
// antigo - cria e entra

git switch -c feature/nome-branch
// novo - cria e entra

git checkout feature/nome-branch
// antigo - entra

git switch feature/nome-branch
// novo - entra
```

------------------------------------------------------------------------

## 25. Desfazer commit local

``` bash
git reset --hard HEAD~2
git reset --mixed HEAD~2
git reset --soft HEAD~1
git revert hash-do-commit
```

------------------------------------------------------------------------

## 26. Desfazer commit remoto

``` bash
git log -2
git revert hash-do-commit
git push nome-branch
```

------------------------------------------------------------------------

## 27. Ignorar arquivo ou pasta

``` bash
echo arquivo.txt >> .gitignore
echo node_modules_nome_pasta/ >> .gitignore
```

------------------------------------------------------------------------

## 28. Renomear repositório remoto

``` bash
git remote set-url origin NOVA_URL_DO_REPOSITORIO
```

------------------------------------------------------------------------

## 29. Vincular repositório local com repositório remoto

``` bash
git remote add origin git@github.com:deise/curso-git.git
```

------------------------------------------------------------------------

## 30. Clonar apenas uma branch específica

``` bash
git clone git@github.com:deisesalless/nome_do_repositorio_ssh.git --branch nome_branch_especifica --single-branch
```

------------------------------------------------------------------------

# 🚀 Observação final

Esse guia é focado em produtividade no dia a dia.\
Não substitui documentação oficial, mas evita perder tempo lembrando
comandos básicos/intermediários.
