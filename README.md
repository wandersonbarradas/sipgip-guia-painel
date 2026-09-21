# Publicar o guia no GitHub Pages

Esta pasta é o site. Só entram aqui o HTML do guia e as imagens — nada de planos internos, NT de trabalho ou certificados.

O GitHub Pages gratuito publica um **site público**. Mesmo com repositório privado, no plano gratuito o Pages não sobe; e, nos planos em que sobe a partir de repositório privado, o endereço do site continua aberto na internet. Se a homologação (Enel, usuários de teste) não puder ficar pública, não habilite o Pages: mantenha o repositório privado e abra o `index.html` no navegador.

## 1. Criar o repositório e enviar

No computador, nesta pasta (`docs/site`):

```bash
cd "/home/wanderson-barradas/Área de trabalho/cosip/docs/site"

git init
git add index.html imagens .nojekyll README.md .gitignore
git commit -m "docs: publica o guia do painel da concessionária"
git branch -M main
```

Crie o repositório no GitHub e envie. Troque o nome se quiser.

**Público** (necessário para o Pages no plano gratuito):

```bash
gh repo create sipgip-guia-painel --public --source=. --remote=origin --push
```

**Privado** (só o código; Pages em geral não fica disponível no plano gratuito):

```bash
gh repo create sipgip-guia-painel --private --source=. --remote=origin --push
```

Sem `gh`, crie o repositório vazio em https://github.com/new e depois:

```bash
git remote add origin https://github.com/SEU_USUARIO/sipgip-guia-painel.git
git push -u origin main
```

## 2. Ligar o GitHub Pages

1. Abra o repositório no GitHub.
2. **Settings** → **Pages** (menu esquerdo, grupo *Code and automation*).
3. Em **Build and deployment** → **Source**, escolha **Deploy from a branch**.
4. **Branch:** `main`. **Folder:** `/ (root)`.
5. **Save**.

Em 1–2 minutos o GitHub mostra o endereço, no formato:

```text
https://SEU_USUARIO.github.io/sipgip-guia-painel/
```

O arquivo `.nojekyll` evita que o GitHub trate o site como Jekyll e quebre as pastas de imagens.

## 3. Colaboradores

- **Ver o site:** o endereço do Pages (público).
- **Editar o conteúdo:** **Settings** → **Collaborators** → convite. Quem tiver permissão clona, altera e dá push em `main`; o Pages atualiza sozinho.

## 4. Atualizar depois de mudar o guia

Edite `docs/site/index.html` e, se houver tela nova, recapture as imagens:

```bash
cd "/home/wanderson-barradas/Área de trabalho/cosip"
node docs/scripts/capturar-painel-concessionaria.mjs --certificate=/tmp/cosip-docs-login.p12
```

O script grava em `docs/site/imagens/painel-concessionaria/`. Depois, nesta pasta:

```bash
cd docs/site
git add index.html imagens
git commit -m "docs: atualiza o módulo do painel"
git push
```

Espere cerca de um minuto e recarregue o site (se a imagem antiga continuar, use atualização forçada no navegador).

## 5. O que não enviar

- certificados (`.p12`, `.pem`, `.key`)
- senhas e `.env`
- o restante de `docs/` (planos, NT de trabalho, relatórios)
- os repositórios Laravel e microserviço
