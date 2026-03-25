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

## 1. Inicializar repositório Git

Inicializa o Git em uma pasta para começar o versionamento.

``` bash
git init
```

------------------------------------------------------------------------

## 2. Remover inicialização Git incorreta

Remove o repositório Git caso ele tenha sido iniciado na pasta errada.

``` bash
rm -rf .git
```

------------------------------------------------------------------------

## 3. Vincular repositório local a um remoto

Adiciona um repositório remoto a um projeto local existente.

``` bash
git remote add origin LINK_DO_REPOSITORIO.git
```

Fluxo comum:

1.  Criar a pasta do projeto
2.  Desenvolver o projeto localmente
3.  Criar o repositório remoto **sem README**
4.  Executar o comando para vincular o remoto

------------------------------------------------------------------------

## 4. Visualizar histórico de commits

### Histórico completo

``` bash
git log
```

### Histórico resumido

``` bash
git log --oneline
```

### Últimos commits

``` bash
git log -3
```

### Histórico de um arquivo

``` bash
git log -- src/main/java/service/ArquivoService.java
```

### Histórico de um diretório

``` bash
git log -- node_modules/
```

### Histórico gráfico

``` bash
git log --graph
```

### Diferença entre commits recentes

``` bash
git log -p -2
```

### Resumo das alterações

``` bash
git log --stat
```

### Log formatado

``` bash
git log --pretty=format:"%h - %an, %ar : %s"
```

Campos utilizados:

-   `%h` → hash abreviado
-   `%an` → autor
-   `%ar` → data relativa
-   `%s` → mensagem do commit

------------------------------------------------------------------------

## 5. Remover arquivo do stage

Remove o arquivo do stage, mantendo no diretório.

``` bash
git reset ARQUIVO.JAVA
```

ou

``` bash
git rm --cached nome_do_arquivo.java
```

------------------------------------------------------------------------

## 6. Alterar último commit

Adicionar arquivo esquecido ao commit anterior:

``` bash
git commit --amend --no-edit
```

Alterar mensagem do último commit:

``` bash
git commit --amend -m "Nova mensagem"
```

------------------------------------------------------------------------

## 7. Listar branches

Listar branches locais e remotas:

``` bash
git branch -a
```

Listar apenas remotas:

``` bash
git branch -r
```

Mostrar último commit de cada branch:

``` bash
git branch -v
```

------------------------------------------------------------------------

## 8. Listar repositórios remotos

``` bash
git remote
```

Mostrar URLs:

``` bash
git remote -v
```

------------------------------------------------------------------------

## 9. Configurar tracking da branch

``` bash
git push --set-upstream origin NOME-BRANCH
```

ou

``` bash
git push -u origin NOME-BRANCH
```

Depois disso basta usar:

``` bash
git push
```

------------------------------------------------------------------------

## 10. Revisar antes de fazer merge

``` bash
git fetch
git log origin/main
git merge origin/main
```

`git fetch` busca atualizações do remoto sem aplicar automaticamente.

------------------------------------------------------------------------

## 11. Rebase

Reaplica commits da branch atual em outra base.

``` bash
git checkout feature
git rebase main
```

Antes:

    main     A---B---C
                  \
    feature        D---E

Depois:

    main     A---B---C
                  \
    feature        D'---E'

⚠️ Evite usar rebase em commits já enviados ao remoto.

------------------------------------------------------------------------

## 12. Rebase interativo

Permite editar commits.

``` bash
git rebase -i HEAD~3
```

Comandos principais:

    pick   → mantém commit
    reword → altera mensagem
    edit   → editar commit
    squash → juntar commits
    drop   → remover commit

------------------------------------------------------------------------

## 13. Descartar alterações

Todos arquivos:

``` bash
git restore .
```

Arquivo específico:

``` bash
git restore nomeArquivo.java
```

------------------------------------------------------------------------

## 14. Cherry-pick

Aplicar commit específico de outra branch.

``` bash
git cherry-pick HASH_COMMIT
```

------------------------------------------------------------------------

## 15. Comparar alterações

``` bash
git diff A B
```

------------------------------------------------------------------------

## 16. Mostrar detalhes de commit

``` bash
git show HASH_COMMIT
```

------------------------------------------------------------------------

## 17. Remover arquivo ou diretório

Remover arquivo:

``` bash
git rm arquivo.java
git commit -m "Remove arquivo"
```

Remover diretório:

``` bash
git rm pasta
git commit -m "Remove pasta"
```

Remover do versionamento mas manter local:

``` bash
git rm --cached arquivo.txt
```

------------------------------------------------------------------------

## 18. Deletar branch

Após merge:

``` bash
git branch -d nome_branch
```

Forçar remoção:

``` bash
git branch -D nome_branch
```

------------------------------------------------------------------------

## 19. Stash

Salvar alterações temporariamente:

``` bash
git stash
```

Listar:

``` bash
git stash list
```

Aplicar:

``` bash
git stash apply
```

Aplicar e remover:

``` bash
git stash pop
```

Remover stash:

``` bash
git stash drop
```

------------------------------------------------------------------------

## 20. Criar e trocar branch

Forma moderna:

``` bash
git switch -c feature/nova-branch
```

Trocar branch:

``` bash
git switch nome-branch
```

------------------------------------------------------------------------

## 21. Desfazer commits locais

Descartar commits e alterações:

``` bash
git reset --hard HEAD~2
```

Manter alterações no working dir:

``` bash
git reset --mixed HEAD~2
```

Manter alterações no stage:

``` bash
git reset --soft HEAD~1
```

Criar commit de reversão:

``` bash
git revert HASH_COMMIT
```

------------------------------------------------------------------------

## 22. Desfazer commit remoto

Visualizar os últimos commits
``` bash
  git log -2
```

Reverter o commit (abre editor para mensagem)
``` bash  
  git revert hash-do-commit
```

Enviar ao remoto
``` bash   
  git push nome-branch
```
> ```git revert```cria um novo commit desfazendo as alterações do commit alvo, mantendo o histórico íntegro. Ideal para commits já enviados ao repositório remoto.

------------------------------------------------------------------------

## 23. Ignorar arquivos

``` bash
echo arquivo.txt >> .gitignore
```

Ignorar pasta:

``` bash
echo node_modules/ >> .gitignore
```

------------------------------------------------------------------------

## 24. Renomear URL remota

``` bash
git remote set-url origin NOVA_URL
```

------------------------------------------------------------------------

## 25. Clonar branch específica

``` bash
git clone REPO --branch nome_branch --single-branch
```

------------------------------------------------------------------------

# 🚀 Observação

Este guia é focado em **produtividade e consulta rápida**.

Não substitui a documentação oficial do Git, mas ajuda a evitar perder
tempo procurando comandos usados com frequência.
