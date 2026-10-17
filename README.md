# Ramais Prefeitura de Palhoça

Página estática da Informac com atalhos para os servidores da Prefeitura de Palhoça:

- **Lista de ramais**: link para o site de busca de ramais da prefeitura.
- **Abertura de chamado**: link para o 1Doc (`palhoca.1doc.com.br`).
- **Comandos básicos do telefone**: cards explicando como transferir ligação, ligar para DDD, fazer transferência assistida e puxar ligação.

Não tem build, framework nem dependências: é só HTML e CSS.

## Estrutura

```
index.html          # página única (links + cards de comandos)
style/style.css     # importa todos os outros arquivos CSS
style/*.css         # estilos separados por seção (header, nav, card, footer...)
assets/logo.png     # logo da Informac
assets/img/         # ícones usados nos cards
```

## Como rodar localmente

O `index.html` usa caminhos absolutos (`/style/style.css`, `/assets/...`). Se você abrir o arquivo direto no navegador (`file://`), a página aparece sem estilo. Sirva a pasta com um servidor local:

```bash
# Python
python -m http.server 8000

# ou Node
npx serve .
```

Depois abra http://localhost:8000. No VS Code, a extensão **Live Server** também funciona.

## Como atualizar

### Trocar o link da lista de ramais ou do chamado

No `index.html`, dentro do `<nav>`, mude o `href` do link:

```html
<a href="https://sites.google.com/view/pmpramais/in%C3%ADcio" target="_blank" class="label">Lista de ramais</a>
```

O link da lista de ramais já mudou algumas vezes (planilha do Google Sheets → site do Google Sites). Quando a prefeitura mandar um link novo, é só substituir esse `href`.

### Editar ou adicionar um comando do telefone

Cada comando é um `.card` dentro de `<div class="content grid gap">`. Para adicionar um novo, copie um card existente e ajuste o texto:

```html
<div class="card">
    <h1>Puxar ligação</h1>
    <div class="number-input"> <strong class="margin-r">*8</strong> + RAMAL</div>
    <p>Exemplo: </p>
    <div class="code-output"><strong>*8</strong><span style="color: #1e5aa8;">5555</span></div>
</div>
```

### Alterar o visual

Edite o CSS da seção em `style/`. Se criar um arquivo CSS novo, adicione um `@import` dele em `style/style.css`.

### Publicar a alteração

1. Teste localmente (veja acima).
2. Faça o commit seguindo o padrão do repositório (`feature:`, `fix:`, `fixing:`):
   ```bash
   git add .
   git commit -m "fix: atualizar link da lista de ramais"
   git push origin main
   ```
