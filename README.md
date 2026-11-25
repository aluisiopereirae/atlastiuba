# Atlas da Tiúba

Atlas interativo da anatomia da **tiúba** (*Melipona fasciculata* Smith, 1854), a abelha-sem-ferrão do Maranhão. Mostra a abelha por fora e por dentro, com as diferenças entre operária, rainha e macho.

Página didática da **Embrapa Maranhão**, feita na identidade visual da Embrapa.

## O que a página faz

- **Vista externa:** cabeça, mesossoma e metassoma, asas, pernas, corbícula, espiráculos e peças bucais.
- **Vista interna:** sete sistemas que podem ser ligados e desligados um a um: digestório, nervoso, circulatório, respiratório, glândulas, reprodutor e muscular.
- **Castas:** troca entre operária, rainha e macho. A ilustração muda junto:
  - a rainha tem o abdome dilatado (fisogástrica) e ovários desenvolvidos com espermateca;
  - o macho tem antena mais longa e genitália, e não tem ferrão nem glândulas de cera;
  - só a operária tem corbícula funcional.
- **Ficha de cada estrutura:** ao tocar numa parte aparecem o nome, o termo científico em latim, a função e, quando existe, uma nota específica sobre a tiúba.
- **Rótulos:** podem ser ligados e desligados para deixar a ilustração mais limpa.
- **Acesso direto à vista interna:** abra a página com `#interna` no fim do endereço.

## Como usar

A página é um único arquivo HTML. Não precisa de build nem de dependências.

```bash
git clone <url-do-repositorio>
cd atlas-da-tiuba
# abra index.html no navegador, ou sirva localmente:
python3 -m http.server 8000
# e acesse http://localhost:8000
```

### Publicar no GitHub Pages

1. Envie o `index.html` para a branch `main`.
2. No repositório, vá em **Settings → Pages**.
3. Em **Source**, escolha `Deploy from a branch`, depois a branch `main` e a pasta `/ (root)`.
4. A página fica disponível em `https://<usuario>.github.io/<repositorio>/`.

## Estrutura

```
.
├── index.html   # página completa: HTML, CSS, SVG e JavaScript
└── README.md
```

Dentro do `index.html`:

| Parte | O que contém |
|---|---|
| `<style>` | Tokens de cor e tipografia da Embrapa, layout e estilos da ilustração |
| `<svg id="bee">` | Ilustração em vista lateral. O grupo `.ext` tem a anatomia externa e o grupo `.int` tem os sistemas internos, um `.layer` por sistema |
| `<script>` | Objeto `P` com o conteúdo de cada estrutura, mais a lógica de vistas, castas, rótulos e seleção |

### Adicionar ou editar uma estrutura

Cada parte clicável do SVG tem um `data-id`. O conteúdo dela fica no objeto `P` do script:

```js
// id: [sistema, nome, termo científico, descrição, nota sobre a tiúba, [x, y, rótuloX, rótuloY]]
papo: ["dig", "Papo (estômago de mel)", "Ingluvies",
       "Bolsa elástica que guarda o néctar coletado...",
       "O mel de tiúba é mais líquido e ácido...",
       [536, 226, 520, 130]],
```

- `sistema` é uma destas chaves: `ext`, `dig`, `nerv`, `circ`, `resp`, `gland`, `repro` ou `musc`.
- As coordenadas são do `viewBox` do SVG (900 × 540). `x,y` é o ponto da estrutura e `rótuloX,rótuloY` é onde fica o texto do rótulo.
- Para que uma parte apareça só numa casta, use as classes `worker-only`, `queen-only`, `male-only`, `female-only` ou `no-worker`.
- Para que uma parte do abdome cresça junto com o abdome da rainha, use a classe `abd-scale`.

## Identidade visual

A página segue o Manual de Identidade Visual da Embrapa:

| Token | Valor | Referência |
|---|---|---|
| `--emb-azul` | `#003087` | Azul padrão Embrapa, Pantone 287 |
| `--emb-verde` | `#00783E` | Verde padrão Embrapa, Pantone 356 |
| Tipografia | Univers → Lato → Arial | Univers é a família institucional. Lato (Google Fonts) e Arial são as alternativas na web |

As cores dos sistemas internos (digestório em laranja, nervoso em amarelo e assim por diante) e as cores do corpo da abelha têm função informativa. Por isso ficam fora da paleta institucional.

A página tem tema claro e escuro, de acordo com a preferência do sistema.

> O logotipo oficial da Embrapa não está incluído. Na faixa institucional, "Embrapa" está escrito em texto. Para usar a marca oficial, peça os arquivos aos Guardiões da Marca da unidade e substitua o elemento `.brandbar .org`.

## Observações científicas

A ilustração é **esquemática** e serve para fins didáticos. As proporções e as posições dos órgãos internos foram simplificadas a partir da anatomia geral de abelhas Apidae, e não de dissecção da espécie.

## Créditos

Embrapa Maranhão · São Luís, MA
Empresa Brasileira de Pesquisa Agropecuária, Ministério da Agricultura e Pecuária

## Licença

Defina a licença conforme a política de software e conteúdo da Embrapa antes de tornar o repositório público.
