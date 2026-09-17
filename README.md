# Página de links — Paula Ferreira Confeitaria

Página "link na bio" em **um único arquivo HTML**, irmã do media kit e com a mesma
identidade visual (vinho + creme + dourado, Playfair Display + Inter).

## Como abrir

Dê dois cliques em `index.html` — abre direto no navegador, sem servidor e sem
instalar nada. Para ver como fica no celular: `F12` → ícone de celular (Ctrl+Shift+M)
→ escolha uma largura de ~380px.

## Arquivos da pasta

| Arquivo | O que é |
|---|---|
| `index.html` | A página inteira (HTML + CSS + JS) |
| `assets/paula.png` | Foto da criadora, PNG com fundo transparente, 1066×1358 |
| `assets/card-delivery.jpeg` | Imagem 1:1 do card de delivery |
| `assets/card-embalagens.jpeg` | Imagem 1:1 do card de embalagens |
| `assets/card-ebook.jpeg` | Imagem 1:1 do card do e-book |
| `assets/card-panfletos.png` | Imagem 1:1 do card de panfletos |
| `assets/icone.png` | Ícone da aba — navegador no modo **claro** |
| `assets/icone-white.png` | Ícone da aba — navegador no modo **escuro** |

Se alguma imagem faltar, **a página não quebra**: a foto some e aparece um bloco
discreto no lugar, e o card mostra um quadradinho creme com um círculo fininho.

## Ordem dos blocos

No código, o cabeçalho (`<header class="hero-head">`) vem **antes** da foto e dos
cards — é um bloco independente, para poder ficar centralizado na tela inteira no
computador. No celular, o CSS inverte a ordem visual para **avatar → nome → cards**
(regras `order` dentro do bloco `@media (max-width:767px)`). Se um dia você mudar a
ordem no HTML, confira as duas telas: o que manda no celular são essas regras `order`.

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
- **ÍCONE DA PÁGINA**, **ÍCONES CLARO/ESCURO** e **OPEN GRAPH**

### Ícone da aba (claro e escuro)

São dois arquivos: `assets/icone.png` aparece quando o navegador está no modo claro e
`assets/icone-white.png` quando está no modo escuro. A troca acontece sozinha, e muda
na hora se a pessoa virar o modo com a página aberta. Para trocar os arquivos, mantenha
os mesmos nomes — ou, se usar outros nomes, atualize os dois `<link rel="icon">` no
topo do arquivo **e** o trecho marcado `EDITÁVEL · ÍCONES CLARO/ESCURO`, lá no fim.

### Trocar um link

Procure `EDITÁVEL · LINK 2` e troque só o que está entre aspas depois de `href=`:

```html
<a class="card reveal" href="https://COLE-O-NOVO-ENDERECO-AQUI" target="_blank" rel="noopener">
```

Não mexa em `target="_blank" rel="noopener"` — é o que faz o link abrir em uma aba
nova sem devolver acesso à sua página.

### Trocar uma imagem de card

Salve a nova imagem **quadrada (1:1)** na pasta `assets` com o mesmo nome do arquivo
antigo (ex.: `card-ebook.jpeg`) e pronto. Se quiser usar outro nome, troque também o
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

A página usa duas medidas tiradas do canal alfa da foto atual: **o corpo começa em
21,8% e termina em 77,3% da largura da imagem** — ou seja, sobra faixa transparente
dos dois lados e o corpo ocupa 55,5% do arquivo. É disso que saem os três valores:

```css
--photo-col:calc(var(--photo-w) * 0.555);  /* a coluna reserva só o corpo visível */
--head-w:calc(var(--photo-w) * 0.74);      /* largura do texto do cabeçalho */
/* e, na regra .hero-photo: left:calc(var(--photo-x) - var(--photo-w) * .218) */
```

Juntos, eles fazem o corpo encostar na borda da coluna (em vez de ficar recuado), o
texto do cabeçalho ficar centralizado exatamente em cima do corpo, e os cards
chegarem perto da silhueta sem cobrir ninguém.

**Se a nova foto tiver outro enquadramento, os três precisam ser recalculados.** Para
medir sem instalar nada: abra a página, `F12` → Console, e cole:

```js
const i=new Image();i.src='assets/paula.png';await i.decode();
const c=document.createElement('canvas');c.width=i.naturalWidth;c.height=i.naturalHeight;
const x=c.getContext('2d');x.drawImage(i,0,0);
const d=x.getImageData(0,0,c.width,c.height).data;let a=c.width,b=0;
for(let y=0;y<c.height;y+=2)for(let p=0;p<c.width;p+=2)if(d[(y*c.width+p)*4+3]>16){if(p<a)a=p;if(p>b)b=p}
console.log('esquerda',(a/c.width*100).toFixed(1)+'%','direita',(b/c.width*100).toFixed(1)+'%')
```

O primeiro número entra no `.218` (deslocamento), e a diferença entre os dois vira o
`0.555` da coluna. Reajuste também as variáveis `--avatar-*` do celular.

O tamanho da foto no computador é controlado por `--photo-w` (300px no celular, 340px
a partir de 768px e 500px a partir de 1200px). Em telas de altura pequena, 500px faz a
página rolar um pouco — baixe para 420px ou 450px se preferir que tudo caiba sem rolar.

## Largura dos cards no computador (`--links-w`)

No computador, o cabeçalho (nome, @ e frase) é uma **faixa própria, centralizada na
largura inteira da tela**, e abaixo dele a foto e os cards formam um bloco só, também
centralizado, com a mesma margem dos dois lados. A largura
máxima da coluna de cards é `--links-w`: 440px a partir de 768px e 460px a partir de
1200px. Aumente para cards mais largos, diminua para cards mais estreitos —
a foto não muda de tamanho junto, os dois valores são independentes. Em telas menores
a coluna encolhe sozinha para caber, sem nunca passar desse máximo.

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
