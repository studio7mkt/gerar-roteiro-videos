# 04 — O prompt de image-to-video (o still virando movimento)

---

## 1. A regra dura: não redescreva a cena

O modelo **já vê a imagem**. Repetir aparência, roupa, cor de cabelo, luz ou paleta cria
**instruções concorrentes** com o que está no pixel, e o resultado é deriva: o rosto muda no meio
do clipe, a roupa troca de cor, o cenário escorrega.

> ❌ "An elderly wizard in a grey cloak stands by the campfire in a night forest, warm firelight on
> his face, and he turns his head."
> ✅ "He snaps his head to camera-left, eyes widening."

**Gaste as palavras no que muda, não no que já está lá.**

### O que entra

| Bloco | O que é |
|---|---|
| **Quem** | o rótulo do personagem, nunca pronome solto |
| **Postura de entrada** | quando o still é neutro: em que posição ele entra e que segura essa posição |
| **O que se move** | um beat de movimento, com verbo forte |
| **Câmera** | só quando você quer um movimento específico |
| **Fim do movimento** | onde a ação assenta |
| **Fala** | a referência ao áudio, nunca o texto da fala |
| **Som** | música proibida, efeitos nomeados |

**Tamanho:** duas a quatro frases é a faixa que produz saída estável. Prompt de uma linha entrega
movimento genérico; prompt que tenta caber um filme inteiro num parágrafo desmonta. **Cena longa se
resolve em mais shots, não em prompt maior.**

---

## 2. As três regras de escrita

As três nascem do mesmo fato: **o modelo vê uma imagem, um áudio e este texto. Nada mais.**

**1. O prompt é auto-contido.** Nunca referencie outro shot, o que foi dito antes, um personagem
fora de quadro ou o arco da cena. "Turning the wizard's plan over in his mind", "in contrast to what
it's about to say": para o modelo, nada disso existe. Ele não viu o shot anterior e não vai ver o
próximo.

**2. Só afirmativo: descreva o certo, nunca o contraste com o errado.** Ao corrigir um prompt é
tentador escrever a correção como oposição à versão anterior ("pensativo **em vez de** debochado").
O modelo nunca viu a versão errada, então a única coisa que a frase faz é **injetar o conceito
errado no prompt**. Escreva apenas o estado final desejado: "sobrancelha franzida, olhos
semicerrados, lábios comprimidos".

**3. Nada de meta-comentário sobre o efeito pretendido.** "This shot is about dread, not
performance", "so the shot lands with a jolt". O modelo não renderiza intenção de direção, ele
renderiza pixel. Traduza a intenção no fato visível que a produz: em vez de "vendendo a escala",
escreva `shockwave rolls toward camera until it swallows the frame`.

### Negativo de estilo vira NÚMERO

Negar um estilo é a pior forma de pedir o oposto dele: não diz o que fazer, gasta atenção e ainda
planta a palavra indesejada no texto. **O que muda o resultado é o prazo e o rastro.**

- ❌ `never a slow drift`  ✅ `the crash zoom lands inside the first two or three frames`
- ❌ `not a gentle glide`  ✅ `the truck crosses its whole distance in well under a second`,
  `streaked with motion blur`

Vale além da câmera: quantidade, duração e consequência visível sempre ganham do adjetivo negado.

### A exceção válida: negação de composição

`Absolutely no trees`, `no text overlays`, `no other people in frame`, `hand not covering the mouth`
são **restrições de enquadramento**, não contraste corretivo. Elas nomeiam um default teimoso pra
derrubá-lo, e são das instruções mais úteis que existem.

A diferença: negação de composição diz **o que não pode estar no quadro**; contraste corretivo diz
**como não interpretar**, e é esse que faz mal.

**Mas negação de composição tem prazo de validade.** Uma correção pontual ("não gostei disso aqui,
troca") vale pra **aquele plano**, e não vira `NO <coisa> ANYWHERE` carimbado em todo prompt daí pra
frente. Três estragos, todos já cobrados na prática: (a) a negação atravessa contextos onde é falsa
e passa a brigar com uma instrução positiva do mesmo prompt; (b) come orçamento de atenção; (c)
planta a palavra indesejada no texto.

**O teste, antes de repetir qualquer negação em N prompts:** ela tem causa ativa **neste** plano, ou
é cicatriz herdada de outra peça? Se for cicatriz, apaga. E ao copiar um bloco de prompt de outra
produção, **releia as negações dele primeiro**: elas viajam junto e ninguém percebe.

### O pior tipo de todos: negar ATUAÇÃO

`Nothing else about him moves`, `he performs no large gesture at any point`, `his face barely changes
at all`. Custou seis clipes falados de uma produção inteira: todos voltaram com um ator parado, sem
expressão, sem vida. **É a instrução que o modelo cumpre melhor**, porque não exige nada dele.

Negação de composição tira um objeto do quadro e o resto do plano continua de pé. Negação de atuação
tira o plano inteiro e não põe nada no lugar.

**Personagem contido não é personagem imóvel, e a diferença é escrita, não é grau.** Contenção se
pede como uma **corrente de três ações pequenas e reais durante a fala**, todas afirmativas: o olho
que sobe até o interlocutor e volta pra mesa, o dedo que fecha contra a madeira e abre, o engolir, o
queixo que desce dois graus, o sorriso que **para** (nunca "que não existe").

**E toda postura fecha num ponto de chegada declarado** (`He stays looking down at the screen with
his mouth flat`, `He holds the wince`), senão a ação deriva até o último quadro e a montagem não tem
onde cortar.

**A versão de cenário do mesmo erro é a figuração no pretérito perfeito.** `The young man has just
sat down`, `has fallen asleep against the glass` descrevem estado já consumado, não ação, e o
gerador devolve fundo congelado. O certo é verbo acontecendo agora: `lowers himself onto the chair,
squares the folder on his knees and straightens his back`.

---

## 3. As cinco regras de movimento

1. **Um beat por clipe.** Uma ação clara se sustenta muito melhor que três coisas ao mesmo tempo.
2. **Verbo forte com intensidade.** `rockets`, `erupts`, `snaps`, `violently` ganham de `moves`,
   `starts`, `happens`. Ritmo dramático morno quase sempre é verbo fraco.
3. **Câmera só quando você quer movimento.** Silêncio sobre a câmera não é omissão: é o default, e
   ele já é bom.
4. **Ponto de chegada do movimento.** `...then settles back into place` evita que a ação continue
   derivando até o fim do clipe.
5. **Descreva o que se VÊ**, não o estado interno. "Ombros caem e o olhar desce" ganha de "ele fica
   triste".

### Por que `camera holds static` quase nunca precisa ser escrito

**O default do image-to-video já é câmera parada.** O modelo recebe um still e a tarefa dele é
animar o conteúdo daquele quadro. Ele não sai inventando dolly, e quando a prosa não pede movimento
nenhum, o que ele entrega é um quadro fixo com vida interna. A cláusula não muda o resultado, só
ocupa espaço num prompt em que cada frase compete por atenção.

**Os dois casos em que `static` ainda paga:** (a) quando o que acontece no quadro convida uma câmera
real a perseguir (objeto caindo, explosão, alguém saindo de quadro), porque aí o modelo tende a
acompanhar e você perde o enquadramento; (b) quando o shot vizinho na montagem tem movimento e você
precisa do contraste.

---

## 4. Quando a câmera PODE se mexer, e como pedir

**Movimento de câmera é a diferença mais barata entre "vídeo gerado" e "plano de cinema"**, e um
clipe com fala aceita bem mais violência do que a intuição sugere.

**Movimento lento é o erro padrão.** `slow steady push-in` num clipe de dois a três segundos é
indistinguível de câmera parada, e o resultado tem cara de equipe filmando institucional. É vídeo de
IA, e não há custo de grua: crash zoom, whip lateral, punch-in seco, crane despencando, pull-back
explosivo. O verbo é `slams`, `rips`, `whips`, `launches`, não `moves`.

**As travas, e elas são o que separa agressivo de inutilizável:**

1. **A boca nunca sai de quadro**, por mais violento que seja: `her face and mouth stay fully
   visible, sharp, in focus and unobstructed from the first frame to the last`. Câmera que perde a
   boca não devolve um clipe pior, devolve um clipe inútil.
2. **Arco de 45 graus, o personagem gira junto, e a trava tem que ser MENSURÁVEL.** Peça "orbit" e o
   modelo orbita de verdade: a câmera passa por trás e o plano vira nuca. São três frases, sempre
   juntas: `it turns about 45 degrees in total and no further`; `she pivots by the same amount,
   turning her head and shoulders to keep talking straight into the lens`; e a decisiva, `in every
   single frame both of her eyes and both of her cheeks are visible and her nose points at the
   camera`. **A terceira é o padrão a copiar:** condição que o modelo confere num frame isolado vale
   mais que qualquer descrição de trajetória.
3. **Movimento que ATRAVESSA o espaço arrasta o sujeito junto; movimento de ESCALA não.** Um dolly
   corredor adentro levou a apresentadora junto com a câmera, amarrada na lente, com o cenário
   passando atrás dela. Partindo de um still o modelo não tem como saber se a pessoa pertence ao
   mundo ou à câmera. **Zoom in, zoom out, push e pull são inequívocos.** Travelling, dolly e grua
   exigem a frase que desfaz a ambiguidade: `she does not move at all, her feet stay planted on the
   same spot of floor, and the camera does all of the work`. **Na dúvida, prefira o movimento de
   escala.**
4. **Um movimento por clipe, com ponto de parada seco.** Dois movimentos em três segundos viram
   borrão, e sem `snaps to a dead stop` o modelo deriva até o último frame.
5. **Não negue o estilo lento, declare o prazo.** Ver "Negativo de estilo vira NÚMERO".
6. **Em clipe com fala, o movimento tem que ATRAVESSAR a fala, nunca terminar antes dela.** O prompt
   `snaps to a dead stop exactly as her first word lands` devolveu o crash zoom, a câmera travando,
   cerca de um segundo de silêncio parado e só então a fala. O modelo cumpre ao pé da letra e ainda
   arredonda pra mais.

**A correção da regra 6 é estrutural**, não uma frase enfiada no meio: o prompt **abre** com um
bloco de timing, antes de qualquer descrição de cena.

> `TIMING FIRST, BECAUSE IT DECIDES WHETHER THIS CLIP IS USABLE: THE CAMERA MOVE AND THE SPEECH ARE
> LOCKED TOGETHER AND THERE IS NO GAP BETWEEN THEM. She is already speaking as the clip opens, or she
> starts speaking while the camera is still moving, and the camera move runs ACROSS her first words
> rather than finishing before them. The clip never opens with a still, silent beat.`

No corpo, troque `as her first word lands` por `while she is already two or three words into the
line`. As três formas válidas são fala **durante** o efeito (o padrão), **logo antes** ou **logo
depois** sem respiro. O que não existe é espaço entre os dois.

**Escolha o movimento pelo argumento, não pelo gosto:** slam pra dentro pra intimidade, whip lateral
pra rasgar o ambiente, pull-back explosivo pra revelar tamanho, crane caindo pra apresentar um lugar,
dutch torto pra dizer que algo está errado.

**E varie ao longo da peça.** O mesmo efeito repetido cansa na terceira vez e vira tique.
**Enumeração é a exceção**, e a forma boa não é repetir o mesmo movimento nos três planos: é uma
**escada**, um punch-in seco por plano, cada um fechando um degrau (aberto → médio → close).

**Se o modelo ignorar, não se perde nada:** um push-in na edição resolve por fora. O que só o
gerador entrega é o **parallax**, o fundo se reorganizando em profundidade, e é por isso que vale
pedir mesmo sabendo que pode não vir.

---

## 5. Som: música não, efeito sonoro sim

São duas coisas opostas, e o prompt trata cada uma no seu sentido.

**Música fora.** Trilha gerada é inutilizável: nasce com o tempo do clipe, não com o tempo da
montagem, e vem grudada no resto do áudio. Na hora de cortar sobra música brigando com música e
nenhum stem pra separar. A trilha entra na edição, sempre.

**Efeito sonoro dentro, e NOMEADO.** Martelada, corda de arco, passo, vento, fogo: é som que
pertence ao quadro, cabe dentro do clipe e chega pronto, poupando foley.

**Pedir genérico não basta.** `whatever the action in frame would actually make` é fraco demais: o
modelo devolve clipe mudo ou um som errado qualquer. **Liste os sons, um a um.**

> `No background music and no musical score of any kind. Diegetic sound only, and all of it mixed
> very low and well under the voice so that it never competes with the dialogue: <a lista dos sons
> deste clipe>.`

**O ambiente do lugar é um som contínuo, e ele conta a cena.** Um showroom tem murmúrio distante e
hum de ar-condicionado; um call center de madrugada tem dezenas de atendimentos sobrepostos; um
estúdio vazio tem silêncio morto. Declarar essa camada em todos os planos é o que amarra a sequência
num lugar só.

**E ela muda de propósito ao longo da cena:** o murmúrio da loja some quando o chefe grita, volta
tímido quando ele se recompõe, e some de vez no plano do constrangimento final. **Silêncio de gente
ouvindo é o efeito sonoro mais barato e mais eficaz que existe**, e só acontece se estiver escrito.

**Corte da lista o que disputa faixa com a voz.** Som de multidão, risada, música de ambiente e
qualquer coisa "média" competem por natureza; som pontual e distante (um baque, um clique, um
rangido) convive.

⚠️ **Não conte com o efeito sonoro.** Alguns modelos declaram não suportar SFX e ainda assim
entregam; outros devolvem silêncio. Deixe a cláusula no prompt (não custa e às vezes entrega), mas
**trate efeito sonoro como trabalho de edição** e **ouça cada clipe antes de montar**: som que você
não pediu também não estava no seu roteiro.

---

## 6. Figuração precisa se mexer no clipe, não só no still

Figurante parado na imagem e parado no vídeo vira manequim, e manequim ao fundo denuncia clipe
gerado. Todo prompt diz **o que a figuração faz naquele clipe**, sempre em movimento pequeno: o
vendedor dá mais um passo em volta do carro, o cliente se agacha pra olhar a roda, alguém vira uma
página.

**E ela reage ao que acontece em primeiro plano.** É a camada de comédia mais barata que existe: o
vendedor congelando no meio do passo quando o chefe grita, a loja inteira parando de olhar no
segundo grito, alguém fingindo estar ocupado no plano seguinte. Custa uma frase por prompt e nenhum
shot a mais.

**Quando o still-base serve quatro planos, essa camada é 100% do prompt de vídeo**, e é ela que
impede os quatro de parecerem o mesmo plano repetido. Faça o fundo **andar**: a pessoa se ajoelha
num plano, o garçom passa na frente no outro, ela diz sim no terceiro, todo mundo congela no quarto.
Custa zero geração a mais.

**A trava:** figurante nunca em foco, nunca de frente pra lente, nunca perto do protagonista,
movimento sempre pequeno. Rosto nítido ou gesto grande no fundo disputa atenção com a boca do
protagonista e o modelo às vezes anima a boca errada.

### "Não reagir" e "não se mexer" são coisas diferentes

**A gag de indiferença** (o desastre no fundo que ninguém liga) é o caso em que a figuração **não**
reage. E é exatamente aí que se erra: escrever `not one person moves, turns or reacts in any way`
devolve uma **sala de manequins**, e o clipe inteiro lê como falso.

As duas metades se escrevem separadas, e a afirmativa vem primeiro:

> `Everyone beyond the glass keeps moving naturally and busily the whole time and the room never goes
> still: the speaker keeps walking, gesturing and talking; the seated audience shift in their chairs
> and glance at their phones; at the desks people carry on typing and walking past with cups. Not one
> of them reacts to what just happened: nobody looks up at it, nobody stands, nobody points and nobody
> stops what they are doing.`
>
> **`It is not that they are frozen, it is that they simply do not care.`**

**Essa última frase é a que faz o trabalho**, porque nomeia a intenção em vez de listar proibição.

---

## 7. Ação curta em clipe de duração mínima vira slow motion

O gerador tem **piso de duração** (uns 5s na maioria). Uma ação violenta de verdade dura meio
segundo. O modelo resolve a conta do único jeito que sabe: **estica a ação pra preencher o clipe**, e
volta câmera lenta, que é o oposto do que ação cômica precisa.

Duas defesas, e precisa das **duas**:

1. **Negue o slow motion com todas as letras.** `Everything plays at full real-time speed: absolutely
   no slow motion, no slow-motion ramp, no speed ramping and no dramatic slowdown at any point, and no
   floating or hanging in the air.` Sozinha, essa frase costuma não bastar.
2. **Escreva o RESCALDO.** Dê a ele o que fazer nos segundos que sobram, em duas partes declaradas:
   `THE ACTION, violent and over almost immediately: ... THE AFTERMATH, filling the rest of the clip:
   ...`. Papel ainda caindo, mesa parando de balançar, nuvem de farinha assentando, figuração
   reagindo. Sem o rescaldo ele estica a ação de novo, porque não tem outra opção.

**Na montagem você usa quase só a ação**, cortando no pico do impacto: o rescaldo existe pra ocupar o
clipe, não pra entrar no corte.

**De quebra, o rescaldo resolve compliance.** Trocar "congela no auge do pulo" por "ele passa reto e
sai de quadro, e a mesa capota" entrega o estrago sem entregar a agressão, que é o que anúncio pago
aceita.

---

## 8. Fala e sincronia labial

### A rota atual: o áudio entra junto com a imagem

Os modelos atuais de vídeo aceitam **still + mp3 na mesma chamada** e devolvem o clipe já falando,
com a boca sincronizada, em português, num estágio só e em alta resolução. Não existe passe separado
de lip sync e não existe estágio de boca fechada.

**Duas rotas antigas que valem conhecer só pra não cair nelas:**

| Rota | Estágios | Resolução | Situação |
|---|---|---|---|
| vídeo com referência de áudio | 1 | até 2K | a rota atual |
| talking head (só anima a cabeça) | 1 | teto de 720p | perde nos dois eixos que importam |
| gerar mudo + passe de lip sync | 2 | livre | contingência, se o modelo mudar |

**E não confunda com áudio nativo.** Áudio nativo é o modelo **gerando a voz** junto com a imagem, e
em geral só faz inglês e chinês: em português ele traduz. O que se usa é o seu arquivo de áudio como
referência, e aí a língua é indiferente.

### O que o prompt escreve, e o que ele nunca escreve

> `Using @img1 as the reference image for this exact frame, animate it. <postura de entrada>. He
> speaks the line captured in @audio1, his mouth moving naturally in sync with it. As he talks,
> <descrição rica da atuação: olhar, gesto, o que a figuração faz>.`

- **Nunca repita a fala em português dentro do prompt de vídeo.** Ela já está no áudio. Repetir cria
  instrução concorrente. É o erro mais fácil de cometer quando as duas etapas ficam lado a lado no
  mesmo documento.
- **Nunca use pronome solto no lugar do rótulo.** O modelo troca de personagem.
- **Quando o still é neutro, o prompt abre pela POSTURA:** `At the very start of the clip, as the
  voice begins, he comes out of the neutral resting position into the posture described next, and he
  holds that posture for the rest of the clip: <postura>`. Postura enfiada no meio do parágrafo o
  modelo trata como detalhe.

### A trava do áudio curto

Áudio de 2,3s num clipe de 5s deixa 2,7s de buraco, e o modelo preenche **inserindo pausa dentro da
fala**. A trava vai na **primeira linha** do prompt:

> `The voice in the reference audio starts at the very first frame of the clip and plays exactly as
> recorded, at its natural pace, with no added pause, no stretching, no slowing and no silence
> inserted anywhere inside it.`

Assim o silêncio sobrando cai **no fim**, que é onde a edição corta sem dó.

### O que a montagem corta, o gerador não deveria ter gerado

**A primeira e a última ponta do clipe são as duas coisas que o editor apaga**, porque o corte entra
em cima da fala. Então beat de atuação e gag no silêncio antes ou depois da voz é **geração paga e
jogada fora**, e é justamente onde o modelo prefere resolver ação, porque tem espaço vazio.

> `EVERYTHING DESCRIBED BELOW HAPPENS WHILE HE IS SPEAKING, not before the voice and not after it.`

E cada gag de fundo entra amarrada: `At the same time, while he is still speaking, beyond the glass
...`. Só o que **precisa** de silêncio (o rescaldo de uma ação violenta, o congelamento que emenda no
fecho) fica depois da voz.

### Quando o clipe tem fala E ação grande: declare duas metades

Ação grande no meio da fala faz o modelo escolher entre a boca e o movimento, e ele escolhe errado.
Pedir isso em prosa não basta: "only after the line ends does he swing", solto no meio do parágrafo,
é lido como sugestão e o modelo golpeia na metade da frase.

O que funciona é **declarar a estrutura, em caixa alta, como esqueleto do prompt**:

> `The clip has two clearly separate halves, in this order. FIRST HALF: he does nothing but speak the
> line captured in @audio1, the sword held perfectly still from the first word to the last. SECOND
> HALF, beginning only once the voice has completely stopped: he strikes ...`

Reforce dentro da primeira metade o que **não** se move e o que o resto do quadro faz enquanto isso.
Metade sem instrução é metade que o modelo preenche.

⚠️ **Isso não contradiz a regra 6 de movimento de câmera.** O que se separa no tempo é **ação de
corpo**, que briga com a boca pela atenção do modelo. Movimento de câmera não briga, porque não é o
personagem que se mexe: ação grande espera a voz acabar, câmera corre por cima dela.

**Bônus: o modelo obedece "duas metades" mesmo sem ação violenta**, e isso economiza plano. Escrever
`FIRST HALF: ... SECOND HALF, beginning only once the voice has completely stopped: ...` já fundiu o
plano da fala e o plano de fecho num clipe só: um still a menos e uma geração a menos.

---

## 9. Ação com impacto: nomeie o contato

Modelo de vídeo entrega "efeito de ação" sem causa: inimigos desabando sozinhos, sem a arma encostar
em nada. Não parece luta, parece bug, e é um dos defeitos que mais denuncia IA.

Duas instruções resolvem, e as duas são necessárias:

1. **Nomeie o contato físico e o alvo único.** `the hammer slams squarely into the leading orc and
   launches that single orc through the air`. Sem alvo nomeado o modelo espalha o efeito por todo
   mundo.
2. **Negue a queda sem causa, explicitamente.** `No orc falls at any moment without being physically
   struck by the hammer.` É negação de composição, a exceção válida.

E **o still tem que nascer limpo**: se a imagem inicial já tem alguém caindo, o clipe herda a queda
sem causa. Descreva os figurantes `all of them upright and running, none of them falling`.

---

## 10. Foto dentro do plano não pode ganhar vida

O medo legítimo de mandar um inserto de foto pro image-to-video é o modelo animar quem está dentro da
foto. Segura um push-in de 9 segundos:

> `THE PHOTOGRAPH ON THE SCREEN IS A STILL PHOTOGRAPH AND IT NEVER ANIMATES. The two men inside the
> photograph do not blink, do not breathe, do not move their heads, do not change expression and do
> not shift at all: treat the entire screen content as a frozen printed image for the whole clip,
> exactly as it is in the first frame.`
