# Gerenciamento de Repositórios
## Removendo Repositórios Locais
**1. Remover um repositório localmente:**
- Para excluir um repositório Git localmente, você pode simplesmente excluir o diretório onde ele está localizado. Por exemplo:
```shell
# bash
rm -rf /caminho/para/seu/repositório
git commit -m "Remove tests_git directory"
git push

# power shell
git rm -r --cached /projects/portfolio/tests_git
Remove-Item -Path "C:\Projects\portfolio\tests_git" -Recurse -Force
git commit -m "Remove tests_git directory"
git push
```

- Use este comando com cautela, pois ele excluirá permanentemente todos os arquivos e o histórico de commits no repositório.

## Excluindo Repositórios Remotos no GitHub
Vá para a página do repositório no serviço de hospedagem.

Nas configurações do repositório, procure a opção para excluir o repositório.
- ![delete_repository](/ebook-pt/content/imgs/05/delete_repository.jpg)

- ![delete_repository_2](/ebook-pt/content/imgs/05/delete_repository_2.jpg)

Confirme a exclusão com a senha ou acessando o GitHub Mobile.

## Limpeza de Histórico (`Rebase`, `Squash`)
**1. Rebase:**

O rebase é usado para reescrever o histórico de commits. 

O Git Rebase move um branch para o topo de outro, reescrevendo o histórico no processo. Ao invés de realizar um merge ele reescreve o histórico.

Por exemplo, para rebasear sua branch `dev` na branch `main`:
```shell
git checkout dev
git rebase main
```

A ideia do rebase é criar um histórico de commits mais linear, facilitando futuros reviews de código.

**2. Interactive Rebase:**

Para combinar ou reordenar commits, use o rebase interativo:
```shell
git rebase -i HEAD~n
```

- Onde `n` é o número de commits que você deseja revisar. Você verá uma lista de commits que pode editar, combinar (squash) ou reordenar.

Quando rodar o rebase, seu terminal vai retornar dessa maneira:
```shell
pick f7f3f6d Meu commit 01
edit 310154e Meu commit 02
squash a5f4a0d Meu commit 03
drop a5f4a0d Meu commit 04

# Rebase 9b9bd4c..9b9bd4c onto 9b9bd4c (1 command)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
~  
```

Cada comando especifica exatamente o que você pode fazer com os commits.

Os seus commits vão aparecer acima dos comandos, basta você selecionar a linha do commit desejado e clicar apenas na letra inicial de cada comando. O comando vai adicionar automaticamente no início do commit.

#### O que o script completo faz?
- Aplica o commit `f7f3f6d` como está.
- Aplica o commit `310154e` e para para permitir edição.
- Combina o commit `a5f4a0d` com o commit `310154e` anterior.
- Remove o commit `a5f4a0d` do histórico.

**Isso resulta em:**
- O primeiro commit (`f7f3f6d`) sendo aplicado normalmente.
- O segundo commit (`310154e`) sendo aplicado e editado conforme necessário.
- O terceiro commit (`a5f4a0d`) sendo combinado (`squash`) com o segundo commit.
- O quarto commit (`a5f4a0d`) sendo removido do histórico.

**Observações adicionais**
- O comando `squash` vai pedir para editar a mensagem do commit resultante. 
- O `squash` combina vários commits em um único commit.
- O comando `edit` vai interromper o rebase para permitir modificações no commit.
- O comando `drop` remove completamente o commit do histórico.

## Tags e Releases
**1. Criar uma Tag:**
- Tags são usadas para marcar pontos específicos na história do commit, geralmente usadas para marcar versões de release.
```shell
git tag <nome-da-tag>
```

**2. Criar uma Tag Anotada:**
Tags anotadas são recomendadas para releases porque contêm informações adicionais.
```shell
git tag -a <nome-da-tag> -m "Mensagem da tag"
```

**3. Enviar uma Tag para o Repositório Remoto:**
Sempre que criar um tag você precisa enviar para o repositório remoto.
```shell
git push origin <nome-da-tag>
```

**4. Enviar Todas as Tags Locais para o Repositório Remoto:**
```shell
git push --tags
```

**5. Listar Todas as Tags:**
```shell
git tag
```

**6. Excluir uma Tag Localmente:**
```shell
git tag -d <nome-da-tag>
```

**7. Excluir uma Tag no Repositório Remoto:**
```shell
git push origin --delete <nome-da-tag>
```

**8. Criar uma Release no GitHub:**
- No GitHub, vá para a página do repositório.
- Vá para a seção "Code" > "Create a New Release".
- ![release](/ebook-pt/content/imgs/05/release.jpg)

- Preencha as informações, adicione a tag e clique em "Publish a New Release":
- ![release_2](/ebook-pt/content/imgs/05/release_2.jpg)

- Suas releases ficam organizados na seção "Code"
- ![release_3](/ebook-pt/content/imgs/05/release_3.jpg)
---