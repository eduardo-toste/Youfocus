<div align="center">

<img src="icones/128.png" width="80" alt="">

# Youfocus

**Uma extensão de navegador que devolve o controle do seu YouTube.**

Dois modos, sessões de foco e teto diário de minutos.
Sem conta, sem servidor, sem telemetria — roda inteira na sua máquina.

<img src="https://img.shields.io/badge/Manifest-V3-06171F?style=flat-square" alt="Manifest V3">
<img src="https://img.shields.io/badge/depend%C3%AAncias-nenhuma-16736B?style=flat-square" alt="Sem dependências">
<img src="https://img.shields.io/badge/rede-zero%20chamadas-C6E85E?style=flat-square&labelColor=06171F" alt="Offline">
<img src="https://img.shields.io/badge/licen%C3%A7a-MIT-06171F?style=flat-square" alt="MIT">

</div>

<br>

## O problema

Bloquear o YouTube inteiro não funciona: mais cedo ou mais tarde você precisa de
uma aula, uma referência, um tutorial — e aí desliga o bloqueador e nunca liga de
volta. Deixar aberto também não funciona, porque a maior parte do tempo gasto lá
não vem do vídeo que você foi buscar. Vem do próximo.

O Youfocus separa as duas coisas. Você mantém o acesso ao que procurou e perde o
que só apareceu.

<br>

## A interface

Não há página de configurações. Tudo acontece numa janela só, ao clicar no ícone.

<div align="center">
<img src="docs/popup.png" width="330" alt="Janela do Youfocus com seletor de modo, sessões de foco e ajustes">
</div>

O seletor no topo alterna entre os dois modos. O bloco escuro inicia uma sessão de
foco. Os ajustes ficam recolhidos até você precisar deles.

| Modo | O que acontece |
|:--|:--|
| **Livre** | YouTube aberto, com os ajustes valendo — Shorts, recomendados e comentários conforme sua escolha |
| **Fechado** | Nada abre: nem `youtu.be`, nem `m.youtube.com`, nem `music.youtube.com`, nem player embutido em outra página |

Três gatilhos forçam o **Fechado**, nesta ordem de precedência:

1. **Sessão de foco** — 30 min, 1 h, 2 h, uma duração livre em minutos ou um
   horário-alvo. O ícone mostra a contagem regressiva e não há como liberar antes
   da hora sem encerrar a sessão de propósito.
2. **Horário fixo** — dias da semana e faixa de horas, para a rotina que se repete.
3. **Teto diário** — quando os minutos do dia acabam.

<br>

## Quando o teto estoura

Não é uma tela de bloqueio, é uma prestação de contas. A partir daí, qualquer
endereço do YouTube leva até aqui — não só as páginas de vídeo.

<div align="center">
<img src="docs/limite.png" width="720" alt="Tela de balanço mostrando 67 minutos assistidos, teto de 60, barras dos últimos sete dias e contagem até a meia-noite">
</div>

A trilha mostra em limão o que coube dentro do teto e em teal o excedente. As
barras trazem os últimos sete dias com a linha tracejada marcando o limite, e o
relógio conta até a virada do dia. O botão discreto inicia uma sessão de foco até
a meia-noite — é o momento em que você está mais propenso a aceitar, e evita a
tentação de ir aumentar o teto para ganhar mais dez minutos.

<br>

## Quando o YouTube está fechado

<div align="center">
<img src="docs/bloqueio.png" width="640" alt="Placa de bloqueio durante uma sessão de foco, informando o horário de término">
</div>

A placa muda de texto conforme o motivo: sessão de foco, horário fixo, modo
Fechado ou Shorts desligados. Sempre diz **por que** e **até quando**.

<br>

## Ajustes

- **Bloquear Shorts** — o rolo vertical não abre, a aba some do menu lateral e as
  prateleiras somem dos feeds. Sem precisar fechar o YouTube inteiro.
- **Contar até 10** — ao abrir um vídeo, uma tela cobre o player e pergunta se
  você veio mesmo por causa dele. O botão de assistir só destrava depois da
  contagem. É o freio mais eficaz do conjunto, porque pega o clique impulsivo.
- **Esconder recomendados e telas finais** — some a barra lateral e as sugestões
  que aparecem sobre o vídeo terminando.
- **Esconder comentários** — opcional, desligado por padrão.
- **Teto diário** — conta só o tempo com vídeo realmente rodando na aba visível.
  Pausar ou trocar de aba não consome.
- **Tema claro e escuro**, acompanhando a preferência do sistema.

<br>

## Instalação

A extensão não está em nenhuma loja. Instale localmente:

1. Baixe o repositório em **Code → Download ZIP** e descompacte numa pasta que
   possa ficar parada — o navegador lê os arquivos de lá, não faz cópia.
2. Abra `chrome://extensions` (ou `brave://extensions`, `edge://extensions`).
3. Ligue o **Modo do desenvolvedor**, no canto superior direito.
4. Clique em **Carregar sem compactação** e escolha a pasta do projeto.
5. Fixe o ícone na barra pelo menu de peça de quebra-cabeça.

Funciona em qualquer navegador baseado em Chromium: Chrome, Brave, Edge, Opera e
Vivaldi. **Firefox ainda não** — a API `declarativeNetRequest` tem diferenças de
implementação que exigiriam um segundo caminho de código.

<br>

## Privacidade

A extensão não faz nenhuma requisição de rede. Não há `fetch`, `XMLHttpRequest`,
CDN, biblioteca externa nem endpoint no código — dá para verificar em dois minutos
procurando por esses termos nos arquivos.

| Permissão | Para quê |
|:--|:--|
| `storage` | Guardar configurações e o contador do dia em disco, localmente |
| `alarms` | Conferir o horário uma vez por minuto |
| `declarativeNetRequest` | Declarar as regras de bloqueio. O navegador as aplica internamente: a extensão **não recebe** as URLs que você visita |
| `host_permissions` | Restrito a `*.youtube.com` e `youtu.be`. Não há acesso a nenhum outro site |

<br>

## Arquitetura

```
manifest.json     Permissões e registro
background.js     Service worker: decide o modo vigente e emite as regras de rede
youtube.js        Content script: esconde elementos, conta o tempo, segura o vídeo
popup.html/.js    A única interface — não existe página de opções
blocked.html/.js  A tela que substitui o YouTube, com o motivo do bloqueio
limite.html/.js   A tela de balanço, quando o teto diário estoura
styles.css        Variáveis de cor e tipografia, compartilhadas por todas as telas
icones/           16, 32, 48 e 128 px
```

**Os modos são mutuamente exclusivos, e essa é a decisão central do projeto.**
Fechado emite apenas regras de bloqueio; Livre emite apenas as regras dos ajustes.
Uma versão anterior emitia os dois conjuntos ao mesmo tempo e o redirecionamento
vencia por prioridade — o YouTube abria mesmo estando bloqueado. Sem sobreposição,
o conflito não tem como existir.

**Quem bloqueia é o service worker, nunca a página.** O content script só conta o
tempo e pausa o vídeo em andamento. Foi assim que o teto diário passou a valer já
na abertura do YouTube, em vez de esperar você clicar num vídeo.

O contador é honesto, não é à prova de você mesmo: dá para zerá-lo apagando a
chave `uso` pelo DevTools. É proposital. Isto é um freio, não uma prisão.

<br>

## Personalizar

**Cores** — todas as variáveis vivem no topo do `styles.css`. A paleta é uma
escala análoga contínua: azul-noite `#06171F` → teal `#16736B` → limão `#C6E85E`.
O limão só aparece sobre fundo escuro; nas superfícies claras o acento é o teal,
que passa em contraste.

**Elementos que voltaram a aparecer** — o YouTube renomeia suas tags de tempos em
tempos. Abra o inspetor (<kbd>F12</kbd>), veja o nome do elemento e ajuste os
seletores no topo do `youtube.js`. Depois recarregue a extensão na página de
extensões do navegador.

**Frases da contagem de 10 segundos** — a lista `FRASES`, no `youtube.js`.

<br>

## Licença

[MIT](LICENSE).
