# Um Guia para Começar no Git & GitHub

Quem são eles? Onde vivem? O que comem? E, o melhor de tudo, como instalar?

## O que é Git?
Git é um **sistema de controle de versão** projetado para rastrear mudanças em projetos de software e coordenar o trabalho de várias pessoas neles.

Desenvolvido por **Linus Torvalds em 2005**, o Git se destaca por sua eficiência, flexibilidade e capacidade de lidar com projetos de qualquer tamanho.

Ele registra alterações no código-fonte, permite que múltiplos branches de desenvolvimento existam simultaneamente e facilita a mesclagem de código de diferentes contribuidores.

A principal função do Git é permitir que várias pessoas trabalhem no mesmo código simultaneamente, sem causar conflitos ou perda de dados.

## Instalação e Configuração Inicial do Git
### Instalando o Git
#### Windows
1. Baixe o Git em: https://git-scm.com/downloads
2. Execute o instalador e selecione as opções padrão
3. Abra o Git Bash e verifique a instalação:
```bash
git --version
```

#### macOS:
1. Instale o Git via Homebrew:
```bash
brew install git
```

2. Verifique a instalação:
```bash
git --version
```

#### Linux (baseado em Debian):
```bash
sudo apt update && sudo apt install git
git --version
```

### Configuração Inicial do Git
Após instalar o Git, configure sua identidade:
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@example.com"
```

Verifique suas configurações com:
```bash
git config --list
```

Essas configurações garantem que seus commits sejam corretamente atribuídos.

## O que é GitHub?

GitHub é uma plataforma para controle de versão e colaboração usando Git. Ele permite que vários desenvolvedores trabalhem no mesmo projeto, rastreiem mudanças e gerenciem repositórios de código de forma eficiente.  

Com o GitHub, você pode:  
- Hospedar e compartilhar repositórios  
- Colaborar com equipes usando pull requests e revisões de código  
- Automatizar fluxos de trabalho com GitHub Actions  
- Gerenciar tarefas do projeto com Issues e Projects   

## Autenticações do GitHub
O GitHub não suporta mais a autenticação por senha para operações Git via HTTPS desde agosto de 2021. Se você tentou se conectar, provavelmente recebeu um erro.

Para resolver isso, é necessário usar um dos métodos de autenticação atualmente suportados. A maneira mais comum é usar um **personal access token (PAT)** ou uma **chave SSH**.

### SSH

#### 1. Verificar Chaves SSH Existentes
Antes de gerar uma nova chave SSH, verifique se você já possui uma no seu sistema:
```bash
ls -al ~/.ssh
```

Se você vir arquivos como `id_rsa` e `id_rsa.pub`, já possui um par de chaves SSH. Caso contrário, prossiga para gerar uma nova.

#### 2. Gerar uma Nova Chave SSH
Para gerar um novo par de chaves SSH, execute o seguinte comando:
```bash
ssh-keygen -t ed25519 -C "your_email@gmail.com"
```
- *Substitua `your_email@gmail.com` pelo e-mail que você usa no GitHub.*

Se seu sistema não suportar o algoritmo `ed25519`, use `rsa`:
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@gmail.com"
```
- *Substitua `your_email@gmail.com` pelo e-mail que você usa no GitHub.*

Esse comando cria uma nova chave SSH usando o e-mail fornecido como etiqueta.

#### 3. Salvar a Chave SSH
Quando for solicitado a "Inserir um arquivo para salvar a chave", pressione **Enter** para aceitar o local padrão `(~/.ssh/id_ed25519 ou ~/.ssh/id_rsa)`.

Em seguida, será solicitado que você insira uma senha. Você pode:
- Digitar uma senha segura (recomendado para maior segurança), ou  
- Pressionar **Enter** para pular a criação da senha (menos seguro, mas mais conveniente).

#### 4. Adicionar Sua Chave SSH ao Agente SSH
Para gerenciar sua chave SSH, é necessário garantir que o agente SSH esteja em execução:
```bash
eval "$(ssh-agent -s)"
```

Agora, adicione sua chave SSH privada ao agente:
```bash
ssh-add ~/.ssh/id_ed25519
```
- *(Ou `~/.ssh/id_rsa` se você usou RSA.)*

#### 5. Adicionar a Chave SSH ao GitHub
Agora você precisa adicionar a chave pública ao GitHub:
- Exiba a chave pública:
```bash
cat ~/.ssh/id_ed25519.pub
```
- Copie a saída (essa é sua chave pública).
- Acesse [SSH and GPG Keys](https://github.com/settings/keys) no GitHub.
- Clique em **New SSH key**, forneça um título (exemplo: "Meu Computador SSH") e cole sua chave pública no campo "Key".
- Clique em **Add SSH key**.

#### 6. Testar Sua Conexão SSH
Teste se a chave SSH está funcionando executando:
```bash
ssh -T git@github.com
```

Se for bem-sucedido, você verá uma mensagem como:
```bash
Hi lorenzouriel! You've successfully authenticated, but GitHub does not provide shell access.
```

#### 7. Alterar a URL Remota do Git para Usar SSH
Agora atualize seu repositório Git para usar SSH:
```bash
git remote set-url origin git@github.com:lorenzouriel/ebook-git-github.git
```

#### 8. Enviar Suas Alterações
Agora tente enviar suas alterações:
```bash
git push -u origin main
```

Isso deve funcionar sem pedir seu nome de usuário ou senha.

Agora você pode começar a trabalhar com Git & GitHub!