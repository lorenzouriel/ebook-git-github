# Conceitos Fundamentais
## Introdução aos Repositórios e Conceitos
Um repositório é o local onde o projeto, suas alterações e arquivos são armazenados. Ele pode ser local ou remoto, cada um com suas características específicas:
- **Remoto:** Hospedado em plataformas como GitHub, outros sistemas de controle de versão (CVS) ou servidores dedicados.
- **Local:** Armazenado diretamente na máquina do desenvolvedor.

### Principais Conceitos
**Branches (ou Ramos)**
- As **branches (ou ramos), que são versões paralelas do projeto.** A branch principal geralmente é chamada de **main**, mas é possível criar novas branches para desenvolver alterações específicas sem afetar a branch principal.
    - **Exemplo:** Crie um branch chamada **dev-task-13**, nesse branch você vai focar em finalizar a task 13 do seu backlog, quando finalizar você **commita** e faz um **merge** com a branch principal. Assim, você não afeta o seu branch principal com alterações que podem quebrar o código.

**Commit**
- Um **commit** é uma operação que captura o estado atual do projeto. É como tirar uma foto dos arquivos naquele momento. Cada commit tem um identificador único (`hash`) e uma mensagem descritiva.

**Merge**
- O **merge** é a operação de combinar as mudanças de diferentes branches. Geralmente, você realiza um merge quando deseja integrar as alterações de uma branch de feature ou correção de bug de volta à branch principal.

**Issues**
- No contexto do Git, uma issue refere-se a uma maneira de rastrear tarefas, melhorias, erros (bugs) ou discussões relacionadas a um projeto específico.

### Estrutura do Repositório
**Working Tree**
- A Working Tree é o local onde os arquivos estão realmente armazenados e onde você faz suas alterações.

**Index (Índice)**
- O index (ou índice) é o local onde o Git armazena o que será commitado. Ele atua como uma área intermediária entre a Working Tree e o repositório Git. Para adicionar arquivos ao índice, usamos o comando: `git add arquivo.txt`

### Arquitetura Git e Conceitos
- ![architecture_git](/topics/img/02/architecture_git.jpg)

## Principais Comandos
#### `Commit` 
Acontece quando queremos salvar as última atualizações que foram realizadas.

**Processos relacionados ao Commit:**
- Verificar o status dos arquivos modificados:
```shell
git status
```

- Adicionar os arquivos para o commit:

```shell
git add arquivo1.txt arquivo2.js

git add .
```

- Realizar o commit:
```shell
git commit -m "Primeiro Commit"
```

O `-m` é utilizado para adicionarmos uma mensagem no commit, em seguida temos o texto `"Primeiro Commit"`.

#### `Push` 
Acontece quando enviamos as alterações para o repositório - "empurra" as modificações para o repositório remoto

**Processos relacionados ao Push:**
- Realizar o push para o repositório remoto:
```shell
git push

# ou

git push origin nome-da-branch
```

- Se for a primeira conexão e primeiro push: 
```shell
git push -u origin nome-da-branch
```

É necessário configurar a relação entre as branches locais e remotas usando o comando acima.

O `-u` estabelece uma relação de acompanhamento, facilitando futuros pushes e pulls.

#### `Pull` 
Atualiza o seu repositório local com as alterções no repositório remoto - "puxa" as alterações do repositório remoto.

Ele traz todas as alterações do seu repositório remoto para o local.

**Processos relacionados ao Pull:**
- Realizar o pull para obter as alterações mais recentes:
```shell
git pull origin nome-da-branch
```

- Se você já configurou a relação de acompanhamento durante o git push `-u`, pode usar apenas:
```shell
git pull
```

#### `Tag` 
Uma tag no Git é uma referência específica a um ponto na história do seu repositório. É comumente usado para marcar versões estáveis ou importantes do seu projeto. 

As tags são úteis para criar pontos de referência fixos que não se movem à medida que novos commits são feitos.

**Processos relacionados ao Tag:**
- Listar as tags existentes:
```shell
git tag
```

- Criar uma nova tag:
```shell
git tag -a v1.0 -m "Versão 1.0"
```
- Este comando cria uma tag anotada chamada `"v1.0"` com uma mensagem descritiva `"Versão 1.0"`.
    - **1. a: Cria uma tag anotada.**
    - **2. v1.0: Nome da tag.**
    - **3. -m "Versão 1.0": Mensagem descritiva associada à tag.**

- Compartilhar a tag no repositório remoto:
```shell
git push origin v1.0
```

#### `init`
Inicializa um novo repositório Git no diretório atual.
```shell
git init
```

#### `clone`
Clona um repositório remoto para o seu computador.
```shell
git clone <url-do-repositorio>
```

## Criando um Repo Local e Remoto
**1. Vá até o seu GitHub e crie um novo repositório:**
- ![1](/topics/img/02/1.png)

**2. Navegue até o diretório local onde deseja criar o repositório — use o comando cd para entrar no diretório desejado.**
```shell
cd c:\path\vagrant
```

**3. Este comando cria um arquivo chamado README.md e insere o texto #up-website-with-vagrant nele. O >> é um operador de redirecionamento que acrescenta o texto ao final do arquivo, ou cria o arquivo se ele não existir.**
```shell
echo "# up-website-with-vagrant" >> README.md
```

**4. Inicializa um novo repositório Git no diretório atual.**
```shell
git init
```

**5. Adiciona o arquivo README.md ao índice. Isso prepara o arquivo para ser incluído no próximo commit.**
```shell
git add README.md
```

**6. Adiciona todas as alterações (Se houver)**
```shell
git add .
```

**7. Cria o primeiro commit no repositório com uma mensagem. O -m permite adicionar a mensagem de commit diretamente na linha de comando.**
```shell
git commit -m "first commit"
```

**8. Renomeia a branch padrão do repositório para main. Este comando é usado para atualizar o nome da branch principal para seguir as práticas mais recentes em relação ao uso de nomes, substituindo a antiga master**
```shell
git branch -M main
```

**9. Adiciona um repositório remoto chamado "origin". O termo "origin" é um padrão utilizado para referenciar o repositório remoto principal. O URL é o endereço do repositório no GitHub.**
```shell
git remote add origin https://github.com/lorenzouriel/up-website-with-vagrant.git
```

**10. Envia o repositório local para o repositório remoto ("origin") na branch principal (main). O -u estabelece uma relação de acompanhamento, associando automaticamente a branch local com a branch remota. Isso é útil para futuros git pull  e git push sem a necessidade de especificar a branch.**
```shell
git push -u origin main
```

Podemos verificar o nosso repositório remoto:
- ![10](/topics/img/02/10.png)

### O que é Versionamento e Tags?
Já trabalhou com lançamento de versões?

Ou com Tags no Git?

As tags são bem importantes em nossos projetos - com elas conseguimos identificar em qual momento no tempo ocorreram os principais lançamentos e versões.

É um meio de organizar e documentar o seu trabalho.

Mas quando você for adicionar as tags, vai saber a diferença de cada número?

Vou te explicar a diferença de forma simples e prática:
- **Major:** São alterações incompatíveis com as versões anteriores (Reestruturou tudo? Adicione +1 - v2.0.0)
- **Minor:** São alterações importantes e compativéis com a versão anterior (Adicionou uma nova funcionalidade? Adicione +1 v2.1.0)
- **Correção:** Erros e bugs que não afetam a versão (Encontrou um bug e corrigiu? Adicione +1 v2.1.1)
- **Build:** É um controle interno do Git e do versionamento, ele não fica necessariamente à vista quando você especifica a versão.

**Exemplo:**
- ![tags_versioning](/topics/img/02/tags_versioning.png)

## Introdução ao Markdown
Markdown é uma linguagem de marcação leve usada para formatar texto de forma simples e fácil de ler. 

Criada por John Gruber e Aaron Swartz em 2004, seu objetivo é ser legível em texto plano e, ao mesmo tempo, permitir a conversão para HTML de forma automática. Markdown é amplamente utilizado para criar documentos, escrever posts em blogs, e produzir `README.md` em repositórios de código.

#### Cabeçalhos:
- Os cabeçalhos são criados usando o símbolo `#`. O número de `#` indica o nível do cabeçalho.
```md
# Cabeçalho Nível 1
## Cabeçalho Nível 2
### Cabeçalho Nível 3
```

#### Listas:
- Markdown suporta listas ordenadas e não ordenadas.
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
- Para criar links, use colchetes para o texto do link e parênteses para a URL.
```md
[Link para o meu site](https://www.exemplo.com)
```

#### Imagens:
- As imagens são inseridas de forma semelhante aos links, mas com um ponto de exclamação `!` antes.
```md
![Logo do Projeto](imagens/logo.png)
```

#### Ênfase (negrito e itálico):
- Para criar ênfase em texto, você pode usar asteriscos ou sublinhados.
```md
Este é um **projeto incrível** que usa _tecnologias modernas_.
```

#### Citações:
- Para criar uma citação, use o símbolo `>`.
```md
> "Seja a sua melhor versão." - Einstein
```

#### Tabelas:
- Tabelas podem ser criadas usando `|` para separar colunas e `-` para criar a linha do cabeçalho.
```md
| Nome       | Função           |
|------------|------------------|
| João       | Desenvolvedor    |
| Maria      | Designer         |
```

#### Código:
- Para incluir blocos de código, utilize três acentos graves antes e depois do bloco. Você pode especificar a linguagem de programação para realce de sintaxe.
    - ![md_code](/topics/img/02/md_code.png)
---