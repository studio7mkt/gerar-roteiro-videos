# 02 — Storyboard, mapa de assets e o contrato do `PROMPTS.md`

O roteiro diz o que acontece. Este arquivo diz **quantos arquivos precisam existir** pra isso
acontecer, e em que ordem eles nascem.

---

## 1. A economia inteira mora aqui

O instinto errado é "um shot, um still". Numa cena de dez planos isso significa dez imagens, dez
conferências, dez rostos ligeiramente diferentes e uma deriva de identidade que só aparece na
montagem, quando refazer já custa caro.

**O certo é o still-base neutro:** uma imagem por personagem, reutilizada em todos os planos dele.
Na prática, dez shots costumam sair de cinco ou seis imagens.

Três ganhos, e o volume é o menor deles:

- **Consistência de graça.** Quatro clipes que saem do mesmo pixel têm o mesmo rosto, a mesma luz e
  o mesmo fundo, exatos. Deriva simplesmente deixa de existir neles.
- **A cena fica editável.** Fala nova, ordem trocada, um shot a mais: é só mais um vídeo do mesmo
  still, sem gerar imagem nenhuma.
- **Menos conferência.** Cinco imagens pra checar cenário, mão e identidade, em vez de doze.

### Quando um shot precisa de still próprio

**A pergunta é sempre a mesma: a diferença deste shot é MOVIMENTO ou é TEXTURA?**

| O vídeo faz (sai do still-base) | O vídeo não faz (exige still próprio) |
|---|---|
| postura: inclinar, encolher, largar na cadeira | rubor, suor, veia saltada |
| olhar, ombro, boca, gesto de mão | ruga travada, músculo contraído |
| figuração ao fundo se mexendo | ângulo de câmera diferente |
| a emoção sutil durante a fala | personagem de pé quando o still tem ele sentado |

**"Neutro" não é "inexpressivo".** O still-base carrega o tipo, o figurino e a postura de base do
personagem (o desengonçado meio torto, o gordo largado na poltrona). O que ele **não** carrega é o
estado emocional de um shot específico: nada de sorriso, careta, suor ou testa franzida, porque
isso ficaria congelado em todos os clipes que saírem dele.

### A escalada física precisa de degraus

Quando o personagem escala (irritado → furioso → explodindo), cada degrau é um still. E **não pule
degrau**: se o primeiro pico já sai com ele rugindo em cima da mesa, o segundo não tem pra onde ir
e a virada final vira repetição.

Dois picos colados na montagem, separados por um único plano curto, precisam ser **visivelmente
diferentes**: mude a altura da câmera, o figurino desarrumando, a distância. Senão o espectador lê
como o mesmo plano repetido.

---

## 2. O mapa de assets

Uma tabela por tipo de arquivo, no topo do `PROMPTS.md`. É ela que a pessoa usa como lista de
tarefas.

```markdown
## Os anexos

**Retratos de referência** (a identidade dos personagens, geradas uma vez e nunca mais):
- `referencias/<personagem-1>.jpg`
- `referencias/<personagem-2>.jpg`

**Stills** — a gerar. **<N>:**

| Arquivo | O que é | Serve os shots |
|---|---|---|
| `stills/<personagem>-base.jpg` | <personagem> no cenário, **neutro** | 1, 4, 6, 8 |
| `stills/<personagem>-pico.jpg` | o pico de fúria, testa travada | 5 |
| ... | | |

**Vozes** — a gravar ou sintetizar. A numeração bate com o shot.

| Arquivo | Shot | Quem | Palavras | Estimativa | Duração real |
|---|---|---|---|---|---|
| `vozes/1.mp3` | 1 | <personagem> | 17 | ~6s | |
| ... | | | | | |
```

**A coluna "duração real" é preenchida depois de gravar**, e é ela, não a estimativa, que define o
tamanho de cada clipe. Nenhum arquivo abaixo de 3s (o gerador tem piso) e nenhum acima de 10s (é o
teto do clipe).

---

## 3. As duas numerações que não se misturam

Nos geradores que trabalham com anexo (`@img1`, `@img2`, `@audio1`), a numeração é **da ordem em
que você anexa naquela geração**, não do documento inteiro. Então:

- **Ao gerar os stills:** `@img1` é o retrato do personagem 1, `@img2` o do personagem 2, fixos.
- **Ao gerar os vídeos:** a numeração **reseta a cada geração**. `@img1` é sempre "o still que
  estou anexando agora" e `@audio1` é sempre o mp3 deste shot.

Confundir as duas é o jeito mais fácil de gerar um clipe com o still do shot errado, e o erro não
aparece até a montagem.

**Rodando por ferramenta (API/MCP) não existe `@`:** as referências entram estruturadas e o texto
passa a falar delas por extenso ("the reference image", "the reference audio"). O resto do prompt
é idêntico. Ver [07-gerar-no-magnific.md](07-gerar-no-magnific.md).

---

## 4. Contrato do `PROMPTS.md`

```markdown
# <Nome da peça> — prompts prontos

Roteiro e direção em [ROTEIRO.md](ROTEIRO.md). Não duplique fala aqui: fala mora em um lugar só.

## Os anexos
<as tabelas da seção 2>

## Antes de começar

1. **Retrato nos stills, still nos vídeos.** Nunca redescreva rosto e corpo em nenhuma das duas etapas.
2. **Configuração fixa dos stills:** modelo <X>, proporção 9:16, resolução 2K.
3. **Um personagem por imagem** em todo shot com fala.
4. **Ângulo fixo por personagem**, e fundo fixo por personagem.
5. **Os shots com fala levam o mp3 anexado**, e o prompt nunca escreve a fala em português.
6. **O prompt de vídeo abre pela POSTURA**, porque o still é neutro.

**Os defaults teimosos deste cenário:** <liste os 2 ou 3 clichês que o dataset entrega sozinho
neste tipo de lugar, e como estão negados nos prompts>

---

## Etapa 1 — Os <N> stills

### `stills/<arquivo>.jpg` — <o que é>
**Anexa:** `@img1` (retrato de <personagem>) · **serve os shots <n>, <n>**

<uma ou duas linhas em português: o que conferir quando a imagem voltar>

```
<o prompt em inglês, um bloco só>
```

---

## Etapa 2 — Os <N> vídeos

### Shot <n> — <o que acontece>
**Anexa:** `stills/<arquivo>.jpg` + `vozes/<n>.mp3` · Duração: **<N>s**

```
<o prompt em inglês, um bloco só>
```
```

**A configuração que rodou fica registrada no arquivo** (modelo, proporção, resolução, duração de
cada clipe, custo). É o que permite refazer um shot meses depois sem redescobrir tudo.

---

## 5. A ordem de produção, e o que acontece se ela for invertida

```
1. Roteiro aprovado
2. Áudio de todas as falas          ← a duração real nasce aqui
3. Retratos de referência           ← uma vez por personagem, nunca mais
4. Stills                           ← conferir ANTES de gerar qualquer vídeo
5. Clipes                           ← still + mp3 na mesma chamada
6. Montagem
```

**O passo 4 tem um portão.** Confira cada still antes de partir pro vídeo: o rosto bate com o
retrato, a mão tem cinco dedos, o texto do letreiro está escrito e acentuado certo, a cara está
mesmo em repouso, a gag está legível. Um still errado que passa vira quatro clipes errados, porque
o still-base serve vários shots.

**Gere primeiro o shot mais exigente da cena** (aquele em que a postura e a expressão mudam durante
a fala). Ele decide a rota da produção inteira: se voltar bom, o resto vai.
