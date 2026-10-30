# 03 — O prompt de still (a imagem inicial)

Escreva como **briefing pra um diretor de fotografia**, não como lista de objetos. Quanto mais o
prompt fala a língua de quem filma, mais o resultado parece frame de produção e menos parece render
de IA.

**A regra que organiza tudo:** o still decide **o que a cena É** (personagem, cenário, figurino,
luz, enquadramento, cor). O prompt de vídeo decide **o que MUDA**. Misturar as duas etapas é a
causa da maioria dos defeitos.

---

## 1. Os 7 blocos, nesta ordem

1. **Enquadramento e câmera** — plano (medium, close-up, wide), altura (eye-level, low angle), de
   que lado a câmera está, onde o sujeito cai no quadro.
2. **Proporção** — sempre declarada. Vertical é `Vertical 9:16 composition`, e a composição nasce
   pensada pra vertical, não é wide cortado.
3. **Cenário** — 3 a 5 elementos concretos, com profundidade (primeiro plano desfocado, meio,
   fundo).
4. **Sujeito** — pose, mãos, expressão, para onde olha. Detalhe físico, nunca adjetivo de emoção.
5. **Luz** — direção, temperatura, qualidade (dura ou difusa), contraluz, e a **fonte nomeada**.
6. **Óptica e textura** — lente, profundidade de campo, granulação, look de filme.
7. **Negativos explícitos** — `no text overlays, no logos, no other people in frame`.

**Nomear equipamento e filmstock reais é a instrução isolada mais potente.** O modelo entende o
comportamento tonal de `Kodak Portra 400` ou `Kodak Vision3 500T` muito melhor do que entende
"cores bonitas e quentes". Vale pra lente, câmera e esquema de luz.

**Cada prompt é standalone.** Repita o cenário inteiro em todo shot, mesmo que fique repetitivo: o
gerador não tem memória do shot anterior.

**Identidade de personagem entre shots:** gere o retrato de referência **uma vez** e passe-o como
imagem de referência em todos os stills (`@img1`, `@img2`), sem nunca redescrever rosto e corpo no
texto. Redescrever é o que faz o personagem mudar de cara entre planos.

---

## 2. Mão é o que mais quebra

Mão continua sendo o defeito número um de geração de imagem, e o caso pior é sempre o mesmo: **as
duas mãos se tocando.** Mão torcendo mão, dedos entrelaçados, as duas agarrando o mesmo objeto: são
dez dedos em contato pro modelo resolver, e ele inventa dedo, funde dedo ou entrega uma pinça sem
função.

1. **As duas mãos nunca se tocam no still.** Nada de `wringing`, `clasped together`,
   `fingers interlaced`.
2. **Assimetria.** Uma mão faz uma coisa simples contra uma superfície grande e plana (espalmada na
   mesa, no braço da cadeira); a outra fica solta ou **sai do quadro**. Mão que não aparece nunca
   sai errada.
3. **Mão longe do rosto.** Além da anatomia, mão perto da boca atrapalha a sincronia labial: o
   gerador anima a boca por baixo dela e embola.
4. **O gesto mora no prompt de VÍDEO, não no still.** O still segura a posição de repouso; quem
   levanta a palma, aponta e fecha o punho é o vídeo. Modelo de vídeo resolve mão em movimento
   melhor do que modelo de still resolve mão parada num gesto, e o movimento ainda esconde o
   defeito residual.

**E vale além da mão: pose armada denuncia imagem gerada.** `frozen half-raised`, corpo reto e
simétrico: tudo isso lê como manequim de vitrine. Peça naturalidade explicitamente, em todo still
de gente:

> `His hands read as real hands: five clearly separated fingers on each, correct proportions, and
> the two hands never touching, interlocking or fidgeting against each other. The whole pose is
> loose and asymmetric, the weight settled, like someone caught in the middle of a conversation
> rather than holding a position for a camera.`

### A exceção: contar N com a mão mora no STILL

Gerador de imagem obedece contagem de dedo; gerador de vídeo **não conta dedo**. Pedir
`four fingers spread` no prompt de vídeo devolve cinco dedos, e regerar não resolve.

**A correção é estrutural:** o still nasce com a mão já erguida mostrando quatro, com o polegar
dobrado na palma escrito no prompt de imagem, e o prompt de vídeo só **preserva**
(`THE HAND NEVER OPENS INTO A FIVE-FINGERED PALM AND THE THUMB NEVER COMES OUT`).

**Gesto que carrega informação (número, direção, contagem) entra no still; gesto que é só energia
continua no vídeo.** E se ainda assim sair errado, tire o número da mão: dedo mostrando 5 enquanto
a voz diz "4" é pior que gesto nenhum.

---

## 3. Rosto: se está longe, volta deformado

**Em plano que vai virar clipe com fala, a pessoa não pode estar distante da lente no still.** O
gerador gasta pixel proporcional ao tamanho do elemento no quadro, e rosto pequeno volta com
estrutura óssea errada, olho fora de lugar e semelhança perdida. Depois, o vídeo **anima o rosto
errado**.

**O sintoma é sempre o mesmo:** "ficou parecendo outra pessoa" num plano geral bonito. Não é o
personagem, não é o prompt de vídeo, é a distância.

**A régua:** o rosto ocupa pelo menos algo como um oitavo da altura do quadro. Na prática, **plano
médio (cintura pra cima) é o mais aberto que um plano falado aceita**, e o rosto tem que continuar
sendo o maior elemento do quadro. Se voltar uma foto de restaurante com um rapaz dentro, o plano
abriu demais.

**Quando o plano PRECISA ser aberto** (mostrar um prédio inteiro, uma multidão), a saída não é
afastar a câmera: é **começar fechado e abrir o quadro no vídeo**. O still nasce em plano médio e
o zoom out acontece no clipe. O modelo de vídeo extrapola o que está fora do quadro muito melhor do
que o de imagem resolve um rosto de cinquenta pixels.

---

## 4. Testa lisa: ruga não é expressão, é textura

O gerador de vídeo **não desfaz um sulco que já está no pixel**. Testa franzida, sobrancelha
erguida, pé de galinha de careta: tudo isso fica congelado do primeiro ao último quadro, e o
personagem passa a fala inteira com a mesma cara. É um dos defeitos que mais denuncia clipe gerado.

A régua tem dois lados:

- **Expressão de PICO vai travada na imagem** (a fúria, o susto, a ofensa). É o único jeito de ela
  existir.
- **Expressão SUTIL nasce neutra**, com a testa lisa, e vem do que o modelo mexe durante a fala:
  olhar, canto da boca, ombros, mãos. No still:
  `forehead completely smooth and relaxed with no frown lines, eyebrows level and unfurrowed`.

A confusão é fácil: constrangimento, dúvida e culpa **parecem** pedir testa franzida, mas o
resultado é uma careta parada por sete segundos.

**Ruga de idade não conta:** sulco permanente num personagem de cinquenta anos é anatomia, não
atuação, e fica.

---

## 5. Robô, mascote e criatura amigável

Pedir `friendly humanoid robot with human proportions` devolve, com consistência incômoda, um
manequim de cerâmica com peito e clavícula, cabeça lisa e dois pontos acesos no lugar dos olhos.
**A palavra `humanoid` não pede simpatia, pede anatomia**, e anatomia humana em material errado é a
definição de vale da estranheza.

1. **Proporção de brinquedo, nunca humana.** `cute toy-like proportions`, cabeça arredondada
   valendo um terço da altura, corpo em cápsula, membro curto e roliço em junta de bolinha. E negue
   o resto: `no human anatomy of any kind`. As palavras `humanoid` e `human proportions` ficam fora.
2. **Dê uma boca.** `No mouth` parece design limpo e é o oposto: sem boca o rosto não tem por onde
   ser amigável, e o que sobra é máscara. A solução barata é **uma tela escura ocupando a cara
   inteira**, com dois olhos redondos grandes e um sorriso em arco desenhados nela.
3. **Nada de mão humana.** Mão de três dedos gordinhos, tipo luva. É a mão que o gerador acerta.
4. **Declare a altura em relação a uma pessoa** (`about shoulder height on a grown adult`). Sem
   isso o modelo alterna entre bibelô e coisa de três metros de um plano pro outro.

**A tela do rosto compra uma vantagem técnica de graça:** sorriso que alarga, olho que brilha mais
forte, uma piscada. É emoção em amplitude minúscula, que é exatamente o que o gerador consegue
executar enquanto está ocupado com a boca.

**Escada de qualidade é o MESMO design em N estados, nunca N designs.** Quando o plano mostra
evolução (do tosco ao bom), mantenha a silhueta idêntica em todos os degraus e varie só material,
cara acesa ou apagada, luz e postura. N designs diferentes lado a lado leem como prateleira de
loja; um design em N estados lê como escada.

---

## 6. Quando o modelo tem um default teimoso

Todo gênero tem um cenário que o dataset entrega sozinho. Fantasia épica com fogueira à noite vira
**floresta de pinheiros** quase sempre, mesmo com "desfiladeiro rochoso" escrito no prompt.
Pizzaria vira cantina de toalha xadrez. Escritório vira open space de banco de imagem.

Três defesas, em ordem de força:

1. **Abra o prompt com a locação em CAIXA ALTA.** O que vem primeiro pesa mais, e o modelo trata o
   resto como detalhe.
2. **Descreva a matéria, não o nome.** "Paredão de pedra cinza rachada, cascalho e pedregulho no
   chão" segura muito mais que "desfiladeiro rochoso". Nomear é fraco; descrever textura e material
   é forte.
3. **Negue o default explicitamente.** `Absolutely no trees and no vegetation anywhere in the shot`
   é a defesa que mais funciona, e a única que costuma resolver quando as outras duas falham.

**Nunca aceite o shot desviado "porque ficou bonito".** Um shot fora do cenário no meio de doze
certos só aparece na montagem, quando refazer já custa caro.

---

## 7. Objeto que volta errado não pede adjetivo, pede PLANO, CÂMERA e METRO

O caso clássico é a mesa: "ele do lado oposto de uma mesa de escritório, câmera do outro lado".
Voltou **bancada de refeitório** cinco vezes seguidas, com quatro travas empilhadas no prompt. Duas
delas trabalhavam contra o pedido: `runs away into the picture` é literalmente o pedido de uma mesa
comprida em fuga, e a negação em caixa alta mantém "mesa" no topo da atenção o clipe inteiro.

Encurtar pra uma frase com medida consertou o tamanho e não a posição. Porque `far side`,
`near edge` e `the opposite side of it` são **relação espacial abstrata**, e gerador de imagem não
resolve geometria abstrata: ele resolve **nome de plano** e **ordem de profundidade**.

**A ordem que funciona, e é ela que se copia pra qualquer objeto teimoso:**

1. **Nome de plano que existe em cinema**, em caixa alta, abrindo o bloco:
   `THIS IS THE REVERSE ANGLE OF A CONVERSATION ACROSS AN OFFICE DESK.` O dataset tem milhares
   dessas imagens, e isso sozinho já põe a câmera no lugar.
2. **A posição da câmera dita como PESSOA**, não como coordenada: `the camera is placed exactly
   where the seated boss would be, on his side of the desk, at eye level`.
3. **Ordem de profundidade explícita:** `the near edge of that desktop is the nearest object in the
   whole shot`. É isto que impede o objeto de escorregar pro lado.
4. **Orientação e dimensão:** `runs straight across the very bottom of the frame, horizontal and
   level, left to right` + `about two metres wide`.
5. **Só então a negação**, curta: `nothing runs away from the camera into the depth of the picture`.

**Adjetivo e negação são a última linha, não a primeira.**

---

## 8. Texto na imagem: depende do modelo

**Modelo bom escreve texto certo hoje.** A proibição automática de texto é herança de gerador
antigo, e onde ela continua valendo é em geração local mais fraca, que escreve garrancho em
qualquer superfície plana.

Quando dá pra usar, texto é um dos recursos mais fortes contra a cara de banco de imagem: o nome do
lugar numa placa situa a cena, dá vida e ainda pode carregar a piada.

**Peça a frase exata, em caixa alta, com `reads exactly`:**

> `mounted on the wall above the counter, a clean modern sign in warm brass sans-serif capitals
> reads exactly CLÍNICA ENTRE PATAS & PÊLOS, correctly spelled and correctly accented, well lit and
> easy to read.`

**Acento é a primeira coisa que cai.** Circunflexo e til somem com frequência. Peça
`correctly spelled and correctly accented` e, se cair mesmo assim, **regere o still**: letreiro
retocado à mão numa peça de treze imagens aparece no primeiro corte de escala.

**Nome fictício, sempre.** Marca real (logo, marca registrada, emblema de carro, embalagem de
produto de verdade) continua proibida em qualquer modelo. Isso é compliance, não estética, e é
motivo de reprovação de anúncio.

---

## 9. Prompt entupido não é executado

O gerador tem **orçamento de atenção**. Dez detalhes específicos numa cena fazem ele escolher três
ao acaso e ignorar o resto, e o que costuma cair é justamente o detalhe que você mais queria.

**Dois elementos de atenção por cena, no máximo**, numerados e seguidos da negação. A doutrina
completa, com o passo a passo de como enxugar um prompt já entupido, está em
[05-cena-anti-stock-e-gags.md](05-cena-anti-stock-e-gags.md).
