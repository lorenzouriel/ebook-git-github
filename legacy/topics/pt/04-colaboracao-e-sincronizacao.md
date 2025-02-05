# Sincronização e Colaboração

## Configurando Repositórios Remotos
**1. Adicionar um repositório remoto:**
```shell
git remote add origin <url-do-repositório-remoto>
```
- Substitua `<url-do-repositório-remoto>` pelo URL do seu repositório remoto (por exemplo, no GitHub, GitLab ou Bitbucket).

**2. Verificar os repositórios remotos configurados:**
```shell
git remote -v
```

**3. Alterar a URL de um repositório remoto:**
```shell
git remote set-url origin <nova-url-do-repositório-remoto>
```

**4. Remover um repositório remoto:**
```shell
git remote remove origin
```

## Enviando Mudanças para o Repositório Remoto (`git push`)
**1. Enviar mudanças para a branch principal (main):**
```shell
git push origin main
```

**2. Enviar uma branch específica para o repositório remoto:**
```shell
git push origin <nome-da-branch>
```

**3. Enviar todas as tags locais para o repositório remoto:**
```shell
git push --tags
```

## Obtendo Mudanças do Repositório Remoto (`git pull` e `git fetch`)

**1. Atualizar o repositório local com mudanças do repositório remoto e mesclar automaticamente:**
```shell
git pull origin main
```
- Isso é equivalente a `git fetch` seguido de `git merge`.

**2. Obter mudanças do repositório remoto sem mesclar:**
```shell
git fetch origin
```

**3. Mesclar mudanças obtidas do repositório remoto:**
```shell
git merge origin/main
```

## Trabalhando com Forks e Pull Requests

**1. Criar um fork de um repositório:**
- No GitHub, GitLab ou Bitbucket, use a interface web para criar um fork do repositório desejado.

**2. Clonar o repositório forkado:**
```shell
git clone <url-do-repositório-forkado>
```

**3. Adicionar um repositório upstream para sincronizar com o repositório original:**
```shell
git remote add upstream <url-do-repositório-original>
```
- O termo "**upstream" é utilizado para se referir ao repositório remoto que é a fonte oficial de um projeto.** É o repositório principal do qual você geralmente deseja sincronizar as atualizações.

**4. Sincronizar o fork com o repositório original:**
- Buscar mudanças do repositório original:
```shell
git fetch upstream
```

- Mesclar mudanças na branch principal:
```shell
git checkout main
git merge upstream/main
```

- Enviar mudanças para o seu fork no GitHub:
```shell
git push origin main
```

**5. Criar uma pull request:**
- No GitHub, GitLab ou Bitbucket, **use a interface web para criar uma pull request do seu fork para o repositório original.** Descreva as mudanças que você fez e solicite a revisão.

## Exemplo de Fluxo Completo
**1. Adicionar Repositórios Remotos:**
```shell
git remote add origin <url-do-seu-fork>
git remote add upstream <url-do-repositório-original>
```

**2. Fazer Mudanças e Comitar:**
```shell
git add .
git commit -m "Minha contribuição"
```

**3. Enviar Mudanças para o Fork:**
```shell
git push origin main
```

**4. Criar uma Pull Request:**
- No GitHub, **vá para o repositório original e clique em "New Pull Request".**
    - ![example_pull_request](/topics/imgs/04/pull_request_01.jpg)

- Na aba **Pull Request**, clique em **New Pull Request**
    - ![example_pull_request](/topics/imgs/04/pull_request_02.jpg)

- Selecione a branch que possui alterações (`compare:dev`) e a que deseja fazer o merge (`base:main`). Clique em **Create Pull Request**
    - ![example_pull_request](/topics/imgs/04/pull_request_03.jpg)

- O GitHub vai navegar para essa aba e testar novamente se as alterações não possuem conflitos, depois da verificação clique em **Merge pull request**
    - ![example_pull_request](/topics/imgs/04/pull_request_04.jpg)

- Caso possua essa cultura, já pode deletar a branch direto na etapa de **Pull Request**
    - ![example_pull_request](/topics/imgs/04/pull_request_05.jpg)


**5. Sincronizar com o Repositório Original:**
- Após aplicar as alterações, você precisa enviar para o seu repositório local:
```shell
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

- Depois, pode deletar a branch do repositório local:
```shell
git checkout -d dev
```
---