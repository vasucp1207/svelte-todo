<script>
  let id = 0;
  let todos = [
    { id: id++, text: "svelte is love", done: false },
    { id: id++, text: "reactivity is love", done: false },
  ];
  let text = "";
  let hide = false;
  let todoType = [];

  function addTodo() {
    todos.push({ id: id++, text: text, done: false });
    todos = todos;
    text = "";
  }

  function computeTodoType() {
    if (!hide) return todos;
    else return todos.filter((todo) => todo.done === true);
  }

  function toogleHide() {
    hide = !hide;
    hide = hide;
  }

  $: {
    console.log(todos);
    if (!hide) todoType = todos;
    else todoType = todos.filter((todo) => todo.done !== true);
  }
</script>

<div class="app">
  <h1>Svelte todo 🧡</h1>
  <div class="top-cont">
    <input bind:value={text} />
    <button on:click={addTodo}>Add Todo</button>
  </div>

  <div class="todo-wrap">
    {#each todoType as todo (todo.id)}
      <div class="todo-cont">
        <input type="checkbox" bind:checked={todo.done} />
        <span class:done={todo.done === true}>{todo.text}</span>
      </div>
    {/each}
  </div>

  <div class="bottom-cont">
    <button on:click={toogleHide}>Show all</button>
    <button on:click={toogleHide}>Hide complete</button>
  </div>
</div>

<style>
  .done {
    text-decoration: line-through;
  }

  .top-cont > input {
    width: 200px;
    height: 30px;
    font-size: 16px;
  }

  .todo-cont {
    display: flex;
    align-items: center;
  }

  .app {
    font-family: sans-serif;
    display: flex;
    flex-direction: column;
    gap: 20px;
    align-items: center;
    justify-content: center;
  }

  .bottom-cont {
    display: flex;
    align-items: center;
    gap: 20px;
  }

  button {
    width: 100px;
    height: 40px;
    font-size: 15px;
    cursor: pointer;
    border: 2px solid #ff3e00;
    color: #ff3e00;
    background: white;
  }

  button:hover {
    color: white;
    background: #ff3e00;
    transition: 0.5s;
  }
</style>
