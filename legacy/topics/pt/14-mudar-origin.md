# Alterar o Origin
Para alterar o remote origin do seu repositório Git atual para o novo URL, siga os passos abaixo:

### Passos para Alterar o Origin

1. Verifique o remote atual:
```bash
git remote -v
```
- Isso mostrará o endereço atual do `origin`.

2. Altere o remote origin para o novo URL:
```bash
git remote set-url origin https://github.com/lorenzouriel/kafka-temperature-monitoring
```

3. Confirme a alteração:
```bash
git remote -v
```
- O novo endereço `origin` deverá aparecer listado.

### Comandos Explicados
- `git remote set-url`: Atualiza o URL de um repositório remoto.
- `origin`: Nome padrão do repositório remoto principal.
- `Novo URL`: Substitui o endereço do repositório remoto anterior.

Após a mudança, você pode realizar push, pull ou outras operações normalmente com o novo repositório.