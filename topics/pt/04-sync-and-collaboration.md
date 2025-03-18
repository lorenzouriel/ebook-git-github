# Um Guia para Sincronização e Colaboração

Aqui está o ponto principal para usar o GitHub: sincronização e colaboração entre equipes ou projetos pessoais com um amigo. Foque em utilizá-lo dessa forma e você entenderá como ele é funcional.

## Configurando Repositórios Remotos
Repositórios remotos são versões do seu projeto hospedadas na internet ou em uma rede, permitindo que vários desenvolvedores colaborem. Eles servem como o hub central para armazenar e compartilhar alterações no projeto.

Para trabalhar com repositórios remotos, você precisa adicioná-los, modificá-los ou removê-los conforme necessário. Abaixo estão os comandos principais para gerenciar repositórios remotos:

### 1. Adicionar um Repositório Remoto
```bash
git remote add origin https://github.com/lorenzouriel/ebook-git-github.git
```
- Substitua pela URL do seu repositório remoto.

### 2. Verificar Repositórios Remotos Configurados
```bash
git remote -v
```
- Este comando lista todos os repositórios remotos configurados, juntamente com suas URLs de fetch e push.

### 3. Alterar a URL de um Repositório Remoto
```bash
git remote set-url origin https://github.com/lorenzouriel/ebook-git-github.git
```
- Útil ao mudar a localização remota, como migrar para outro provedor.

### 4. Remover um Repositório Remoto
```bash
git remote remove origin
```
- Remove a conexão com o repositório remoto especificado.

## Enviando Alterações para o Repositório Remoto (`git push`)

Depois de fazer e confirmar alterações localmente, você precisa enviá-las para o repositório remoto.

### 1. Enviar Alterações para a Branch Principal
```bash
git push origin main
```
- Envia as atualizações da branch `main` local para o repositório remoto.

### 2. Enviar uma Branch Específica para o Repositório Remoto
```bash
git push origin dev
```
- Substitua `dev` pelo nome da branch que deseja enviar.

### 3. Enviar Todas as Tags Locais para o Repositório Remoto
```bash
git push --tags
```
- Envia todas as tags criadas localmente para o repositório remoto.

## Obtendo Alterações do Repositório Remoto (`git pull` e `git fetch`)
Para se manter atualizado com as alterações remotas, você pode usar `pull` ou `fetch`.

### 1. Atualizar Seu Repositório Local com as Últimas Alterações e Fazer Merge Automaticamente
```bash
git pull main
```
- Equivalente a `git fetch` seguido de `git merge`, baixa e integra alterações remotas.

### 2. Buscar Alterações do Repositório Remoto Sem Fazer Merge
```bash
git fetch
```
- Baixa atualizações, mas não as aplica automaticamente.

### 3. Fazer Merge Manual das Alterações Buscadas
```bash
git merge
```
- Faz o merge das atualizações buscadas na sua branch local.

## Removendo Repositórios Locais e Remotos

### 1. Remover um Repositório Localmente

Para deletar um repositório Git do seu computador, você pode remover o diretório onde ele está armazenado. Tenha cuidado, pois isso removerá todos os arquivos e histórico de commits dentro do repositório.
```bash
# Usando Bash (Linux/macOS)
rm -rf /path/to/your/repository

# Usando PowerShell (Windows)
Remove-Item -Path "C:\Projects\portfolio\tests_git" -Recurse -Force

git commit -m "Remove tests_git directory"
git push
```

### 2. Deletar Repositórios Remotos no GitHub

Para deletar um repositório remoto no GitHub:
1. Navegue até a página do repositório no GitHub.
2. Vá até a seção **Configurações** do repositório.
- ![delete_repository](/topics/imgs/05/delete_repository.jpg)
3. Role até encontrar a opção **Deletar repositório**.
4. Confirme a exclusão inserindo sua senha ou usando o GitHub Mobile.

## Exemplo Completo de Fluxo
Este exemplo demonstra um fluxo completo de contribuição via fork e pull request:

### 1. Clonar o Repositório
```bash
git clone https://github.com/lorenzouriel/ebook-git-github.git
git remote add upstream https://github.com/lorenzouriel/ebook-git-github.git

cd ebook-git-github/
```

### 2. Criar uma Nova Branch, Fazer Alterações e Confirmar (Commit)
```bash
git checkout -b my-chapter

# Modifique os arquivos

git add .
git commit -m "Added a new chapter"
```

### 3. Enviar Alterações para Seu Fork
```bash
git push
```

### 4. Criar um Pull Request no GitHub
- Navegue até o repositório original.
- Clique em **New Pull Request**.
- Selecione sua branch (`my-chapter`) e a branch principal do repositório original.
- Adicione uma descrição e envie o pull request.

### 5. Sincronizar com o Repositório Original Após um Merge
Atualize seu repositório local com as últimas alterações:
```bash
git fetch upstream
git checkout main
git merge upstream/main
```

Envie a branch principal sincronizada de volta ao seu fork:
```bash
git push
```

### 6. Deletar a Branch Mesclada (Merged)
```bash
git branch -d my-chapter

# Opcionalmente, delete também a branch remota:
git push origin --delete my-chapter
```

Este fluxo garante sincronização e colaboração enquanto contribui para projetos open-source.

# Trabalhando com Tags e Releases
### 1. Criar uma Tag
As tags são usadas para marcar pontos específicos no histórico de commits, como lançamentos.
```bash
git tag v1
```

### 2. Criar uma Tag Anotada
Tags anotadas incluem metadados adicionais, como uma mensagem de tag, tornando-as ideais para lançamentos.
```bash
git tag -a v1 -m "Versão 01"
```

### 3. Enviar uma Tag para o Repositório Remoto
Após criar uma nova tag, envie-a para o repositório remoto:
```bash
git push origin v1
```

### 4. Enviar Todas as Tags Locais para o Repositório Remoto
Para enviar todas as tags de uma vez:
```bash
git push --tags
```

### 5. Listar Todas as Tags
Para listar todas as tags no seu repositório local:
```bash
git tag
```

### 6. Deletar uma Tag Localmente
Para deletar uma tag do seu repositório local:
```bash
git tag -d v1
```

### 7. Deletar uma Tag no Repositório Remoto
Para deletar uma tag do repositório remoto:
```bash
git push origin --delete v1
```

### 8. Criar um Release no GitHub
Para criar um release no GitHub:
1. Navegue até a seção **Releases** do repositório.
2. Clique em **Create a New Release**.
- ![release](/topics/imgs/05/release.jpg)
3. Preencha as informações da versão, associe uma tag e clique em **Publish a New Release**:
- ![release_2](/topics/imgs/05/release_2.jpg)
4. Seus releases serão organizados na seção releases na aba **Code**:
- ![release_3](/topics/imgs/05/release_3.jpg)


## Trabalhando com Forks e Pull Requests
Fazer um fork de um repositório permite que você contribua para um projeto sem modificar diretamente o repositório original. É uma forma comum de colaborar em projetos open-source.

### 1. Fazer Fork de um Repositório
No GitHub, use a interface web para fazer fork do repositório desejado.
- ![fork](/topics/imgs/04/fork.png)

### 2. Clone o Repositório
```bash
git clone https://github.com/lorenzouriel/opentelemetry-python-contrib.git
```
- Isso cria uma cópia local do seu repositório forkado.

### 3. Adicionar um Repositório Upstream para Sincronizar com o Projeto Original
```bash
git remote add upstream https://github.com/open-telemetry/opentelemetry-python-contrib.git
```
- O **upstream** refere-se ao repositório original de onde você fez o fork.

### 4. Sincronizar Seu Fork com o Repositório Original
Busque alterações do repositório upstream:
```bash
git fetch upstream
```

- Faça merge das atualizações na sua branch principal:
```bash
git checkout main
git merge upstream/main
```

- Envie as atualizações para o seu fork:
```bash
git push origin main
```

### 5. Criar um Pull Request
- No GitHub, vá até o repositório original e clique em **New Pull Request**.
- Compare as alterações entre seu fork e o repositório original.
- Clique em **Create Pull Request** e adicione uma mensagem descritiva.
- Após revisão e aprovação, o mantenedor pode fazer o merge da sua contribuição.

# Mais Sobre o Comando `git remote`

O comando `git remote` é usado para gerenciar repositórios remotos no Git. Ele permite visualizar, adicionar e remover remotos no seu repositório.

### 1. Visualizar os Remotos Atuais
Para listar todos os repositórios remotos vinculados ao seu repositório local, use o seguinte comando:
```bash
git remote -v
```
- Isso exibirá as URLs dos repositórios remotos para fetch e push.

### 2. Adicionar um Novo Remote
Para adicionar um novo repositório remoto, use o seguinte comando:
```bash
git remote add nome-repo url-repo
```

Por exemplo:
```bash
git remote add new-origin https://github.com/lorenzouriel/ebook-git-github.git
```

### 3. Remover um Remote
Para remover um remote existente, use o seguinte comando:
```bash
git remote remove nome-repo
```

Por exemplo, para remover o remote `origin`:
```bash
git remote remove new-origin
```

### 4. Renomear um Remote
Se você quiser renomear um repositório remoto, use:
```bash
git remote rename nome-antigo nome-novo
```

Por exemplo:
```bash
git remote rename new-origin upstream
```

### 5. Alterar a URL de um Remote
Para alterar a URL de um remote existente:
```bash
git remote set-url nome-repo nova-url-repo
```

Por exemplo:
```bash
git remote set-url origin https://github.com/lorenzouriel/ebook-git-github.git
```

### 6. Mostrar Informações Sobre um Remote
Para visualizar informações detalhadas sobre um repositório remoto, use:
```bash
git remote show nome-repo
```

Por exemplo:
```bash
git remote show origin
```
Isso exibirá informações detalhadas, incluindo URLs de fetch e push, branches rastreadas e mais.

### 7. Buscar Atualizações de um Remote
Para buscar atualizações de um repositório remoto:
```bash
git fetch nome-repo 
```

Por exemplo:
```bash 
git fetch origin 
```
Isso recupera alterações do repositório remoto sem fazer merge automático na branch atual.

A ideia aqui foi mostrar alguns exemplos e fluxos que você repetirá ao desenvolver seus projetos.