# Página de links — Paula Ferreira Confeitaria

Página "link na bio" em **um único arquivo HTML**, irmã do media kit e com a mesma
identidade visual (vinho + creme + dourado, Playfair Display + Inter).

## Como abrir

Dê dois cliques em `index.html` — abre direto no navegador, sem servidor e sem
instalar nada. Para ver como fica no celular: `F12` → ícone de celular (Ctrl+Shift+M)
→ escolha uma largura de ~380px.

## Arquivos da pasta

| Arquivo | O que é | Obrigatório |
|---|---|---|
| `index.html` | A página inteira (HTML + CSS + JS) | sim |
| `paula.png` | Foto da criadora, PNG com fundo transparente, 1066×1600 | recomendado |
| `card-delivery.jpg` | Imagem 1:1 do card de delivery | recomendado |
| `card-embalagens.jpg` | Imagem 1:1 do card de embalagens | recomendado |
| `card-ebook.jpg` | Imagem 1:1 do card do e-book | recomendado |
| `card-panfletos.jpg` | Imagem 1:1 do card de panfletos | recomendado |
| `icone.png` | Ícone da aba do navegador (favicon), quadrado | recomendado |

Se alguma imagem faltar, **a página não quebra**: a foto some e aparece um bloco
discreto no lugar, e o card mostra um quadradinho creme com um círculo fininho.

## Como editar

Abra o `index.html` em qualquer editor de texto (Bloco de Notas serve) e procure por
**`EDITÁVEL`** — todo ponto que você pode mexer está marcado com um comentário
`<!-- EDITÁVEL · ... -->`. São eles:

- **FOTO** — o arquivo `paula.png`
- **NOME** — "Paula Ferreira Confeitaria"
- **@ E LINK DO INSTAGRAM** — o `@` que aparece na pílula e para onde ele leva
- **FRASE DE POSICIONAMENTO** — a frase em serifada; o que está entre `<em>` e `</em>`
  aparece em dourado
- **LINK 1 a 4** — o endereço (`href`) de cada card
- **TÍTULO DO CARD 1 a 4**
- **DESCRIÇÃO DO CARD 1 a 4**
- **IMAGEM DO CARD 1 a 4**
- **ÍCONE DA PÁGINA** e **OPEN GRAPH**

### Trocar um link

Procure `EDITÁVEL · LINK 2` e troque só o que está entre aspas depois de `href=`:

```html
<a class="card reveal" href="https://COLE-O-NOVO-ENDERECO-AQUI" target="_blank" rel="noopener">
```

Não mexa em `target="_blank" rel="noopener"` — é o que faz o link abrir em uma aba
nova sem devolver acesso à sua página.

### Trocar uma imagem de card

Salve a nova imagem **quadrada (1:1)** na mesma pasta com o mesmo nome do arquivo
antigo (ex.: `card-ebook.jpg`) e pronto. Se quiser usar outro nome, troque também o
`src="..."` do card correspondente.

### Trocar um texto

Título e descrição são texto puro dentro das tags — troque o que está escrito e
mantenha as tags:

```html
<h2 class="card-title">Meu delivery&nbsp;🧁</h2>
<span class="card-desc">Doces e salgados, com pedido direto pelo WhatsApp.</span>
```

O `&nbsp;` antes do emoji é de propósito: segura o emoji junto da última palavra para
ele não cair sozinho na linha de baixo. Descrições muito longas são cortadas com "..."
no celular (limite de 3 linhas) — mantenha cada uma em **uma frase curta**.

### Antes de publicar: Open Graph

Procure `EDITÁVEL · OPEN GRAPH` e troque `TROCAR-PELA-URL-FINAL` pelo endereço real
da página, nos dois lugares. É isso que faz o link aparecer bonito quando alguém
manda no WhatsApp ou no Instagram.

## Ajustar o enquadramento do avatar (celular)

No celular a foto de corpo inteiro vira um **círculo**. O círculo é uma janela sobre a
foto — você move e aproxima a foto por trás dela com quatro variáveis:

| Variável | O que faz | Padrão |
|---|---|---|
| `--avatar-size` | tamanho do círculo | `172px` |
| `--avatar-zoom` | o quanto a foto é ampliada (maior = mais perto do rosto) | `111%` |
| `--avatar-x` | move a foto para os lados (negativo = para a esquerda) | `-3%` |
| `--avatar-y` | move a foto para cima/baixo (positivo = para baixo) | `4%` |

**Jeito rápido de achar o valor certo, sem ficar salvando arquivo:** abra a página no
Chrome, aperte `F12`, vá na aba **Console**, cole e aperte Enter:

```js
document.documentElement.style.setProperty('--avatar-zoom','130%')
```

A mudança acontece na hora, ao vivo. Teste também:

```js
document.documentElement.style.setProperty('--avatar-y','-2%')
```

Vá testando até o rosto ficar centralizado. Quando gostar, abra o `index.html` e
escreva os valores que você achou no bloco `:root`, em
`/* --- enquadramento do avatar redondo do mobile --- */`. **O console não salva
nada** — se você recarregar a página sem editar o arquivo, volta tudo ao que era.

## Se trocar a foto `paula.png`

A página usa uma medida específica da foto atual: **a silhueta ocupa 77,3% da largura
da imagem** e o resto da direita é transparente. Por isso a coluna reservada para a
foto no computador é menor que a foto:

```css
--photo-col:calc(var(--photo-w) * 0.74);
```

É isso que faz os cards chegarem perto da silhueta sem cobrir o corpo. **Se a nova
foto tiver outro enquadramento, esse `0.74` precisa ser recalculado** (mais ou menos:
porcentagem da largura ocupada pela silhueta, menos uns 3 pontos de folga). Reajuste
também as variáveis `--avatar-*`.

O tamanho da foto no computador é controlado por `--photo-w` (300px no celular, 340px
a partir de 768px e 500px a partir de 1200px). Em telas de altura pequena, 500px faz a
página rolar um pouco — baixe para 420px ou 450px se preferir que tudo caiba sem rolar.

## Como publicar

A página é estática, então qualquer uma destas opções funciona — e todas são gratuitas.

**Netlify Drop (mais rápido, sem conta no começo)**
1. Acesse <https://app.netlify.com/drop>
2. Arraste a **pasta inteira** (com `index.html` e as imagens) para a área indicada
3. Em segundos você recebe um endereço tipo `nome-aleatorio.netlify.app`
4. Crie uma conta gratuita para manter o site no ar e poder trocar o nome do endereço

**GitHub Pages**
1. Crie um repositório novo e suba todos os arquivos da pasta
2. No repositório: **Settings → Pages**
3. Em "Source", escolha a branch `main` e a pasta `/ (root)` → **Save**
4. O endereço fica `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO`

**Vercel**
1. Acesse <https://vercel.com/new> e conecte o repositório do GitHub
2. Não precisa configurar build — é HTML puro; é só clicar em **Deploy**

Depois de publicar, volte no `index.html`, troque `TROCAR-PELA-URL-FINAL` pelo
endereço real, e suba de novo.

## Detalhes técnicos

- Um arquivo só, sem bibliotecas. A única coisa externa é o Google Fonts.
- **Não usa `localStorage`** nem nenhum armazenamento do navegador.
- Responsivo em 380px, 768px e 1200px, sem rolagem horizontal.
- Os cards aparecem com uma animação suave conforme você rola (`IntersectionObserver`).
  Se o navegador não suportar, ou se o JavaScript estiver desligado, ou se a pessoa
  tiver pedido "menos animações" no sistema, tudo aparece de uma vez. Na impressão,
  tudo sai visível.
- Acessibilidade: um `<h1>` (o nome) e os títulos dos cards em `<h2>`; contorno dourado
  visível ao navegar por teclado; área de toque de no mínimo 56px nos cards.
- Os três dourados não são decoração: `--gold` só sobre o vinho, `--gold-deep` em
  textos grandes sobre creme e `--gold-ink` em textos pequenos sobre creme. Trocar um
  pelo outro quebra o contraste mínimo de leitura.
