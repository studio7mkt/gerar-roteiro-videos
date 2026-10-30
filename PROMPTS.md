# O pedido de Manaus — prompts prontos

Roteiro e direção em [ROTEIRO.md](ROTEIRO.md). **Fala mora em um lugar só:** o texto falado está no
teleprompter do roteiro, não aqui.

---

## Os anexos

**Retratos de referência** (gerados uma vez, nunca mais):

- `referencias/marquinho.jpg` — o rapaz baixo, 19 anos
- `referencias/chefe.jpg` — o homem pesado, careca, 58 anos

**Stills** — a gerar. **Quatro, pra seis shots:**

| Arquivo | O que é | Serve os shots |
|---|---|---|
| `stills/marquinho-base.jpg` | Marquinho na bancada, **neutro** | 1, 3, 5 |
| `stills/chefe-base.jpg` | Chefe do outro lado da bancada, **neutro** | 2 |
| `stills/chefe-pico.jpg` | Chefe debruçado, mão erguida, berrando | 4 |
| `stills/chefe-pulo.jpg` | O pulo, contra-plongée | 6 |

**Quatro imagens, seis planos.** Os três shots do Marquinho saem do mesmo pixel: o que muda entre
eles está inteiro no prompt de vídeo (postura, olhar, e o fundo andando).

**Vozes** — a gravar. A numeração bate com o shot.

| Arquivo | Shot | Quem | Palavras | Estimativa | Duração real |
|---|---|---|---|---|---|
| `vozes/1.mp3` | 1 | Marquinho | 16 | ~6s | |
| `vozes/2.mp3` | 2 | Chefe | 12 | ~4,5s | |
| `vozes/3.mp3` | 3 | Marquinho | 14 | ~5s | |
| `vozes/4.mp3` | 4 | Chefe | 15 | ~5,5s | |
| `vozes/5.mp3` | 5 | Marquinho | 11 | ~4s ⚠️ | |

O shot 6 não tem fala e não leva áudio.

---

## Antes de começar

1. **Retrato nos stills, still nos vídeos.** Na etapa 1 você anexa o retrato (`@img1`/`@img2`) e cita
   o marcador dentro do prompt. Na etapa 2 você anexa o still gerado (que vira `@img1` daquela
   geração) mais o mp3. **Nunca redescreva rosto e corpo.**
2. **Configuração fixa dos stills:** proporção **9:16**, resolução **2K**. Em outra proporção a
   composição nasce errada pro vertical.
3. **Um protagonista por imagem.** Figuração ao fundo sim, desde que longe, fora de foco e de costas
   ou de lado.
4. **Ângulo e fundo fixos por personagem.** Marquinho à esquerda com a parede de tijolo e o salão
   atrás; Chefe à direita com o forno e o letreiro atrás. As exceções são o shot 6 (o pulo) e a
   câmera mais baixa dele, e as duas são de propósito.
5. **Os 5 shots com fala levam o mp3 anexado**, e o prompt cita a referência de áudio sem nunca
   escrever a fala em português.
6. **O prompt de vídeo dos shots neutros abre pela POSTURA**, porque o still é neutro. Os prompts do
   pico e do pulo não abrem por postura: ela já está travada na imagem.

**Duração de cada clipe = duração real do mp3 + 1 segundo, arredondando pra cima**, piso de 5s. Os
dois shots sem áudio vão no piso.

## Os defaults teimosos deste cenário são três

Pizzaria é um dos cenários mais contaminados de dataset que existe. Os três estão negados em todos os
prompts, e vale conferir os três em cada imagem que voltar:

1. **Cantina italiana de clichê:** toalha xadrez, garrafa de vinho com vela, guirlanda de alho, mural
   do Vesúvio.
2. **Cozinha industrial de aço inox e luz fluorescente**, que é o que o dataset entrega quando você
   pede "cozinha de pizzaria".
3. **Marca em embalagem.** Caixa de pizza puxa logotipo, e isso é reprovação de anúncio.

**A locação abre o prompt em CAIXA ALTA**, porque o que vem primeiro pesa mais.

---

## Etapa 1 — Os 4 stills

### `stills/marquinho-base.jpg` — Marquinho na bancada, neutro
**Anexa:** `@img1` (retrato do Marquinho) · **serve os shots 1, 3 e 5**

Três dos seis planos saem daqui, então gere 3 ou 4 versões e escolha com calma. Confira quatro
coisas: o rosto bate com o retrato e ainda está grande o suficiente pra ler emoção pequena, o
entregador está legível na porta, o pedido de casamento está visível sem roubar o quadro, e a cara
está mesmo **em repouso** (nenhum sorrisinho, testa lisa). Emoção desenhada aqui aparece nos três
clipes.

```
Eye-level medium shot framing him from the waist up, camera frontal from slightly camera-right, subject framed left-of-center and still the single largest thing in the frame, face clearly visible and angled toward the lens, looking off-camera toward camera-right, mouth closed and unobstructed. INSIDE A BEAUTIFUL MODERN NEAPOLITAN PIZZERIA with an open kitchen, a warm high-ceilinged room that opens out behind him. He stands at a long marble preparation counter, white stone with soft grey veining, dusted with flour, a wooden peel and a scatter of dough trimmings lying along it. Behind him a white-painted exposed brick wall with one thick oak shelf carrying glass jars and plain unlabelled tins, an open side doorway beside it, and past that the full dining room: eight or nine small marble tables with bentwood chairs, most of them occupied, low amber glass pendant lamps hanging over them, big windows along the far wall. Warm firelight spills onto him from the wood-fired oven off-camera behind the lens, throwing a soft flicker across one side of his face. The near foreground is the blurred edge of the marble counter cut by the bottom of the frame. Two things in the background are meant to catch the eye, in this order of prominence. FIRST, and clearly readable even on a small screen: in the open side doorway behind him, a delivery rider in a helmet with a large insulated backpack still on his shoulders stands eating a slice of pizza, caught mid-bite and looking at nothing in particular. SECOND, softer and smaller, out at a table in the middle of the dining room and easy to miss on a first look: a young man down on one knee beside his date holding up an open ring box, the woman with both hands over her mouth, neither of them looking anywhere near the camera. Beyond those two, the ordinary life of the restaurant fills the rest of the room, all of it small, soft and unimportant: a pizzaiolo in a white apron sliding a long wooden peel toward the oven, a waiter crossing the room carrying two pizzas, and a couple at a window table eating in silence with both of them looking at their phones. Everyone in the background is caught mid-action, busy with their own thing, and nobody is facing the camera or posing. @img1 the young man wears a plain white uniform t-shirt and a canvas apron smudged with flour, the apron strings hanging loose. He stands at the counter, upright but a little slack, one forearm resting on the marble with that hand open and flat on the stone, his other arm down at his side. His face is completely at rest: mouth closed and relaxed, forehead completely smooth with no frown lines, eyebrows level and unfurrowed, eyes calmly toward the person off-camera. No expression of any kind is being performed: no smile, no worry, no tension anywhere in the face. His hands read as real hands: five clearly separated fingers on each, correct proportions, and the two hands never touching, interlocking or fidgeting against each other. Neither hand is near his mouth. The whole pose is loose and asymmetric, the weight settled, like someone caught in the middle of a conversation rather than holding a position for a camera. The room is warm, expensive and well kept, the quality of a food-and-interiors magazine spread rather than a generic stock-photo pizzeria: no red-and-white checked tablecloths, no straw-covered wine bottles, no hanging garlic, no painted murals of Italy, no stainless-steel industrial kitchen, no fluorescent lighting. Any pizza boxes visible are plain, unprinted and unbranded. Photorealistic, shot on ARRI Alexa Mini with spherical prime lenses, Kodak Vision3 500T look, warm naturalistic grade, soft contrast, fine organic grain, gentle vignette, moderate depth of field with the background softened but still clearly readable rather than melted into bokeh. Vertical 9:16 composition. No text overlays, no logos and no brand names anywhere in the frame. Nobody else in the near foreground beside him, and nobody in the background in sharp focus or looking at the camera.
```

### `stills/chefe-base.jpg` — Chefe do outro lado da bancada, neutro
**Anexa:** `@img2` (retrato do Chefe) · **serve o shot 2**

⚠️ **É aqui que o letreiro nasce.** Confira letra por letra antes de seguir, incluindo o acento do
`SÓ`, que é a primeira coisa a cair.

```
Eye-level medium close-up, camera frontal from slightly camera-left, subject framed right-of-center, face clearly visible and angled toward the lens, looking off-camera toward camera-left, mouth closed and unobstructed. INSIDE A BEAUTIFUL MODERN NEAPOLITAN PIZZERIA with an open kitchen, a warm high-ceilinged room. He stands at a long marble preparation counter, white stone with soft grey veining, dusted with flour, a disc of stretched dough in front of him. Behind him, dominating the background, a wood-fired dome oven clad in deep emerald-green glazed tile with a polished brass mouth, live flames burning inside it and split wood stacked underneath, throwing a warm flicker across the room. Low amber glass pendant lamps hang over the counter. The near foreground is the blurred edge of the marble counter cut by the bottom of the frame. Exactly two things in this room are meant to catch the eye, and they are these. FIRST: mounted on the white-painted brick wall directly above the oven, a clean hand-painted sign in dark green capitals reads exactly PIZZARIA SANTA MASSA on the first line and, in smaller capitals underneath, ENTREGAMOS SÓ NO BAIRRO, both lines correctly spelled and correctly accented, well lit and easy to read. SECOND: to one side and further back, small in the frame, a pizzaiolo in a white apron is sliding a long wooden peel into the mouth of the oven, seen from behind and softly out of focus. Apart from those two the rest of the room stays simple and calm, with no other props, notices or clutter competing for attention. @img2 the heavy-set balding older man wears a dark business suit one size too small, the jacket straining across his belly, and over it a white pizzaiolo's apron hanging open around his neck and untied at the back, with flour on one sleeve. He stands at the counter, settled and comfortable, weight on one leg, one hand resting open and flat on the marble beside the dough and the other arm down at his side and out of the bottom of the frame. His face is completely at rest: mouth closed and relaxed, eyebrows level, eyes calmly toward the person off-camera, the deep lines of his age visible in the skin but no expression pulled into them. No expression of any kind is being performed: no smile, no anger, no tension anywhere in the face. His hands read as real hands: five clearly separated fingers on each, correct proportions, and the two hands never touching, interlocking or fidgeting against each other. Neither hand is near his mouth. The whole pose is loose and asymmetric, the weight settled, like someone caught in the middle of a conversation rather than holding a position for a camera. The room is warm, expensive and well kept, the quality of a food-and-interiors magazine spread rather than a generic stock-photo pizzeria: no red-and-white checked tablecloths, no straw-covered wine bottles, no hanging garlic, no painted murals of Italy, no stainless-steel industrial kitchen, no fluorescent lighting. Any pizza boxes visible are plain, unprinted and unbranded. Photorealistic, shot on ARRI Alexa Mini with spherical prime lenses, Kodak Vision3 500T look, warm naturalistic grade, soft contrast, fine organic grain, gentle vignette, shallow depth of field. Vertical 9:16 composition. No text overlays and no logos or brand names anywhere in the frame apart from the hand-painted sign described above. No other people in the near foreground and nobody in the background in sharp focus or facing the camera.
```

### `stills/chefe-pico.jpg` — A explosão
**Anexa:** `@img2` (retrato do Chefe) · **serve o shot 4**

**Este não sai do neutro:** cara vermelha, olho saltado e veia na testa moram no pixel, e o gerador de
vídeo não os inventa. **Gere com folga, 3 ou 4 versões.** Fúria cômica tem uma janela estreita: um
grau acima vira careta de meme, um grau abaixo vira chefe entediado.

**A mão erguida é um gesto de incompreensão**, aberta e virada pra cima na altura do ombro. A fala
dele aqui é uma pergunta sem resposta possível, não uma acusação, e a placa acusa sozinha atrás dele,
sem gesto nenhum apontando pra ela.

```
Eye-level medium close-up, camera frontal from slightly camera-left, subject framed right-of-center, face clearly visible and angled toward the lens, mouth wide open mid-shout and unobstructed. INSIDE A BEAUTIFUL MODERN NEAPOLITAN PIZZERIA with an open kitchen, a warm high-ceilinged room. He is at a long marble preparation counter, white stone with soft grey veining, dusted with flour, a disc of stretched dough in front of him. Behind him, dominating the background, a wood-fired dome oven clad in deep emerald-green glazed tile with a polished brass mouth, live flames burning inside it and split wood stacked underneath. Low amber glass pendant lamps hang over the counter. The near foreground is the edge of the marble counter cut by the bottom of the frame. Exactly two things in this room are meant to catch the eye, and they are these. FIRST: mounted on the white-painted brick wall directly above the oven, a clean hand-painted sign in dark green capitals reads exactly PIZZARIA SANTA MASSA on the first line and, in smaller capitals underneath, ENTREGAMOS SÓ NO BAIRRO, both lines correctly spelled and correctly accented, well lit and easy to read. SECOND: to one side and further back, small in the frame, a pizzaiolo in a white apron has stopped with a long wooden peel half raised and turned his head slightly toward the noise, seen from behind and softly out of focus. Apart from those two the rest of the room stays simple and calm, with no other props, notices or clutter competing for attention. @img2 the heavy-set balding older man wears a dark business suit one size too small with a white pizzaiolo's apron hanging open around his neck, flour on one sleeve. He has pitched forward over the counter, weight thrown onto one hand planted flat and open on the marble, face flushed dark red, eyes bulging wide, forehead veins standing out, mouth wide open in a full roar, his other arm raised at shoulder height and well clear of his face, that hand open with the palm turned up and the fingers spread in a wide baffled question. His hands read as real hands: five clearly separated fingers on each, correct proportions, and the two hands never touching, interlocking or fidgeting against each other. Neither hand is near his mouth. The whole pose is loose and asymmetric, like someone caught in the middle of an argument rather than holding a position for a camera. The room is warm, expensive and well kept, the quality of a food-and-interiors magazine spread rather than a generic stock-photo pizzeria: no red-and-white checked tablecloths, no straw-covered wine bottles, no hanging garlic, no painted murals of Italy, no stainless-steel industrial kitchen, no fluorescent lighting. Any pizza boxes visible are plain, unprinted and unbranded. Photorealistic, shot on ARRI Alexa Mini with spherical prime lenses, Kodak Vision3 500T look, warm naturalistic grade, soft contrast, fine organic grain, gentle vignette, shallow depth of field. Vertical 9:16 composition. No text overlays and no logos or brand names anywhere in the frame apart from the hand-painted sign described above. No other people in the near foreground and nobody in the background in sharp focus or facing the camera.
```

### `stills/chefe-pulo.jpg` — O pulo
**Anexa:** `@img2` (retrato do Chefe) · **serve o shot 6**

O único shot em contra-plongée, e é de propósito: a virada física precisa de outro plano pra ler como
ruptura. **Ele passa reto e sai de quadro, e quem fica é a farinha.** Não mostre o contato: a piada é
a ameaça, e contato explícito é o que atrai reprovação de anúncio.

⚠️ **O still nasce com a farinha só COMEÇANDO a subir.** Se a imagem já vier com a nuvem formada, o
clipe herda a nuvem parada e você perde o efeito inteiro, que é justamente ela crescendo.

```
Low-angle medium-wide shot from just below counter height, camera positioned to his right and facing him, the whole marble preparation counter in frame. INSIDE A BEAUTIFUL MODERN NEAPOLITAN PIZZERIA with an open kitchen, a warm high-ceilinged room. A long marble preparation counter fills the lower third of the frame, white stone dusted heavily with flour, a wooden peel and a disc of stretched dough lying across it and a stack of plain unprinted pizza boxes at one end. Behind him, dominating the background, a wood-fired dome oven clad in deep emerald-green glazed tile with a polished brass mouth, live flames burning inside it. Low amber glass pendant lamps hang over the counter. Mounted on the white-painted brick wall directly above the oven, a clean hand-painted sign in dark green capitals reads exactly PIZZARIA SANTA MASSA on the first line and, in smaller capitals underneath, ENTREGAMOS SÓ NO BAIRRO, both lines correctly spelled and correctly accented. Further back and softly out of focus, the pizzaiolo and the diners in the room beyond are frozen watching, one of them with a hand half raised. @img2 the heavy-set balding older man in a dark suit one size too small, jacket open and the white apron flying loose off his neck, is caught at the very start of a lunge across the counter: both hands planted flat on the marble taking his full weight, one knee coming up onto the surface, torso already low and driving forward toward camera-left, both arms beginning to reach out ahead of him with the fingers spread, face contorted in exaggerated comedic rage, mouth open in a roar. The flour on the counter is only just beginning to lift around his hands, a thin wisp of it rising, and the disc of dough is starting to slide. Nothing has scattered yet. His hands read as real hands: five clearly separated fingers on each, correct proportions, and the two hands never touching or interlocking. The room is warm, expensive and well kept, the quality of a food-and-interiors magazine spread rather than a generic stock-photo pizzeria: no red-and-white checked tablecloths, no straw-covered wine bottles, no hanging garlic, no painted murals of Italy, no stainless-steel industrial kitchen, no fluorescent lighting. All pizza boxes are plain, unprinted and unbranded. Photorealistic, shot on ARRI Alexa Mini with spherical prime lenses, Kodak Vision3 500T look, warm naturalistic grade, soft contrast, fine organic grain, gentle vignette, shallow depth of field. Vertical 9:16 composition. No text overlays and no logos or brand names anywhere in the frame apart from the hand-painted sign described above.
```

---

## Etapa 2 — Os 6 vídeos

Em cada geração você anexa **o still da tabela + o mp3 daquele shot**. O still vira `@img1` daquela
sessão e o mp3 vira `@audio1`. O shot 6 não leva áudio.

**Todo prompt proíbe música e NOMEIA os efeitos sonoros.** O ambiente da pizzaria é um som contínuo, e
ele **muda de propósito ao longo da cena**: o murmúrio do salão cai quando o Chefe grita no 4, e no 5
a casa inteira está em silêncio ouvindo. Silêncio de gente constrangida é o melhor efeito sonoro da
cena, e é de graça.

**O fundo do Marquinho ANDA.** O mesmo still serve três planos, e se as gags fossem estáticas elas
repetiriam idênticas três vezes, o que entrega a reutilização na hora. Cada prompt move uma coisa
diferente, e o pedido de casamento avança um passo por clipe.

### Shot 1 — Marquinho abre o assunto
**Anexa:** `stills/marquinho-base.jpg` + `vozes/1.mp3` · Duração: **7s**

```
Using @img1 as the reference image for this exact frame, animate it. At the very start of the clip, as the voice begins, he comes out of the neutral resting position into the posture described next, and he holds that posture for the rest of the clip: he wipes his hand once down the front of his apron and rests that forearm on the counter, standing easily and almost normally, with a small thin half-smile on his face. He speaks the line captured in @audio1, his mouth moving naturally in sync with it. EVERYTHING DESCRIBED BELOW HAPPENS WHILE HE IS SPEAKING, not before the voice and not after it. As he talks his eyes flick up toward the person across the counter and drop back to the marble, his chin lowers a couple of degrees, and the half-smile thins slightly on the last words, settling flat as he finishes. Behind him the delivery rider in the doorway takes another bite of his slice and shifts his weight; out in the dining room the young man at the middle table is just lowering himself down onto one knee beside his date and reaching into his jacket pocket, and further back the pizzaiolo pushes the peel forward and out of frame while a waiter starts across the room with two pizzas. No background music and no musical score of any kind. Diegetic sound only, and all of it mixed very low and well under the voice, and specifically: the dry scuff of his hand on the canvas apron, a light knock of his forearm on stone, the constant soft roar of the wood fire, a low murmur of conversation from the dining room, and cutlery on plates.
```

### Shot 2 — Chefe, ele já sabe
**Anexa:** `stills/chefe-base.jpg` + `vozes/2.mp3` · Duração: **6s**

```
Using @img1 as the reference image for this exact frame, animate it. At the very start of the clip, as the voice begins, he comes out of the neutral resting position into the posture described next, and he holds that posture for the rest of the clip: he leans forward onto the counter with one forearm and his face opens into a broad knowing grin with the eyes creased, like a man who already knows the answer and is asking only to hear it again. He speaks the line captured in @audio1, his mouth moving naturally in sync with it, grinning throughout. As he talks he brushes the flour off one palm against his hip and lets that hand turn over loosely in the air, low and well clear of his face, his eyebrows lifting on the last words and staying up as he finishes. Behind him the pizzaiolo slides the peel into the oven mouth and the fire flares brighter for a moment. No background music and no musical score of any kind. Diegetic sound only, and all of it mixed very low and well under the voice, and specifically: a soft puff of flour off his hands, the scrape of the peel on the oven floor and the fire flaring, the constant soft roar of the wood fire, and a low murmur of conversation from the dining room.
```

### Shot 3 — Marquinho entrega a cidade
**Anexa:** `stills/marquinho-base.jpg` + `vozes/3.mp3` · Duração: **6s**

Mesmo still do shot 1, um degrau abaixo na energia. **É aqui que a régua do contido mais importa:**
nada de ombro subindo, careta ou gesto de desculpa. Só o olhar que desce e a voz que baixa.

```
Using @img1 as the reference image for this exact frame, animate it. At the very start of the clip, as the voice begins, he comes out of the neutral resting position into the posture described next, and he holds that posture for the rest of the clip: he stands very slightly back from the counter with both arms low and loose, his weight settled onto one leg, his chin dropped a little. He speaks the line captured in @audio1, his mouth moving naturally in sync with it. EVERYTHING DESCRIBED BELOW HAPPENS WHILE HE IS SPEAKING. As he talks the smile simply stops and his mouth settles flat, his eyes drop to the marble in front of him and stay down through the last words, and one finger presses closed against the stone and opens again. He stays looking down at the counter with his mouth flat as the clip ends. Behind him the delivery rider is still in the doorway working through his slice, and out in the dining room a waiter crosses the room carrying two pizzas and passes directly in front of the man on one knee at exactly the wrong moment. No background music and no musical score of any kind. Diegetic sound only, and all of it mixed very low and well under the voice, and specifically: the light tap of his fingertip on stone, the constant soft roar of the wood fire, and a low murmur of conversation from the dining room that thins slightly toward the end.
```

### Shot 4 — A explosão
**Anexa:** `stills/chefe-pico.jpg` + `vozes/4.mp3` · Duração: **7s**

**Este prompt não abre por postura:** ela já está travada no still. O trabalho aqui é manter a fúria
viva durante a fala inteira sem que a câmera perca a boca.

```
Using @img1 as the reference image for this exact frame, animate it. He roars the line captured in @audio1, his mouth moving naturally in sync with it, his face and mouth staying fully visible, sharp, in focus and unobstructed from the first frame to the last. EVERYTHING DESCRIBED BELOW HAPPENS WHILE HE IS SPEAKING. His raised hand shakes once in the air on the stressed word and stays up, open and turned toward the ceiling, the fingers spread; his weight drives further forward onto the planted hand and the marble takes it; his head pushes a few degrees closer to the other man across the counter; a small puff of flour lifts under the planted palm. He holds the roar and the raised hand through the very last word and stays braced there. The camera slams a short punch-in toward him that lands inside the first two or three frames and snaps to a dead stop, and it is already moving as he is two or three words into the line, never before the voice. Behind him the pizzaiolo stops dead with the peel half raised and turns his head toward the noise, and in the dining room beyond two of the diners look up from their plates. No background music and no musical score of any kind. Diegetic sound only, and all of it mixed very low and well under the voice, and specifically: the dull slap of his palm on marble, a soft puff of flour, and the constant roar of the wood fire, with the murmur of conversation from the dining room dropping away almost to nothing as he shouts.
```

### Shot 5 — O detalhe gratuito
**Anexa:** `stills/marquinho-base.jpg` + `vozes/5.mp3` · Duração: **5s**

Terceiro plano do mesmo still, e o mais baixo de energia da cena. **O áudio é o mais curto (~4s):**
ele já vem com um beat de silêncio na frente, e é esse silêncio que dá a pausa constrangida.

```
Using @img1 as the reference image for this exact frame, animate it. The voice in the reference audio starts at the very first frame of the clip and plays exactly as recorded, at its natural pace, with no added pause, no stretching, no slowing and no silence inserted anywhere inside it. At the very start of the clip he comes out of the neutral resting position into the posture described next and holds it for the rest of the clip: standing straight but small, both hands flat and still on the counter well apart from each other, shoulders level and down. He speaks the line captured in @audio1, his mouth moving naturally in sync with it, very quietly. As he talks he swallows once, his eyes come up to the other man for a fraction of a second and go straight back down to the marble, and his mouth settles flat and stays flat. He stays looking down as the clip ends. Behind him the delivery rider quietly steps back out through the side doorway and disappears, and out in the dining room the woman at the middle table says yes and throws her arms around the kneeling man while nobody else in the restaurant notices, because they are all turned toward the argument. No background music and no musical score of any kind. Diegetic sound only, and all of it mixed very low and well under the voice, and specifically: his swallow, the faint creak of the side door, and the constant soft roar of the wood fire, with the dining room now almost completely silent.
```

### Shot 6 — O pulo
**Anexa:** `stills/chefe-pulo.jpg` · **sem áudio** · Duração: **5s** (o piso)

Sem fala, e é o clipe que mais precisa das duas defesas contra slow motion. **Na montagem você usa
uns 1,5s disso**: o rescaldo existe pra ocupar o clipe, não pra entrar no corte.

```
Using @img1 as the reference image for this exact frame, animate it. The clip has two clearly separate parts, in this order. THE ACTION, violent and over almost immediately: he launches himself forward across the marble counter in one explosive movement, driving off both planted hands, and passes straight out of the left side of the frame without ever making contact with anything on screen; the flour on the counter erupts upward into a thick white cloud where his hands and knee pushed off, the wooden peel spins away and the disc of dough is flung off the edge. Everything plays at full real-time speed: absolutely no slow motion, no slow-motion ramp, no speed ramping and no dramatic slowdown at any point, and no floating or hanging in the air. THE AFTERMATH, filling the rest of the clip: the frame is left on the empty counter with the flour cloud billowing, drifting and slowly settling back down through the warm light of the oven, a pizza box sliding to a stop at one end, and further back the pizzaiolo and the diners frozen mid-gesture staring toward where he went, one hand halfway to a mouth. The camera holds static throughout and does not follow him out of frame. No background music and no musical score of any kind. Diegetic sound only, and specifically: the heavy scuff and thud of his weight going over the marble, the clatter of the wooden peel hitting the floor, and the constant roar of the wood fire, with the whole dining room silent.
```

---

## Depois de gerar

- **Confira os 4 stills antes de gerar qualquer vídeo.** Um still errado que passa vira três clipes
  errados, porque o still-base serve três shots.
- **Meça a fala dentro de cada clipe antes de cortar**, e não pelo relógio do mp3: o modelo às vezes
  empurra a fala pra frente pra abrir espaço pro beat de atuação.
- **Ouça cada clipe.** Efeito sonoro que voltou sem ter sido pedido também não estava no roteiro.
