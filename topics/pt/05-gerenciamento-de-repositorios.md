# Gerenciamento de Repositórios
## Removendo Repositórios Locais
**1. Remover um repositório localmente:**
- Para excluir um repositório Git localmente, você pode simplesmente excluir o diretório onde ele está localizado. Por exemplo:
```shell
rm -rf /caminho/para/seu/repositório
```

- Use este comando com cautela, pois ele excluirá permanentemente todos os arquivos e o histórico de commits no repositório.

## Excluindo Repositórios Remotos no GitHub
Vá para a página do repositório no serviço de hospedagem.

Nas configurações do repositório, procure a opção para excluir o repositório.
- ![delete_repository](/topics/img/05/delete_repository.jpg)

- ![delete_repository_2](/topics/img/05/delete_repository_2.jpg)

Confirme a exclusão com a senha ou acessando o GitHub Mobile.

## Limpeza de Histórico (Rebase, Squash)
**1. Rebase:**
- O rebase é usado para reescrever o histórico de commits. Por exemplo, para rebasear sua branch `feature` na branch `main`:
```shell
git checkout feature
git rebase main
```

**2. Interactive Rebase:**
- Para combinar ou reordenar commits, use o rebase interativo:
```shell
git rebase -i HEAD~n
```

- Onde `n` é o número de commits que você deseja revisar. Você verá uma lista de commits que pode editar, combinar (squash) ou reordenar.

**3. Squash:**
- O squash combina vários commits em um único commit. Durante um rebase interativo, você pode usar o comando `squash` ou `s` para combinar commits.

- Primeiro, inicie o rebase interativo: 
```shell
git rebase -i HEAD~n
```

- No editor que se abre, altere `pick` para `squash` (ou `s`) nos commits que deseja combinar.


**4. Finalizar o Rebase:**
Após resolver conflitos (se houver), finalize o rebase:
```shell
git rebase --continue
```

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
- ![release](/topics/img/05/release.jpg)

- Preencha as informações, adicione a tag e clique em "Publish a New Release":
- ![release_2](/topics/img/05/release_2.jpg)

- Suas releases ficam organizados na seção "Code"
- ![release_3](/topics/img/05/release_3.jpg)
---