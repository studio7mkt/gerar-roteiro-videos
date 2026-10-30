# Como instalar a skill `gerar-roteiro-videos`

Esta pasta inteira **é** a skill. Instalar significa colocá-la no lugar onde a sua IA procura skills.
Escolha abaixo a ferramenta que você usa. As quatro rodam a mesma skill e entregam o mesmo resultado.

| Você usa | Vá para |
|---|---|
| Claude Code (terminal, app desktop ou extensão do VS Code) | [Claude Code](#claude-code) |
| Codex (app desktop, terminal ou extensão do VS Code) | [Codex](#codex) |
| ChatGPT (site ou app, incluindo o ChatGPT Work) | [ChatGPT](#chatgpt) |
| Qualquer outra IA, ou o plano gratuito | [Sem instalar](#sem-instalar-qualquer-ia) |

**Em todos os casos, o `SKILL.md` tem que estar na raiz da pasta**, não dentro de uma subpasta. Se ao
descompactar surgir uma pasta dentro da outra (`gerar-roteiro-videos/gerar-roteiro-videos/SKILL.md`),
suba o conteúdo um nível. A estrutura certa é esta:

```
gerar-roteiro-videos/
  SKILL.md              ← o arquivo que a IA lê primeiro
  INSTALAR.md
  referencias/
    01-roteiro-e-decupagem.md
    02-storyboard-e-assets.md
    03-prompt-de-still.md
    04-prompt-de-video.md
    05-cena-anti-stock-e-gags.md
    06-voz-sintetizada.md
    07-gerar-no-magnific.md
    08-erros-conhecidos.md
  exemplo/
    ROTEIRO.md
    PROMPTS.md
```

**Não apague as pastas `referencias/` e `exemplo/`.** O `SKILL.md` manda a IA ler esses arquivos em
cada fase. Sem eles a skill funciona pela metade e os prompts saem genéricos.

---

## Claude Code

Descompacte o zip em:

```
Windows:  C:\Users\<seu-usuario>\.claude\skills\gerar-roteiro-videos\
Mac:      ~/.claude/skills/gerar-roteiro-videos/
Linux:    ~/.claude/skills/gerar-roteiro-videos/
```

Para usar só num projeto específico, em vez disso: `<pasta-do-projeto>/.claude/skills/gerar-roteiro-videos/`.

**Como usar:** abra o Claude Code e digite `/gerar-roteiro-videos`, ou simplesmente peça *"quero
escrever o roteiro de um vídeo curto feito com IA sobre X"*. Se o comando não aparecer, feche e
reabra o Claude Code: a lista de skills é carregada no início da sessão.

---

## Codex

Descompacte o zip em:

```
Windows:  C:\Users\<seu-usuario>\.agents\skills\gerar-roteiro-videos\
Mac:      ~/.agents/skills/gerar-roteiro-videos/
Linux:    ~/.agents/skills/gerar-roteiro-videos/
```

Repare que a pasta é **`.agents`**, não `.codex`. Ela começa com ponto, então fica oculta: no
Windows, ative "Itens ocultos" no menu Exibir do Explorador de Arquivos; no Mac, aperte
`Cmd + Shift + .` no Finder. Se a pasta `.agents\skills` ainda não existir, crie.

Para usar só num projeto específico, em vez disso: `<pasta-do-projeto>/.agents/skills/gerar-roteiro-videos/`.

**Como usar:** no terminal ou na extensão do VS Code, digite `$` e escolha `gerar-roteiro-videos`
na lista (ou rode `/skills`). Em qualquer versão, inclusive no app desktop, também funciona só pedir:
*"use a skill gerar-roteiro-videos para escrever o roteiro de um vídeo sobre X"*. O Codex costuma
perceber a skill nova sozinho; se ela não aparecer, feche e reabra o Codex.

---

## ChatGPT

No ChatGPT a skill é enviada pelo próprio site ou app, **sem descompactar**:

1. Na barra lateral, clique em **Plugins** e abra a aba **Skills**.
2. Clique em **Create** e escolha **Upload from your computer**.
3. Envie o arquivo `gerar-roteiro-videos.zip` do jeito que você baixou da aula.
4. Espere o ChatGPT analisar o pacote. Quando ele aparecer como disponível, está instalado.

**Como usar:** numa conversa (ou no ChatGPT Work), digite `@` e escolha `gerar-roteiro-videos`, ou
simplesmente peça *"quero escrever o roteiro de um vídeo curto feito com IA sobre X"*. No app
desktop, também dá para chamar com `$gerar-roteiro-videos`.

**Fique atento a duas coisas:**
- Skills no ChatGPT exigem **plano pago**. Nos planos Free e Go a opção não aparece; nesse caso, use
  o caminho [Sem instalar](#sem-instalar-qualquer-ia).
- Hoje a skill instalada no app desktop **não sincroniza** com o site, e vice-versa. Se você usa os
  dois, instale nos dois.

Os nomes dos menus estão em inglês porque é assim que o ChatGPT mostra hoje. A OpenAI muda essa
interface com frequência; se não achar o caminho exato, procure por "Skills" nas configurações.

---

## Sem instalar (qualquer IA)

Funciona no ChatGPT gratuito, no Gemini, no Claude.ai ou em qualquer chat que aceite anexos.

1. Descompacte o zip no seu computador.
2. Abra uma conversa nova e **anexe o `SKILL.md`, os 8 arquivos da pasta `referencias/` e os 2 da
   pasta `exemplo/`**.
3. Mande esta mensagem:

```
Os arquivos anexados são uma skill. Siga o SKILL.md à risca, consulte as referências que ele indica
em cada fase e comece pela Fase 0: me faça o briefing.
```

A diferença para as outras formas: aqui a IA não guarda a skill. **Toda vez que for fazer um vídeo
novo, abra uma conversa nova e anexe os arquivos de novo.** É por isso que, se você puder, vale usar
uma das ferramentas acima.

---

## O que ela entrega

Dois arquivos, prontos pra executar:

1. **`ROTEIRO.md`** — a cena decupada shot a shot, com as falas verbatim, a duração de cada uma e a
   direção em português.
2. **`PROMPTS.md`** — os prompts em inglês, um de imagem e um de vídeo por shot, prontos pra colar no
   gerador.

Veja [exemplo/](exemplo/) pra saber exatamente com o que se parece o resultado.

## O que você precisa ter, do lado de fora

A skill escreve. Quem gera é você, e pra isso precisa de:

- **Um gerador de imagem** que segure identidade de personagem por referência e escreva texto certo
  em placa (Nano Banana 2, Seedream, GPT Image e equivalentes).
- **Um gerador de vídeo que aceite áudio como referência**, pra sincronia labial nativa em português
  (Minimax H3 e equivalentes). Sem isso, o pipeline vira dois estágios.
- **Um jeito de gravar ou sintetizar as falas.** Gravar você mesmo é o mais barato e o mais
  expressivo; se for sintetizar, a referência está em
  [referencias/06-voz-sintetizada.md](referencias/06-voz-sintetizada.md).
- **Um editor de vídeo** pro corte, a trilha e a legenda. Isso nunca sai da IA.

## Uma advertência de custo

Geração de imagem e vídeo custa dinheiro de verdade, e não volta atrás. **A skill nunca dispara nada
sem confirmação**, e é assim de propósito: um lote de dez clipes de 8 segundos custa mais do que a
maioria das pessoas espera. Confira o roteiro inteiro, depois confira os stills, e só então gere os
vídeos. A ordem existe pra proteger o seu bolso.
