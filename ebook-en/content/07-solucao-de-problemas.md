# Solução de Problemas
## Desfazendo Commits (`git revert`, `git reset`, `git checkout`)
### **`git revert`**
Usado para **criar um novo commit que desfaz as mudanças de um commit específico, preservando o histórico.**
```bash
git revert <commit-hash>
```
Isto cria um novo commit que desfaz as mudanças do commit especificado.

Assim fica o seu log, após o `revert`:
```bash
loren@ MINGW64 /c/Projects/portfolio/git_study (dev)
$ git revert 0d3bd1def0f408e07b1249d7c599759b46380640
hint: Waiting for your editor to close the file...
[No write since last change]

Press ENTER or type command to continue
[No write since last change]

Press ENTER or type command to continue
[dev 68feb15] Revert "Commit para reverter"
 1 file changed, 1 insertion(+), 3 deletions(-)

loren@ MINGW64 /c/Projects/portfolio/git_study (dev)
$ git log
commit 68feb159e81c636e290febc9bbe0d94ac8a15ccb (HEAD -> dev)
Author: Lorenzo Uriel <lorenzo.uriel@.com.br>
Date:   Thu Jul 25 22:05:30 2024 -0300

    Revert "Commit para reverter"

    This reverts commit 0d3bd1def0f408e07b1249d7c599759b46380640.

commit 0d3bd1def0f408e07b1249d7c599759b46380640
Author: Lorenzo Uriel <lorenzo.uriel@.com.br>
Date:   Thu Jul 25 22:05:02 2024 -0300

    Commit para reverter
```

Eu fiz um `commit` inicial com a mensagem `Commit para reverter`, logo depois eu peguei o hash do commit e fiz um `git revert 0d3bd1def0f408e07b1249d7c599759b46380640` com a mensagem `Revert "Commit para reverter"`.

### **`git reset`**
Usado para **redefinir o estado do repositório para um commit anterior.** O comando `reset` pode alterar o histórico.

Principais odos de `git reset`:
- `--soft`: Mantém os arquivos e indexação como estão, apenas reseta o ponteiro HEAD
```bash
git reset --soft <commit-hash>
```

- `--mixed`: Mantém os arquivos no diretório de trabalho, mas desfaz as mudanças do index.
```bash
git reset --mixed <commit-hash>
```

- `--hard`: Reseta o ponteiro HEAD, o index e o diretório de trabalho.
```bash
git reset --hard <commit-hash>
```

### **`git checkout`**
Usado para **mudar branches ou restaurar arquivos no diretório de trabalho.** O `checkout` não afeta o histórico.
```bash
git checkout <branch-name>
git checkout <commit-hash> -- <file-path>
```

## Resolução de Conflitos Comuns
### **Conflitos de Merge**
Quando um conflito de merge ocorre, o Git marca os arquivos conflitantes para que você possa resolvê-los manualmente.

**Exemplo:**
```bash
git merge <branch-name>
```
Resolva os conflitos editando os arquivos conflitantes. Exemplo de mensagem:
![merge](/ebook-pt/content/imgs/07/merge_head.jpg)

```bash
loren@ MINGW64 /c/Projects/portfolio/git_study (main)
$ git merge dev
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

- Marque os conflitos como resolvidos:
```bash
git add <file-path>
```

- Complete o merge:
```bash
git commit -m "Erros corrigidos, pronto para seguir"
```

### **Conflitos de Rebase**
Durante o rebase, conflitos são resolvidos de maneira semelhante aos conflitos de merge.

**Exemplo:**
```bash
git rebase <branch-name>
```

- Resolva os conflitos editando os arquivos conflitantes.

- Continue o rebase:
```bash
git rebase --continue
```

- Para abortar o rebase:
```bash
git rebase --abort
```

## Recuperação de Commits Perdidos
### **`git reflog`**
Mantém um registro de todos os **HEADs** que foram alterados no repositório local.

É muito utilizado para commits perdidos.

**Exemplo:**
```bash
git reflog
```

- Identifique o commit que você deseja recuperar e use `git checkout` ou `git reset` para restaurá-lo.

Exemplo de retorno no terminal:
```bash
$ git reflog
76e8ecf (HEAD -> main) HEAD@{0}: commit (merge): Erros ok
3fd367d HEAD@{1}: commit: Vou fazer um merge
7ce5614 (origin/main) HEAD@{2}: checkout: moving from dev to main
1dbfda0 (dev) HEAD@{3}: checkout: moving from dev to dev
1dbfda0 (dev) HEAD@{4}: reset: moving to 1dbfda0a8363529fdbb0abb2023f7ee8f5d43691        
1dbfda0 (dev) HEAD@{5}: reset: moving to 1dbfda0a8363529fdbb0abb2023f7ee8f5d43691        
1dbfda0 (dev) HEAD@{6}: reset: moving to 1dbfda0a8363529fdbb0abb2023f7ee8f5d43691        
1dbfda0 (dev) HEAD@{7}: commit: Commit para dar um reset
68feb15 HEAD@{8}: revert: Revert "Commit para reverter"
0d3bd1d HEAD@{9}: commit: Commit para reverter
7ce5614 (origin/main) HEAD@{10}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{11}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{12}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{13}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{14}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{15}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{16}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{17}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{18}: rebase (finish): returning to refs/heads/dev
7ce5614 (origin/main) HEAD@{19}: rebase (start): checkout main
39f9d27 HEAD@{20}: checkout: moving from main to dev
7ce5614 (origin/main) HEAD@{21}: rebase (finish): returning to refs/heads/main
7ce5614 (origin/main) HEAD@{22}: rebase (start): checkout HEAD
7ce5614 (origin/main) HEAD@{23}: commit (merge): Commit 04
39f9d27 HEAD@{24}: rebase (finish): returning to refs/heads/main
39f9d27 HEAD@{25}: rebase (start): checkout HEAD
39f9d27 HEAD@{26}: checkout: moving from dev to main
39f9d27 HEAD@{27}: checkout: moving from main to dev
39f9d27 HEAD@{28}: checkout: moving from dev to main
39f9d27 HEAD@{29}: rebase (finish): returning to refs/heads/dev
39f9d27 HEAD@{30}: rebase (start): checkout main
52ec99f (origin/dev) HEAD@{31}: rebase (finish): returning to refs/heads/dev
52ec99f (origin/dev) HEAD@{32}: rebase (start): checkout HEAD
52ec99f (origin/dev) HEAD@{33}: checkout: moving from main to dev
```

### `git cherry-pick`
Usado para **aplicar um commit específico de uma branch para outra.**

**Exemplo:**
```bash
git cherry-pick <commit-hash>
```

## Dicas de Troubleshooting
### **Diagnóstico de Problemas**
Use comandos como `git status`, `git log`, e `git diff` para entender o estado atual do repositório e identificar problemas.
- `git status`: Fornece uma visão geral do estado atual do seu repositório. Ele exibe quais arquivos foram modificados, quais estão prontos para o commit e quais não estão rastreados. Isso ajuda a entender rapidamente o que mudou desde o último commit.

- `git log`: Usado para visualizar o histórico de commits. Isso é útil para identificar mudanças feitas ao longo do tempo e entender como o repositório evoluiu. Você pode adicionar opções como `--oneline` para uma visualização mais concisa ou `--graph` para uma representação gráfica dos commits.

- `git diff`: Compara alterações entre commits, entre o repositório e o diretório de trabalho, ou entre diferentes branches. É útil para revisar alterações específicas em arquivos e entender como o código foi modificado.

### **Ignorar Arquivos Localmente**
Se você precisar ignorar mudanças em arquivos que estão rastreados, use
```bash
git update-index --assume-unchanged <file-path>
```

Para desfazer:
```bash
git update-index --no-assume-unchanged <file-path>
```

### **Descartar Mudanças Locais**
Para descartar mudanças em arquivos modificados:
```bash
git checkout -- <file-path>
```

Para descartar todas as mudanças locais:
```bash
git reset --hard
```

### **Resolver Problemas de Push/Pull**
Se você encontrar problemas ao fazer push ou pull, como rejeições de push, primeiro faça fetch para sincronizar seu repositório:
```bash
git fetch
```
- Resolva quaisquer conflitos, então tente novamente

## Resumo
- **Desfazer commits:** Use `git revert` para desfazer mudanças de um commit específico preservando o histórico. Use `git reset` para redefinir o repositório para um estado anterior, com várias opções de modo (`soft`, `mixed`, `hard`). Use `git checkout` para mudar branches ou restaurar arquivos específicos.

- **Resolução de conflitos comuns:** Resolva conflitos de `merge` e `rebase` manualmente, editando os arquivos conflitantes e marcando-os como resolvidos.

- **Recuperação de commits perdidos:** Use `git reflog` para ver o histórico de HEADs e recuperar commits perdidos. Use `git cherry-pick` para aplicar commits específicos de uma branch para outra.

- **Dicas de troubleshooting:** Use comandos de diagnóstico (`git status`, `git log`, `git diff`) para entender o estado do repositório. Ignore mudanças em arquivos rastreados com git update-index. Descarte mudanças locais com `git checkout` e `git reset`. Resolva problemas de push/pull sincronizando com `git fetch` primeiro.
---