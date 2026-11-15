# 🦊🛸 STAR FOX: INVADERS — Super FX 3D

> Um *crossover* arcade em **HTML / CSS / JavaScript monolítico** (zero dependências externas) que funde a estética poligonal 3D do **Star Fox (Super Nintendo, 1993)** com a tensão clássica de formação e avanço do **Space Invaders (Arcade, 1978)**.

---

## 📖 Sobre o Projeto

**STAR FOX: INVADERS** coloca você no comando da icônica nave **Arwing** em um corredor espacial tridimensional renderizado integralmente via software no `<canvas>` HTML5. Em vez de inimigos aleatórios em trilhos, a frota invasora marcha em formação fechada à frente — alternando poses a cada passo, acelerando à medida que é reduzida e avançando em profundidade em direção à sua linha de defesa.

Todo o projeto — motor gráfico 3D, áudio procedural, retratos em *pixel art*, interface CRT e lógica de jogo — reside em um único arquivo HTML autocontido.

---

## 🚀 A História do Star Fox (SNES, 1993)

No início da década de 1990, gráficos 3D em tempo real pertenciam quase exclusivamente a fliperamas caros e estações de trabalho. O Super Nintendo Entertainment System (SNES) havia sido projetado como uma potência 2D de 16 bits e não possuía poder de processamento nativo para renderizar polígonos em 3D.

A virada aconteceu por meio de uma parceria improvável entre a **Nintendo EAD** (com produção e design de **Shigeru Miyamoto**, direção de **Katsuya Eguchi** e arte de **Takaya Imamura**) e o estúdio britânico **Argonaut Software**, fundado por **Jez San** e estrelado por jovens programadores como **Dylan Cuthbert** e **Giles Goddard**. Impressionada com demos 3D que a Argonaut havia criado ilegalmente em hardware de Game Boy, a Nintendo encomendou um chip acelerador personalizado que pudesse viver **dentro do próprio cartucho**.

Assim nasceu o lendário **Chip Super FX** (codinome *MARIO — Mathematical, Argonaut, Rotation, & Input/Output*), um coprocessador RISC dedicado a cálculos matriciais e desenho de polígonos *flat-shaded*. Lançado em **1993** (chamado de *Starwing* na Europa), **Star Fox** apresentou ao mundo o piloto **Fox McCloud** e seu esquadrão mercenário — **Peppy Hare**, **Falco Lombardi** e **Slippy Toad** — defendendo o planeta **Corneria** e o Sistema Lylat contra as forças do cientista louco **Andross**, exilado em **Venom**.

Com mais de 4 milhões de cópias vendidas, *Star Fox* marcou uma geração ao transformar limitações de hardware em identidade visual (polígonos sem textura com sombreamento plano), além de popularizar o gênero *rail shooter* 3D nos consoles domésticos e eternizar bordões como *"Do a barrel roll!"*.

---

## 👾 A História do Space Invaders (Arcade, 1978)

Em **1978**, o engenheiro e designer japonês **Tomohiro Nishikado**, da **Taito**, revolucionou a história do entretenimento digital com **Space Invaders**. Antes dele, os fliperamas eram dominados por variações de *Pong* e *Breakout*. Nishikado queria unir a satisfação de destruir blocos na tela com um tema espacial épico — e, pela primeira vez em grande escala, fazer os alvos **atirarem de volta**.

Para dar vida ao projeto, Nishikado precisou projetar o próprio hardware de arcade baseado em microprocessador e escrever suas ferramentas de desenvolvimento do zero. Suas maiores inspirações vieram de três obras da ficção científica:
- ***A Guerra dos Mundos* (H.G. Wells):** que inspirou a silhueta de lulas, caranguejos e polvos alienígenas;
- ***Patrulha Estelar (Space Battleship Yamato)*:** o anime que moldou o senso de defesa planetária contra uma frota invasora;
- ***Star Wars* (1977):** cuja estreia iminente no Japão reforçou a aposta na temática espacial.

Um detalhe técnico tornou-se uma das descobertas mais famosas do *game design*: quanto mais alienígenas o jogador eliminava, menos sprites o processador tinha que desenhar por quadro, fazendo com que os invasores restantes **marchassem cada vez mais rápido**. Nishikado abraçou esse comportamento e o combinou a um pulso grave contínuo de 4 notas que acelerava junto — criando tensão psicológica crescente. O resultado foi um fenômeno cultural sem precedentes, que inaugurou a Era de Ouro dos Arcades e transformou o alienígena pixelado em um ícone universal dos videogames.

---

## ✨ Inspirações e Fusão de Conceitos

Este projeto nasceu da pergunta: *"E se a invasão de Space Invaders acontecesse na linha do horizonte de um corredor espacial do chip Super FX?"*

| Elemento | Origem: **Star Fox (1993)** | Origem: **Space Invaders (1978)** | Como foi fundido no jogo |
| :--- | :--- | :--- | :--- |
| **Visual e Motor** | Polígonos *flat-shaded* com iluminação direcional e chão em grade | Silhuetas icônicas em pixel art (*Squid*, *Crab*, *Octopus*) | Invasores modelados em **voxel-polígonos 3D** com sombreamento plano e animação em 2 quadros |
| **Movimentação e Câmera** | Câmera em 3ª pessoa seguindo a Arwing, *banking* lateral e mira dupla 3D | Canhão fixo na base da tela | Voo livre no plano X/Y com inclinação suave da nave e mira projetada em profundidade |
| **Defesa** | *Barrel Roll* para rebater lasers | 4 *Bunkers* destrutíveis bloco a bloco | Barreiras 3D em arco que protegem você e se desfazem sob fogo + *Barrel Roll* para defletir tiros |
| **Ritmo e Tensão** | Ondas cinematográficas e chefes de setor | Marcha lateral com aceleração progressiva e batida de 4 notas | Formação marcha em X, avança em **profundidade (Z)** ao tocar as bordas e acelera o pulso sonoro conforme é abatida |
| **Eventos & Áudio** | Rádio com retratos do esquadrão e *Smart/Nova Bombs* | *Mystery UFO* cruzando o topo por pontos bônus | UFO bônus solta anéis 3D de *Power-Up* (*Triple Laser*, *Shield*, *Nova Bomb*) + Chefes Nave-Mãe a cada 3 fases |

---

## 🛠️ Arquitetura Técnica (Monolítico)

- **Motor 3D em Software (`Canvas 2D`):**
  - Projeção em perspectiva com câmera dinâmica que acompanha a nave.
  - Iluminação direcional por produto escalar entre a normal da face e o vetor de luz, além de neblina de profundidade (*depth fog*).
  - Ordenação de polígonos e projéteis via **Algoritmo do Pintor** (*Painter's Algorithm*).
  - *Clipping* analítico no plano próximo (`NEAR_Z = 15`) para evitar inversão de linhas e divisões por zero.
- **Áudio Procedural (`Web Audio API`):**
  - Sem arquivos `.mp3` ou `.wav`: lasers, passo grave de 4 notas, explosões com ruído branco filtrado, *swoosh* do *Barrel Roll*, fanfarras de *power-up* e bipes de rádio dos personagens gerados em tempo real por osciladores.
- **Retratos Pixel Art 16×16:**
  - Grade matricial renderizada diretamente em um mini-canvas com animação bucal sincronizada ao texto digitado e timbre de voz único para **Fox**, **Peppy**, **Falco** e **Slippy**.

---

## 🎮 Controles

| Tecla / Ação | Função |
| :--- | :--- |
| `W` `A` `S` `D` ou `Setas` | Pilotar a Arwing (cima, baixo, esquerda, direita) |
| `Espaço`, `Z` ou `Clique Esq.` | Disparar lasers (Twin / Triple Hyper Laser) |
| `Shift`, `E`, `Q` ou **Duplo Toque** `A`/`D` | **Barrel Roll** (gira 360° e deflete tiros inimigos!) |
| `B` ou `C` | Lançar **Nova Bomb** (onda de choque em área 3D) |
| `P` ou `Esc` | Pausar / Continuar missão |
| `M` | Ligar / Desligar áudio sintetizado |

---

## ▶️ Como Jogar

1. Salve o arquivo HTML completo (por exemplo, `star-fox-invaders.html`).
2. Dê um duplo clique para abrir em qualquer navegador moderno (**Chrome, Firefox, Edge, Safari**).
3. Clique em **INICIAR MISSÃO** (ou pressione `Enter`) e defenda o setor!

### 💡 Dicas Táticas
- **Use os Bunkers 3D com inteligência:** voe baixo para se proteger atrás das barreiras verdes quando houver muitos tiros inimigos, mas lembre-se de que seus próprios lasers também desgastam a cobertura!
- **Acertar o UFO compensa:** o disco voador vermelho que cruza o topo da arena solta um anel de energia que pode ativar o **Triple Hyper Laser**, restaurar **35% do escudo** ou conceder **+1 Nova Bomb**.
- **Sobreviva às Ondas Múltiplas de 3:** nos estágios `3, 6, 9...`, uma **Nave-Mãe Invasora** gigante aparece com barra de vida própria e canhões duplos!