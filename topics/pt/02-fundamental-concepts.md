# Um Guia para Conceitos Fundamentais

Sem entender os fundamentos, sua história e sua composição, não faz sentido para alguém continuar trilhando o caminho.

Ok, eu não precisava dizer essa frase de efeito. Mas vamos focar neste capítulo como uma introdução geral ao que constitui o Git & GitHub.

## Introdução a Repositórios e Conceitos

Um **repositório** é onde os arquivos de um projeto, seu histórico e alterações são armazenados. Ele pode ser:

- **Remoto:** Hospedado em plataformas como GitHub, GitLab ou Bitbucket.
- **Local:** Armazenado diretamente no computador do desenvolvedor.

## **Principais Conceitos**

### **Branches (Ramificações)**
As branches permitem que os desenvolvedores trabalhem em diferentes funcionalidades ou correções sem afetar o código principal. A branch principal geralmente é chamada de **main**, mas você pode criar novas branches para tarefas específicas.

- **Exemplo:** Suponha que você esteja trabalhando na **tarefa 13**. Você cria uma branch chamada **dev-task-13**, faz alterações, realiza commits e, quando o trabalho estiver concluído, mescla de volta para a branch **main**. Isso mantém a branch principal estável.

### **Commit**
Um **commit** captura o estado atual do projeto, como uma captura de tela de todos os arquivos. Cada commit possui:

- Um identificador único (`hash`).
- Uma mensagem descritiva explicando a alteração.

### **Merge**
O **merge** combina alterações de uma branch em outra, geralmente integrando uma branch de funcionalidade de volta para a **main**.

### **Issues**
No GitHub, as **issues** ajudam a acompanhar tarefas, bugs ou solicitações de funcionalidades, proporcionando uma maneira estruturada de gerenciar o desenvolvimento.

## Estrutura do Repositório

### **HEAD**
O `HEAD` é um ponteiro para o commit mais recente na branch atual. Quando você faz um novo commit, o `HEAD` é atualizado para apontar para ele.

### **Working Tree (Área de Trabalho)**
A **Working Tree** contém os arquivos do seu projeto, onde você modifica e cria conteúdo.

### **Index (Área de Staging)**
O **index** é um espaço intermediário onde o Git rastreia alterações antes do commit.

Para adicionar arquivos ao index:
```shell
git add file.txt
```

## Principais Comandos

### `git commit`
Realiza o commit das alterações no repositório.

**Fluxo de Commit:**

1. Verifique o status dos arquivos modificados:
```bash
git status
```

2. Adicione arquivos ao commit:
```bash
git add file1.txt file2.js

# ou adicione todos os arquivos
git add .
```

3. Crie um commit com uma mensagem:
```bash
git commit -m "Primeiro Commit"
```
- O parâmetro `-m` permite especificar uma mensagem.

### `git push`
Envia as alterações locais para o repositório remoto.

**Fluxo de Push:**

1. Envie as alterações para o repositório remoto:
```bash
git push
```

2. Se for o primeiro push para uma nova branch remota:
```bash
git push -u origin main
```
- O parâmetro `-u` configura o rastreamento para futuros pushes e pulls.

### `git pull`
Baixa e mescla as alterações do repositório remoto para a branch local.

**Fluxo de Pull:**

1. Obtenha as atualizações mais recentes:
```bash
git pull origin main
```

2. Se o rastreamento já estiver configurado:
```bash
git pull
```

### `git tag`
Uma **tag** marca um commit específico no histórico do Git, geralmente usada para versionamento.

**Fluxo de Tags:**

1. Liste as tags existentes:
```bash
git tag
```

2. Crie uma nova tag anotada:
```bash
git tag -a v1.0 -m "Versão 1.0"
```
- `-a` cria uma tag anotada.
- `v1.0` é o nome da tag.
- `-m` especifica uma mensagem.

3. Envie a tag para o repositório remoto:
```bash
git push origin v1.0
```

### `git init`
Inicializa um novo repositório Git no diretório atual.
```bash
git init
```

### `git clone`
Cria uma cópia local de um repositório remoto.
```bash
git clone https://github.com/lorenzouriel/ebook-git-github.git
```

## Criando um Repositório Local e Remoto

1. Acesse o GitHub e crie um novo repositório.
- ![1](/topics/imgs/02/1.png)

2. Navegue até o diretório local onde deseja criar o repositório:
```shell
cd c:\path\vagrant
```
3. Crie um arquivo `README.md` e adicione texto a ele:
```shell
echo "# up-website-with-vagrant" >> README.md
```
4. Inicialize um novo repositório Git:
```shell
git init
```
5. Adicione o arquivo `README.md` ao index:
```shell
git add README.md
```
6. Adicione todas as alterações (se houver):
```shell
git add .
```
7. Crie o primeiro commit:
```shell
git commit -m "primeiro commit"
```
8. Renomeie a branch principal para `main`:
```shell
git branch -M main
```
9. Adicione um repositório remoto chamado "origin":
```shell
git remote add origin https://github.com/lorenzouriel/up-website-with-vagrant.git
```
10. Envie o repositório local para o repositório remoto:
```shell
git push -u origin main
```

We can check our remote repository:
- ![10](/topics/imgs/02/10.png)

## What is Versioning and Tags?

Have you ever worked with version releases?

Or with Tags in Git?

Tags are very important in our projects - with them we can identify at what point in time the main releases and versions occurred.

It is a way to organize and document your work.

But when you add tags, will you know the difference between each number?

I'll explain the difference in a simple and practical way:
- **Major:** These are changes that are incompatible with previous versions (Did you restructure everything? Add +1 - v2.0.0)
- **Minor:** These are important changes that are compatible with the previous version (Did you add a new feature? Add +1 v2.1.0)
- **Correction:** Errors and bugs that do not affect the version (Did you find a bug and fix it? Add +1 v2.1.1)
- **Build:** This is an internal control of Git and versioning, it is not necessarily visible when you specify the version.

**Example:**
- ![tags_versioning](/topics/imgs/02/tags_versioning.png)

## Introduction to Markdown
Markdown is a lightweight markup language used to format text in a simple and easy-to-read way.

Created by John Gruber and Aaron Swartz in 2004, its goal is to be readable in plain text while allowing automatic conversion to HTML. Markdown is widely used for creating documents, writing blog posts, and producing `README.md` in code repositories.

#### Headings:
- Headings are created using the `#` symbol. The number of `#` indicates the level of the heading.
```md
# Heading Level 1
## Heading Level 2
### Heading Level 3
```

#### Lists:
- Markdown supports both ordered and unordered lists. ```md
- Item 1
- Item 2
- Subitem 2.1
- Subitem 2.2

1. First item
2. Second item
1. Subitem 2.1
2. Subitem 2.2
```

#### Links:
- To create links, use square brackets for the link text and parentheses for the URL.
```md
[Link to my website](https://www.example.com)
```

#### Images:
- Images are inserted similarly to links, but with an exclamation point `!` before them.
``md
![Project Logo](images/logo.png)
```

#### Emphasis (bold and italics):
- To create emphasis in text, you can use asterisks or underscores. ```md
This is an **amazing project** that uses _modern technologies_.
```

#### Quotes:
- To create a quote, use the `>` symbol.
```md
> "Be the best version of yourself." - Einstein
```

#### Tables:
- Tables can be created using `|` to separate columns and `-` to create the header row.
```md
| Name | Role |
|------------|------------------|
| John | Developer |
| Mary | Designer |
```

#### Code:
- To include code blocks, use three backticks before and after the block. You can specify the programming language for syntax highlighting.
- ![md_code](/topics/imgs/02/md_code.png)

Até aqui entendemos o que compõe o Git e como iniciar o seu primeiro projeto, vamos nos aprofundar mais no que vimos até aqui!