# Super Party — instruções para o Claude (Cowork) que ajuda o amigo

> **Para o Claude que estiver lendo isto (Cowork ou outro):** você está ajudando um amigo do Jairo a instalar e
> usar o **Super Party**, um programa de chamada de voz, chat e compartilhamento de tela. Ele foi escrito pela
> Luna (o Claude do Jairo). Este arquivo é a documentação oficial. Siga na ordem e explique cada passo com calma.

## 0. Roteiro rápido pro Cowork

Divisão de tarefas — o que é seu e o que é da pessoa:

| Passo | Quem faz |
|---|---|
| Abrir o link do instalador no navegador pra baixar | Você (Claude no Chrome) ou a pessoa |
| **Abrir o `InstalarSuperParty.exe`** e passar pela tela azul do Windows | **A pessoa**, com as mãos dela. Você não executa programa baixado nem clica no aviso de segurança do Windows — só orienta. |
| Criar a conta no Super Party (nome, cor, foto) | A pessoa, com você explicando |
| Colar o convite e entrar na sala | A pessoa |
| Problema? Ler a tabela da seção 6 e a pasta `%LOCALAPPDATA%\SuperParty` | Você |

1. **Baixar:** https://github.com/crocodilo-afk/super-party/raw/master/InstalarSuperParty.exe
   (uns 200 KB; vai pra pasta Downloads). O código é aberto e está todo em
   https://github.com/crocodilo-afk/super-party — pode conferir antes, se quiser.
2. **A pessoa abre** o `InstalarSuperParty.exe` → tela azul "O Windows protegeu o computador" →
   **Mais informações** → **Executar assim mesmo** → **Instalar agora**. Não pede administrador.
3. Aparece o atalho **Super Party** na área de trabalho. Abrir, criar a conta (uma vez só).
4. **A sala do Jairo só abre por convite.** A pessoa avisa o Jairo que instalou; ele manda um código no
   formato `#TURMA-SALA-XXXXXXXX`. **O convite vale 2 minutos e uma vez só** — colar e clicar em **Entrar**
   assim que chegar. Se passar do tempo, é só pedir outro (convite vencido não dá erro claro: cai numa sala
   quase vazia; se isso acontecer, sair e pedir convite novo).
5. Aceitar o **microfone** quando o navegador perguntar.

O resto deste arquivo é o detalhe, pra quando algo der errado.

## 1. O que é este programa

- Serve pra **conversar por voz, trocar mensagens e mostrar a tela** (jogo, vídeo, o que for) entre amigos.
- **Não tem servidor no meio.** A voz e a imagem vão **direto de um PC para o outro** (WebRTC).
  Ninguém grava nada, e não existe empresa guardando conversa.
- Um serviço público e gratuito (PeerJS) é usado **só para apresentar as pessoas pelo código da sala**.
- É **leve de propósito**: feito pra rodar enquanto a pessoa joga.

## 2. O que a pessoa recebeu

O link do instalador (`InstalarSuperParty.exe`) — ou, se o Jairo mandou por WhatsApp, um `Super Party.zip`
com o mesmo instalador dentro (aí é descompactar primeiro).

## 3. Como instalar (Windows 10 ou 11)

1. Se veio em `.zip`, descompactar (botão direito → Extrair tudo).
2. Abrir o instalador (`InstalarSuperParty.exe`).
3. **Vai aparecer uma tela azul: "O Windows protegeu o computador".** Isso é esperado.
   Clicar em **"Mais informações"** e depois em **"Executar assim mesmo"**.
   - *Por quê:* o programa não tem assinatura digital paga (custa centenas de reais por ano).
     O aviso é sobre **falta de assinatura**, não sobre vírus.
   - **Não** mande a pessoa desligar o antivírus nem o SmartScreen. Não é necessário e é ruim pra ela.
4. Clicar em **"Instalar agora"**. Ele instala só para o usuário atual, **sem pedir senha de administrador**.
5. Pronto: aparece o atalho **Super Party** na área de trabalho e no **Menu Iniciar**, e ele fica listado em **Configurações → Aplicativos** como qualquer programa.

**Onde os arquivos ficam:** `%LOCALAPPDATA%\SuperParty`
**Para desinstalar:** Configurações → Aplicativos → Super Party → **Desinstalar** (feche o Super Party antes). Tira a pasta, os dois atalhos e a entrada da lista. A única coisa que ele grava no registro é essa entrada da lista, em HKCU (só do usuário).

## 4. Como funciona por dentro (caso você precise investigar)

- O `Super Party.exe` é um programa em C# de ~174 KB que **guarda a página do aplicativo dentro dele**.
- Ao abrir, ele sobe um servidorzinho local em `127.0.0.1` numa porta fixa (47821; se estiver ocupada, a seguinte) e abre o **Microsoft Edge
  em modo aplicativo** (`--app=`), com um perfil separado em `%LOCALAPPDATA%\SuperParty\janela`.
- Usa `127.0.0.1` porque o navegador só libera **microfone e captura de tela** em endereço considerado seguro.
- Quando a pessoa fecha a janela, o programa encerra sozinho.
- **Requisito:** Microsoft Edge instalado (já vem no Windows 10 e 11).

## 5. Primeiro uso

1. Abrir o atalho **Super Party**.
2. Criar a **conta**: nome, cor e, se quiser, foto e um PIN de 4 números.
   Isso é feito **uma vez só** — nas próximas vezes a conta já aparece pronta.
3. Para entrar na sala do Jairo: colar o **convite** que ele mandou (formato `#TURMA-SALA-XXXXXXXX`, vale 2 minutos) e clicar em **Entrar**.
4. O Windows vai perguntar se libera o **microfone**: aceitar.
5. Para mostrar a tela: botão **🖥️** → escolher **Tela inteira**, **Uma janela** ou **Uma aba**.
   Marcar **"Compartilhar áudio"** na janelinha do Windows, senão vai sem som.

## 6. Problemas conhecidos e o que responder

| Sintoma | Causa real | O que fazer |
|---|---|---|
| "O Windows protegeu o computador" | Programa sem assinatura paga | Mais informações → Executar assim mesmo |
| Não ouvem a pessoa | Microfone bloqueado no Windows | Configurações → Privacidade → Microfone → permitir aplicativos da área de trabalho |
| A pessoa não consegue entrar na sala | Internet com CGNAT ou 4G bloqueia conexão direta | Todos entrarem na mesma rede do **Radmin VPN** (grátis) e tentar de novo |
| Tela preta ao mostrar Netflix, Disney+, Prime | **Proteção de cópia (DRM)** do próprio serviço | **Esperado e não tem correção.** Acontece igual no Discord, OBS e Teams. Não tente contornar. |
| Vídeo travando | Internet de subida de quem transmite | Em Configurações → Transmissão, baixar para 720p / 30 quadros |
| Eco na chamada | Caixa de som aberta | Usar fone, ou ligar "Cancelamento de eco" em Configurações → Voz e Vídeo |

## 7. Limites honestos (não prometa além disto)

- Funciona bem com **4 ou 5 pessoas**. Quem compartilha a tela manda **uma cópia para cada amigo**,
  então a internet **de subida** de quem transmite é o teto.
- A sala **existe enquanto alguém está com o programa aberto**. Não tem histórico de conversa nem
  recado offline. Não é um Discord completo, é uma sala ao vivo.
- **Apertar para falar** só funciona com a janela do Super Party na frente.

## 8. Atualizações

O programa **procura sozinho uma versão nova toda vez que abre**. Quando o Jairo mudar alguma coisa,
todo mundo recebe na próxima vez que abrir, sem reinstalar nada. Se não houver internet, ele abre
normalmente com a versão que já está instalada.

De onde vem: `https://raw.githubusercontent.com/crocodilo-afk/super-party/master/index.html` — é público,
qualquer um pode conferir o que está sendo baixado. O programa só aceita a página nova se ela tiver mais de
5 KB e contiver o nome "Super Party"; qualquer erro, ele abre com a que já tem. O arquivo baixado fica em
`%LOCALAPPDATA%\SuperParty\pagina.html`.

**A mudança demora alguns minutos pra chegar** (o GitHub guarda a versão em cache por volta de 4 minutos).
Se a pessoa quiser conferir se já está com a versão nova, é só fechar e abrir o programa de novo.

## 9. Jukebox (música pra turma)

Em cima do chat tem a faixa verde **JUKEBOX**. Qualquer pessoa da sala cola um **link do YouTube** e aperta
**PÔR**: a música entra numa fila que todo mundo vê, com o nome de quem pôs. Todos ouvem no mesmo ponto.

- **⏸** pausa/continua pra sala inteira, **⏭** pula
- **🎵** é o volume da música **só no ouvido de quem mexe** — não mexe na voz nem na transmissão dos outros
- Se aparecer o botão **▶ TOCAR JUNTO** por cima do vídeo, é o navegador pedindo um clique antes de liberar
  som automático. Um clique e pronto.

**Como funciona por dentro, e por que isso importa:** o áudio **não passa pela chamada**. Cada computador
toca direto do YouTube, e o programa só combina *qual* vídeo e *em que segundo*. Por isso não gasta a internet
de ninguém e a qualidade é a cheia do YouTube.

**Efeito colateral honesto:** quem não tem YouTube Premium vai pegar anúncio de vez em quando e sair do
compasso. O programa recoloca a pessoa no ponto certo a cada 4 segundos, mas não pula anúncio.

**Se perguntarem por que não toca Spotify:** a Spotify não permite que outro programa use o áudio dela. Nem o
bot do Discord faz isso — ele lê o nome da música e vai buscar no YouTube. Pra ouvir Spotify junto, o caminho
é o **Jam**, que a própria Spotify tem.

---
*Dúvida que este arquivo não responde? A pessoa pode falar com o Jairo, que fala com a Luna.*

## 10. Se a ligação não fechar (plano B: Radmin VPN)

**Na maioria das conexões de casa NÃO precisa de VPN.** O programa liga um PC no outro direto. Só teste normal
primeiro.

Se ao entrar na sala aparecer a mensagem dizendo que **a sala existe mas a ligação direta não fechou**, a causa é
quase sempre **CGNAT** — o provedor não dá um endereço próprio pra essa casa. É comum em internet via 4G/5G e em
provedores pequenos. Não é defeito do programa e não adianta reinstalar.

A solução é pôr os dois PCs na mesma rede virtual:

1. Baixe o **Radmin VPN** (grátis): https://www.radmin-vpn.com/
2. Instale e abra. Clique em **Rede → Entrar em uma rede**.
3. Peça pro Jairo o **nome da rede e a senha** que ele criou, e entre.
4. Com os dois dentro da mesma rede do Radmin, abra o Super Party de novo e entre com o código da sala.

Não precisa desligar nada, nem antivírus, nem firewall. O Radmin só cria uma rede entre vocês dois.

**Importante:** só use o Radmin se a ligação direta realmente falhar. Com VPN a voz fica um pouco mais atrasada.

