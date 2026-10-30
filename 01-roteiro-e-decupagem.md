# 01 — Roteiro e decupagem

Como a cena vira um documento executável. Este arquivo cobre a **escrita** (estrutura, falas,
duração) e o **contrato de saída** do `ROTEIRO.md`.

---

## 1. A régua de duração, e ela vem antes de tudo

O gerador de vídeo entrega clipes de **5 a 15 segundos**. Não existe clipe de 3 segundos e não
existe clipe de 40. Isso significa que **a duração da fala é o que decide o tamanho do shot**, e
não o contrário.

Em PT-BR falado, com ritmo natural de conversa ou de comédia, conte **~2,8 palavras por segundo**:

| Palavras na fala | Duração | Veredito |
|---|---|---|
| 8 a 15 | 3 a 5,5s | zona ideal |
| 16 a 22 | 6 a 8s | teto confortável |
| 23 a 27 | 8 a 10s | só se não der pra cortar |
| 28 ou mais | passa de 10s | **quebra em dois shots** |

**A quebra não custa uma palavra do roteiro.** São dois planos do mesmo personagem, decupagem
normal. E costuma **melhorar** a cena: cortar antes do último degrau isola o detalhe final num
quadro só, que é exatamente onde a piada mora.

### O problema oposto: fala curta demais

Fala de 7 palavras (~2,5s) num gerador com piso de 5s deixa um buraco de 2,5 segundos, e o modelo
preenche do jeito que sabe: **inserindo pausa dentro da fala**. Volta um `"Chefe............ eu me
demito"` que não existe no arquivo gravado.

**Resolve-se dentro do próprio mp3, nunca esticando o áudio depois:** grave um beat de silêncio
antes e outro depois, no mesmo arquivo, e transforme esse silêncio em atuação (o riso curto antes
da frase, o ar que ele puxa antes de xingar).

**A conta final do clipe:** `duração do clipe = duração do áudio + 1 segundo, arredondando pra
cima`, com piso de 5s. O segundo a mais não é folga de segurança: é o espaço pro beat de atuação
depois que a voz termina, e é o que impede o clipe de cortar em cima da última sílaba.

---

## 2. A estrutura da peça

Existem dois tipos de vídeo curto feito com IA, e eles se escrevem diferente.

### 2.1 Cena encenada (esquete, paródia, dramatização)

Gancho e conteúdo se **fundem na cena**: a esquete inteira é o que prende e o que prova.

```
[setup em 1 fala] → [escalada em degraus] → [o detalhe que piora tudo] → [virada física] → [fecho]
```

- **Setup em uma fala.** O primeiro personagem já nomeia o que aconteceu ("lembra aquele robô que
  eu instalei pra atender no WhatsApp?"). Sem contextualização, sem apresentação, sem "então, deixa
  eu te explicar".
- **Escalada em degraus, nunca de uma vez.** A graça mora na revelação fatiada: vendeu → parcelou
  em 50 vezes → não são meses, são anos → e o cliente tem 90. Cada degrau derruba a reação do outro
  personagem um nível. Entregar o absurdo inteiro na primeira fala mata a cena.
- **O detalhe que piora tudo.** O último degrau é sempre o mais gratuito, o que nem precisava
  existir (a película e o subwoofer de brinde). É ele que faz a piada virar meme.
- **Virada física.** A cena não termina em fala, termina em corpo: o chefe pulando por cima da
  mesa. Congela no auge ou corta seco. **Fala não fecha esquete.**
- **Fecho.** Se a peça tem uma mensagem no fim, ela vem em corte seco, em plano limpo, na voz de
  quem apresenta. Nunca dentro da cena.

**A regra que sustenta a linha inteira:** o vexame tem que mapear numa falha nomeável. A cena
precisa deixar claro, **sem dizer**, qual foi o furo, porque é isso que o fecho vai nomear depois.
Esquete engraçada cujo erro não é um erro de verdade rende risada e nada mais.

**Um exagerado por cena.** Se os dois personagens escracham, vira desenho animado e o público para
de acreditar nos dois. O contido é quem sustenta a graça do explosivo: ele olha pra baixo, fala
mais baixo, para de sorrir e demora um beat a mais pra começar a frase. Constrangimento de verdade
é alguém tentando parecer normal e falhando um pouquinho, não alguém performando vergonha.

**E o contido é a rota tecnicamente mais segura**, não só a mais engraçada: o gerador executa bem
amplitude pequena (olhar, canto da boca, ombros) e executa mal ou ignora gesto grande e postura
extrema.

### 2.2 Vídeo com apresentador ou narração

Aqui existe um bloco falado contínuo, e a decupagem serve pra dar variedade visual.

```
[gancho 0-3s] → [desenvolvimento] → [fecho]
```

- **O gancho tem duas camadas, e as duas são obrigatórias:** o **visual** (o que se vê no primeiro
  frame, antes de qualquer palavra) e o **narrativo** (a primeira frase falada). Roteiro que só traz
  a fala está entregando meio gancho.
- **Regra prática do gancho visual:** se o primeiro frame pode ser descrito como "uma pessoa
  falando", falta gancho visual.
- **A primeira frase cospe o que está em jogo.** Não aquece, não contextualiza, não diz "oi
  pessoal".
- **Cada 5 a 8 segundos pede um plano novo**, senão o vídeo lê como slideshow. Planos sem rosto
  (um objeto, um close de mão, um plano aberto) são os mais baratos e os mais seguros: recebem a
  voz como narração, sem sincronia labial nenhuma pra escorregar.

**Jogue as falas longas pros planos sem rosto.** Cada rosto falando é uma sincronia a mais pra dar
errado, e fala longa é onde ela mais escorrega.

---

## 3. Contrato do `ROTEIRO.md`

```markdown
# <Nome da peça>

**Formato:** 9:16 vertical · **Duração alvo:** ~<N>s · **Voz:** gravada | sintetizada
**Rota de produção:** áudio primeiro, still depois, clipe gerado já falando.

## A cena

**Personagens:** <nome 1> (<papel, característica física forte>), <nome 2> (<papel>)

**Onde:** o cenário em um parágrafo. Concreto, bonito e específico: material, luz, o que está
em cada plano de profundidade. Este parágrafo é a matéria-prima de todo prompt de still.

**Os dois elementos de atenção:** PRIMEIRO <o achado>. SEGUNDO <a gag>.

**Regra de quadro:** um personagem por plano com fala · <nome 1> sempre à esquerda olhando pra
direita, <nome 2> espelhado · o eixo não vira em nenhum shot.

---

**Shot <n> · <Personagem>** · <N> palavras, ~<N>s
*Uma ou duas linhas em português natural: o que se vê e a emoção dele neste plano. Não é o
prompt. É o que a pessoa precisa pra conferir a cena e gravar a fala no tom certo.*

> a fala, verbatim

---

**Shot <n> · <o que acontece>** · sem fala, ~<N>s
*a reação, o susto, a virada física*

---

## TELEPROMPTER

> Só o texto falado, na ordem, com o nome de quem fala. Sem direção, sem prompt, sem colchete.
> É o que a pessoa cola na tela na hora de gravar.

**<Personagem>:** <fala>
**<Personagem>:** <fala>
```

### Regras do contrato

- **A cena é entregue shot a shot, nunca como bloco corrido de diálogo.** É esse formato que expõe
  uma fala longa demais **antes** de ela virar um still pago. Bloco corrido esconde as duas coisas.
- **Descrição de cena é linguagem natural, nunca prompt.** O prompt em inglês mora no `PROMPTS.md`.
- **Toda fala carrega palavras e segundos.**
- **Fala nomeada, uma por vez**, sem fundir dois personagens no mesmo bloco.
- **`[CORTA PARA: ...]`** marca só corte que muda plano ou local; não anote toda troca de fala, o
  nome do personagem já resolve.
- **Shot sem fala também é shot.** Reação, susto e virada física entram como shots próprios.
- **Sem travessão, sem itálico na fala, sem emoji.** Quebra de linha por frase.
- **O teleprompter nunca leva colchete de emoção.** Ele existe pra um humano ler em voz alta.

---

## 4. Checklist antes de gerar qualquer coisa

Rode item por item. Cada um destes já custou uma produção.

- [ ] Toda fala tem contagem de palavras e duração estimada, e nenhuma passa de 27 palavras.
- [ ] Nenhuma fala fica abaixo de ~3s sem ter silêncio planejado dentro do próprio mp3.
- [ ] Todo shot com fala tem **um** personagem em quadro.
- [ ] O mapa de assets diz quantos stills existem, e o número é **menor** que o número de shots.
- [ ] Cada still-base nasce **neutro**: testa lisa, sem sorriso, sem emoção desenhada.
- [ ] Os stills de pico (fúria, susto, choro) estão listados separados, porque textura mora no pixel.
- [ ] Nenhum prompt de vídeo redescreve o cenário ou repete a fala em português.
- [ ] Todo prompt de still declara a proporção e repete o cenário inteiro.
- [ ] Nenhum plano tem mais de dois elementos de atenção.
- [ ] Todo prompt de vídeo proíbe música e **nomeia** os efeitos sonoros.
- [ ] O eixo de câmera não vira: cada personagem fica sempre do mesmo lado do quadro.
- [ ] Nenhuma marca real aparece em lugar nenhum (logo, emblema, embalagem).
- [ ] O usuário confirmou o modelo e o custo antes do disparo.
