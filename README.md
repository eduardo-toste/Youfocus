<div align="center">

<img src="icones/128.png" width="72" alt="">

# Youfocus

**Controle o seu YouTube: bloqueio, sessões de foco e teto diário de minutos.**

Roda inteira na sua máquina — sem conta, sem servidor, sem nenhuma chamada de rede.

</div>

<br>

<div align="center">
<img width="333" height="396" alt="image" src="https://github.com/user-attachments/assets/3fba168f-cfb6-4106-bcff-54d911784a83" />
</div>

<br>

## O que faz

**Dois modos.** No **Livre** o YouTube abre normalmente, com os ajustes que você
escolher. No **Fechado** nada abre — nem `youtu.be`, nem `m.youtube.com`, nem
`music.youtube.com`, nem player embutido em outra página.

**Sessões de foco.** 30 min, 1 h, 2 h, uma duração livre ou um horário-alvo.
Enquanto durar, o YouTube fica fechado e o ícone mostra a contagem regressiva.

**Horário fixo.** Dias da semana e faixa de horas, para a rotina que se repete.

**Teto diário de minutos.** Conta só o tempo com vídeo realmente rodando na aba
visível. Estourou, todo o YouTube passa a cair na tela de balanço até a meia-noite.

**Ajustes.** Bloquear Shorts, esconder recomendados e telas finais, esconder
comentários, e uma contagem de 10 segundos antes de cada vídeo abrir.

<br>

| Teto do dia atingido | YouTube fechado |
|:--:|:--:|
| <img width="1296" height="1308" alt="limite" src="https://github.com/user-attachments/assets/fda35880-59d1-4511-810c-e3c742c7cc80" /> | <img width="1216" height="922" alt="bloqueio" src="https://github.com/user-attachments/assets/b5895468-4dfd-4dca-a521-f59563276dda" /> |

<br>

## Instalação

Não está em nenhuma loja — a instalação é local e leva um minuto.

1. Baixe em **Code → Download ZIP** e descompacte numa pasta que possa ficar
   parada. O navegador lê os arquivos de lá, não faz cópia: se você apagar ou
   mover a pasta depois, a extensão para de funcionar.
2. Abra `chrome://extensions` — ou `brave://extensions`, `edge://extensions`.
3. Ligue o **Modo do desenvolvedor**, no canto superior direito.
4. Clique em **Carregar sem compactação** e escolha a pasta `youfocus`.
5. Fixe o ícone na barra pelo menu de peça de quebra-cabeça.

Depois de editar qualquer arquivo, volte na página de extensões e clique no botão
de recarregar do cartão da extensão.

**Compatibilidade:** Chrome, Brave, Edge, Opera e Vivaldi. Firefox ainda não.

<br>

## Permissões

| Permissão | Para quê |
|:--|:--|
| `storage` | Guardar suas configurações e o contador do dia, localmente |
| `alarms` | Conferir o horário uma vez por minuto |
| `declarativeNetRequest` | Declarar as regras de bloqueio. O navegador as aplica internamente: a extensão não recebe as URLs que você visita |
| `host_permissions` | Restrito a `*.youtube.com` e `youtu.be`. Não há acesso a nenhum outro site |

<br>

## Licença

[MIT](LICENSE).
