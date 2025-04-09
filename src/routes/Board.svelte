<script lang="ts">
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
  }

  type Board = string[][];
  type Point = [number, number];
  type Moves = [string[], string[]];

  const OG_BOARD: Board = [
    '♜♞♝♛♚♝♞♜',
    '♟♟♟♟♟♟♟♟',
    '        ',
    '        ',
    '        ',
    '        ',
    '♙♙♙♙♙♙♙♙',
    '♖♘♗♕♔♗♘♖',
  ].map((line) => line.split(''));
  const LIGHT_PIECES = new Set('♙♖♘♗♕♔');
  const DARK_PIECES = new Set('♟♜♞♝♛♚');

  let board = $state(OG_BOARD);
  let moves = $state([[], []]);
  let selection: Point | [] = $state([]);
  let currentPlayer: 'dark' | 'light' = $state('light');

  const validateMove = (from: Point, to: Point): boolean => {
    return false;
  };

  const movePiece = (from: Point, to: Point) => {
    board[to[0]][to[1]] = board[from[0]][from[1]];
    board[from[0]][from[1]] = ' ';
  };

  export const reset = () => {
    board = OG_BOARD;
  };
</script>

<div class="board">
  {#each board as row, i}
    {#each row as col, j}
      <div
        role="button"
        tabindex="0"
        class:selected={selection[0] === i && selection[1] === j}
        class:dark={(i + j) % 2 === 0}
        onclick={() => {
          if (!selection.length) {
            selection = [i, j];
          } else {
            // validate move
            movePiece(selection, [i, j]);
            selection = [];
          }
        }}
        onkeypress={() => {
          // TODO
        }}
      >
        {col}
      </div>
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
    background: var(--color-bg, gray);
    gap: 0.2rem;
    font-size: 3rem;
    font-family: var(--font-mono);
    user-select: none;

    * {
      background: var(--tile-color-white, lightgray);
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .selected {
      outline: 2px solid var(--color-selected, black);
    }

    .dark {
      background: var(--tile-color-black, darkgray);
    }
  }
</style>
