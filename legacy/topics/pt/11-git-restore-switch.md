# Git Restore e Git Switch

A partir da versão 2.23 do Git, dois novos comandos, `git restore` e `git switch`, foram introduzidos para simplificar os fluxos de trabalho para restaurar arquivos e alternar ramificações. Esses comandos foram projetados para substituir usos específicos do antigo comando `git checkout`, que lidava com múltiplas funções e às vezes poderia ser confuso.

### 1. Restauração do Git
O comando `git restore` concentra-se na restauração de arquivos em seu diretório de trabalho. Ele fornece uma maneira mais intuitiva de descartar alterações, permitindo redefinir os arquivos para seu estado no index (staging area) ou em um commit específico.

**Sintaxe Básica:**
```bash
git restore <opções> <arquivo>
```

**Opções comuns:**
- `--source <commit-hash>`: Restaura os arquivos para o estado em que estavam em um commit específico.
- `--staged`: Restaura arquivos na área de teste (o index).
- `--worktree`: Restaura arquivos apenas no diretório de trabalho (default).

**Exemplos:**

- Restaure um arquivo no diretório de trabalho para corresponder ao último commit:
```bash
git restore <arquivo>
```

- Faça um unstage de um arquivo (removê-lo do teste sem excluir as alterações):
```bash
git restore --staged <arquivo>
```

- Restaure um arquivo para corresponder a um commit anterior:
```bash
git restore --source <commit-hash> <arquivo>
```

## 2. Git Switch
O comando `git switch` simplifica o processo de alteração de ramificações ou criação de novas. Ele fornece uma maneira mais intuitiva e focada de gerenciar filiais em comparação com o git checkout.

**Sintaxe Básica:**
```bash
git switch <opções> <ramo>
```

**Opções comuns:**
- `-c <branch>`: Cria um novo branch e alterna para ele.
- `-C <branch>`: Cria uma nova ramificação ou redefine a ramificação se ela já existir.
- `--detach`: Muda para um commit específico no estado "detached HEAD" (não em qualquer branch).
- `--discard-changes`: Descarta quaisquer alterações não confirmadas ao alternar entre ramificações.

**Exemplos:**

- Mude para uma filial existente:
```bash
git switch feature/develop-database
```

- Crie e mude para um novo branch:
```bash
git switch -c feature/develop-database
```

- Mude para um commit específico em um estado HEAD desanexado:
```bash
git switch --detach <commit-hash>
```

### Principais diferenças do Git Checkout
- `git restore` serve para modificar arquivos no diretório de trabalho ou índice.
- `git switch` é para mudar de branch.
- `git checkout` ainda existe e pode ser usado, mas `git restore` e `git switch` oferecem mais clareza e são melhores para casos de uso específicos.