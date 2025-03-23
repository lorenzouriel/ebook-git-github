# Um Guia para Trabalhar com Branchs
Então, você já sabe o que é um branch e por que você deveria ter um. Mas agora, como você trabalha e utiliza elas?

# O que é uma Git Branch?

**Uma Git branch é uma linha independente de desenvolvimento dentro de um repositório.** Pense nela como um espaço de trabalho separado onde você pode fazer alterações sem impactar a branch principal. 

As branches permitem que os desenvolvedores trabalhem em novas funcionalidades, correções de bugs ou experimentos sem interromper a versão atual do projeto.

# Por que usar Branches?
As branches oferecem diversos benefícios em um fluxo de trabalho de desenvolvimento:
- **Isolamento:** Mantenha tarefas diferentes (funcionalidades, correções de bugs, experimentos) separadas.
- **Colaboração:** Vários desenvolvedores podem trabalhar em branches diferentes sem interferir uns nos outros.
- **Experimentação Segura:** Teste alterações sem impactar o código em produção.
- **Controle de Versão:** Reverta ou alterne facilmente entre diferentes versões do projeto.

No Git, a branch padrão geralmente é chamada de `main` ou `master`. No entanto, novas branches podem ser criadas para diversos propósitos, como:
- **Feature branches (`feature/new-ui`):** Usadas para desenvolver novas funcionalidades.
- **Bugfix branches (`hotfix/login-fix`):** Usadas para corrigir problemas em produção.
- **Release branches (`release/v1.2.0`):** Usadas para preparar versões estáveis para implantação.

# Criando e Gerenciando Branches Locais

As branches no Git permitem que você trabalhe em novas funcionalidades, correções de bugs ou experimentos sem afetar a base de código principal. Aqui está como criar, alternar, renomear e deletar branches de forma eficiente.

### 1. Criar uma Nova Branch
```shell
git branch feature/create-chapter
```
- Isso cria uma nova branch chamada `feature/create-chapter`, mas não muda para ela.
- Útil quando você precisa preparar várias branches, mas não deseja alternar imediatamente.

### 2. Alternar para uma Branch
```shell
git checkout feature/create-chapter
```
- Isso move você para a branch especificada para começar a codificar.

**Alternativa Moderna:** Desde o Git 2.23+, use `git switch`:
```shell
git switch feature/create-chapter
```
É uma alternativa mais limpa e segura ao `checkout`.

### 3. Criar e Alternar para uma Nova Branch (Atalho)
```shell
git checkout -b feature/create-chapter
```
- Cria uma nova branch e alterna para ela imediatamente.
- Economiza tempo ao combinar dois comandos em um só.

**Alternativa Moderna:**
```shell
git switch -c feature/create-chapter
```
Mais intuitivo e recomendado para versões mais recentes do Git.

### 4. Listar Todas as Branches
```shell
git branch
```
- Exibe todas as branches locais. A branch atual é marcada com `*`.
```shell
* dev/ebook-v2
  main
  feature/add-search
  bugfix/fix-typo
```
- Isso ajuda a rastrear as branches disponíveis e navegar entre elas.

Para listar também as branches remotas:
```shell
git branch -a
```

### 5. Renomear uma Branch
```shell
git branch -m feature/create-chapter feature/create-chapter-branch
```
- Renomeia a branch `feature/create-chapter` para `feature/create-chapter-branch`.

Se você já estiver na branch que deseja renomear:
```shell
git branch -m new-branch-name
```

### 6. Deletar uma Branch Local (Com Segurança)
```shell
git branch -d feature/create-chapter-branch
```
- Deleta a branch apenas se ela já foi mesclada em outra branch.
- Se houver alterações não mescladas, o Git impedirá a exclusão para evitar perda de dados.

### 7. Forçar a Exclusão de uma Branch (Perigoso)
```shell
git branch -D feature/create-chapter-branch
```
- Isso exclui a branch incondicionalmente, mesmo se houver alterações não mescladas.
- Use com cuidado para evitar perder trabalho importante.

### Melhores Práticas para Gerenciar Branches
1. Use nomes de branches claros e descritivos (`feature/add-login`, `bugfix/fix-typo`).
2. Delete branches antigas para manter seu repositório organizado.
3. Use `-d` em vez de `-D`, a menos que tenha certeza de que deseja forçar a exclusão.
4. Envie regularmente branches para o remoto (`git push origin branch-name`) para evitar perda acidental.

## Fazendo Merge de Branches
No Git, **`merge` é o processo de integrar alterações de uma branch em outra.** É usado para combinar atualizações de diferentes branches de desenvolvimento na branch principal, como `main` ou `develop`.

### 1. Fazer Merge de uma Branch na Branch Atual

Para integrar alterações de outra branch na sua branch atual:
```shell
git merge feature/create-chapter-branch
```
- Isso integra as alterações da branch `feature/create-chapter-branch` na branch em que você está atualmente.
- Se não houver conflitos, o Git concluirá o merge automaticamente.

Certifique-se de estar na branch correta antes de fazer o merge:
```shell
git checkout main  # ou git switch main
git merge feature/create-chapter-branch
```


### 2. Resolvendo Conflitos de Merge
Durante um merge, se houver conflitos, o Git pausará o processo e informará os arquivos conflitantes. Edite esses arquivos para resolver os conflitos, marcados com:
```shell
<<<<<<< HEAD
(changes in the current branch)
=======
(changes in the branch being merged)
>>>>>>> main
```
- A seção HEAD representa as alterações da sua branch atual.
- A seção abaixo de `=======` vem da branch sendo mesclada.

#### Passos para Resolver Conflitos:

1. Abra os arquivos conflitantes em um editor de texto.
2. Edite manualmente e mantenha a versão correta do código.
3. Marque os arquivos como resolvidos:
```shell
git add .
```
4. Conclua o merge com um commit:
```shell
git commit -m "Conflicting files resolved."
```

Para abortar um merge e retornar ao estado anterior:
```shell
git merge --abort
```

### Tipos de Git Merges
O Git suporta diferentes estratégias de merge dependendo se as branches divergiram ou não.

#### 1. Fast-Forward Merge (Sem Divergência)
Um fast-forward merge acontece quando a branch que está sendo mesclada está à frente da branch atual sem nenhuma alteração na branch atual.

O Git move o ponteiro da branch para frente em vez de criar um commit de merge.

**Exemplo:**
```shell
git checkout main
git merge feature/create-chapter-branch
```
- Isso funciona quando `main` não foi alterado desde que `feature/create-chapter-branch` foi criado.

#### 2. Three-Way Merge (Branches Divergentes)
Um three-way merge ocorre quando as duas branches têm históricos diferentes e não podem ser fast-forwarded.

O Git cria um novo commit de merge para combinar as alterações.
```shell
git checkout main
git merge feature/create-chapter-branch
```

Você verá uma mensagem de commit como:
```shell
Merge branch 'feature/create-chapter-branch' into main
```

### Melhores Práticas para Fazer Merge
1. Sempre faça pull das últimas alterações antes de fazer merge.
2. Teste seu código após fazer merge para garantir que tudo funcione.
3. Use feature branches para desenvolvimento para manter `main` estável.
4. Delete branches mescladas para manter o repositório limpo.

## Fazendo Rebase de Branches
Rebasing é um recurso do Git que **permite integrar alterações de uma branch em outra, movendo sua branch para o estado mais recente da branch de destino.** Ao contrário do merge, que cria um novo commit de merge, **o rebasing repete seus commits em cima das últimas alterações, mantendo o histórico de commits mais limpo.**

Quando usar rebase?
- Para manter uma feature branch atualizada com a branch principal.
- Para limpar o histórico de commits antes de fazer merge.
- Para reescrever o histórico de commits para melhor legibilidade.


### 1. Fazer Rebase de uma Branch em Outra Branch
```shell
git checkout feature/create-chapter-branch
git rebase main
```

Isso atualiza a `feature/create-chapter-branch` com os commits mais recentes de `main`, garantindo que ela seja baseada nas alterações mais recentes.

### 2. Cancelar um Rebase em Andamento
Se algo der errado durante o rebasing e você quiser cancelar o processo, use:
```shell
git rebase --abort
```

Isso restaura sua branch para o estado anterior ao início do rebase.

### 3. Continuar um Rebase Interrompido Após Resolver Conflitos
Quando ocorre um conflito, o Git pausa o rebase e pede para você resolver os conflitos manualmente nos arquivos afetados.

Após corrigir os conflitos, adicione os arquivos resolvidos ao stage:
```shell
git add .
```

Então, continue o rebase:
```shell
git rebase --continue
```

O Git continuará aplicando os commits restantes. Se outro conflito ocorrer, repita o processo.

### 4. Rebase Interativo (modificar histórico de commits)
Para editar, reordenar, juntar (squash) ou remover commits, use o rebase interativo:
```shell
git rebase -i HEAD~3
```

`HEAD~3` significa que você está interagindo com os 3 últimos commits.

Após executar este comando, o Git abre um editor interativo com opções como:
- `pick` → Manter o commit como está.
- `reword` → Alterar a mensagem do commit.
- `edit` → Modificar o conteúdo do commit.
- `squash` → Juntar os commits.
- `drop` → Deletar um commit.

Exemplo de uma janela de editor de rebase interativo:
```shell
pick 123abc filename3
squash 456def commit
pick 789ghi first commit

# Rebase db14708..ca382f6 onto db14708 (1 command)
#
# Commands:
# p, pick  = use commit
# r, reword  = use commit, but edit the commit message
# e, edit  = use commit, but stop for amending
# s, squash  = use commit, but meld into previous commit
# f, fixup [-C | -c]  = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec  = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop  = remove commit
# l, label  = label current HEAD with a name
# t, reset  = reset HEAD to a label
# m, merge [-C  | -c ]  [# ]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c  to reword the commit message
# u, update-ref  = track a placeholder for the  to be updated
#                       to this position in the new commits. The  is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
~ 
.git/rebase-merge/git-rebase-todo [unix] (20:33 16/02/2025)
```

Isso irá juntar o segundo commit no primeiro, combinando suas alterações.

### Melhores Práticas para Rebasing:
- Sempre faça rebase de branches locais antes de fazer merge para manter o histórico limpo.
- Evite fazer rebase de branches compartilhadas (`main`, `dev`), pois isso reescreve o histórico de commits.
- Use `git rebase --interactive` para reescrever o histórico de forma organizada.
- Se não tiver certeza, crie uma branch de backup antes de fazer rebase.

## Branches Remotas e Rastreamento de Branches
Branches remotas são versões das suas branches armazenadas em um repositório remoto. Essas branches permitem a colaboração entre vários desenvolvedores, mantendo seus repositórios locais sincronizados com o remoto.

### Por que usar branches remotas?
- Para colaborar com outras pessoas enviando e recebendo alterações.
- Para manter um backup do seu trabalho em um repositório central.
- Para gerenciar diferentes ambientes (`main`, `dev`, `staging`).

### 1. Listar Branches Remotas
Para ver todas as branches armazenadas no repositório remoto:

```shell
git branch -r
```

- Isso lista apenas as branches remotas, prefixadas por `origin/`.

Para listar as branches locais e remotas:
```shell
git branch -a
```

Isso ajuda a verificar quais branches existem localmente e remotamente.

### 2. Criar uma Branch Rastreando uma Branch Remota
Se você deseja trabalhar em uma branch remota localmente, use:

```shell
git checkout --track origin/dev
```
- Isso cria uma branch local que rastreia automaticamente a remota.

O retorno será:
```shell
branch 'dev' set up to track 'origin/dev'.
Switched to a new branch 'dev'
```

Isso é útil quando o Git não rastreia automaticamente a branch.

### 3. Atualizar Branches Remotas
Buscar atualizações do repositório remoto garante que você tenha a lista de branches mais recente:

```shell
git fetch
```
- Isso baixa as alterações remotas, mas não as aplica ao seu diretório de trabalho.

#### 4. Mesclar Alterações de uma Branch Remota na Branch Atual
Para obter as atualizações mais recentes de uma branch remota na sua branch local:
```shell
git pull origin main
```

Isso é equivalente a executar:
```shell
git fetch
git merge origin/main
```

Se a branch já estiver rastreando `origin/main`, você pode simplesmente executar:
```shell
git pull
```

### 5. Enviar uma Nova Branch Local para o Repositório Remoto
Depois de criar uma nova branch localmente, envie-a para o repositório remoto:

```shell
git push -u origin dev
```

- O sinalizador `-u` configura o rastreamento, para que os futuros comandos `git pull` e `git push` possam ser executados sem especificar a branch remota.

### 6. Excluir uma Branch Remota
Se uma branch remota não for mais necessária, exclua-a usando:

```shell
git push origin --delete dev
```
- Isso remove `origin dev` do repositório remoto.

Para excluir uma referência local à branch remota excluída:

```shell
git remote prune origin
```

### Melhores Práticas para Gerenciamento de Branch Remota

1. Use nomes de branch descritivos (`feature/login`, `bugfix/navbar-issue`).
2. Sempre faça fetch antes de mesclar para evitar conflitos.
3. Limpe branches excluídas regularmente
4. Não envie branches de trabalho em andamento, a menos que seja necessário.

## Guardando Alterações (Stashing)
O Git stash **permite que você salve temporariamente as alterações não commitadas sem commitá-las.** Isso é útil quando você precisa:
- Trocar de branch sem commitar trabalho incompleto.
- Manter seu diretório de trabalho limpo enquanto recebe alterações.
- Salvar trabalho temporário que você não está pronto para commitar.

Ao usar o stashing, o Git armazena suas alterações com segurança para que você possa recuperá-las posteriormente.

### 1. Guardar Alterações Não Commitadas
Para guardar todos os arquivos modificados e adicionados ao stage:
```shell
git stash
```
- Isso remove as alterações do diretório de trabalho e as salva em uma pilha.

Para guardar com uma mensagem personalizada:
```shell
git stash push -m "Fixing ETL"
```
- Ajuda você a identificar o que cada stash contém.

### 2. Listar Alterações Guardadas
Para visualizar todos os stashes salvos:
```shell
git stash list
```
- Cada entrada de stash é rotulada como `stash@{n}`, onde `n` é seu índice.

**Exemplo de saída:**
```shell
stash@{0}: On main: Fixing ETL
stash@{1}: On dev: Debugging API issue
```
- O stash mais recente é sempre `stash@{0}`.

### 3. Aplicar as Alterações Guardadas Mais Recentes
Para aplicar o stash mais recente sem removê-lo da lista de stashes:
```shell
git stash apply
```
- Isso restaura as alterações guardadas, mas as mantém no stash.

Para aplicar um stash específico:
```shell
git stash apply --index 2
```
- Substitua `2` pelo índice do stash desejado.

### 4. Aplicar e Remover as Alterações Guardadas Mais Recentes
Para restaurar e remover o stash mais recente:
```shell
git stash pop
```

Para remover um stash específico:
```shell
git stash pop --index 1
```
- Isso remove `stash@{1}` após aplicar suas alterações.

### 5. Descartar um Stash Específico
Para excluir um stash específico sem aplicá-lo:
```shell
git stash drop --q 1
```
- Remove `stash@{1}` da lista de stashes.

### 6. Limpar Todos os Stashes
Para excluir todos os stashes de uma vez:
```shell
git stash clear
```
- Use com cautela - isso exclui permanentemente todas as alterações guardadas.

### 7. Criar uma Nova Branch a partir de um Stash
Para criar uma branch com as alterações guardadas:
```shell
git stash branch feature-fix
```
- Isso cria uma nova branch `feature-fix` a partir do stash mais recente e aplica o stash.

### Melhores Práticas para Stashing
1. Use mensagens de stash significativas.
2. Aplique o stash antes de trocar de branch, se necessário.
3. Limpe stashes antigos para manter seu repositório limpo.
4. Use stash branches para alterações complexas.

## Workflow com Branches (Feature Branch, Hotfix e Release)

Este guia descreve o workflow típico usando branches Git para features, hotfixes e releases. Ele garante que os processos de desenvolvimento, correção de bugs e lançamento sejam otimizados.

### 1. Feature Branch
As feature branches permitem que você trabalhe em novas funcionalidades de forma independente, sem afetar a base de código principal.

- Crie uma nova branch para a feature:
```shell
git checkout -b feature/create-chapter-branch
```

- Trabalhe na feature e faça commits, commitando regularmente suas alterações à medida que avança.
- Faça merge da feature branch na branch principal (`main` ou `dev`).
```shell
git checkout main
git merge feature/create-chapter-branch
```

### 2. Hotfix Branch
Hotfixes são usados para correções urgentes de bugs no ambiente de produção, geralmente com base na branch principal.

- Crie uma nova branch para o hotfix a partir da branch principal:

```shell
git checkout -b hotfix/main-app-filter main
```

- Trabalhe no hotfix e faça commit.
- Faça merge da hotfix branch na branch principal:

```shell
git checkout main
git merge hotfix/main-app-filter main
```

- Também faça merge do hotfix na branch `dev`: Se você tiver uma branch `dev`, certifique-se de que o `hotfix` também seja mesclado lá, para manter a branch de desenvolvimento atualizada.

```shell
git checkout dev
git merge hotfix/main-app-filter main
```

### 3. Release Branch
As release branches são criadas para preparar uma nova versão do software para produção. Elas permitem testes, ajustes finais e versionamento.

- Crie uma nova release branch a partir da dev branch: A release branch deve ser baseada na dev branch para incluir todas as novas funcionalidades.

```shell
git checkout -b release/1.0.0 dev
```

- Teste e prepare o release, commitando conforme necessário. Faça os ajustes finais, realize os testes e commite quaisquer alterações necessárias.
- Faça merge da release branch na branch principal e tag o release: Após os testes, faça merge da release branch na main e tag com o número da versão para marcar o lançamento oficial.

```shell
git checkout main
git merge release/1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"
```

- Faça merge da release branch de volta na dev branch: Para garantir que quaisquer alterações finais feitas durante o processo de lançamento sejam refletidas na branch de desenvolvimento, faça merge da release branch de volta na dev.

```shell
git checkout dev
git merge release/1.0.0
```

### Melhores Práticas para Workflows
1. Use Nomes de Branch Descritivos
2. Mantenha as Branches de Curta Duração
3. Commite Frequentemente e Logicamente
4. Mantenha a Branch principal Estável
5. Use dev para Desenvolvimento Contínuo
6. Faça Merge em vez de Envio Direto para main ou dev
7. Use Tags para Releases
8. Garanta Testes Adequados nas Release Branches
9. Limpe as Branches Após o Merge

## Selecionando Commits (Cherry-Picking)
Cherry-picking **permite que você aplique seletivamente commits específicos de uma branch para outra.** Em vez de fazer merge ou rebase de uma branch inteira, você pode escolher apenas os commits de que precisa.

Isso é útil quando:
- Uma correção de bug está em uma feature branch e precisa ser aplicada à main.
- Um commit da branch de outro desenvolvedor deve ser adicionado à sua.
- Um commit foi adicionado incorretamente à branch errada e precisa ser movido.

### 1. Aplicar um Commit Específico de Outra Branch
Para aplicar um commit de outra branch à sua branch atual:
```shell
git cherry-pick a1b2c3d
```

- Isso aplica o commit com o hash `a1b2c3d` à sua branch atual.

### 2. Aplicar Vários Commits
Para cherry-pick vários commits em um comando:
```shell
git cherry-pick a1b2c3d e4f5g6h
```

- Isso aplica ambos os commits em sequência.

### 3. Abortar uma Operação de Cherry-Pick
Se você encontrar um conflito e quiser cancelar a operação:
```shell
git cherry-pick --abort
```

- Isso restaura sua branch ao estado anterior ao início do cherry-picking.

#### 4. Cherry-Picking Sem Commitar
Se você quiser aplicar as alterações de um commit sem commitar:
```shell
git cherry-pick -n a1b2c3d
```

- Isso aplica as alterações, mas não cria um commit.
- Você pode modificar os arquivos antes de commitar manualmente.

### 5. Cherry-Picking com uma Mensagem de Commit Personalizada
Para usar uma mensagem personalizada em vez da mensagem de commit original:
```shell
git cherry-pick -e a1b2c3d
```

- Isso abre um editor onde você pode modificar a mensagem de commit.

### Melhores Práticas para Cherry-Picking
1. Certifique-se de estar na branch correta antes de fazer cherry-picking.
2. O uso de cherry-picking pode levar a commits duplicados.
3. Verifique o histórico de commits após o cherry-picking para evitar conflitos.
4. Considere fazer merge ou rebase em vez de cherry-picking quando apropriado.

## Desfazendo Alterações
Às vezes, erros acontecem, e você precisa desfazer alterações no Git. Dependendo do cenário, você pode querer:
- Manter as alterações adicionadas ao stage enquanto desfaz um commit.
- Apagar completamente um commit e suas alterações.
- Reverter um commit mantendo o histórico intacto.
- Restaurar arquivos para um estado anterior.

### 1. Desfazer o Último Commit (Manter Alterações no Stage)
Se você quiser desfazer o último commit, mas manter as alterações adicionadas ao stage:
```shell
git reset --soft HEAD~1
```

- O commit é desfeito, mas as alterações permanecem na área de stage.
- Útil quando você commita acidentalmente muito cedo e deseja modificar o commit antes de enviar.

**Exemplo:**
```shell
git reset --soft HEAD~1
git commit -m "Updated commit message"
```

#### 2. Desfazer o Último Commit (Descartar Alterações)
Se você quiser desfazer o último commit e descartar todas as alterações:
```shell
git reset --hard HEAD~1
```

- Isso remove completamente o commit e suas alterações.

**Exemplo:**
```shell
git reset --hard HEAD~1
git log --oneline
```

### 3. Restaurar um Arquivo Excluído
Se você excluiu acidentalmente um arquivo e ainda não commitou a exclusão:
```shell
git checkout -- nome_do_arquivo.txt
```

- Isso restaura o arquivo para seu último estado commitado.

### 4. Redefinir um Arquivo para o Último Estado Commitado
Se um arquivo foi modificado, mas não adicionado ao stage, e você deseja descartar as alterações:
```shell
git checkout HEAD -- nome_do_arquivo.txt
```

- Isso restaura o arquivo para sua última versão commitada, descartando as modificações locais.

### 5. Reverter um Commit
Se você quiser desfazer um commit, mas manter o histórico intacto:
```shell
git revert 0a91ea2
```

- Isso cria um novo commit que reverte as alterações do commit especificado.
- Ao contrário do `reset`, ele não remove o histórico, tornando-o mais seguro para repositórios compartilhados.

### 6. Desfazer um Commit Enviado (Pushed)
Se você enviou (pushed) um commit acidentalmente e precisa desfazê-lo antes que outros o recebam:
```shell
git reset --hard HEAD~1
git push --force
```

- *`git push --force` sobrescreve o histórico e pode causar problemas se outros já tiverem recebido o commit.*

Se o commit já tiver sido compartilhado, use revert em vez disso:
```shell
git revert 0a91ea2
git push
```

#### 7. Desfazer Todas as Alterações Locais
Se você quiser redefinir tudo para o último estado commitado:
```shell
git reset --hard HEAD
```

- Isso remove todas as alterações não commitadas. Use com cautela.

### Melhores Práticas para Desfazer Alterações
- Use `reset --soft` quando quiser refazer um commit, mas manter suas alterações no stage.
- Use `reset --hard` com cautela, pois ele exclui as alterações permanentemente.
- Use `revert` em vez de `reset` ao trabalhar em um repositório compartilhado.
- Sempre verifique o histórico de commits (`git log --oneline`) antes de fazer alterações destrutivas.