<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import { v4 as uuidv4 } from "uuid";

  import type { todoObj } from "./lib/types/todo";
  import Todo from "./lib/components/Todo.svelte";
  import { onMount } from "svelte";

  let Todos: Array<todoObj> = [];
  let todoText = "";
  let completed = false;
  onMount(() => {
    let Todo = JSON.parse(localStorage.getItem("todos")!);
    if (Todo === null) {
      return;
    }
    Todos = [...Todo];
  });
  const AddTodo = () => {
    Todos = [...Todos, { id: uuidv4(), todo: todoText, completed: false }];
    localStorage.setItem("todos", JSON.stringify(Todos));
    todoText = "";
  };
  const completetodo = (id: string) => {
    let TodosCopy = [...Todos];
    TodosCopy = TodosCopy.filter((todo) => {
      return todo.id === id;
    });
    TodosCopy[0].completed = true;
    localStorage.setItem("todos", JSON.stringify(TodosCopy));
    Todos = [...TodosCopy];
  };
  const deleteTodo = (id: string) => {
    let TodosCopy = [...Todos];
    TodosCopy = TodosCopy.filter((todo) => {
      return todo.id !== id;
    });
    localStorage.setItem("todos", JSON.stringify(TodosCopy));
    Todos = [...TodosCopy];
  };
</script>

<main
  class="flex h-screen items-center justify-center flex-col bg-slate-400 gap-4"
>
  <header class="flex flex-col items-center gap-3">
    <h1 class="font-bold text-3xl">Task Trove 😎</h1>
    <p class="text-base">Track Your Tasks 📝</p>
  </header>
  <div class="input">
    <input
      type="text"
      name="todoInput"
      id="Todoinput"
      bind:value={todoText}
      class="p-2 text-base"
    />
    <button
      on:click={AddTodo}
      class="py-3 px-6 bg-gray-700 rounded-2xl hover:rounded-full transition-all"
    >
      Add Todo
    </button>
  </div>
  <Todo {Todos} {completetodo} {deleteTodo} />
</main>
