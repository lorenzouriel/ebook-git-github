# Solução de Problemas
## Desfazendo Commits (`git revert`, `git reset`, `git checkout`)
### **`git revert`**
- Usado para **criar um novo commit que desfaz as mudanças de um commit específico, preservando o histórico.**
```shell
git revert <commit-hash>
```

Isto cria um novo commit que desfaz as mudanças do commit especificado.

### **`git reset`**
- Usado para **redefinir o estado do repositório para um commit anterior.** O `reset` comando pode alterar o histórico.

Modos de `git reset`:
- `--soft`: Mantém os arquivos e indexação como estão, apenas reseta o ponteiro HEAD
```shell
git reset --soft <commit-hash>
```

- `--mixed`: Mantém os arquivos no diretório de trabalho, mas desfaz as mudanças do index.
```shell
git reset --mixed <commit-hash>
```

- `--hard`: Reseta o ponteiro HEAD, o index e o diretório de trabalho.
```shell
git reset --hard <commit-hash>
```

### **`git checkout`**
- Usado para **mudar branches ou restaurar arquivos no diretório de trabalho.** O `checkout` não afeta o histórico.
```shell
git checkout <branch-name>
git checkout <commit-hash> -- <file-path>
```

## Resolução de Conflitos Comuns
### **Conflitos de Merge**
- Quando um conflito de merge ocorre, o Git marca os arquivos conflitantes para que você possa resolvê-los manualmente.

**Exemplo:**
```shell
git merge <branch-name>
```
- Resolva os conflitos editando os arquivos conflitantes.

- Marque os conflitos como resolvidos:
```shell
git add <file-path>
```

- Complete o merge:
```shell
git commit
```

### **Conflitos de Rebase**
Durante o rebase, conflitos são resolvidos de maneira semelhante aos conflitos de merge.

**Exemplo:**
```shell
git rebase <branch-name>
```

- Resolva os conflitos editando os arquivos conflitantes.

- Continue o rebase:
```shell
git rebase --continue
```

- Para abortar o rebase:
```shell
git rebase --abort
```

## Recuperação de Commits Perdidos
### **`git reflog`**
Mantém um registro de todos os **HEADs** que foram alterados no repositório local.
- Em Git, o termo "HEAD" refere-se ao commit atual no qual você está trabalhando. É um ponteiro especial que sempre aponta para o commit mais recente na sua cópia de trabalho. 

É muito utilizado para commits perdidos.

**Exemplo:**
```shell
git reflog
```

- Identifique o commit que você deseja recuperar e use `git checkout` ou `git reset` para restaurá-lo.

### `git cherry-pick`
Usado para **aplicar um commit específico de uma branch para outra.**

**Exemplo:**
```shell
git cherry-pick <commit-hash>
```

## Dicas de Troubleshooting
### **Diagnóstico de Problemas**
Use comandos como `git status`, `git log`, e `git diff` para entender o estado atual do repositório e identificar problemas.

### **Ignorar Arquivos Localmente**
Se você precisar ignorar mudanças em arquivos que estão rastreados, use
```shell
git update-index --assume-unchanged <file-path>
```

Para desfazer:
```shell
git update-index --no-assume-unchanged <file-path>
```

### **Descartar Mudanças Locais**
Para descartar mudanças em arquivos modificados:
```shell
git checkout -- <file-path>
```

Para descartar todas as mudanças locais:
```shell
git reset --hard
```

### **Resolver Problemas de Push/Pull**
Se você encontrar problemas ao fazer push ou pull, como rejeições de push, primeiro faça fetch para sincronizar seu repositório:
```shell
git fetch
```
- Resolva quaisquer conflitos, então tente novamente

## Resumo
- **Desfazer commits:** Use `git revert` para desfazer mudanças de um commit específico preservando o histórico. Use `git reset` para redefinir o repositório para um estado anterior, com várias opções de modo (`soft`, `mixed`, `hard`). Use `git checkout` para mudar branches ou restaurar arquivos específicos.

- **Resolução de conflitos comuns:** Resolva conflitos de `merge` e `rebase` manualmente, editando os arquivos conflitantes e marcando-os como resolvidos.

- **Recuperação de commits perdidos:** Use `git reflog` para ver o histórico de HEADs e recuperar commits perdidos. Use `git cherry-pick` para aplicar commits específicos de uma branch para outra.

- **Dicas de troubleshooting:** Use comandos de diagnóstico (`git status`, `git log`, `git diff`) para entender o estado do repositório. Ignore mudanças em arquivos rastreados com git update-index. Descarte mudanças locais com `git checkout` e `git reset`. Resolva problemas de push/pull sincronizando com `git fetch` primeiro.
---