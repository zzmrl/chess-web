<script lang="ts">
  import Board from './Board.svelte';

  let board: Board;
  let turn: 'w' | 'b' = 'w';
</script>

<div class="m-auto max-h-2/3 max-w-2/3">
  <Board bind:this={board} bind:turn />
  <div class="mt-2 flex items-center gap-2">
    <div class="grow">
      <strong>Turn:</strong>
      <span class:text-white={turn === 'w'}>
        {turn === 'w' ? 'white' : 'black'}
      </span>
    </div>
    <div class="flex-col items-center justify-center">
      <button
        class={[
          'px-2',
          'py-1',
          'rounded-md',
          'bg-gray-300',
          'hover:bg-gray-400',
          'transition-colors',
          'cursor-pointer',
          'active:translate-0.5',
        ]}
        onclick={() => board.reset()}
      >
        Reset
      </button>
    </div>
  </div>
</div>
