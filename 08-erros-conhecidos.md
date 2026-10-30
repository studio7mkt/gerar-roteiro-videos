# 08 — Erros conhecidos

Tudo que já quebrou uma produção, com a correção de cada um. Consulte antes de diagnosticar um
resultado ruim: quase todo defeito de vídeo gerado está nesta lista.

---

## Roteiro e decupagem

| Erro | O que acontece | Correção |
|---|---|---|
| Escrever a cena, o storyboard e os prompts antes de o diálogo estar aprovado | a primeira troca de fala joga fora o documento inteiro, porque todo o resto depende dela | entregue as falas primeiro, sozinhas, e monte o resto só depois do OK |
| Bloco corrido de diálogo em vez de shot a shot | esconde a fala longa demais até a hora de gerar, quando o still já foi pago | um shot por fala, com contagem de palavras e duração |
| Fala de 30 palavras | passa de 10s e não cabe em clipe nenhum | quebre em dois shots: é decupagem, não corte de texto |
| Fala de 7 palavras num clipe com piso de 5s | o modelo insere pausa **dentro** da fala e devolve um "Chefe........ eu me demito" | grave silêncio nas duas pontas do próprio mp3, e nunca estique o áudio depois |
| Misturar prompt em inglês dentro do roteiro | a pessoa lê prompt quando queria ler cena, e o mesmo texto passa a existir em dois lugares | roteiro em português natural, prompts em arquivo separado |
| Entregar o absurdo inteiro na primeira fala | a escalada não tem degraus e a cena morre no meio | um absurdo por fala, cada um derrubando a reação um nível |
| Terminar a esquete em fala | não fecha; falta o soco final | a cena fecha em corpo, na virada física, congelada no auge ou cortada seca |
| Dois personagens escrachados na mesma cena | vira desenho animado e o público para de acreditar nos dois | um exagerado por cena; o outro é contido, e é o contraste que faz a graça |

---

## Assets e storyboard

| Erro | O que acontece | Correção |
|---|---|---|
| Um still próprio pra cada shot | doze rostos ligeiramente diferentes, doze conferências, e deriva que só aparece na montagem | still-base neutro por personagem, reutilizado; still próprio só onde a diferença é textura |
| Still-base com emoção desenhada | a emoção fica congelada em todos os clipes que saírem dele | still-base nasce neutro: testa lisa, sem sorriso, sem tensão |
| Dois personagens no mesmo quadro num shot com fala | a sincronia labial arruína os dois | um personagem por imagem; o diálogo se resolve no corte |
| Trocar o lado do quadro no meio da cena | os dois parecem estar olhando pro mesmo canto vazio | ângulo fixo por personagem, do primeiro ao último shot |
| Dois picos de emoção com stills parecidos demais | o espectador lê como o mesmo plano repetido | mude a altura da câmera, o figurino desarrumando, a distância |
| Pular degrau na escalada física | o pico seguinte não tem pra onde ir e a virada vira repetição | um still por degrau, e cada um mais alto que o anterior |
| Confundir a numeração de `@img` entre etapas | o clipe sai com o still do shot errado, e só aparece na montagem | `@` é a ordem em que você anexa **naquela** geração, e reseta a cada uma |

---

## Prompt de still

| Erro | O que acontece | Correção |
|---|---|---|
| As duas mãos se tocando | dez dedos em contato pro modelo resolver: dedo a mais, dedo fundido, pinça sem função | mãos nunca se tocam; uma faz algo simples contra superfície plana, a outra sai do quadro |
| Gesto congelado no still | lê como manequim de vitrine, e fica assim o clipe inteiro | still em repouso + `loose and asymmetric`; o gesto vai no prompt de vídeo |
| Pedir contagem de dedos no prompt de vídeo | o modelo de vídeo não conta dedo: pede quatro, volta cinco | o número mora no STILL, com o polegar dobrado escrito; o vídeo só preserva |
| Rosto pequeno num plano que vai ter fala | volta com estrutura óssea errada e semelhança perdida, e o vídeo anima o rosto errado | plano médio é o mais aberto que um plano falado aceita; abra o quadro no vídeo, não no still |
| Testa franzida num still de emoção sutil | a ruga fica congelada os sete segundos e o personagem faz a mesma careta a fala toda | testa lisa no still; a emoção sutil vem de olhar, boca, ombros e mãos, no prompt de vídeo |
| `humanoid` + `human proportions` + `no mouth` num robô "amigável" | volta um manequim de cerâmica com anatomia humana e cara de máscara | `cute toy-like proportions`, `no human anatomy of any kind`, e uma boca desenhada na tela do rosto |
| Escada de qualidade feita com N designs diferentes | lê como prateleira de loja, não como evolução | o MESMO design em N estados; varie só material, cara acesa, luz e postura |
| Nomear a locação e confiar que ela vai sair | o modelo entrega o default do gênero (fantasia + fogueira = floresta de pinheiros, toda vez) | locação em CAIXA ALTA na abertura + matéria descrita fisicamente + negação explícita do default |
| Empilhar travas sobre um objeto de cenário que volta errado | duas delas trabalham contra o pedido, e a negação em caixa alta mantém o objeto no topo da atenção | nome de plano de cinema → câmera dita como pessoa → objeto mais próximo da lente → dimensão em metros; negação por último |
| Prompt de still sem proporção | composição horizontal cortada no 9:16 | declare a proporção e componha vertical |
| Redescrever rosto em vez de usar imagem de referência | o personagem muda de cara entre shots | retrato de referência + `@imgN`, e zero descrição de rosto |
| Pedir "lugar bonito" e aceitar o primeiro resultado | o modelo entrega o genérico da categoria, que lê como banco de imagem | nomeie a arquitetura e escreva a régua: `architecture-magazine quality, not a generic stock photo` |
| Still que já tem alguém caindo | o clipe herda a queda sem causa e ela vira o default do movimento | figurantes `all upright, none falling` no prompt do still |
| Proibir texto por hábito | joga fora o recurso anti-stock mais forte que existe (o nome do lugar numa placa) | em modelo bom, peça a frase exata com `reads exactly` |
| Aceitar um letreiro com acento faltando | ele aparece em cinco planos e o retoque some no primeiro corte de escala | `correctly spelled and correctly accented`, e regere o still se cair |

---

## Prompt de vídeo

| Erro | O que acontece | Correção |
|---|---|---|
| Redescrever a cena | instrução concorrente com o pixel: deriva de identidade e de cenário no meio do clipe | só o que muda |
| Referenciar outro shot ou o arco da cena | o modelo não viu o outro shot; a frase vira ruído | prompt auto-contido, só o que está neste quadro |
| Escrever a correção como contraste ("pensativo em vez de debochado") | injeta o conceito errado no prompt e ele aparece ponderado no resultado | só o estado final desejado, afirmativo |
| Meta-comentário de direção ("selling the scale", "this shot is about dread") | o modelo renderiza pixel, não intenção | traduza a intenção no fato visível que a produz |
| Negar atuação (`nothing else about him moves`) | volta um ator parado, sem expressão, sem vida: é a instrução que o modelo cumpre melhor | contenção é uma corrente de três ações pequenas e afirmativas, com ponto de chegada |
| Negar estilo (`never a slow drift`) | restrição vazia que ainda planta a palavra indesejada | declare o prazo e o rastro: `lands inside the first two or three frames`, `streaked with motion blur` |
| Carimbar uma negação pontual em todos os prompts | ela atravessa contextos onde é falsa e passa a brigar com uma instrução positiva do mesmo prompt | negação tem causa ativa **neste** plano, ou é cicatriz e se apaga |
| Pronome no lugar do rótulo ("he says") | o modelo troca de personagem | `[Rótulo, emoção]:` sempre |
| Três ações no mesmo clipe | nenhuma delas fica boa | um beat por clipe, corte a mais |
| Pedir "só depois que a fala acabar" em prosa | o modelo lê como sugestão e golpeia no meio da frase, matando a sincronia | declare `FIRST HALF: ... SECOND HALF, beginning only once the voice has completely stopped: ...` |
| Movimento de câmera que termina antes da fala | o clipe volta com um segundo de silêncio parado no começo, e cortar isso mata o efeito | bloco de TIMING abrindo o prompt: movimento e fala travados um no outro |
| Pedir "orbit" | a câmera passa por trás e o plano vira nuca | 45 graus no total, o personagem gira junto, e a trava mensurável: os dois olhos visíveis em todo frame |
| Dolly ou travelling num clipe que nasce de still | o modelo arrasta o sujeito junto com a câmera, amarrado na lente | prefira zoom/push (movimento de escala), ou declare `her feet stay planted and the camera does all of the work` |
| Fechar todo prompt com `camera holds static` | frase morta: o default do image-to-video já é câmera parada | declare a câmera só quando quiser movimento |
| Ação de meio segundo num clipe de 5s | o modelo estica a ação e devolve slow motion | negue o slow motion explicitamente E escreva o rescaldo pra ele ocupar o tempo que sobra |
| Repetir a fala em português no prompt de vídeo | instrução concorrente com o áudio | a fala já está no mp3; o prompt só cita a referência |
| Beat de atuação ou gag **antes** ou **depois** da fala | é exatamente o pedaço que a edição corta: geração paga e jogada fora | `EVERYTHING DESCRIBED BELOW HAPPENS WHILE HE IS SPEAKING` |
| Áudio curto num clipe com piso de 5s | o modelo preenche o buraco inserindo pausa dentro da fala | trava na primeira linha: a voz começa no primeiro quadro, `no added pause, no stretching` |
| Deixar o gerador escolher a trilha | volta música no tempo do clipe, que não casa com o corte e não tem stem pra separar | proibir música no fim de todo prompt, sempre |
| Pedir efeito sonoro genérico | o modelo devolve clipe mudo ou um som errado qualquer | liste os sons um a um, e declare a camada de ambiente do lugar |
| Listar sons sem declarar o volume | o ambiente compete com a fala e o plano fica sem inteligibilidade no celular | `all of it mixed very low and well under the voice`, e corte da lista o que disputa faixa |
| Figuração parada no still e parada no clipe | vira manequim ao fundo, e manequim denuncia vídeo gerado | diga o que a figuração faz naquele clipe, em movimento pequeno, e faça ela reagir ao primeiro plano |
| Escrever indiferença como `nobody moves or reacts` | volta uma sala de manequins | separe as duas metades e feche com `It is not that they are frozen, it is that they simply do not care` |
| Ação de impacto sem contato nomeado | os inimigos desabam sozinhos; parece bug, não luta | nomeie o contato e o alvo único, e negue a queda sem causa |
| Traduzir "sorriso" por `laugh` ou `grin` | o personagem **ri** ao receber uma má notícia e a cena perde o sentido | sorriso é expressão, risada é som e evento |
| Repetir a mesma expressão em planos consecutivos | a curva do personagem vira linha reta e o pico seguinte perde altura | se o plano anterior fechou em `grin`, o próximo entra por outra porta |
| Acrescentar emoção que o roteiro não pediu | o personagem fica inconsistente de um corte pro outro | a direção do roteiro é o **teto**, não o piso |

---

## Cena e composição

| Erro | O que acontece | Correção |
|---|---|---|
| Prompt que descreve a categoria ("atendimento ao cliente") | o modelo devolve a média do dataset, que é literalmente foto de banco de imagem | descreva o instante específico, com figuração em ação e camada desfocada no primeiro plano |
| Cenário limpo, simétrico e com luz sem fonte | lê como catálogo, e o público descarta em meio segundo | bagunça pequena e específica, algo cortado pela borda, luz vinda de uma janela nomeada |
| Traduzir "usado" como "sujo" | volta uma clínica encardida de luz fluorescente | uso é vestígio de gente (casaco na cadeira), não desgaste de material (mofo, rachadura) |
| Cena sem nada acontecendo no fundo | ninguém para pra olhar duas vezes | uma gag por plano, atrás, ação em curso, legível em dois segundos |
| Encher o prompt de detalhes "pra ficar rico" | o modelo executa três ao acaso e ignora o resto, e o que cai costuma ser o que importava | dois elementos de atenção por cena, resto simples, e declare isso no prompt |
| Seis piadas igualmente legíveis no mesmo quadro | não é fundo rico, é bagunça: o protagonista some | três camadas de nitidez; só a primeira compete com o protagonista |
| Apresentador com expressão triste porque a cena é negativa | apresentador abatido mata a mensagem | quem está mal é o problema, não quem explica |
| Marca real em qualquer lugar do quadro | reprovação de anúncio | nome fictício sempre, e `no logos or brand names anywhere in the frame` |
| Ação física impossível (mão nua no fogo) | o modelo entrega o que "parece certo", não o que é certo | nomeie a ferramenta e a técnica |

---

## Voz e produção

| Erro | O que acontece | Correção |
|---|---|---|
| Escrever faixa de TTS pra quem vai gravar | trabalho jogado fora e roteiro poluído de colchete | pergunte de onde sai a voz na fase 0 |
| Tag de emoção no teleprompter | quem grava fala "colchete whispers" ou trava | faixa de voz em seção própria, teleprompter limpo |
| Trocar a voz de um personagem regravando com outra pessoa | a nova leitura não cai na mesma sílaba e a sincronia do clipe pronto quebra | speech-to-speech por cima da sua gravação: preserva a duração exata |
| Gerar TTS frase por frase | prosódia picotada, entrega instável | uma geração por cena, mais de 250 caracteres |
| Confundir áudio nativo com referência de áudio | conclui que "não dá pra fazer em português" e joga fora a rota | o áudio de referência é o seu arquivo, e a língua é indiferente |
| Gerar imagem antes de saber a duração da fala | a duração do clipe é um parâmetro pago, e ela vem do áudio | áudio primeiro, sempre |
| Aceitar um still "porque ficou bonito" mesmo fora do cenário | um shot desviado no meio de doze certos só aparece na montagem | confira cada still contra o roteiro antes de gerar qualquer vídeo |
