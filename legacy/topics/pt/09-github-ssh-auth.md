# Autenticações GitHub
O GitHub não oferece mais suporte à autenticação por senha para operações HTTPS Git desde 13 de agosto de 2021. Se você tentou conectar, provavelmente recebeu um erro.

Para resolver isso, você precisa usar um dos métodos de autenticação suportados atualmente. A maneira mais comum é usar um token de acesso pessoal (PAT) ou usar uma chave SSH.

## SSH

### 1. Verifique as chaves SSH existentes
Antes de gerar uma nova chave SSH, verifique se você já possui uma em seu sistema
```bash
ls -al ~/.ssh
```

Se retornar arquivos como `id_rsa` e `id_rsa.pub`, você já possui um par de chaves SSH. Caso contrário, prossiga para gerar um novo.

### 2. Gere uma nova chave SSH
Para gerar um novo par de chaves SSH, execute o seguinte comando:
```bash
ssh-keygen -t ed25519 -C "seu_email@gmail.com"
```
- *Substitua `seu_email@gmail.com` pelo e-mail que você usa para GitHub.*

Se o seu sistema não suporta o algoritmo `ed25519`, use `rsa`:
```bash
ssh-keygen -t rsa -b 4096 -C "seu_email@gmail.com"
```
- *Substitua `seu_email@gmail.com` pelo e-mail que você usa para GitHub.*

Este comando cria uma nova chave SSH usando o e-mail fornecido como rótulo identificador.

### 3. Salve a chave SSH
Quando solicitado a "Inserir um arquivo no qual salvar a chave", pressione Enter para aceitar o local padrão `(~/.ssh/id_ed25519 ou ~/.ssh/id_rsa)`.

Em seguida, você será solicitado a inserir uma senha. Você pode:
- Digite uma senha segura (recomendada para melhor segurança) ou
- Pressione Enter para pular a criação de uma senha (menos segura, mas mais conveniente).

### 4. Adicione sua chave SSH ao agente SSH
Para gerenciar sua chave SSH, você precisa garantir que o agente SSH esteja em execução:
```bash
eval "$(ssh-agent -s)"
```

Agora, adicione sua chave privada SSH ao agente:
```bash
ssh-add ~/.ssh/id_ed25519
```
- *(Ou `~/.ssh/id_rsa` se você usou RSA.)*

### 5. Adicione a chave SSH ao GitHub
Agora você precisa adicionar a chave pública ao GitHub:

- Exibir a chave pública:
```bash
cat ~/.ssh/id_ed25519.pub
```
- Copie a saída (esta é a sua chave pública).
- Acesse GitHub [chaves SSH e GPG](https://github.com/settings/keys).
- Clique em Nova chave SSH, forneça um título (por exemplo, "My Machine SSH") e cole sua chave pública no campo "Chave".
- Clique em Adicionar chave SSH.

### 6. Teste sua conexão SSH
Teste se a chave SSH está funcionando executando:
```bash
ssh -T git@github.com
```

Se for bem-sucedido, você verá uma mensagem como:
```bash
Hi lorenzouriel! You've successfully authenticated, but GitHub does not provide shell access.
```

### 7. Altere seu URL remoto do Git para usar SSH
Agora atualize seu controle remoto Git para usar SSH:
```bash
git remote set-url origin git@github.com:lorenzouriel/ebook-git-github.git
```

### 8. Promova suas alterações
Agora tente enviar suas alterações:
```bash
git push -u origin main
```

Isso deve funcionar sem solicitar seu nome de usuário ou senha!