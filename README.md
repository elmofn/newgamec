# O Intervalo — protótipo (vertical slice de combate)

Protótipo **gameplay-first** de um roguelite isométrico de **horror urbano e
ocultismo**, ambientado no subsolo da cidade decadente de **Santa Véspera**.
O objetivo desta fatia é validar o **ritmo de combate entre dois planos**:
enfraquecer e marcar na **Matéria**, finalizar e romper no **Espírito**.

Feito em HTML5 + Canvas 2D, **sem dependências externas**. Depois de validado,
a ideia migra para a **Godot engine**.

> Esta é uma fatia de combate — não há inventário, drops, árvore de habilidades,
> metaprogressão, múltiplos personagens nem geração procedural nesta etapa.

## Como jogar

Abra `index.html` em qualquer navegador — **não precisa de build nem servidor**.
O arquivo é autossuficiente e serve como o "HTML independente para compartilhar".

## Controles (desktop)

| Ação | Tecla |
|------|-------|
| Mover | `WASD` / setas |
| Mirar | mouse |
| Atirar / golpear (arma do plano atual) | segurar clique esquerdo |
| Trocar de plano (Matéria ↔ Espírito) | `Espaço` ou `E` |
| **Avanço** (romper um alvo com 3 marcas) | `Q` |
| Entrar pela porta liberada | `F` |
| Pausar / continuar | `Esc` (ou botão ⏸) |
| Reiniciar tentativa | `R` |
| Ligar/desligar som | botão 🔇 |

## Loop de combate

1. **Matéria** (frio, concreto): **pistolas duplas** à distância. Ferem com dano
   reduzido e aplicam **marcas** — 1 marca a cada 2 acertos, até 3 por inimigo.
   As marcas duram um tempo e renovam a cada novo acerto material. A matéria
   **não mata** (deixa o inimigo em 1 de vida) e **alivia a opressão**.
2. **Espírito** (espectral, agressivo): **mãos espectrais** (melee). Causam dano
   cheio, **finalizam** inimigos e cravam um **eco** (ressonância). Ficar aqui
   **aumenta a opressão**: rajadas maiores/rápidas e **fissuras** (que avisam
   antes de causar dano).
3. **Avanço** `Q` (só no espírito): mire num alvo com **3 marcas** e atravesse-o.
   É o **único** detonador das marcas — tiros/golpes comuns não as rompem. Tem
   i-frames, afterimages e feedback forte; consome as 3 marcas, interrompe o
   ataque do alvo e causa uma **ruptura**. A ruptura **elimina ecos** e causa
   dano alto no **Inquilino** (que exige várias rupturas). Está disponível **na
   hora** em que o alvo completa 3 marcas — sem barra de carga — e pode
   **encadear** entre vários alvos marcados.
4. **Eco** (espírito → matéria): um inimigo com eco, ao ser atingido pelas
   pistolas na matéria, dispara uma **bala-fantasma** (segundo impacto atrasado).
   O eco **não** aplica marcas sozinho — só beneficia as pistolas.

A decisão central: ficar mais tempo no espírito para preparar ecos e finalizar,
assumindo a opressão crescente, ou voltar à matéria para marcar com segurança e
esfriar.

## Salas e partida

- **Átrio dos ausentes** — sala aberta com **4 ecos**. Na matéria avançam e dão
  investidas curtas; no espírito disparam projéteis (mais intensos sob opressão
  alta). Eliminados os quatro, a saída abre — vá até a porta e aperte `F`.
- **Arena do Inquilino** — o chefe, com vida compartilhada entre os planos. Na
  matéria tem carapaça (resistente) e anuncia uma investida reta; no espírito
  fica exposto, recua e solta rajadas. Derrotá-lo encerra a partida em vitória.
- Vida, plano, opressão e progresso **continuam** do átrio para o chefe. Sem cura
  nem checkpoint na transição. `R` recomeça do átrio.

## Interface

Vida, plano atual + cooldown de troca, **opressão** e alerta de perigo, ecos
restantes / vida do Inquilino, as **marcas** sobre cada inimigo (3 pips + selo ao
completar), indicador **AVANÇO PRONTO** quando há alvo válido sob a mira, estado
de eco, objetivo, sala e tempo da tentativa.

## Áudio e acessibilidade

- Sons **sintetizados localmente** com Web Audio (sem arquivos externos).
- O som **começa desligado** — ligue no botão 🔇.
- **Movimento reduzido**: se o sistema pedir (`prefers-reduced-motion`), tremores
  e flashes são removidos sem alterar dano ou tempo de jogo.

## Estrutura técnica

- Um único `index.html` autossuficiente (HTML + CSS + JS, Canvas 2D).
- **Simulação e renderização separadas** (`update(dt)` vs `draw()`), loop com
  pausa e `prefers-reduced-motion`.
- Balanceamento centralizado no objeto **`TUNE`** no topo do `<script>`.

## Decisões provisórias

- **Visual isométrico estilizado**: o chão é um losango/elipse com grade
  diagonal e sombras projetadas (representação de perspectiva iso), não uma
  projeção isométrica por tiles. Trocável depois.
- **Mãos espectrais** e toda a arte são silhuetas/formas vetoriais provisórias.
- O **encadeamento do avanço** mira automaticamente o próximo alvo marcado mais
  próximo (sem limite de usos) — a versão com fila manual pode vir depois.
- Balanceamento (dano, opressão, vida do chefe, etc.) é um primeiro passe para
  ajuste.

## Validação

Testado via navegador headless (Playwright), sem erros de console, confirmando:
marcar na matéria, alternar, avanço `Q` consumir as 3 marcas, golpe/tiro comum
**não** detonar marcas, dano material **não** finalizar (mín. 1 de vida) enquanto
o espiritual finaliza, criar eco e a bala-fantasma na matéria, opressão subir no
espírito e cair na matéria, e o fluxo átrio → porta `F` → Inquilino → vitória.
