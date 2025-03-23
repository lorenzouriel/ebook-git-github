# Um Guia para Boas Práticas

Você precisa aprender algumas práticas recomendadas antes de fazer seu próximo commit.

Qual é o melhor tipo de mensagem? Ou o melhor nome para os branches?

Sempre buscamos aplicar as melhores práticas em nossos projetos. Se você ainda não faz isso, é hora de começar.

Ainda mais quando trabalhamos em equipe, compartilhamos repositórios e fazemos revisões de código.

Sabe aquele commit que quebrou todo o código e a mensagem só dizia: "Agora vai!"? Pois é disso que estou falando.

Então o que fazer?

Quais são as melhores práticas quando se trata de Git e GitHub?

## Commits Claros e Frequentes

Com certeza o mais importante e o primeiro da lista: Escreva de uma forma que as pessoas possam entender!

Faça commits pequenos e frequentes para manter um histórico de alterações claro.

Use mensagens de commit descritivas e padronizadas explicando o que foi alterado e o porquê.

**Exemplo:**
```bash
git commit -m "fix: login issue by correcting password validation"
```

Evite commits genéricos como apenas "fix" ou "update". Prefira algo com mais detalhes.

Faça commits pequenos, onde cada um aborda uma única alteração. Pare de fazer commits e escrever um texto inteiro explicando o que mudou, isso é péssimo quando precisamos reverter.

### Dicas para Mensagens de Commits
O que escrever na sua mensagem de commit?

Eu sei que você já teve essa dúvida, principalmente quando fazemos várias alterações e precisamos especificar tudo em um único commit.

Eu sigo algumas práticas que considero boas nos meus projetos. Eles são:
- `feat: adicionado suporte para backup automático`
- `fix: ajustado normalização de dados`
- `revert: revertida alteração no esquema do banco`
- `delete: removida tabela [old_logs]`
- `update: atualizada estrutura do banco de dados`
- `config: ajustada conexão do banco de dados em .env`
- `ci: adicionada etapa de migração no pipeline`
- `docs: documentada estrutura da tabela`
- `test: adicionados testes para funções ETL`

A ideia é colocar no início uma descrição do que é o commit, seguido por um detalhe claro do que foi realizado.

Commits frequentes são sempre melhores! Não espere para fazer tudo de uma vez.

## Gerenciamento de Branch
Use branches para gerenciar o desenvolvimento de recursos, implantações, lançamentos e outras tarefas. Adote um fluxo de trabalho que seja bom para sua equipe, como:
- **Git Flow:** A maneira mais comum e popular de trabalhar, dividida por branches principais (`dev`, `main`) e secundários (`feature`, `release`, `hotfix`).
- **Trunk-Based Development:** O projeto é centralizado em apenas um branch exclusivo para toda a equipe, o `main` e temos o conceito de `feature-branchs` para alterações.

### Dicas para nomes de branches
E sempre nos encontramos com a mesma pergunta, qual título colocar neste branch?

#### Branches principais
O padrão que vejo na indústria para as branches principais é:
- `dev` - `development`
- `qa` - `test`
- `main`

#### Branches de alteração
Para branches de alterações, sempre especifique o objetivo e adicione uma mensagem descritiva:
- `feature/add-backup-automation`
- `fix/fix-null-values-in-report`
- `hotfix/fix-production-database-issue`
- `refactor/normalize-user-table`
- `release/1.0.0`

Uma boa dica é relacionar o ID da tarefa e o título da tarefa, se seu backlog suportar:
- `feature/task544-add-backup-automation`
- `fix/task17-fix-null-values-in-report`

### Rebase
Outra boa dica ao trabalhar com branches é o comando `git rebase`. Você pode reordenar ou editar commits antes de mesclar. Isso ajuda a manter um histórico linear e legível:
```bash
git rebase -i HEAD~3 # Reordene ou edite os últimos três commits interativamente
```

*Evite rebasear branches compartilhados como `main` ou `dev` para evitar conflitos e confusão para os outros.*

### Delete
Exclua regularmente branches antigos ou desatualizados para manter o repositório limpo:

```bash
git branch -d feature/task544-add-backup-automation # Exclua um branch mesclado
git branch -D feature/task544-add-backup-automation # Exclua um branch não mesclado à força
```

## Use .gitignore
Sempre configure um arquivo `.gitignore` apropriado para seu projeto para evitar versionamento de arquivos desnecessários.

Exclua arquivos de build, dependências, credenciais e todas as configurações de ambiente possíveis.

Recomendo que você use o [site toptal](https://www.toptal.com/developers/gitignore), ele gera os arquivos `.gitignore` mais completos para cada linguagem. Este é um [exemplo python gerado com toptal.](https://www.toptal.com/developers/gitignore/api/python)

Você também pode verificar os modelos prontos feitos pelo github no [repositório github/gitignore](https://github.com/github/gitignore).

## Git Hooks
Com Git Hooks você pode automatizar regras e padrões que precisam ser aplicados em vários estágios do seu fluxo de trabalho.

### Pre-commit Hooks
Use pre-commit hooks para executar verificações automatizadas antes que as alterações sejam confirmadas. Esses hooks podem impor ao código seus padrões de qualidade predefinidos, alguns exemplos:
- Executar linters para capturar erros de sintaxe ou estilo.
- Executar testes de unidade para garantir que as alterações não quebrem o código.
- Validar mensagens de confirmação para seguir um formato consistente.

Aqui você pode detectar erros antecipadamente e impedir que o desenvolvedor envie qualquer código que possa afetar o projeto principal.

### Post-receive Hooks
Use post-receive hooks para automatizar tarefas após as alterações serem enviadas para um repositório remoto. Esses hooks são ideais para:
- Atualizar ambientes de preparação ou produção automaticamente.
- Acionar pipelines de CI/CD para implantar ou testar alterações.
- Enviar notificações para sua equipe sobre novas atualizações.

Claro, minimizando erros e criando uma implantação inicial de forma automática.