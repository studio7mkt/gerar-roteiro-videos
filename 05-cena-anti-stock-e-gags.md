# 05 — Regras de cena: anti-stock e gags de bastidor

Vale pra **toda imagem e todo vídeo**, gerado ou fotografado. Duas doutrinas que andam juntas,
porque atacam o mesmo problema por lados opostos: **a imagem que ninguém para pra olhar.**

- **Anti-stock** tira o que faz a imagem parecer catálogo.
- **Gag de bastidor** põe o que faz a pessoa voltar e olhar de novo.

---

## Parte 1 — Anti-stock

### Por que a imagem sai com cara de banco de imagem

O gerador não erra: ele acerta **a média**. Pedir "atendente ajudando cliente numa loja" devolve a
média de milhares de fotos de banco de imagem, que é exatamente o que o dataset tem mais. E foto de
banco de imagem tem uma assinatura reconhecível, que o público já viu dez mil vezes e descarta em
meio segundo:

- **Todo mundo posa.** Figurante a três quartos, sorrindo pra coisa nenhuma, esperando a foto
  acontecer.
- **O lugar está vazio de gente demais.** Loja recém-inaugurada onde ninguém entrou, escritório sem
  um casaco no encosto, sala de espera com as cadeiras alinhadas com régua.
- **A composição é simétrica e centrada**, com o assunto inteiro no quadro e nada perto da lente.
- **A luz não tem fonte.** Vem de todo lado, macia, sem sombra que denuncie janela ou luminária.
- **A óptica é perfeita:** foco infinito, zero grão, zero vinheta, zero aberração.
- **A cena é uma CATEGORIA, não um momento.** "Atendimento ao cliente" em vez de "a senhora tirou o
  óculos pra ler a tela".

A pesquisa de mercado bate com isso: busca por `unfiltered`, `candid` e `authentic lifestyle` passou
`professional`, `clean` e `studio`. O que vende é justamente o que o gerador entrega pior: pessoa
real, em lugar real, com expressão real.

### As 5 travas, e as cinco entram em todo prompt

**1. Momento específico, nunca categoria.** Descreva o instante, não a atividade. Não "o robô atende
a cliente", e sim "a caixa já está virada de cabeça pra baixo e o dedo dele está parado num ponto
específico embaixo dela, e a cliente inclinou pra ver". Momento tem antes e depois; categoria não tem
nada.

**2. Ninguém posa e ninguém olha pra lente** (exceto quem apresenta). Figuração é sempre pega no meio
de alguma coisa: de costas, cortada pela borda do quadro, no meio de um passo, no meio de uma risada.
Escreva isso explicitamente, porque o default do gerador é o contrário.

**3. Camada de primeiro plano.** Alguma coisa perto da lente, desfocada, cortada pelo quadro: a quina
de um monitor, uma folha de planta, o ombro de alguém passando, a borda de um balcão. **É a trava que
mais funciona**, porque ela prova que a câmera está DENTRO do lugar, e não plantada na frente dele.

**4. O lugar tem que parecer que alguém esteve nele hoje, e ainda assim ser bonito.** Aqui mora o
erro mais fácil de cometer: traduzir "usado" como "sujo" e devolver uma clínica encardida de luz
fluorescente esverdeada. **Bagunçado não é antônimo de bonito.**

**Uso é vestígio de GENTE, não desgaste de MATERIAL.**

| ✅ Isso é uso, e deixa a imagem viva | ❌ Isso é feiura, e derruba a imagem |
|---|---|
| casaco no encosto da cadeira, revista aberta, mochila no chão | mancha, encardido, mofo, marca de dedo no vidro |
| xícara ainda fumegando, copo pela metade, caderno aberto | caneca encardida, copo velho jogado no chão |
| cadeiras fora de esquadro, caixa entreaberta com produto novo | rachadura, tinta descascando, ferrugem, remendo de fita |
| planta viva e bem cuidada, flores no balcão | planta morta, planta murcha |
| adesivo no notebook, bicicleta encostada, pilha de cadernos | cartaz torto e amarelado colado com durex |
| luz quente de janela ou de luminária boa | fluorescente esverdeado, luz de repartição pública |

**E o cenário em si é sempre BONITO:** arquitetura boa, material bom, luz boa. A régua é revista de
interiores, e ela vale até no cenário do vilão. Quando o lugar precisa ser precário, **quem é feio é
o objeto da cena, nunca o lugar**: um robô de sucata numa sala bonita e bagunçada conta a história
melhor do que o mesmo robô num cubículo imundo, porque aí ele é a única coisa errada no quadro.

**5. Óptica de câmera de verdade.** Grão fino, leve vinheta, um pouco de aberração cromática nas
altas luzes, profundidade rasa com algo fora de foco, e **luz com fonte identificável** (janela à
esquerda, luminária de mesa à direita). Nomeie a fonte: softbox invisível é a assinatura do stock.

### A régua final, antes de aceitar a imagem

**Dá pra imaginar essa foto num banco de imagem?** Se dá, ela não vai pro ar. Não importa se está
bonita: bonita e genérica é exatamente o produto que o público aprendeu a ignorar.

---

## Parte 2 — Gags de bastidor

**Toda cena carrega uma coisa engraçada acontecendo atrás.** Não é enfeite: é o mecanismo de retenção
mais barato que existe. Uma piada no fundo faz a pessoa parar, voltar e olhar de novo, e é a
diferença entre "vi" e "assisti duas vezes".

O nome disso em animação é **funny background event**, e o efeito depende de o primeiro plano seguir
sério: a piada mora atrás, enquanto a conversa continua na frente.

### ⚠️ No máximo DOIS elementos de atenção por cena

A regra que custou uma bateria de testes pra aprender: **prompt entupido de detalhe não é
executado.** O gerador tem um orçamento de atenção, e uma lista de dez coisas específicas faz ele
escolher três ao acaso e ignorar o resto, incluindo, muitas vezes, justamente a gag.

**Dois elementos, e só dois:** a gag, mais um segundo achado que dê vida (um letreiro, um bicho, um
objeto improvável). O resto do cenário fica **simples e calmo de propósito**, porque é o vazio em
volta que faz os dois aparecerem.

**Escreva numerado, e feche com a negação.** O gerador obedece muito melhor a duas coisas nomeadas do
que a uma lista solta:

> `Exactly two things in this room are meant to catch the eye, and they are these. FIRST: <o achado>.
> SECOND: <a gag>. Apart from those two the rest of the room stays simple and calm, with no other
> props, notices or clutter competing for attention.`

**Dois é TETO, não cota.** Cena que já é cheia por natureza (uma sala de aula lotada, uma plateia de
pé) roda melhor com UM elemento; cena que existe pra ser vazia (um estúdio, um ciclorama) também. Só
encha até dois quando o segundo realmente acrescenta.

**O que é ASSUNTO não conta como elemento.** A dupla que prova o argumento, a chave passando de mão,
a plateia aplaudindo: isso é a fala acontecendo, é o motivo do plano existir. Elemento de atenção é o
que a pessoa acha **depois** de entender o plano.

### As três camadas de um fundo rico

Quando o plano abre e sobra sala no fundo, o teto de dois continua valendo. **O que muda não é o
número de gags, é a NITIDEZ delas.** Seis piadas igualmente legíveis no mesmo quadro não é fundo
rico, é bagunça: o olho não sabe pra onde ir, o protagonista some, e o gerador começa a fundir os
elementos uns nos outros.

| Camada | Nitidez | O que ela faz |
|---|---|---|
| **1. A gag principal** | legível de primeira, mesmo no celular | é a piada que todo mundo pega |
| **2. A gag de replay** | visível mas suave, precisa de meio segundo de atenção | é o que faz o vídeo ser reassistido |
| **3. A vida da casa** | fora de foco, pequena, quase textura | mata a cara de cenário vazio sem roubar atenção |

**Só a camada 1 compete com o protagonista.** A camada 3 não é gag, é ruído com graça: se o
espectador pegar, ganhou; se não pegar, o quadro só parece um lugar de verdade. É por isso que ela
pode ter quatro coisas sem estourar o teto.

### Como enxugar um prompt que já está entupido

Não reescreva do zero: **apague**, nesta ordem, que é a ordem do que menos custa perder.

1. **O terceiro elemento de atenção.** Sempre existe um, e ele quase sempre é o mais fraco dos três.
2. **As marcas de uso que sobram.** Elas disputam o mesmo orçamento que a gag. **Uma por cena
   basta.** Cinco listadas viram zero executadas.
3. **A figuração repetida.** Três duplas trabalhando ao fundo leem pior que uma dupla em foco, e
   custam três vezes mais atenção.
4. **O prop que só enfeita.** Vaso de flor, caneta no barbante, xícara na pia: some no resultado toda
   vez, e cada um custava uma vaga.

**O que nunca sai:** a camada desfocada no primeiro plano e a fonte de luz nomeada.

### O letreiro é a gag mais barata que existe

**Modelo bom escreve texto certo hoje**, e isso abre a categoria de piada mais eficiente de todas: o
**nome do lugar**. "CLÍNICA ENTRE PATAS & PÊLOS" numa parede dá mais vida e mais graça que qualquer
prop, é de bom gosto, e ainda situa a cena sem uma palavra de narração.

**E ele é o elemento mais barato do orçamento**, porque faz dois trabalhos numa coisa só: entrega a
piada e explica onde a cena se passa. Num plano que já tem uma gag física, o letreiro é quase sempre
o melhor segundo elemento.

| Onde | O que faz | Exemplo |
|---|---|---|
| placa ou letreiro do lugar | nome fictício, e a segunda linha carrega a piada | `EMPÓRIO DO SEU ORLANDO` / `DESDE TERÇA` |
| relógio na parede | informa e argumenta ao mesmo tempo | `03:14` numa cena de "atende 24 horas" |
| cardápio de quadro-negro | um item improvável no meio dos normais | |
| camiseta de uniforme, crachá, caneca | dá personagem a um figurante sem uma fala | |
| quadro branco ao fundo | o que alguém desenhou ali no meio do trabalho | |

**Peça a frase exata, em caixa alta, com `reads exactly`**, e diga que ela está bem iluminada e
legível. Nunca deixe o modelo inventar o texto.

⚠️ **Acento é a primeira coisa que cai.** Peça `correctly spelled and correctly accented` e, se cair
mesmo assim, **regere o still**.

⚠️ **Nome fictício, sempre.** Marca real é compliance, não estética.

⚠️ **O letreiro que carrega a regra da cena é o item mais frágil da produção.** Se a piada depende
de uma placa dizendo "ENTREGAMOS SÓ NO BAIRRO" e ninguém verbaliza isso em nenhuma fala, um letreiro
ilegível não deixa a cena feia: deixa a cena **sem sentido**. Confira letra por letra, e confira em
todos os planos em que ele aparece.

### As 6 regras da gag

**1. Uma por plano, e ela acontece ATRÁS.** Duas gags competem entre si e a pessoa não vê nenhuma. O
segundo elemento de atenção **não é uma segunda piada**: é um achado que dá vida. E gag no primeiro
plano rouba a fala, que é o que o plano existe pra entregar.

**2. É uma AÇÃO em curso, não uma pose.** "O robô martelando o próprio dedo" e não "o robô segurando
um martelo". Pose não tem piada porque não tem tempo; ação tem o instante antes e o depois.

**3. Legível em dois segundos, em tela de celular.** Silhueta clara, contraste com o fundo, escala
grande o suficiente. Detalhe minúsculo não é gag, é desperdício.

**4. Improvável, mas possível naquele lugar.** É a mecânica inteira: um robô regando uma planta de
plástico, um porta-retrato na baia com a foto de uma torradeira, um robozinho no banco do motorista
sem alcançar os pedais. Coisa impossível vira alucinação; coisa comum não é piada.

**5. O alvo é a situação ou o incompetente da história, nunca a audiência e nunca o cliente.**

**6. A gag não contradiz o argumento do plano.** No plano que prova competência, ela é fofa. No plano
que mostra o problema, ela é o desastre. Gag que desmente o que a fala está afirmando mata a venda
pra ganhar uma risada.

### O que multiplica: a gag recorrente

Uma gag que **volta** ao longo da peça vale mais que três gags soltas. O personagem espia pela borda
do quadro no primeiro plano, reaparece no meio, e paga no último. Quem viu uma vez pega o fio na
segunda, e é isso que gera o comentário e o replay.

### Como pedir no prompt

Escreva a gag como parte do cenário, no mesmo tom do resto, **com a ação no ponto certo**: a imagem
congela um instante, então congele o instante engraçado, não o segundo antes. E no prompt de vídeo,
**deixe a gag continuar em amplitude pequena**, porque é o movimento dela que faz o olho achar.

> `Behind them and off to one side, small in the frame but clearly readable: <a gag, escrita como
> ação em curso>.`

---

## E os dois juntos

Anti-stock sozinho entrega uma imagem que parece real e que ninguém comenta. Gag sozinha, num
cenário de catálogo, entrega uma piada que ninguém acredita. **Juntos, entregam a única coisa que
importa: uma imagem que a pessoa para pra olhar e depois volta.**
