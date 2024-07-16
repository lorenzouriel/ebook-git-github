# Práticas Recomendadas
## Commits Claros e Frequentes
**Commits Frequentes:**
- Faça commits pequenos e frequentes para facilitar a identificação de problemas e a reversão de mudanças específicas.
- Cada commit deve representar uma única mudança lógica no código.
- Toda alteração deve ter um commit.

**Mensagens de Commit Claras:**
- Use mensagens de commit descritivas e significativas.
- A linha deve ser um resumo curto e conciso (50 caracteres ou menos), pode adicionar uma descrição mais detalhada, se necessário.
```shell
git commit -m "Corrige bug na função de login"
git commit -m "Adiciona testes unitários para o módulo de autenticação"
```

## Uso de `.gitignore`
**Criar e Usar o Arquivo `.gitignore`:**
- O arquivo `.gitignore` é usado para especificar quais arquivos e diretórios devem ser ignorados pelo Git.

- Exemplos comuns incluem arquivos de configuração local, diretórios de build, e arquivos temporários.

- Você pode usar o site [toptal](https://www.toptal.com/developers/gitignore) para buscar arquivos `.gitignore` completos e preenchidos para a respectiva linguagem.

Exemplo de um arquivo `.gitignore`:
```shell
# Logs
*.log

# Diretórios de build
/build/
/dist/

# Arquivos de configuração
.env
.vscode/

# Arquivos temporários
*.tmp
```

- Para criar ou editar o arquivo `.gitignore`, adicione-o na raiz do seu repositório.

## Reposicionamento de Branches
**Rebase em vez de Merge:**
Use `git rebase` para aplicar commits de uma branch no topo de outra, criando um histórico mais linear.
```shell
git checkout feature-branch
git rebase main
```
- O comando `git rebase` é usado para integrar mudanças de um ramo em outro, mas de uma forma diferente do comando `git merge`. Enquanto o `merge` cria um novo commit de `merge`, o `rebase` reaplica os commits de um ramo sobre a ponta de outro ramo, resultando em um histórico linear. 

Resolve conflitos se necessário e continue com:
```shell
git rebase --continue
```

**Mesclar Branches:**
Use `git merge` para combinar mudanças de uma branch em outra, preservando o histórico de commits.
```shell
git checkout main
git merge feature-branch
```

## Manutenção de Histórico Limpo e Compreensível
**Rebase Interativo para Limpar Histórico:**
Use `git rebase -i` para reordenar, editar, combinar (squash) ou descartar commits.
```shell
git rebase -i HEAD~n
```
- No editor que se abre, altere `pick` para `squash` para combinar commits.

Evite commits de merge desnecessários usando `git pull --rebase` em vez de `git pull`.

## Automação de Tarefas com Hooks do Git
**Configurar Hooks do Git:**
Os hooks do Git são scripts que são executados automaticamente em determinados eventos, como antes de um commit ou após um push.

Exemplos de hooks incluem `pre-commit`, `pre-push`, `post-commit`, entre outros.

Exemplo de um hook `pre-commit` para verificar o estilo de código:
```shell
@echo off
# Pre-commit hook para rodar pytest

echo Running pytest
pytest

# se pytest falhar, não faça o commit
if errorlevel 1 (
    echo Tests failed
    exit /b 1
)
```

Coloque os scripts de hook no diretório `.git/hooks/` do seu repositório e torne os scripts executáveis:
```shell
chmod +x .git/hooks/pre-commit
```

## Resumo
- Commits claros e frequentes facilitam a colaboração e o gerenciamento de código.

- Uso de .gitignore mantém o repositório limpo de arquivos desnecessários.

- Reposicionamento de branches com rebase e merge adequados mantém o histórico legível e linear.

- Manutenção de histórico limpo com ferramentas como rebase interativo evita complexidade desnecessária.

- Automação de tarefas com hooks do Git assegura a qualidade do código e a consistência do repositório.
---