<script lang="ts">
  import type { todoObj } from "../types/todo";

  export let Todos: todoObj[];
  export let completetodo: (id: string) => void;
  export let deleteTodo: (id: string) => void;
</script>

<div class="todo p-2 flex flex-col gap-1">
  {#each Todos as todo, i}
    <div class="flex items-center justify-center gap-2 m-4">
      <input
        type="checkbox"
        name="TodoCompleted"
        bind:checked={todo.completed}
        class="p-10 text-2xl"
      />
      <p
        class="font-serif {todo.completed && 'line-through'} flex-1 capitalize"
      >
        {todo.todo}
      </p>
      {#if !todo.completed}
        <button
          on:click={() => completetodo(todo.id)}
          class="py-3 px-6 bg-gray-700 rounded-2xl hover:rounded-full transition-all"
        >
          Complete Todo
        </button>
      {/if}
      <button
        on:click={() => deleteTodo(todo.id)}
        class="py-3 px-6 bg-gray-700 rounded-2xl hover:rounded-full transition-all"
      >
        Delete Todo
      </button>
    </div>
  {/each}
</div>
