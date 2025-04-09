<script lang="ts">
  import Board from './Board.svelte';

  let board: Board;
</script>

<div class="m-auto max-h-2/3 max-w-2/3">
  <Board bind:this={board} />
  <div class="m-4 flex items-center justify-center">
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
