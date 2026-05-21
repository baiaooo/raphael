# Portfolio · Raphael Bravo

Site portfolio single-page de desenvolvedor full-stack. HTML/CSS/JS puro, sem build, sem framework. Funciona 100% offline depois de carregado.

## Como subir

Site é estático e roda em qualquer host. Opções recomendadas:

### GitHub Pages (grátis, recomendado)
1. Cria um repo público chamado `zfcx00.github.io` na conta `zfcx00`
2. Sobe os arquivos na raiz do repo (mantendo as pastas `vendor/` e `logos/`)
3. Em **Settings → Pages**, escolhe a branch `main` e source root `/`
4. Acessa em `https://zfcx00.github.io`

### Vercel ou Netlify
Arrasta a pasta do projeto na interface deles. Subdomain grátis sai em 30s.

### Hostgator / cPanel / FTP
Sobe os arquivos via FTP pra `public_html/` mantendo a estrutura.

### Servidor local pra testar
```bash
cd raphael-site
python3 -m http.server 8000
# abre http://localhost:8000
```
**Importante:** abrir o `index.html` direto via `file://` não funciona por causa de CORS no fetch dos SVGs e WebAssembly. Sempre rodar via servidor HTTP, mesmo local.

## Estrutura

```
raphael-site/
├── index.html          # tudo: HTML + CSS + JS
├── raphael.jpg         # foto do hero
├── logo-lago.png       # logo do cliente (LAGO)
├── logos/              # ícones da stack (SVGs do simple-icons)
│   ├── react.svg
│   ├── supabase.svg
│   ├── postgresql.svg
│   └── ... (11 logos)
└── vendor/             # bibliotecas
    ├── three.module.min.js    # Three.js r160 (655 KB)
    └── rapier.mjs             # Rapier 3D com WASM embutido (2.2 MB)
```

Total: ~3 MB descompactado, ~1.1 MB compactado.

## Seções do site

1. **Hero** com background animado de partículas em onda (Three.js)
2. **Sobre** com foto circular grayscale + colored on hover, formação, certificações
3. **Stack** em 4 categorias (frontend mobile, frontend web, backend & dados, automação)
4. **Terminal interativo** abaixo da stack, escrivível (só pelo meme)
5. **Projetos** com card da LAGO
6. **Contrate-me** com background de cubos com física Rapier 3D

## Customização rápida

### Trocar dados pessoais

| O quê | Onde editar |
|---|---|
| Nome no nav e footer | procurar por `raphael.dev` e `raphael · 2026` |
| WhatsApp | procurar `wa.me/5567992682833` e `+55 67 9268-2833` |
| LinkedIn | procurar `linkedin.com/in/carlos-raphael-bravo-pires` |
| GitHub | procurar `github.com/zfcx00` |
| Localização | procurar `Campo Grande, MS` |
| Foto | substitui `raphael.jpg` mantendo o nome |

### Trocar cor accent (verde neon)

Editar a variável CSS no topo do `<style>`:
```css
--accent: #c8ff00;
--accent-dim: #8aa800;
```
Trocar nos dois lugares. Também atualizar `0xc8ff00` no JavaScript da animação Three.js (waves).

### Reduzir performance do background físico

Se travar em mobile antigo, achar no script do Rapier:
```js
const TOTAL = 40;   // baixar pra 20-25
```

E no waves do hero:
```js
const SEPARATION = 140, AMOUNTX = 35, AMOUNTY = 35;
// baixar pra AMOUNTX = 25, AMOUNTY = 25
```

### Trocar comandos do terminal

Procurar o bloco `const commands = {` dentro do script do terminal. Cada chave é um comando, cada valor uma função que retorna array de strings (ou `null` pra clear). Adicionar/remover à vontade.

## Stack do próprio site

- **HTML/CSS/JS puro**, sem build
- **Three.js r160** pra background de partículas em onda (hero) e cubos físicos (contrate-me)
- **Rapier 3D** (WebAssembly) pra simulação de física
- **Fontes:** JetBrains Mono + Space Grotesk via Google Fonts (única dependência externa restante)
- **Lazy loading:** o Rapier WASM só inicializa quando a seção contrate-me entra na viewport
- **Pause inteligente:** as animações Three.js param de renderizar quando saem da tela (economia de bateria)

## Riscos / pontos de atenção

### GitHub do Raphael está vazio
`github.com/zfcx00` não tem nenhum repositório público até a data deste README. O site linka pra lá em 3 lugares (nav, hero, terminal). Antes de divulgar o portfolio, é importante subir pelo menos 2-3 projetos públicos com README decente. Senão a primeira impressão técnica do visitante é de um portfolio vazio.

### WhatsApp pessoal exposto
O número `+55 67 9268-2833` está em URL pública (`wa.me/5567992682833`). Bots de spam podem coletar. Se começar a receber muito spam, vale trocar pelo formulário de contato ou e-mail.

### Posicionamento "full-stack" sendo júnior
O site se posiciona como dev full-stack experiente. Pelo histórico real, o Raphael é júnior em formação prática (1 mês de experiência formal em dev na LAGO). Se um cliente técnico for fundo na entrevista, ele precisa ser honesto sobre o nível atual e usar a confiança comercial do site como porta de entrada, não como promessa exagerada de senioridade.

### Performance em mobile antigo
O background do contrate-me usa WebAssembly + WebGL com 40 cubos físicos. Em Android pré-2018 pode ter drop de FPS. Se virar problema, baixar o `TOTAL` no JS (ver seção Customização).

### Dependência única externa: Google Fonts
Tudo o mais foi empacotado local. As fontes ainda vêm do CDN do Google. Se quiser 100% offline, baixar as fontes e hospedar local também. Recomendado se for usar em apresentação sem internet.

### `file://` não funciona
Abrir o `index.html` direto via duplo-clique no Windows/Mac vai falhar silenciosamente nos SVGs e na física. Sempre servir via HTTP, mesmo localmente.

## Contato (do Raphael)

- WhatsApp: [+55 67 9268-2833](https://wa.me/5567992682833)
- GitHub: [@zfcx00](https://github.com/zfcx00)
- LinkedIn: [/in/carlos-raphael-bravo-pires](https://www.linkedin.com/in/carlos-raphael-bravo-pires-8a70743a5/)

---

Construído iterativamente em 2026. Site sem framework, sem build, sem dependências de CDN (exceto Google Fonts). Foco em simplicidade de deploy e zero lock-in.
