# 06 — Voz sintetizada e as tags de emoção

Como escrever **texto que vai virar áudio** num TTS moderno com direção de atuação inline, entre
colchetes: `[whispers]`, `[laughs]`, `[sarcastic]`. A referência aqui é o **ElevenLabs v3**
(`eleven_v3`), que é o padrão da categoria, mas a lógica vale pra qualquer modelo que aceite tag.

Vale pra toda fala que **não** sai da boca de um humano gravando: clone de voz em cena de ficção, o
objeto que responde, narração de b-roll, dublagem de personagem.

---

## 1. As duas faixas de fala nunca se misturam

| Faixa | Quem fala | Leva tag? |
|---|---|---|
| **humana** | a pessoa lendo o teleprompter, inclusive dublando personagem | ❌ nunca |
| **sintetizada** | clone, personagem, objeto que responde, narração sem rosto | ✅ sempre |

**Colchete em texto que um humano vai ler em voz alta é defeito**: quem grava lê "colchete whispers"
ou trava no meio da frase. Por isso a faixa de TTS é sempre uma **seção própria** do roteiro, e o
teleprompter continua 100% limpo.

**Pergunte de onde sai a voz antes de escrever o documento.** Personagem de esquete não é sinônimo de
TTS: muita gente dubla os dois papéis, e aí a faixa inteira é trabalho jogado fora e ainda polui o
roteiro com colchete que ninguém vai usar.

---

## 2. A hierarquia de controle (a tag é o terceiro degrau)

1. **A voz.** É o parâmetro mais importante. A voz precisa ser próxima o suficiente da entrega
   desejada: voz de gritar com `[whispers]` não obedece.
2. **Stability.** O botão que decide se as tags pegam.
3. **As tags.**
4. **A pontuação.**

**Tag não conserta voz errada, e não conserta stability errada.** Empilhar tag pra forçar uma entrega
que a voz não tem é o desperdício mais comum: troque a voz.

---

## 3. Stability

| Modo | O que faz | Quando usar |
|---|---|---|
| **Creative** | mais emocional e expressivo, propenso a alucinação | comédia, esquete, o take onde a atuação é a piada |
| **Natural** | mais perto da gravação original, equilibrado | **default**: narração, VO, fala de personagem que precisa parecer o clone |
| **Robust** | estabilíssimo, pouco responsivo a direção | quando precisa de N takes idênticos; aceite que as tags quase não vão pegar |

---

## 4. O catálogo de tags

### 4.1 As documentadas (use estas primeiro)

**Voz e emoção:** `[laughs]` `[laughs harder]` `[starts laughing]` `[wheezing]` `[whispers]`
`[sighs]` `[exhales]` `[sarcastic]` `[curious]` `[excited]` `[crying]` `[snorts]` `[mischievously]`

**Efeito sonoro:** `[gunshot]` `[applause]` `[clapping]` `[explosion]` `[swallows]` `[gulps]`

**Experimentais:** `[strong X accent]` `[sings]` `[woo]`

### 4.2 O vocabulário é aberto

Os exemplos do próprio guia oficial usam dezenas de tags fora do catálogo: `[frustrated sigh]`
`[happy gasp]` `[pauses]` `[dismissive]` `[giggles]` `[sympathetic]` `[reassuring]` `[deadpan]`
`[nervously]` `[alarmed]` `[sheepishly]` `[stifling laughter]` `[desperately]` `[panicking]`
`[warmly]` `[amazed]` `[impressed]` `[dramatically]` `[jumping in]` `[overlapping]` `[interrupting]`.

Ou seja: **a tag é descrição livre de entrega, em inglês.** Tag documentada é mais confiável; tag
inventada funciona na maioria das vezes e às vezes sai **lida em voz alta**. Invente quando precisar,
e escute o take.

### 4.3 Do beat da cena pra tag

O erro de quem escreve tag pela primeira vez é etiquetar o **sentimento do personagem** ("ele está
envergonhado") em vez da **entrega audível**. A tag descreve o que o microfone captaria.

| O beat da cena | Tag | Por quê |
|---|---|---|
| ele abre a besteira achando que é notícia boa | `[proudly]` | o orgulho é o que faz a queda funcionar |
| cada degrau novo do absurdo | `[casually]` | quanto mais banal ele conta, mais engraçado |
| o outro entendendo o tamanho do estrago | `[alarmed]` | a reação escala, não a fala |
| o degrau final, o detalhe gratuito | `[sheepishly]` ou `[whispers]` | baixar o volume no pior detalhe é o timing da piada |
| a explosão | `[shouting]` | só se a voz tiver grito no dataset |
| pausa antes da virada | `[pauses]` ou reticências | pausa é metade da comédia |
| ironia de quem narra | `[sarcastic]` `[deadpan]` | as duas mais confiáveis do catálogo |
| narração explicando o mecanismo | `[calm]` `[curious]` | narração não precisa de tag em toda frase |

**Não use tag pra emoção que a própria frase já entrega.** Se o texto diz "eu não acredito nisso",
`[surprised]` é redundante e engessa a leitura.

---

## 5. As 8 regras de escrita

1. **A tag vem colada no trecho que ela rege**, logo antes (`[annoyed] Isso tá difícil.`) ou logo
   depois, quando é reação (`Isso tá difícil. [sighs]`).
2. **Uma tag por beat.** Empilhar tags contraditórias na mesma frase produz saída imprevisível.
3. **Troca de emoção pede frase nova**, ou um `[pause]` entre os dois estados. Emoção não vira no
   meio de uma oração.
4. **A tag descreve o que se OUVE.** Nada de `[standing]`, `[grinning]`, `[pacing]`, `[music]`: isso
   é direção de cena e mora no prompt de vídeo.
5. **A tag não substitui palavra nenhuma.** Ela é acrescentada; nunca coloque um trecho do texto
   original dentro de colchete, e nunca reescreva a fala pra caber numa tag.
6. **Tag em inglês, texto em PT-BR.** O modelo fala português nativamente, mas o vocabulário de tag
   treinado é inglês. Tag em português é aposta, e é o cenário em que ela sai lida em voz alta.
7. **Gere blocos, não frases soltas.** Texto curto sai instável porque o modelo perde o arco
   emocional. Uma geração por cena, mirando mais de 250 caracteres, não uma por fala.
8. **Escute antes de fechar.** A checagem é sempre a mesma: alguma tag foi lida em voz alta? A voz
   obedeceu, ou a tag pediu o que ela não tem?

---

## 6. Pontuação faz metade do trabalho

- **Reticências (`...`)** criam pausa e peso. É o marcador de pausa do modelo.
- **CAPS** aumenta ênfase (`Eu falei AGORA.`). Use em uma palavra, não na frase inteira.
- **Pontuação normal** dá o ritmo. Ponto final é pausa; vírgula é respiro.
- **Não existe `<break time="1.5s" />`** no v3. Pausa se resolve com reticências, quebra de linha ou
  `[pause]`.
- **Quebra de linha por frase** é o formato que o modelo lê melhor.
- **Sem travessão.** Como marcador de pausa ele é menos consistente que as reticências.

---

## 7. Diálogo com mais de uma voz

O formato é rótulo de falante, tag, fala:

```text
Speaker 1: [proudly] Lembra daquele robô que eu instalei pra atender no WhatsApp?
Speaker 2: [wary] Lembro...
Speaker 1: [casually] Então. Ele parcelou um carro em cinquenta vezes.
Speaker 2: [alarmed] Cinquenta MESES?
Speaker 1: [sheepishly] Anos.
```

A fala nomeada do roteiro (`**Marquinho:**`, `**Chefe:**`) vira `Speaker 1:` / `Speaker 2:` na hora
de gerar, e o mapeamento personagem → voz é declarado uma vez por peça.

**Interrupção e sobreposição têm tags próprias** (`[interrupting]`, `[overlapping]`, `[jumping in]`).
A frase cortada termina em reticências, não em travessão.

---

## 8. Contrato da seção no roteiro

```markdown
## Faixa de voz

**Vozes:** <Personagem 1> = <voz> (Speaker 1) · <Personagem 2> = <voz> (Speaker 2)
**Stability:** Creative (comédia) | Natural (default)
**Fora da faixa:** o fecho é do apresentador real, gravado, sem tag.

Speaker 1: [tag] fala
Speaker 2: [tag] fala
```

O texto falado aqui é **idêntico** ao das falas do roteiro, verbatim: a faixa só acrescenta as tags.

---

## 9. Onde a faixa entra no pipeline

```
FAIXA DE VOZ  →  still gerado  →  still + áudio = clipe já falando  →  montagem
```

**A faixa vem ANTES do vídeo, e alimenta ele**, porque é a duração dela que define a duração de cada
clipe.

**Fala longa vai pra plano sem rosto**, porque cada rosto falando é uma sincronia a mais pra
escorregar, e o plano sem rosto (objeto, mão, plano aberto) recebe a voz como narração, sem risco
nenhum.

### Voz de personagem: speech-to-speech, nunca regravar

Personagem com voz diferente da sua **não se resolve com TTS nem regravando**. Grave você mesmo, com
a entonação certa, e passe pelo **voice changer** (speech-to-speech), que troca só o timbre.

- **Interpretação:** TTS entrega leitura correta e morna; ênfase, pausa e ironia continuam humanas por
  esse caminho.
- **Sincronia:** o speech-to-speech preserva a duração exata do arquivo. Se o clipe já existe, a boca
  continua batendo. **Regravar numa voz diferente quebra o sync**, porque a nova leitura nunca cai na
  mesma sílaba.

---

## 10. O que quebra

| Erro | O que acontece | Correção |
|---|---|---|
| Tag em roteiro que um humano vai gravar | quem lê fala "colchete whispers" ou trava | faixa de TTS em seção própria, teleprompter limpo |
| Tag que a voz não sustenta (`[shouting]` em voz calma) | sai abafado, parece que a tag não funcionou | troque a voz, não empilhe tags |
| Stability em Robust esperando atuação | as tags praticamente não pegam | Natural ou Creative |
| Tags contraditórias na mesma frase | saída imprevisível | uma tag por beat, ou `[pause]` entre estados |
| Tag inventada, principalmente em português | o modelo lê a tag em voz alta | tag em inglês, catálogo primeiro, escute o take |
| Tag de imagem (`[grinning]`, `[music]`) | ignorada ou lida | só o que se ouve; o resto é prompt de vídeo |
| Gerar frase por frase | prosódia picotada, entrega instável | uma geração por cena, mais de 250 caracteres |
| Emoção descrita no texto ("ele disse, tremendo") | o modelo pode LER a descrição | a direção vai na tag, o texto é só a fala |
