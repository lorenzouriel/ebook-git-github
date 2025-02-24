# Um Guia para Boas Práticas

Você precisa aprender algumas boas práticas antes de fazer seu próximo commit.

Qual é o melhor tipo de mensagem? Ou o melhor nome para as branches?

Sempre buscamos aplicar boas práticas em nossos projetos. Se você ainda não faz isso, é hora de começar.

Ainda mais quando trabalhamos em equipe, compartilhamos repositórios e realizamos revisões de código.

Sabe aquele commit que quebrou todo o código e a mensagem só dizia: "Agora vai!"? Pois é, é disso que estou falando.

Então, o que fazer?

Quais são as melhores práticas quando se trata de Git & GitHub?

## Commits Claros e Frequentes
Com certeza a mais importante e a primeira da lista: Escreva de forma que as pessoas consigam entender!

Faça commits pequenos e frequentes para manter um histórico de mudanças claro.

Use mensagens de commit descritivas e padronizadas, explicando o que foi alterado e por quê.

**Exemplo:**
```bash
git commit -m "fix: problema de login ao corrigir validação de senha"
```

Evite commits genéricos como apenas "fix" ou "update". Prefira algo mais detalhado.

Faça commits pequenos, onde cada um aborda uma única mudança. Pare de fazer commits e escrever um texto enorme explicando o que mudou, isso é terrível quando precisamos reverter.

### Dicas para Mensagens de Commit
O que escrever na sua mensagem de commit?

Eu sei que você já teve essa dúvida, especialmente quando fazemos várias alterações e precisamos especificar tudo em um único commit.

Eu sigo algumas práticas que considero boas nos meus projetos. São elas:
- `feat: adicionada compatibilidade com backup automático`
- `fix: ajustada normalização dos dados`
- `revert: revertida alteração no esquema do banco`
- `delete: removida tabela [old_logs]`
- `update: atualizada estrutura do banco de dados`
- `config: ajustada conexão com o banco no .env`
- `ci: adicionado passo de migração no pipeline`
- `docs: documentada estrutura das tabelas`
- `test: adicionados testes para funções de ETL`

A ideia é colocar no início uma descrição do que o commit trata, seguida de um detalhe claro do que foi feito.

**Commits frequentes são sempre melhores!** Não espere para fazer tudo de uma vez.

## Gerenciamento de Branches

Use branches para gerenciar o desenvolvimento de funcionalidades, deploys, releases e outras tarefas. Adote um fluxo de trabalho que seja adequado para sua equipe, como:

- **Git Flow:** A forma mais comum e popular de trabalhar, dividida entre branches principais (`dev`, `main`) e secundárias (`feature`, `release`, `hotfix`).
- **Trunk-Based Development:** O projeto é centralizado em uma única branch para toda a equipe, a `main`, e temos o conceito de `feature-branches` para mudanças.

### Dicas para Nomeação de Branches

E sempre nos deparamos com a mesma pergunta: **qual título colocar nesta branch?**

#### Branches Principais
O padrão que vejo na indústria para branches principais é:

- `dev` - `development`
- `qa` - `test`
- `main`

#### Branches de Alteração
Para branches de alteração e secundárias, sempre especifique o objetivo e adicione uma mensagem descritiva:

- `feature/adicionar-automatizacao-backup`
- `fix/corrigir-valores-nulos-no-relatorio`
- `hotfix/corrigir-problema-no-banco-em-producao`
- `refactor/normalizar-tabela-usuarios`
- `release/1.0.0`

Uma boa dica é relacionar o **ID da tarefa** e o **título da tarefa**, se seu backlog permitir:

- `feature/task544-adicionar-automatizacao-backup`
- `fix/task17-corrigir-valores-nulos-no-relatorio`

### Rebase

Outra boa dica ao trabalhar com branches é o comando `git rebase`. Você pode reordenar ou editar commits antes de mesclar. Isso ajuda a manter um histórico linear e legível:

```bash
git rebase -i HEAD~3  # Reordenar ou editar os últimos três commits interativamente
```

### Deleção de Branches
Regularmente, exclua branches antigas ou desatualizadas para manter o repositório limpo:
```bash
git branch -d feature/task544-adicionar-automatizacao-backup  # Excluir uma branch já mesclada
git branch -D feature/task544-adicionar-automatizacao-backup  # Forçar a exclusão de uma branch não mesclada
```

## Use `.gitignore`

Sempre configure um arquivo `.gitignore` apropriado para seu projeto, para evitar versionar arquivos desnecessários.

**Exclua arquivos de build, dependências, credenciais e todas as configurações de ambiente possíveis.**

Recomendo o uso do [toptal site](https://www.toptal.com/developers/gitignore), que gera os arquivos `.gitignore` mais completos para cada linguagem. Aqui está um exemplo gerado para [**Python**.](https://www.toptal.com/developers/gitignore/api/python)

Você também pode conferir os templates prontos feitos pelo GitHub no repositório [github/gitignore](https://github.com/github/gitignore).

## Git Hooks

Com os **Git Hooks**, você pode automatizar regras e padrões que precisam ser aplicados em várias etapas do seu fluxo de trabalho.

### Hooks de Pre-Commit

Use hooks de **pre-commit** para executar verificações automatizadas antes que as alterações sejam commitadas. Esses hooks podem impor padrões de qualidade no código. Alguns exemplos:

- Rodar **linters** para detectar erros de sintaxe ou estilo.
- Executar **testes unitários** para garantir que as mudanças não quebrem o código.
- Validar **mensagens de commit** para seguir um formato consistente.

Isso permite detectar erros cedo e impedir que o desenvolvedor envie qualquer código que possa afetar o projeto principal.

### Hooks de Post-Commit

Use hooks de **post-commit** para automatizar tarefas após o **push** para um repositório remoto. Esses hooks são ideais para:

- **Atualizar ambientes** de staging ou produção automaticamente.
- Acionar **pipelines de CI/CD** para implantar ou testar mudanças.
- Enviar **notificações** para sua equipe sobre novas atualizações.

Isso ajuda a minimizar erros e a criar um processo inicial de deploy automatizado.
