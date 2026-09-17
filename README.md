# Tinder de Estilo — Quiz Decorafit

Versão em formato "Tinder" do quiz de estilo de decoração: em vez de perguntas de múltipla escolha, a pessoa arrasta fotos de ambientes, móveis e objetos de decoração para a direita (gostei) ou esquerda (não é o meu estilo). No final, revelamos o "match": o estilo de decoração com mais curtidas.

Reaproveita a identidade visual e o fluxo de captura de lead do [`bussola-de-estilo`](../bussola-de-estilo), a versão original em quiz de perguntas. As fotos são exclusivas (geradas com IA especificamente para este quiz, contexto de apartamento em São Paulo — não loft/casa).

Estilos cobertos (6, um subconjunto dos 9 do quiz original): Industrial, Contemporâneo, Clássico Contemporâneo, Boho Chic, Japandi e Escandinavo.

## Estrutura

- `index.html` — página única (HTML + CSS + JS), sem dependências além das fontes do Google Fonts.
- `img/` — fotos exclusivas do quiz: 3 por estilo (`<estilo>-ambiente.jpg`, `<estilo>-movel.jpg`, `<estilo>-objeto.jpg`), geradas via Gemini e comprimidas para ~120–170KB cada.

## Como funciona o match

- O deck tem 18 cards (6 estilos × 3 fotos: ambiente, móvel, objeto), embaralhados a cada sessão.
- Arrastar para a direita (ou botão ♥) = curtiu aquele card → +1 ponto pro estilo dele.
- Arrastar para a esquerda (ou botão ✕) = não curtiu → 0 pontos, sem penalidade.
- "← Voltar" desfaz o último swipe (disponível a partir do 2º card, e também na tela de lead para corrigir o último antes de ver o resultado).
- No final, o estilo com mais curtidas vira o "match". Em caso de empate, prevalece a ordem em `STYLE_ORDER` (mesmo critério do quiz original). A foto de "ambiente" do estilo vencedor é usada como imagem principal do resultado.

## Lead e comunicação

Usa o mesmo endpoint (Google Apps Script) do `bussola-de-estilo` para registrar nome, e-mail, WhatsApp e estilo. Foi adicionado um campo `quiz: "tinder-de-estilo"` no payload para diferenciar a origem — **confirme que o Apps Script/planilha não ignora ou quebra com esse campo extra** antes de considerar o tracking confiável.

O texto da tela de lead segue a mesma lógica corrigida do quiz original: deixa claro que o resultado aparece na hora, e que os dados servem para receber mais conteúdo depois (não para "enviar" o resultado).

## Rodar localmente

```
python -m http.server 8000
```

## Publicar no GitHub Pages

1. Crie um repositório no GitHub e suba esta pasta (`git init`, `git remote add origin ...`, `git push`).
2. Em **Settings → Pages**, selecione a branch `main` e a pasta raiz (`/`).
3. O quiz fica disponível em `https://<seu-usuario>.github.io/<repo>/`.
