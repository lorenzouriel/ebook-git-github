# Gerar Arquivo Zip

Para criar e gerar um arquivo ZIP contendo o conteúdo de um repositório Git, siga os passos abaixo:

## 1. Usando `git archive`

O Git fornece o comando `git archive` para criar um arquivo ZIP ou tar diretamente do repositório.

**Passo a passo:**
1. Abra o terminal no diretório do repositório.
2. Use o seguinte comando para criar o arquivo ZIP com o conteúdo da branch atual (por exemplo, main):
```bash
git archive --format=zip --output=nome-do-arquivo.zip main
```
- Substitua `main` pelo nome da branch que você deseja compactar.
- Substitua `nome-do-arquivo.zip` pelo nome desejado para o arquivo ZIP.
5. O arquivo ZIP será gerado no diretório atual.

## 2. Incluir Diretórios Específicos
Se quiser incluir apenas partes específicas do repositório, especifique os diretórios ou arquivos:
```bash
git archive --format=zip --output=nome-do-arquivo.zip main path/to/directory path/to/file
```

## 3. Criar um ZIP da Última Versão de um Commit Específico
Para gerar um ZIP de um commit específico, use o hash do commit:
```bash
git archive --format=zip --output=nome-do-arquivo.zip <hash-do-commit>
```

Após executar qualquer um dos métodos acima, você terá um arquivo ZIP contendo os arquivos e pastas do seu repositório, pronto para ser compartilhado ou usado.