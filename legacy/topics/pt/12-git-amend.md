# Git AlAmed

O comando `git commit --amend` permite modificar o commit mais recente. Isso é útil quando você precisa fazer alterações no último commit, como adicionar arquivos esquecidos, modificar mensagens de commit ou corrigir erros sem criar um novo commit.

**Sintaxe:**
```bash
git commit --amend
```

**Por padrão, `git commit --amend` irá:**
- Abra o editor de mensagens de commit, permitindo modificar a mensagem de commit do último commit.
- Incluir quaisquer alterações preparadas (adicionadas à área de preparação) no commit alterado.

### Modifique a mensagem de commit
Para alterar a mensagem de commit do commit mais recente:
```bash
git commit --amend -m "nova mensagem de commit"
```

### Alterar sem alterar a mensagem de commit
Se você deseja apenas alterar o conteúdo do commit sem alterar a mensagem do commit, você pode usar a opção `--no-edit`:

1. Prepare os arquivos:
```bash
git add<arquivo>
```

2. Altere o commit:
```bash
git commit --amend --no-edit
```

### Alterando o autor do commit

Você também pode alterar o autor do commit ao usar `git commit --amend` especificando a opção `--author`:
```bash
git commit --amend --author="Novo autor <autor@example.com>"
```

### Cenários de casos de uso para Git Amend
- Corrigindo pequenos erros no último commit: Se você esqueceu de preparar um arquivo ou cometeu um erro de digitação na mensagem do commit, você pode alterar o commit.
- Fazer pequenas alterações sem criar um novo commit: Em vez de criar um novo commit para cada pequena correção, você pode alterar o último commit para manter o histórico mais limpo.
- Alterando o autor do commit: Se você fez um commit com o autor errado, você pode alterá-lo e alterar as informações do autor.