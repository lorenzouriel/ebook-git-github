# Trabalhando com Branches
## Criando e Gerenciando Branches Locais
**1. Criar uma nova branch:**
```shell
git branch <nome-da-branch>
```

**2. Mudar para uma branch:**
```shell
git checkout <nome-da-branch>
```

**3. Criar e mudar para uma nova branch:**
```shell
git checkout -b <nome-da-branch>
```

**4. Listar todas as branches:**
```shell
git branch
```

**5. Renomear uma branch:**
```shell
git branch -m <nome-da-branch>
```

**6. Excluir uma branch:**
```shell
git branch -d <nome-da-branch>
```

## Mesclando Branches (Merge)
**1. Mesclar uma branch na branch atual:**
```shell
git merge <nome-da-branch>
```

### Resolução de Conflitos de Merge
Durante um merge, se houver conflitos, o Git irá pausar o processo e te informar sobre os arquivos conflitantes. Edite esses arquivos para resolver os conflitos, marcados com:
```git
<<<<<<< HEAD
(mudanças na branch atual)
=======
(mudanças na branch que está sendo mesclada)
>>>>>>> <nome-da-branch>
```

Depois de resolver os conflitos, marque os arquivos como resolvidos:
```shell
git add .
```

Finalize o merge:
```shell
git commit -m "Arquivos conflitantes resolvidos."
```

### Branches Remotos e Rastreamento de Branches
**1. Listar branches remotos:**
```shell
git branch -r
```

**2. Criar uma branch rastreando uma branch remota:**
```shell
git checkout --track origin/<nome-da-branch-remota>
```
- Só precisa realizar o rastreio se a branch remota não existir em seu repositório local.

**3. Atualizar branches remotos:**
```shell
git fetch
```

**4. Mesclar mudanças de uma branch remota na branch atual:**
```shell
git pull origin <nome-da-branch-remota>

# Ou apenas

git pull
```

## Fluxo de Trabalho com Branches (Feature Branch, Hotfix e Release.)
**1. Feature Branch:**
- Criar uma nova branch para a feature:
```shell
git checkout -b feature/<nome-da-feature>
```

- Trabalhar na feature e fazer commits.

- Mesclar a branch da feature na branch principal (geralmente `main` ou `dev`):
```shell
git checkout main
git merge feature/<nome-da-feature>
```

**2. Hotfix Branch:**
- Criar uma nova branch para o hotfix a partir da branch principal:
```shell
git checkout -b hotfix/<nome-do-hotfix> main
```

- Trabalhar no hotfix e fazer commits.

- Mesclar a branch do hotfix na branch principal:
```shell
git checkout main
git merge hotfix/<nome-do-hotfix>
```

- Mesclar a branch do hotfix na branch de `dev` (se houver):
```shell
git checkout dev
git merge hotfix/<nome-do-hotfix>
```

**3. Release Branch:**
- Criar uma nova branch para a release a partir da branch de desenvolvimento:
```shell
git checkout -b release/<versao> <nome-da-branch>

# Código
git checkout -b release/1.0.0 dev
```

- Testar e preparar a release, fazendo commits conforme necessário.

- Mesclar a branch da release na branch principal e taguear a versão:
```shell
git checkout main
git merge release/<versao>
git tag -a v<versao> -m "Versão <versao>"

# Código
git checkout main
git merge release/1.0.0
git tag -a v1.0.0 -m "Versão 1.0.0"
```

- Mesclar a branch da release de volta na branch de `dev`:
```shell
git checkout dev
git merge release/<versao>
```
---