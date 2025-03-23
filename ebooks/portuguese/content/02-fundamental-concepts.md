# Um Guia para Conceitos Fundamentais

Sem entender os fundamentos, sua história e o que o compõe, não faz sentido para um homem continuar trilhando o caminho.

Ok, eu não precisava dizer essa frase de efeito. Mas vamos focar neste capítulo como uma introdução geral ao que constitui Git & GitHub.

## Introdução a Repositórios e Conceitos

Um **repositório** é onde os arquivos, histórico e alterações de um projeto são armazenados. Ele pode ser:

- **Remoto:** Hospedado em plataformas como GitHub, GitLab ou Bitbucket.
- **Local:** Armazenado diretamente na máquina do desenvolvedor.

## **Conceitos Principais**

### **Branches**
Branches permitem que desenvolvedores trabalhem em diferentes funcionalidades ou correções sem afetar o código principal. A branch principal geralmente é chamada de **main**, mas você pode criar novas branches para tarefas específicas.

- **Exemplo:** Suponha que você esteja trabalhando na **task 13**. Você cria uma branch chamada **dev-task-13**, faz alterações, realiza commits e depois faz um merge de volta para **main** quando o trabalho estiver concluído. Isso mantém sua branch principal estável.

### **Commit**
Um **commit** captura o estado atual do projeto, como uma fotografia de todos os arquivos. Cada commit tem:

- Um identificador único (`hash`).
- Uma mensagem descritiva explicando a alteração.

### **Merge**
Um **merge** combina alterações de uma branch em outra, geralmente integrando uma branch de funcionalidade de volta para **main**.

### **Issues**
No GitHub, **issues** ajudam a rastrear tarefas, bugs ou solicitações de funcionalidades, proporcionando uma forma estruturada de gerenciar o desenvolvimento.

## Estrutura do Repositório

### **HEAD**
`HEAD` é um ponteiro para o commit mais recente na branch atual. Quando você faz um novo commit, `HEAD` é atualizado para apontar para ele.

### **Working Tree**
O **Working Tree** contém os arquivos do seu projeto, onde você pode modificar e criar conteúdo.

### **Index (Staging Area)**
O **index** é uma área de armazenamento intermediária onde o Git rastreia alterações antes do commit.

Para adicionar arquivos ao index:
```shell
git add file.txt
```

## Comandos Principais

### `git commit`
Realiza o commit das alterações preparadas, criando uma nova versão no repositório.

**Fluxo do Commit:**
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
- A flag `-m` permite especificar uma mensagem.

### `git push`
Envia as alterações locais para o repositório remoto.

**Fluxo do Push:**
1. Envie as alterações para o repositório remoto:
```bash
git push
```

2. Se for o primeiro push para uma nova branch remota:
```bash
git push -u origin main
```
- A flag `-u` configura o rastreamento para futuros pushes e pulls.

### `git pull`
Busca e mescla alterações do repositório remoto para a branch local.

**Fluxo do Pull:**
1. Obtenha as atualizações mais recentes:
```bash
git pull origin main
```

2. Se o rastreamento já estiver configurado:
```bash
git pull
```

### `git tag`
Uma `tag` marca um commit específico no histórico do Git, comumente usada para versionamento.

**Fluxo de Tags:**
1. Liste as tags existentes:
```bash
git tag
```

2. Crie uma nova tag anotada:
```bash
git tag -a v1.0 -m "Versão 1.0"
```

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

### **Arquitetura, Conceitos e Comandos:**
- ![architecture_git](content/imgs/02/architecture_git.jpg)

## Criando um Repositório Local e Remoto
1. Vá para seu GitHub e crie um novo repositório:
- ![1](content/imgs/02/1.jpg)

2. Navegue até o diretório local onde você quer criar o repositório
```shell
cd c:\path\vagrant
```

3. Este comando cria um arquivo chamado `README.md` e insere o texto `#up-website-with-vagrant` nele. O `>>` é um operador de redirecionamento que anexa o texto ao final do arquivo, ou cria o arquivo se ele não existir.
```shell
echo "# up-website-with-vagrant" >> README.md
```

4. Inicializa um novo repositório Git no diretório atual.
```shell
git init
```

5. Adiciona o arquivo `README.md` ao índice. Isso prepara o arquivo para ser incluído no próximo commit.
```shell
git add README.md
```

6. Adiciona todas as alterações (se houver)
```shell
git add .
```

7. Cria o primeiro commit no repositório com uma mensagem. O `-m` permite que você adicione a mensagem de commit diretamente na linha de comando.
```shell
git commit -m "first commit"
```

8. Renomeia o branch padrão do repositório para `main`. Este comando é usado para atualizar o nome do branch principal para seguir as práticas de nomenclatura mais recentes, substituindo o antigo master.
```shell
git branch -M main
```

9. Adiciona um repositório remoto chamado "origin". O termo "origin" é um termo padrão usado para se referir ao repositório remoto principal. A URL é o endereço do repositório no GitHub.
```shell
git remote add origin https://github.com/lorenzouriel/up-website-with-vagrant.git
```

10. Envia o repositório local para o repositório remoto ("origin") no branch principal. O -u estabelece um relacionamento de rastreamento, associando automaticamente o branch local ao branch remoto. Isso é útil para futuros git pull e git push sem precisar especificar o branch.
```shell
git push -u origin main
```

Podemos verificar nosso repositório remoto:
- ![10](content/imgs/02/10.jpg)


## O que é Versionamento e Tags?

Você já trabalhou com versões de lançamento?

Ou com Tags no Git?

Tags são muito importantes nos nossos projetos - com elas podemos identificar em que momento ocorreram os principais lançamentos e versões.

Mas quando você adiciona tags, saberá a diferença entre cada número?

Vou explicar de forma simples e prática:

- **Major:** Mudanças incompatíveis com versões anteriores (Reestruturou tudo? Adicione +1 - v2.0.0)
- **Minor:** Mudanças importantes compatíveis com a versão anterior (Adicionou uma nova funcionalidade? Adicione +1 - v2.1.0)
- **Correction:** Correções de erros e bugs que não afetam a versão (Encontrou um bug e corrigiu? Adicione +1 - v2.1.1)
- **Build:** Controle interno do Git e versionamento, não necessariamente visível ao especificar a versão.

**Exemplo:**
- ![tags_versioning](content/imgs/02/tags_versioning.jpg)

## Introdução ao Markdown

Markdown é uma linguagem de marcação leve usada para formatar texto de forma simples e legível.

Criada por John Gruber e Aaron Swartz em 2004, seu objetivo é ser lida em texto puro enquanto permite conversão automática para HTML. Markdown é amplamente utilizada para criar documentos, escrever posts de blog e produzir `README.md` em repositórios de código.

#### Cabeçalhos:
- Os cabeçalhos são criados usando o símbolo `#`. O número de `#` indica o nível do cabeçalho.
```md
# Nível de cabeçalho 1
## Nível de cabeçalho 2
### Nível de cabeçalho 3
```

#### Listas:
- O Markdown suporta listas ordenadas e não ordenadas. 
```md
- Item 1
- Item 2
- Subitem 2.1
- Subitem 2.2

1. Primeiro item
2. Segundo item
1. Subitem 2.1
2. Subitem 2.2
```

#### Links:
- Para criar links, use colchetes para o texto do link e parênteses para o URL.
```md
[Link para meu site](https://www.example.com)
```

#### Imagens:
- As imagens são inseridas de forma semelhante aos links, mas com um ponto de exclamação `!` antes delas.
```md
![Logotipo do projeto](images/logo.jpg)
```

#### Ênfase (negrito e itálico):
- Para criar ênfase no texto, você pode usar asteriscos ou sublinhados. 
```md
Este é um **projeto incrível** que usa _tecnologias modernas_.
```

#### Citações:
- Para criar uma citação, use o símbolo `>`.
```md
> "Seja a melhor versão de si mesmo." - Einstein
```

#### Tabelas:
- As tabelas podem ser criadas usando `|` para separar colunas e `-` para criar a linha de cabeçalho.
```md
| Nome | Função |
|------------|------------------|
| John | Desenvolvedor |
| Mary | Designer |
```

#### Código:
- Para incluir blocos de código, use três acentos graves antes e depois do bloco. Você pode especificar a linguagem de programação para realce de sintaxe.
- ![md_code](content/imgs/02/md_code.jpg)

Até agora entendemos o que compõe o Git e como começar seu primeiro projeto, vamos nos aprofundar no que vimos até agora!