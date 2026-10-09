# newgamec — Entre Planos (protótipo de action RPG)

Protótipo **gameplay-first** de um action RPG com feel **Diablo** (ritmo de abate
rápido, reações em cadeia) e uma mecânica central: **alternar entre o plano
material e o plano espiritual**. Fase de validação em HTML5 + Canvas (JavaScript
puro); depois de testado e aprovado, a ideia migra para a **Godot engine**.

## Jogar

Abra `index.html` em qualquer navegador — não precisa de build nem servidor.

## Controles

| Ação | Teclado | Mouse/Toque |
|------|---------|-------------|
| Mover (8 direções) | `WASD` / setas | arrastar no lado esquerdo |
| Ataque corpo a corpo | `Espaço` / `J` | clique / toque à direita |
| Dash (esquiva com i-frames) | `Shift` / `K` | segurar toque à direita |
| **Trocar de plano** | `Q` / `F` / botão direito | botão azul na tela |

## Mecânica central — dois planos

- **Plano material** (âmbar): carniça rápida. Os **grunts** são sólidos aqui.
  Mas criaturas materiais **não morrem de vez** — ao serem derrubadas viram
  uma **alma** (husk) que precisa ser finalizada no plano espiritual.
- **Plano espiritual** (ciano): onde você **finaliza as almas** e enfrenta as
  **aparições** (wraiths), tangíveis e perigosas só aqui.
- Cada alma tem um **retorno gradual**: no plano material o espírito **possui o
  corpo aos poucos** (o corpo vai se preenchendo); quando completa, a criatura
  se levanta de volta. Esse preenchimento É o tempo de retorno — se você demorar,
  ela volta. Finalize no espiritual antes disso.
- A troca de plano emite um **pulso** que empurra e fere inimigos tangíveis no
  novo plano — vale como ferramenta defensiva.

## Reações em cadeia (o ritmo de abate)

Finalizar uma alma gera uma **explosão de alma** que fere inimigos próximos e
**finaliza outras almas** no raio — que explodem também, encadeando. O loop
divertido: encha o campo de almas no material, troque pro espiritual e **detone
tudo numa cascata**. O HUD mostra sua maior cadeia.

## Inimigos

- **Grunt** — criatura material; vira alma ao cair, finalize no espiritual.
- **Aparição (wraith)** — criatura espiritual; inofensiva/intangível no material,
  mortal no espiritual. Destruída direto, com explosão de alma.
- **Brute** — tanque presente nos dois planos; leva dano extra no espiritual.

## Feel / tuning

Todos os valores de combate ficam no objeto `CFG` no topo do `<script>` em
`index.html`, pra afinar rápido (velocidade, dano, cadência, raios de explosão,
timer de ressurreição, etc.).
