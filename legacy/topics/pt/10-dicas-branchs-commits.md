# Dicas de Criação de Branchs e Commits
Uma dica para você que está com dúvida do que adicionar no seu commit e como nomear uma branch.

### Commits
Aqui estão algumas dicas para você que está em dúvida sobre como nomear seus commits:

- **Feat**: Usado quando você está adicionando uma nova funcionalidade.
  - Exemplo: `feat: adicionar funcionalidade de login`

- **Fix**: Usado para corrigir um bug ou erro.
  - Exemplo: `fix: corrigir erro de autenticação`

- **Style**: Usado para mudanças de formatação, como espaçamento ou estilo de código, sem alterar a lógica.
  - Exemplo: `style: ajustar espaçamento nos botões`

- **Refactor**: Usado para refatorar código sem adicionar novas funcionalidades ou corrigir bugs.
  - Exemplo: `refactor: reorganizar módulo de usuários`

- **Revert**: Usado para reverter commits anteriores.
  - Exemplo: `revert: reverter alteração de dependências`

- **Delete**: Usado para remover código, arquivos ou dependências que não são mais necessários.
  - Exemplo: `delete: remover módulo depreciado`

- **Update**: Usado para atualizações pequenas, como de documentação ou dependências.
  - Exemplo: `update: atualizar README`

- **Build**: Usado para mudanças no sistema de build ou nas dependências.
  - Exemplo: `build: atualizar configuração do Webpack`

- **Config**: Usado para mudanças nas configurações da aplicação ou do ambiente.
  - Exemplo: `config: ajustar variáveis de ambiente`

- **Chore**: Usado para tarefas menores ou de manutenção que não alteram o código-fonte diretamente.
  - Exemplo: `chore: limpar arquivos não utilizados`

- **CI**: Usado para mudanças na configuração de integração contínua.
  - Exemplo: `ci: ajustar pipeline do GitHub Actions`

- **Docs**: Usado para mudanças ou adição de documentação.
  - Exemplo: `docs: adicionar exemplos de uso da API`

- **Perf**: Usado para otimizações de performance.
  - Exemplo: `perf: melhorar desempenho da consulta ao banco`

- **Test**: Usado para adicionar ou modificar testes.
  - Exemplo: `test: adicionar testes unitários para módulo de login`

# Branches e Git Flow
No **Git Flow**, as branches seguem uma estrutura definida para organizar o fluxo de desenvolvimento. Aqui estão as dicas de como nomear as branches dentro desse fluxo:

- **Feat**: Usado para adicionar uma nova funcionalidade. Geralmente criado a partir da branch `develop`.
  - Exemplo: `feature/nova-funcionalidade-login`

- **Fix e Hotfix**: Usado para corrigir bugs ou erros. Geralmente criado a partir de `develop` ou `hotfix` (se for uma correção urgente).
  - Exemplo: `fix/corrigir-erro-autenticacao` - `hotfix/corrigir-erro-produção`

- **Refactor**: Usado para refatorar código sem mudar a funcionalidade. Criado a partir de `develop`.
  - Exemplo: `refactor/reorganizar-modulo-usuario` 

- **Release**: Usado para preparar uma nova versão do código, geralmente criado a partir de `develop` e depois mesclado em `main` e `develop`.
  - Exemplo: `release/1.0.0`