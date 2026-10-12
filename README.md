# Corrida Didática

Jogo de corrida simples feito com HTML, CSS e JavaScript puro, usando o elemento `<canvas>`. Você controla um carro numa pista de três faixas e precisa desviar dos carros que vêm em sentido contrário. O projeto tem fins didáticos: o código é curto e não usa bibliotecas, frameworks nem etapa de build.

## Como jogar

| Tecla               | Ação                     |
| ------------------- | ------------------------ |
| `←` / `A`           | Move o carro para a esquerda |
| `→` / `D`           | Move o carro para a direita  |
| `Enter`             | Inicia ou reinicia o jogo    |

- Cada obstáculo que passa sem bater rende **12 pontos**.
- A cada **150 pontos** o nível sobe: a pista fica mais rápida e os obstáculos aparecem com mais frequência. A partir do nível 3, às vezes surgem dois obstáculos ao mesmo tempo.
- Uma colisão encerra a partida. O recorde fica salvo no `localStorage` do navegador.

## Como executar

Não há nada para instalar. Duas opções:

**Abrir direto no navegador**

```bash
xdg-open index.html
```

**Servidor local**

```bash
python3 -m http.server 8000
```

Depois acesse <http://localhost:8000>.

## Estrutura do projeto

```
.
├── index.html   # Página com o <canvas> do jogo
├── style.css    # Estilo da página e centralização do canvas
└── script.js    # Toda a lógica do jogo
```

## Como o código funciona

O `script.js` está organizado em poucas partes:

- **Estado do jogo**: objetos `pista`, `carro` e a lista `obstaculo`, além das variáveis `pontos`, `recorde`, `nivel` e `estado` (`'menu'`, `'jogando'` ou `'fim'`).
- **`loop(tempoAgora)`**: o loop principal, chamado por `requestAnimationFrame`. Calcula o `dt` (tempo desde o último quadro, limitado a 33 ms) e chama `atualizar` e `desenhar`.
- **`atualizar(dt)`**: move o carro, anima as faixas da pista, aumenta a velocidade, cria obstáculos e verifica colisões.
- **`desenhar()`**: pinta pista, carro, obstáculos, placar e as telas de menu e de fim de jogo.
- **`retangulosColidem(a, b)`**: detecção de colisão entre retângulos alinhados aos eixos (AABB).
- **Teclado**: os eventos `keydown` e `keyup` atualizam o objeto `teclas`, que `atualizar` lê a cada quadro.

Multiplicar as velocidades por `dt` faz o jogo rodar na mesma velocidade independentemente da taxa de quadros do monitor.

## Ideias para praticar

- Adicionar pausa com a tecla `P` ou `Espaço`.
- Trocar os retângulos por imagens (sprites) de carros.
- Incluir efeitos sonoros na colisão e na troca de nível.
- Adicionar controles por toque para jogar no celular.
