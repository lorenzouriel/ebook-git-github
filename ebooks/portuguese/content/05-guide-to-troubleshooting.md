# Um Guia para Solução de Problemas
Se algo der errado, você precisa saber como responder, o Git não é apenas sobre o caminho feliz:
- Você trabalha
- Você faz um commit
- Mescla o branch
- Faz o deploy

Nós amamos o caminho feliz, é por isso que é feliz!

Mas, na maioria das vezes, as coisas não saem como planejado e precisamos saber como reagir nesses casos.

Como você recupera alterações perdidas? Como você reverte erros?

Isso não é apenas sobre o Git, se aplica a todos os projetos.

É exatamente isso que abordarei neste capítulo.

## Desfazendo Commits (`git revert`, `git reset`, `git checkout`)

Ao trabalhar com Git, pode ser necessário desfazer commits por alguns motivos, como corrigir erros, reverter alterações inesperadas ou limpar o histórico.

O Git fornece três comandos principais para desfazer commits: `git revert`, `git reset` e `git checkout`. Cada um tem um comportamento diferente e deve ser usado de acordo.

## git revert

`git revert` cria um novo commit que desfaz as alterações introduzidas por um commit específico sem modificar o histórico do repositório.

Isso é útil quando você deseja manter o histórico limpo e não remover commits.

### Uso:

```bash
git revert hash-do-commit
```

### Exemplo:

#### 1. Verifique o commit que você deseja reverter:

```bash
git log --oneline

# Retorno
PS C:\ebooks\git-github-ebook-test> git log --oneline
56c9845 revert
3d87987 herge tag 'v1.0' into dev Showw show
d207431 (tag: v1.0, main) Merge branch 'release/v1.0'
28b146b Yes
0a91ea2 Updated commit message
ca382f6 (origin/main) filename3
db14708 new file
5a26f39 (tag: v1.0.0) first commit
PS C:\ebooks\git-github-ebook-test>
```

#### 2. Copie o hash e execute `git revert`:

```bash
git revert 56c9845

# Retorno
PS C:\ebooks\git-github-ebook-test> git log --oneline
4134ad2 (HEAD -> dev) Revert "revert"
56c9845 revert
3d87987 herge tag 'v1.0' into dev Showw show
d207431 (tag: v1.0, main) Merge branch 'release/v1.0'
28b146b Yes
0a91ea2 Updated commit message
ca382f6 (origin/main) filename3
db14708 new file
5a26f39 (tag: v1.0.0) first commit
PS C:\ebooks\git-github-ebook-test>
```

- Isso cria um novo commit que reverte as alterações do commit `56c9845`.

## `git reset`

`git reset` move o ponteiro HEAD para um commit anterior; isso é usado para modificar o histórico de commits. Ele tem três modos principais:

### Modos de `git reset`:

- **Soft (`--soft`)**: Redefine o HEAD para um commit anterior, mas mantém as alterações na área de staging, permitindo que você modifique ou emende o commit.
- **Mixed (`--mixed`)**: Redefine o HEAD para um commit anterior e remove as alterações da área de staging, mas deixa as alterações no diretório de trabalho.
- **Hard (`--hard`)**: Remove completamente o commit e todas as alterações, tanto da área de staging quanto do diretório de trabalho.

### Exemplo `--soft`:

A opção `--soft` desfaz o último commit, mas mantém as alterações na área de staging, para que você possa modificar facilmente o commit ou alterar a mensagem do commit. Isso é útil se você deseja refazer um commit sem perder o trabalho que fez.

Você volta para a etapa `git add .`.

```bash
git reset --soft HEAD~1
```

- Neste exemplo, `HEAD~1` move o HEAD um commit para trás; todas as alterações permanecem em stage, para que você possa re-commitá-las após fazer ajustes.

### Exemplo `--mixed`:

A opção `--mixed` redefine o HEAD para o commit especificado, remove as alterações da área de staging, mas as deixa no diretório de trabalho. Este é o comportamento padrão de `git reset` se nenhum modo for especificado.

É semelhante a `--soft`; a principal diferença é que com `--mixed` você volta antes de `git add .`.

```bash
git reset --mixed HEAD~1
```

- Este comando desfaz o último commit e remove as alterações do stage, mas as alterações permanecem no seu diretório de trabalho, para que você ainda possa modificá-las.

### Exemplo `--hard`:

A opção `--hard` redefine tanto a área de staging quanto o diretório de trabalho para corresponder ao commit especificado. Isso significa que todas as alterações são perdidas e não podem ser recuperadas, a menos que você tenha backups ou use `git reflog`.

Ação destrutiva, cuidado aqui!

```bash
git reset --hard HEAD~1
```

- Isso removerá o último commit e todas as alterações associadas a ele, tanto na área de staging quanto no diretório de trabalho.

## `git checkout`

`git checkout` pode ser usado para desfazer alterações em arquivos individuais ou trocar de branch. Falamos sobre ele apenas para branches até agora.

`git checkout` também é usado para desfazer commits, mas agora `git switch` e `git restore` são recomendados para essas tarefas.

### Uso para restaurar arquivos específicos:

`git checkout` pode ser usado para desfazer alterações em arquivos individuais e restaurá-los ao último estado commitado.

```bash
git checkout -- nome_do_arquivo.txt
```

- Este comando descartará quaisquer alterações não commitadas no arquivo `nome_do_arquivo.txt` e o restaurará ao seu último estado commitado.

O `--` é usado para informar ao Git que você está se referindo a um arquivo (não a uma branch) e que deseja descartar as alterações no diretório de trabalho, restaurando o arquivo ao estado do último commit.

### Exemplo `git restore`:

`git restore` é o comando recomendado para restaurar arquivos, e é mais intuitivo do que usar `git checkout` para esse propósito.

```bash
git restore nome_do_arquivo.txt
```

- Este comando descartará quaisquer alterações não commitadas no arquivo `nome_do_arquivo.txt` e o restaurará à versão do último commit, assim como `git checkout -- nome_do_arquivo.txt`.

## Recuperando Commits Perdidos

Se você perder acidentalmente um commit no Git, poderá recuperá-lo usando comandos como `git reflog` e `git fsck`. Essas ferramentas ajudam você a identificar e restaurar commits que parecem ter sido perdidos.

Com certeza, é um tipo de comando que você não usa muito, mas precisa saber que existe.

### Recuperando um Commit Perdido com `git reflog`

`git reflog` registra atualizações na ponta das branches (HEAD), permitindo que você veja o histórico de commits e outras ações do Git, mesmo que o commit não faça mais parte de nenhuma branch ou referência.

#### 1. Visualize as mudanças recentes do HEAD:

```bash
git reflog
```

- Este comando exibirá uma lista de mudanças recentes no HEAD, incluindo commits, merges, rebases e resets.

#### 2. Identifique o hash do commit perdido.

```bash
PS C:\ebooks\git-github-ebook-test> git reflog
4134ad2 (HEAD -> dev) HEAD@{0}: reset: moving to HEAD~1
73ac997 HEAD@{1}: commit: git reset example
4134ad2 (HEAD -> dev) HEAD@{2}: reset: moving to HEAD~1
bed2cc3 HEAD@{3}: commit: git reset example
4134ad2 (HEAD -> dev) HEAD@{4}: revert: Revert "revert"
56c9845 HEAD@{5}: commit: revert
3d87987 HEAD@{6}: merge vv1.0: Merge made by the 'ort' strategy.
28b146b HEAD@{7}: checkout: moving from main to dev
d207431 (tag: vv1.0, main) HEAD@{8}: checkout: moving from main to main
d207431 (tag: vv1.0, main) HEAD@{9}: merge release/v1.0: Merge made by the 'ort' strategy.
ca382f6 (origin/main) HEAD@{10}: checkout: moving from release/v1.0 to main
28b146b HEAD@{11}: checkout: moving from dev to release/v1.0
28b146b HEAD@{12}: checkout: moving from feature/feature-article to dev
28b146b HEAD@{13}: checkout: moving from dev to feature/feature-article
28b146b HEAD@{14}: reset: moving to HEAD
```

- Examine a saída para encontrar o commit que você precisa recuperar. Cada entrada está associada a uma referência, como `HEAD@{2}`, e um hash de commit.

#### 3. Faça checkout ou reset para o commit perdido:

Depois de identificar o hash do commit, você pode fazer checkout ou reset para esse commit.

- **Usando `git checkout`:** Isso moverá seu HEAD para o commit específico, mas não modificará seu diretório de trabalho ou área de staging.

```bash
git checkout hash-do-commit
```

- **Usando `git reset --hard`:** Isso redefinirá seu HEAD e diretório de trabalho para o commit específico, descartando quaisquer alterações não commitadas.

```bash
git reset --hard hash-do-commit
```

### Exemplo:

Visualize o reflog para encontrar o commit perdido:

```bash
git reflog
```

Exemplo de saída:

```bash
8b3dac5 (HEAD, dev) HEAD@{2}: commit: git checkout
4134ad2 HEAD@{3}: reset: moving to HEAD~1
73ac997 HEAD@{4}: commit: git reset example
4134ad2 HEAD@{5}: reset: moving to HEAD~1
bed2cc3 HEAD@{6}: commit: git reset example
4134ad2 HEAD@{7}: revert: Revert "revert"
56c9845 HEAD@{8}: commit: revert
3d87987 HEAD@{9}: merge vv1.0: Merge made by the 'ort' strategy.
```

Recupere o commit fazendo checkout dele:

```bash
git checkout 73ac997
```

Ou, se você quiser redefinir sua branch para este commit, use:

```bash
git reset --hard 56c9845
```

Se você executar `git reflog` novamente, verá que todas as alterações são feitas como um novo commit:

```bash
56c9845 (HEAD) HEAD@{0}: reset: moving to 56c9845
8b3dac5 (dev) HEAD@{1}: reset: moving to 8b3dac5
73ac997 HEAD@{2}: checkout: moving from dev to 73ac997
8b3dac5 (dev) HEAD@{3}: commit: git checkout
4134ad2 HEAD@{4}: reset: moving to HEAD~1
73ac997 HEAD@{5}: commit: git reset example
4134ad2 HEAD@{6}: reset: moving to HEAD~1
bed2cc3 HEAD@{7}: commit: git reset example
4134ad2 HEAD@{8}: revert: Revert "revert"
56c9845 (HEAD) HEAD@{9}: commit: revert
```

### Encontrando Commits Pendurados com `git fsck`
Se você não conseguir encontrar o commit no reflog, ele pode estar "pendurado", o que significa que não é referenciado por nenhuma branch ou tag, mas ainda existe no banco de dados do Git. Você pode procurar por esses commits pendurados usando `git fsck`.

Imagine que exista um commit perdido no repositório, você pode encontrar com o comando `git fsck`. Os commits perdidos podem acontecer quando esquecemos de fazer merge de branches e deletamos o trabalho.

#### 1. Execute `git fsck` para encontrar commits pendurados:

```bash
git fsck --lost-found
```

- Isso listará objetos que não fazem parte de nenhuma referência, incluindo commits pendurados.

#### 2. Inspecione os commits:

Procure por entradas rotuladas como "dangling commit" na saída e use `git show` para inspecioná-las.

```bash
git show hash-do-commit
```

### Exemplo:

Encontre commits pendurados com `git fsck`:

```bash
git fsck --lost-found
```

Exemplo de saída:

```bash
dangling commit 047885dbe5a76825fa1780cecb741f76eeb9ec35
dangling commit 18baee9d1b898ee1d82504174672b80d63aafa9a
dangling commit 227a6260d4d24c359aa5d4bcf667326c5cf10724
dangling tree 36e529c29f83cad089c8ddc57b7a1fa329564e87
dangling commit 413e484a74bef6b89674ecc6108f5f4364b9395f
dangling commit 726c4249600cb31b5bc8b52238faf3c3e31b4f68
dangling commit 73ac997c040ffda224e4a387614e2f860a8e0905
dangling commit 74a4b8ab890536d2ab8dacf076eaa64a5b24e486
dangling tree 96fc3be44051489ebc3303a66c07108bbcb563da
dangling commit a2d081673eb8bdd9f8e3159d787050c77116e901
dangling commit bed2cc3d74faff05c84ba21f84b29ab37357af63
dangling commit c2df1cab9005791812dd7efb690f9ce5f799bf70
dangling commit c8a104a4a311e3ee8cc2a696aeae5e4dc46cbeea
dangling commit fcde575ac34212c1187cee90604d35f0f6b00202
```

Inspecione o commit pendurado:

```bash
git show 047885dbe5a76825fa1780cecb741f76eeb9ec35
```

O retorno:

```bash
commit 047885dbe5a76825fa1780cecb741f76eeb9ec35
Author: Lorenzo Uriel 
Date:   Sun Feb 16 21:01:01 2025 -0300

    Updated commit message

diff --git a/filename.txt b/filename.txt
index 8d1c8b6..91b27f5 100644
--- a/filename.txt
+++ b/filename.txt
@@ -1 +1,2 @@

+Lorenzo Uriel
\ No newline at end of file
```

- Exibe todos os detalhes do commit, permitindo que você decida se é o commit que deseja recuperar.

## Mais Sobre `git status`, `git log`, `git show` e `git diff`
Sim... nós já os usamos acima.

Compreender os comandos `git status`, `git log`, `git show` e `git diff` pode ajudá-lo a rastrear as alterações e gerenciar seu repositório Git de uma forma mais inteligente.

Com esses comandos, você pode verificar o estado atual do seu repositório, ajudá-lo a explorar os históricos de commit e permitir que você veja as diferenças entre vários estados de seus arquivos.

É como um monte de instruções de consulta.

### `git status`
`git status` fornece uma visão geral do estado atual do diretório de trabalho e da área de staging. Ele ajuda você a rastrear quais alterações foram adicionadas ao stage, quais não foram e quais arquivos não estão sendo rastreados.

```bash
git status
```

Exemplo de saída:

```bash
HEAD detached from 73ac997
Changes not staged for commit:
  (use "git add ..." to update what will be committed)
  (use "git restore ..." to discard changes in working directory)
        modified:   README.md
        modified:   filename.txt
        modified:   filename2.txt
        modified:   filename3.txt

Untracked files:
  (use "git add ..." to include in what will be committed)
        filename3 copy.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

- Changes to be committed: Esses arquivos foram adicionados ao stage e estão prontos para serem commitados.
- Untracked files: Esses arquivos ainda não estão sendo rastreados pelo Git.

### `git log`
`git log` mostra o histórico de commits do repositório, permitindo que você explore commits anteriores, suas mensagens, autores e timestamps. Você também pode usar várias opções para filtrar e formatar a saída do log.

```bash
git log
```

Exemplo de saída:
```bash
commit 71333c330b93ffe20e02e6bac2b9a57ce15e355c (HEAD)
Author: Lorenzo Uriel 
Date:   Mon Mar 10 21:56:23 2025 -0300

    oh yeah

commit 56c9845e9e0ff4298def3b693456f8857d82824b
Author: Lorenzo Uriel 
Date:   Sun Mar 9 21:33:00 2025 -0300

    revert

commit 3d87987f33e66c859aa25f6a950995815c8caf50
Merge: 28b146b d207431
Author: Lorenzo Uriel 
Date:   Wed Mar 5 23:14:00 2025 -0300

    show
```

- Commit hash: O identificador exclusivo para o commit.
- Author: Quem fez o commit.
- Date: Quando o commit foi feito.
- Commit message: Uma breve descrição das alterações feitas nesse commit.

Você também pode usar `git log --oneline` para detalhes mais resumidos:

```bash
git log --oneline
```

Exemplo de saída:
```bash
5b07142 (HEAD) html example for git show
71333c3 oh yeah
56c9845 revert
3d87987 herge tag 'vv1.0' into dev Showw show
d207431 (tag: vv1.0, main) Merge branch 'release/v1.0'
28b146b Yes
0a91ea2 Updated commit message
ca382f6 (origin/main) filename3
db14708 new file
5a26f39 (tag: v1.0.0) first commit
```

### `git show`
`git show` permite que você veja informações detalhadas sobre um commit específico, incluindo a mensagem do commit, autor, data e as alterações feitas.

Foi o comando que usamos no tópico acima.

```bash
git show 5b07142
```

Exemplo de saída:
```bash
commit 5b071427e8369b85a56a5ee6b5388a2e2586306c (HEAD)
Author: Lorenzo Uriel 
Date:   Mon Mar 10 22:02:09 2025 -0300

    html example for git show

diff --git a/README.md b/README.md
index 49d8b13..a71ae21 100644
--- a/README.md
+++ b/README.md
@@ -1,3 +1,3 @@
 "# git-github-ebook-test"

-git revert test
+git revert testfcfdefd
diff --git a/filename.txt b/filename.txt
index 8d1c8b6..8ebae4c 100644
--- a/filename.txt
+++ b/filename.txt
@@ -1 +1,2 @@

+sdfdfdfadf
\ No newline at end of file
diff --git a/filename2.txt b/filename2.txt
```

- Isso mostrará as alterações feitas no commit (o diff) junto com outros metadados.

### `git diff`
`git diff` mostra as diferenças entre vários estados do repositório, como alterações entre o diretório de trabalho e o último commit, entre dois commits ou entre branches.

Compare o diretório de trabalho com o último commit:

```bash
git diff
```

Exemplo de saída:
```bash
diff --git a/index.html b/index.html
index 64b907a..a24d290 100644
--- a/index.html
+++ b/index.html
@@ -3,7 +3,7 @@
 
     
     
-    My First HTML Page
+    My Second HTML Page
 
 
     Welcome to My First HTML Page
```

- Isso mostra as alterações entre o diretório de trabalho e o último commit. O sinal `+` indica uma linha adicionada e o sinal `-` indica uma linha removida.

#### Comparar dois commits:
Você também pode comparar as alterações entre dois commits especificando seus hashes:

```bash
git diff 5b07142 e0f5e31
```

- Isso mostra as diferenças entre os dois commits especificados.

Exemplo de saída:

```bash
diff --git a/index.html b/index.html
index a24d290..685af61 100644
--- a/index.html
+++ b/index.html
@@ -3,7 +3,7 @@
 
     
     
-    My Second HTML Page
+    My Third Example HTML Page
 
 
     Welcome to My First HTML Page
```

#### Comparar branches:
Para ver as diferenças entre branches, use:

```bash
git diff main dev
```

- Isso mostra as diferenças entre as duas branches, ajudando você a ver quais alterações estão em uma branch, mas não na outra.

Exemplo de saída:

```bash
diff --git a/README.md b/README.md
index f3e1357..f70444d 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,3 @@
 "# git-github-ebook-test"
+
+git reset example
\ No newline at end of file
diff --git a/filename3.txt b/filename3.txt
index 8d1c8b6..3ad7dfd 100644
--- a/filename3.txt
+++ b/filename3.txt
@@ -1 +1,2 @@

+Changes on files
\ No newline at end of file
```

## Mais Sobre `git commit --amend`
Um dia você fez uma mensagem de commit grande e bonita e 5 minutos depois você encontra uma mudança de código e precisa commitar novamente?

Por que não apenas commitar para o mesmo último commit se for apenas uma pequena mudança? `--amend` pode ajudar com isso.

O comando `git commit --amend` é usado para modificar o commit mais recente no Git. Ele permite que você corrija a mensagem do commit, adicione ou remova alterações do commit ou até mesmo atualize as alterações e a mensagem de uma só vez.

Este comando é particularmente útil quando:

- Você percebe que a mensagem do commit precisa ser aprimorada.
- Você esqueceu de incluir algumas alterações no commit.

### Uso:
```bash
git commit --amend
```

Por padrão, executar este comando abrirá o editor de commit para permitir que você modifique a mensagem do commit. Você também pode passar a opção `-m` para atualizar diretamente a mensagem do commit.

#### Exemplo 1: Modificar a Mensagem do Commit
Se você quiser atualizar a mensagem do último commit, pode usar:

```bash
git commit --amend -m "Mensagem de commit atualizada"
```

- Isso substituirá a mensagem do último commit pela nova.

#### Exemplo 2: Adicionar Alterações Perdidas
Se você perceber que esqueceu de adicionar algumas alterações ao stage para o último commit, você pode:

1. Adicionar as alterações que você perdeu ao stage:

```bash
git add .
```

2. Emendar o commit com as alterações adicionadas ao stage:

```bash
git commit --amend
```

- Isso abrirá o editor de commit novamente, onde você pode modificar a mensagem do commit, se desejar. Se você não quiser alterar a mensagem, simplesmente salve e feche o editor.

O commit emendado agora incluirá as alterações originais e as alterações recém-adicionadas ao stage.

#### Exemplo 3: Substituir Completamente o Commit (Mensagem + Alterações)

Se você quiser alterar a mensagem do commit e as alterações, adicione as alterações ao stage primeiro e, em seguida, execute o comando `--amend`:

```bash
git add .
git commit --amend -m "Nova mensagem de commit com alterações atualizadas"
```

- Isso substituirá o último commit pelas novas alterações e a nova mensagem de commit.

***`git commit --amend`** reescreve o último commit, então ele muda seu hash de commit. Isso pode causar problemas se o commit já tiver sido enviado para um repositório compartilhado. Recomenda-se emendar apenas commits que ainda não foram enviados ou usá-lo com cautela se você já tiver compartilhado suas alterações.*