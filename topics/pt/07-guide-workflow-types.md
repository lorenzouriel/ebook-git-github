# Um Guia para Tipos de Workflows

O que é um workflow? E por que você deveria usar um?

É isso que quero explicar hoje. Tenho certeza de que você começará a usá-lo ainda hoje.

Um workflow define como você e sua equipe podem colaborar usando Git e GitHub. Escolher o workflow correto dependerá de como sua equipe está estruturada, da complexidade do projeto e de suas estratégias para lançar uma nova versão.

Vou explorar os workflows mais comuns e seus casos de uso.

## Trunk-Based Development
O mais utilizado, com certeza. Você provavelmente já usou esse modelo e nem sabia que ele tinha um nome.

Mas como ele funciona?

Os desenvolvedores trabalham diretamente na branch `main` ou criam **feature branches de curta duração.** Todas as alterações são mescladas na `main` várias vezes ao dia.

Isso resulta em integração frequente, minimizando conflitos de merge. Com isso, temos entrega rápida, colaboração em tempo real e menos conflitos de merge.

### Passos do Workflow

1. Iniciar o trabalho:
```bash
git checkout -b feature-article
```

2. Fazer alterações e enviar frequentemente:
```bash
git commit -m "Finish Article"
```

3. Mesclar a branch:
```bash
git checkout main
git merge feature-article
git push origin main
```

### Diagrama
![trunk-based](/topics/imgs/07-guide-workflow-types/trunk-based.png)

## GitFlow
Em vez de ter apenas uma branch principal, sempre temos duas: `main` e `dev`.

Com base em `dev`, podemos criar outras branches para diferentes propósitos, como:
- `feature branches`: Criadas a partir da `dev`, mescladas de volta quando concluídas.
- `release branches`: Criadas a partir da `dev` ao preparar um lançamento.
- `hotfix branches`: Criadas a partir da `main` para corrigir problemas urgentes e mescladas tanto na `main` quanto na `dev`.

A branch `main` sempre armazena o código de produção, enquanto `dev` integra todas as feature branches. Desenvolvemos na branch `dev` para evitar mexer no código de produção.

GitFlow é a melhor opção para propósitos de CI/CD.

### Passos do Workflow
1. Inicializar o GitFlow:
```bash
git flow init
```

Durante a inicialização, será feito um pequeno questionário para configurar o projeto.
```bash
Which branch should be used for bringing forth production releases?
   - dev
   - main
Branch name for production releases: [main]

Which branch should be used for integration of the "next release"?
   - dev
Branch name for "next release" development: [dev] 

How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? [v] 
Hooks and filters directory? [C:/ebooks/git-github-ebook-test/.git/hooks]
```

O próprio `git flow init` criará toda a estrutura.

2. Iniciar uma nova feature:
```bash
git flow feature start feature-article
```
- Esta ação cria um novo branch de recurso baseado em `dev` e alterna para ele

3. Finalizar a feature:
```bash
git flow feature finish feature-article
```
- Mescla `feature-article` em `dev`
- Remove o branch feature
- Volta para o branch `dev`

4. Publicar a feature:
```bash
git flow feature publish feature-article
```
- Este comando publica o próprio recurso no repositório remoto para outros usuários.

5. Criar uma branch de release:
```bash
git flow release start v1.0
```
- Cria uma branch de lançamento criada a partir da branch `dev`.

6. Finalizar & deploy da release:
```bash
git flow release finish 'v1.0'
```
- Mescla o branch `release` em `main`
- Faz a Tag do `release` com o nome.
- Mescla o branch `release` em `dev` novamente
- Então, remove o branch `release`

A mensagem de prompt é a seguinte:
```bash
C:\ebooks\git-github-ebook-test>git flow release finish 'v1.0'
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
Merge made by the 'ort' strategy.
Already on 'main'
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)
Switched to branch 'dev'
Merge made by the 'ort' strategy.
Deleted branch release/v1.0 (was 28b146b).

Summary of actions:
- Release branch 'release/v1.0' has been merged into 'main'
- The release was tagged 'vv1.0'
- Release tag 'vv1.0' has been back-merged into 'dev'
- Release branch 'release/v1.0' has been locally deleted
- You are now on branch 'dev'
```

Se quiser saber mais sobre os comandos, recomendo este [GitFlow cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/index.html).

### Diagrama
![gitflow](/topics/imgs/07-guide-workflow-types/gitflow.png)

## Feature Branch
Ideal para equipes que trabalham em múltiplas features simultaneamente. Cada feature é desenvolvida em uma branch separada e só é mesclada na `main` após revisão.

### Passos do Workflow
1. Criar uma feature branch:
```bash
git checkout -b feature-article
```

2. Trabalhar e realizar commits:
```bash
git add .
git commit -m "Added Feature Branch Topic"
```

3. Enviar a branch e abrir um Pull Request:
```bash
git push origin feature-article
```

4. Após a aprovação, mesclar na `main` no repositório remoto e local.

### Diagrama
![feature-branch](/topics/imgs/07-guide-workflow-types/feature-branch.png)

## Forking Workflow
Os desenvolvedores fazem um fork do repositório em vez de trabalhar diretamente nele. Este modelo é recomendado e amplamente utilizado em projetos Open-Source.

Os desenvolvedores clonam o repositório, criam uma branch, fazem alterações e enviam suas mudanças para seu próprio fork. Depois disso, submetem as alterações como um **Pull Request (PR).**

### Passos do Workflow
1. Fazer um fork do repositório no GitHub.

2. Clonar o repositório forkado:
```bash
git clone https://github.com/lorenzouriel/ebook-git-github.git
```

3. Criar uma branch e fazer alterações:
```bash
git checkout -b feature-article
git add .
git commit -m "Added feature article"
git push origin feature-article
```

4. Submeter um Pull Request para o repositório original.

### Diagrama
![forking-workflow](/topics/imgs/07-guide-workflow-types/forking-workflow.png)

Ao aprender isso, você poderá decidir qual workflow mais se adapta a você e sua equipe, lembrando que em muitos casos já utilizamos um sem nem perceber.