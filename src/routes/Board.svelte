<script lang="ts">
  import { Chess, type Square, type Color, SQUARES } from 'chess.js';

  interface Props {
    /**
     * Color of light tiles
     *
     * @default lightgray
     */
    '--tile-color-white'?: string;
    /**
     * Color of dark tiles
     *
     * @default darkgray
     */
    '--tile-color-black'?: string;
    /**
     * Color of background
     *
     * @default gray
     */
    '--color-bg'?: string;
    /**
     * Color of selected
     *
     * @default black
     */
    '--color-selected'?: string;
    /**
     * Current turn player's color
     */
    turn?: Color;
  }
  let { turn = $bindable('w') }: Props = $props();

  const chess: Chess = $state(new Chess());

  let board = $state(chess.board());
  let selection = $state<Square | ''>('');

  const tryMovePiece = (from: Square, to: Square): boolean => {
    try {
      chess.move({ from, to });
      return true;
    } catch (e) {
      return false;
    }
  };

  /**
   * Synchronize local data with current chess data.
   *
   * Because the chess game object updates don't propagate
   * to svelte, we have to set data we need manually.
   */
  const sync = () => {
    board = chess.board();
    turn = chess.turn();
  };

  export const reset = () => {
    chess.reset();
    sync();
    selection = '';
  };
</script>

<div class="board">
  {#each board as row, i}
    {#each row as piece, j}
      {@const square = SQUARES[i * 8 + j]}
      <div
        role="button"
        tabindex="0"
        class:selected={square === selection}
        class:dark={chess.squareColor(square) === 'dark'}
        class={piece && `${piece.color}${piece.type}`}
        onclick={() => {
          if (!selection) {
            selection = square;
          } else {
            const success = tryMovePiece(selection, square);
            if (success) {
              sync();
            }
            selection = '';
          }
        }}
        onkeypress={() => {
          // TODO
        }}
      ></div>
    {/each}
  {/each}
</div>

<style>
  .board {
    display: grid;
    aspect-ratio: 1;
    grid-template-columns: repeat(8, minmax(0, 1fr));
    grid-template-rows: repeat(8, minmax(0, 1fr));
    border: 1px solid;
    font-size: 3rem;
    font-family: var(--font-mono);
    user-select: none;

    * {
      background-repeat: no-repeat;
      background-position: center;
      background-color: var(--tile-color-white, lightgray);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .selected {
      border: 2px solid var(--color-selected, black);
    }

    .dark {
      background-color: var(--tile-color-black, darkgray);
    }

    .wp {
      background-image: url('$lib/sprites/Chess_plt45.svg');
    }

    .wn {
      background-image: url('$lib/sprites/Chess_nlt45.svg');
    }

    .wb {
      background-image: url('$lib/sprites/Chess_blt45.svg');
    }

    .wr {
      background-image: url('$lib/sprites/Chess_rlt45.svg');
    }

    .wq {
      background-image: url('$lib/sprites/Chess_qlt45.svg');
    }

    .wk {
      background-image: url('$lib/sprites/Chess_klt45.svg');
    }

    .bp {
      background-image: url('$lib/sprites/Chess_pdt45.svg');
    }

    .bn {
      background-image: url('$lib/sprites/Chess_ndt45.svg');
    }

    .bb {
      background-image: url('$lib/sprites/Chess_bdt45.svg');
    }

    .br {
      background-image: url('$lib/sprites/Chess_rdt45.svg');
    }

    .bq {
      background-image: url('$lib/sprites/Chess_qdt45.svg');
    }

    .bk {
      background-image: url('$lib/sprites/Chess_kdt45.svg');
    }
  }
</style>
