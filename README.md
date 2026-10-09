# newgamec — protótipo de action RPG

Protótipo **gameplay-first** do núcleo de combate de um action RPG, para rodar no
navegador. Fase de validação em HTML5 + Canvas (JavaScript puro); após o combate
ser testado e aprovado, a ideia migra para a **Godot engine**.

## Jogar

Abra `index.html` em qualquer navegador — não precisa de build nem servidor.

## Controles

| Ação | Teclado | Mouse/Toque |
|------|---------|-------------|
| Mover (8 direções) | `WASD` / setas | arrastar no lado esquerdo |
| Ataque corpo a corpo | `Espaço` / `J` | clique / toque à direita |
| Dash (esquiva com i-frames) | `Shift` / `K` | segurar toque à direita |

## Núcleo de combate (o que torna divertido)

- **Movimento** em 8 direções com aceleração e atrito (sensação de peso leve).
- **Ataque** em arco com hitbox, knockback e feedback (partículas, screen shake, números de dano).
- **Dash** rápido com breve invencibilidade (i-frames) para atravessar inimigos e escapar.
- **3 tipos de inimigo:** *grunt* (persegue), *rusher* (telegrafa e avança), *brute* (tanque lento).
- **Arena** simples com ondas crescentes.

## Feel atual

Default inspirado em **Hades** (ação rápida, dash central). Ajustável via o objeto
`CFG` no topo do `<script>` em `index.html`.
