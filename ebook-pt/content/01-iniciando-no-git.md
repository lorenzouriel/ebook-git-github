# Iniciando no Universo do Git & GitHub
## O que é o Git?
O Git é um **sistema de controle de versão**, projetado para rastrear alterações em projetos de software e coordenar o trabalho de várias pessoas neles.

Desenvolvido por **Linus Torvalds em 2005**, o Git se destaca por sua eficiência, flexibilidade e capacidade de lidar com projetos de qualquer tamanho.

Ele registra as alterações no código-fonte, permite que várias ramificações de desenvolvimento existam simultaneamente e facilita a fusão de código de diferentes colaboradores.

A principal função do Git é permitir que múltiplas pessoas trabalhem no mesmo código simultaneamente, sem causar conflitos ou perda de dados.

**Principais características do Git:**
- **Distribuído:** Cada desenvolvedor possui uma cópia completa do histórico do repositório.
- **Desempenho:** Projetado para ser rápido e eficiente, mesmo com grandes quantidades de dados.
- **Segurança:** Garante a integridade do código e das mudanças realizadas.
- **Flexibilidade:** Suporta diversos fluxos de trabalho e processos de desenvolvimento.

## Instalação e Configuração Inicial do Git
**Passo 1: Instalação do Git**

Para instalar o Git, siga os passos abaixo de acordo com o seu sistema operacional:

**Windows:**
- Baixe o instalador do Git no site oficial: https://git-scm.com/.
- Execute o instalador e siga as instruções na tela, mantendo as configurações padrão.

**macOS:**
- Abra o Terminal.
- Execute o comando: `brew install git`. (Requer Homebrew, que pode ser instalado a partir de https://brew.sh/).

**Linux:**
- Abra o terminal.
- Execute o comando apropriado para sua distribuição:
    - Debian/Ubuntu: `sudo apt-get install git`.

**Passo 2: Configuração inicial do Git**

Após instalar o Git, é necessário configurá-lo. Use os seguintes comandos no terminal para configurar seu nome de usuário e email, que serão usados em seus commits:
```shell
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@example.com"
```

Você pode verificar suas configurações com o comando:
```shell
git config --list
```

## Instalação e Configuração Inicial do GitHub
**GitHub é uma plataforma de hospedagem de código-fonte que utiliza o Git para controle de versão.** Ele permite colaborar em projetos e compartilhar código com outros desenvolvedores.

**Passo 1: Criando uma conta no GitHub**
- Acesse https://github.com/.
- Clique em "Sign up" e siga os passos para criar uma nova conta.

**Passo 2: Configurando o Git para usar o GitHub (Windows)**
- Inicie o Git Bash e gere uma chave SSH para autenticação segura:
    - No terminal, execute: `ssh-keygen -t rsa -C "seuemail@example.com"`.
    - Pressione Enter para aceitar o local padrão do arquivo.
    - Digite uma senha segura (ou deixe em branco).

- Adicione a chave SSH ao seu GitHub:
    - Copie a chave pública que foi gerada.
    - Vá até as configurações do GitHub (Settings) > "SSH and GPG keys".
    - Clique em "New SSH key", cole a chave e salve.

Os passos são os mesmos para os outros sistemas operacionais, você vai precisar entender quais os comandos e onde eles salvam as chaves SSH que foram geradas.

**Passo 3: Conectando-se ao GitHub**
Para clonar um repositório do GitHub, use o comando:
```shell
git clone git@github.com:usuario/nome-do-repositorio.git
```
---