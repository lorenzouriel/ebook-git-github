# Git Reflog
`git reflog` é um comando Git que registra atualizações na ponta dos ramos e outras referências. Ele permite que você rastreie alterações (como commits, alterações de branch, redefinições, checkouts, rebases e mesclagens) que podem não aparecer no histórico regular de commits.

### Por que usar `git reflog`?
`git reflog` é particularmente útil quando você deseja:
- **Recuperar commits perdidos:** Se você perdeu um commit devido a uma redefinição, checkout ou rebase, muitas vezes você pode recuperá-lo através do reflog.
- **Desfazer erros:** Ao listar todas as referências, você pode reverter para um estado anterior, mesmo que esse commit não esteja em seu histórico atual.
- **Ver o histórico de movimentos de filiais:** Ele monitora todos os chefes de filiais, independentemente de as alterações terem sido enviadas.

**Uso:**
```bash
git reflog
```

A execução deste comando mostra uma lista de atualizações recentes no `HEAD` do repositório (commits mais recentes), com cada alteração listada com um número de índice e uma descrição.

**Exemplo:**
```bash
9779a62 (HEAD -> main, origin/main, origin/HEAD) HEAD@{0}: commit: Novos tópicos adicionados: 11: Git Restore e Git Switch e 12: Git Amend
713bf98 HEAD@{1}: commit: feat: dicas de como adicionar nomes corretos de branch e commits adicionados
2844264 HEAD@{2}: commit: Iniciação de um novo capítulo, GitHub Authentications
e54b0ab HEAD@{3}: commit: Iniciação de um novo capítulo, GitHub Authentications
420278c HEAD@{4}: clone: ​​de https://github.com/lorenzouriel/ebook-git-github.git
```

**Cada linha indica:**
- **Hash de commit:** O identificador exclusivo do commit.
- **Referência:** Um índice como `HEAD@{0}` (0 sendo a alteração mais recente).
- **Ação:** O que foi feito, como commit, reset ou checkout.
- **Mensagem:** Informações adicionais sobre o commit.

**Recuperando commits perdidos:**
Para voltar a um commit anterior, use:
```bash
git cherry-pick <commit-hash>
```