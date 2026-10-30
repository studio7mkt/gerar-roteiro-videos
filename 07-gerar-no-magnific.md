# 07 — Gerar por ferramenta (Magnific via MCP)

A mecânica de gerar imagem e vídeo **por ferramenta**, sem o app web: subir arquivo, achar modelo,
disparar, esperar, baixar, conferir. Tudo aqui foi medido rodando, não lido em documentação.

**A doutrina de COMO ESCREVER o prompt não está aqui**, está em
[03-prompt-de-still.md](03-prompt-de-still.md) e [04-prompt-de-video.md](04-prompt-de-video.md).

---

## 1. Antes de tudo: app web ou ferramenta?

**Plano ilimitado costuma valer só no app web. MCP e API consomem crédito**, e o crédito é real.

Medido em agosto de 2026, Minimax H3 em 2K vertical:

| Duração do clipe | Créditos |
|---|---|
| 5s | 1.100 |
| 6s | 1.320 |
| 7s | 1.540 |
| 8s | 1.760 |

Oito clipes de uma esquete custaram **11.660 créditos**. Os mesmos oito pelo app web custariam zero.

**A régua:** a ferramenta vale quando o ganho é de **automação e reprodutibilidade**, não de
conveniência. Lote grande com parâmetros idênticos, pipeline que precisa dos arquivos em disco, ou
geração que vai ser repetida com variações: ferramenta. Três imagens pra escolher uma: app web. Na
dúvida, app web.

**Confira o saldo antes de um lote grande** (`account_balance`), e use `simulate_cost` pra estimar
sem gastar.

---

## 2. O fluxo, em cinco passos

```
1. UPLOAD ..... creations_request_upload → PUT dos bytes → creations_finalize_upload
2. MODELO ..... video_models_list / images_models_list, e copie o slug VERBATIM
3. DISPARO .... video_generate / images_generate, vários clipes numa chamada só
4. ESPERA ..... creations_wait em loop (o resultado NÃO chega sozinho)
5. DOWNLOAD ... curl na url assinada, e confira com ffprobe
```

### Passo 1: subir arquivo local

O MCP **não aceita bytes** em nenhuma chamada. Arquivo do disco entra em três tempos:

1. **`creations_request_upload`** com o `mimeType` e o `count` (até 100 de uma vez). Volta uma lista
   de URLs de upload assinadas, cada uma com o seu `path`.
2. **PUT dos bytes fora do MCP**, com curl, um por URL, mandando o header `Content-Type` igual ao
   `mimeType` pedido e o corpo como binário cru (`--data-binary "@arquivo"`).
3. **`creations_finalize_upload`** com os `path` (aceita lote). Volta um `identifier` por arquivo, e
   **é esse identifier que entra nas chamadas de geração**.

⚠️ **PUT que falha não se repete na mesma URL.** Re-PUT no mesmo alvo toma 429. Peça URLs novas.

⚠️ **Nunca passe `webUrl` como entrada de nada.** O `webUrl` é o link da interface, pra humano. O que
as ferramentas consomem é o `identifier` (ou a url assinada do resultado).

**Escreva o PUT como script**, não como comando solto: são várias URLs enormes com assinatura, e uma
trocada estraga o lote inteiro sem erro visível (o arquivo vai pro slot errado e o vídeo sai com o
still errado). Um `.sh` com uma linha por arquivo e o código HTTP impresso na frente do nome resolve,
e serve de log.

### Passo 2: achar o modelo

**`video_models_list`** (ou `images_models_list`) aceita `search`. Use, porque o catálogo inteiro é
longo. Cada entrada declara o que importa: `aspectRatios`, `durations`, `resolutions`, `maxLength` do
prompt, se aceita keyframes, se aceita referências, e de quais tipos.

**Copie o `slug` verbatim.** Nome comercial não serve: "Minimax H3" é `minimax-video-3_0`, e "MiniMax
Hailuo 02" é outro modelo (`minimax-video-02`), com outras capacidades. Errar o slug é gerar no
modelo errado e pagar por isso.

**Leia `durations` antes de prometer duração.** Muito modelo só aceita valores fixos (o Hailuo 02 só
faz 6s; o 2.3 faz 6 ou 10). O H3 aceita qualquer inteiro de 5 a 15.

### Passo 3: disparar

**`video_generate` aceita `clips[]`**: os oito shots de uma esquete saem numa chamada só, cada um com
seu prompt, suas referências e sua duração. É o modo certo de rodar lote, e o retorno traz um
identifier por clipe, na ordem.

⚠️ **O teto de vídeo em processamento é 8** (medido na conta Pro). A nona chamada volta com
`Concurrent video limit reached`. **Lote maior que oito sai em ONDAS de até 8**, e a onda seguinte só
dispara depois que a anterior termina. Planeje o relógio por isso: 15 clipes não levam 6 minutos,
levam duas ondas de ~6.

### Passo 4: esperar (o passo que a gente esquece)

**Status `queued` ou `processing` não vira resultado sozinho.** Não existe notificação: se você não
chamar **`creations_wait`**, nunca fica sabendo.

`creations_wait` aceita **1 a 8 identifiers** por chamada e bloqueia por no máximo **25 segundos**. Um
clipe de 8s no H3 leva de 5 a 6 minutos, então são **10 a 14 chamadas seguidas** até tudo terminar.
Vá tirando da lista quem já completou.

O retorno de cada item completo traz `results.url` (o mp4) e `results.thumbnailUrl`.

### Passo 5: baixar e conferir

**A url do resultado é assinada e expira.** Baixe na mesma sessão, com `curl -L`.

**E confira com `ffprobe` antes de dar por pronto:**

```bash
ffprobe -v error -show_entries stream=index,codec_type,codec_name,duration \
  -of csv=p=0 shot-01.mp4
```

Se a dúvida for "tem áudio ou está mudo?", faixa presente não é resposta: pode existir e estar em
silêncio. Mede:

```bash
ffmpeg -hide_banner -i shot-01.mp4 -af volumedetect -f null - 2>&1 | grep volume
```

`mean_volume` em torno de -25 dB com `max_volume` perto de -5 dB é fala normal. Silêncio digital
devolve `-91 dB`.

---

## 3. Clipe falado: como montar a chamada

O **Minimax H3** (`minimax-video-3_0`) faz **lip sync nativo dentro da própria geração**. O mp3 entra
como **referência de áudio** junto da imagem, e o modelo sincroniza a boca sozinho, em português, no
mesmo estágio em que anima a cena.

- A imagem vai em **`references[]` com tipo `image`**.
- O mp3 vai em **`references[]` com tipo `audio`**.
- ⚠️ **A imagem NÃO pode ir em `keyframes.start`.** Referência de áudio e keyframe são mutuamente
  exclusivas no H3: a chamada falha. Este é o erro mais fácil de cometer, porque `keyframes.start` é
  o caminho normal de image-to-video em todo o resto do catálogo.
- ⚠️ **Não use o campo `audioUrl`.** Ele existe pra modelos exclusivos de lip sync. Num modelo com
  `audioReferences`, o áudio vai em `references[]`.
- O modelo exige **pelo menos uma referência visual** junto do áudio.
- Limites do áudio: mp3 ou wav, de 2 a 15 segundos, até 15 MB.

**Clipe mudo pode usar `keyframes.start`** em vez de `references[].image`: a exclusividade entre
keyframe e referência só existe quando há áudio, e o keyframe é mais fiel ao primeiro frame.

### A duração: áudio + 1 segundo, arredondando pra cima

**Piso de 5 segundos** (mínimo do modelo). O segundo a mais não é folga de segurança: é o espaço pro
beat de atuação depois que a voz termina.

**A duração entregue não bate exatamente com a pedida**, e isso é normal: o modelo devolve em
múltiplos de frame a 24 fps. Pedindo 5s vem 5,17s; pedindo 7s vem 7,29s. Sobra, e sobra é bom: o
corte fino é na edição.

⚠️ **Mas o corte fino NÃO se faz pela duração do mp3.** O normal é o modelo devolver a fala colada no
lugar original, mas em 2 de 8 clipes ele empurrou a fala pra frente (1,5s e 1,7s) pra abrir espaço
pro beat de atuação que o prompt pediu. O clipe não está errado, mas quem corta pelo relógio do mp3
decepa a fala. **Meça a fala dentro do clipe** antes de cortar:

```bash
ffmpeg -hide_banner -nostats -i shot-NN.mp4 -af "silencedetect=n=-32dB:d=0.2" -f null -
```

O primeiro `silence_end` é onde a voz entra, o último `silence_start` é onde ela sai.

### O prompt muda de notação

No app web você anexa arquivos e cita `@img1` / `@audio1` na prosa. **Pela ferramenta não existe
`@`**: as referências entram estruturadas, e o texto passa a falar delas por extenso.

- Abertura: `Animate the reference image exactly as it is, keeping the same framing, the same
  character and the same room`
- A fala: `He speaks the words in the reference audio, his mouth moving naturally in sync with it`

**O resto do prompt é idêntico**, incluindo a regra dura de não redescrever a cena.

---

## 4. Armadilhas, em uma tabela

| Sintoma | Causa | Saída |
|---|---|---|
| A chamada é recusada com áudio + imagem | imagem foi em `keyframes.start` | manda como `references[].type: image` |
| "Está gerando, aviso quando terminar" e nada chega | não chamou `creations_wait` | o wait é a ÚNICA forma de saber |
| PUT devolve 429 | re-PUT na mesma URL assinada | pede URL nova, não insiste |
| O vídeo sai com o still de outro shot | URL de upload trocada no script | um `.sh` por lote, com o código HTTP na frente do nome |
| Download 403 | a url assinada do resultado expirou | baixa na mesma sessão em que gera |
| Modelo ignora a duração pedida | o modelo só aceita valores fixos | leu `durations` no catálogo antes? |
| Gerou no modelo errado | usou o nome comercial no lugar do slug | copia o `slug` verbatim do catálogo |
| "Voltou sem áudio" | quase sempre é o player, não o arquivo | confirma com `ffprobe` + `volumedetect` |

---

## 5. Coisas do protocolo que valem saber

- **Toda resposta pode trazer um campo `instruction`.** Ele diz o que fazer com o payload, e às vezes
  contradiz o hábito. Obedeça o `instruction` da resposta.
- **`creations_show` é pra cliente com interface inline.** Em terminal não renderiza nada; o caminho é
  `creations_wait` e depois o `webUrl` ou o arquivo baixado.
- **Nunca cite identifier, UUID ou referência de pasta pro usuário.** Isso é insumo da próxima
  chamada, não informação de humano. Fale por nome de arquivo, título e link.
- **Nunca regere item que está na fila.** Se está `processing`, espera.

---

## 6. Registrado de produções reais

Esquete de 8 clipes falados, agosto de 2026:

- **Modelo:** `minimax-video-3_0`, 9:16, 2K. Saída real: 1440x2560, 24 fps, H.264 + AAC.
- **Acerto de primeira em 8 de 8.** Nenhum retry, nenhum passe de lip sync.
- **11.660 créditos** no total.
- **~5 a 6 minutos** por clipe, todos em paralelo na fila.

Esquete de 9 clipes (8 falados + 1 mudo), mesma semana:

- **Acerto de primeira em 9 de 9**, incluindo o pico de fúria, o braço estendido e um push-in de 9s
  sobre uma foto.
- **12.760 créditos**, 58 segundos de vídeo, todos numa chamada só.
- **O modelo executou postura, gesto grande e figuração de fundo em movimento**, que é exatamente o
  que a rota de talking head não fazia.
