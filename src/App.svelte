<!-- Javascript code -->
<script>

  //: Variables

let todos = [];
let task = "";
let filter = 'all';

//: Functions

const addTask = () =>{
    todos = [{
      task:task,
      status: "pending"
    }, ...todos];

    task = "";
}

const markComplete = (i) =>{
    todos[i].status = "completed";
    todos = [ ...todos ];

}

const removeTask = (i) =>{
  todos.splice( i, 1 );
  todos = [ ...todos ];
}

</script>

<!-- Css Styles -->

<style>
  *{
    margin: 0px;
    padding: 0px;
  }
  h1{
    text-align: center;
    font-size: 400;
    font-family: cursive;
    margin-bottom: 50px;
    color: #ffc300;
  }
  .container1{
    display:flex;
    justify-content:center;
		align-items:center;
    width:98%;
		height:90vh;
    flex-direction: column;
    border: #000814 solid 5px;
    border-radius: 10%;
    margin-top: 10px;
  }
  .container {
		width:30%;
		height:50vh;
		background:#000814;
		display:flex;
		justify-content:center;
		align-items:center;
    border-radius: 10px;
	}
  .todo > div {
    margin: 20px 0px;
  }

  .todo .form {
    display: flex;
  }

  .todo .form input
  .todo .form buttom{
    border: 1px solid #ffc300;
    height: 40px;
    outline: none;
    border-radius: 20px;
  }
  .todo .form input {
		flex:1;
		text-indent:20px;
	}
  .todo .form button {
		width:60px;
		margin-left:5px;
		color:#ffc300;
		cursor:pointer;
	}
  .todo .tasks {
		min-height:100px;
    color:#f5f5f5;
	}
  .todo .tasks > .task {
		margin:10px 0px;
		display:flex;
	}
  .todo .tasks > .task > div {
		flex:1;
	}
  .todo .tasks > .task > button {
		width:25px;
		height:25px;
		border:1px solid #ffc300;
		color:#ffc300;
		border-radius:50%;
		margin:0px 5px;
		cursor:pointer;
	}
  .todo .tasks > .task > button.active{
		background:#ffc300;
		color:#f5f5f5;
	}
  .todo .filters {
		display:flex;
		justify-content:space-between;
	}
  .todo .filters > button {
		padding:10px 8px;
		border:1px solid #ffc300;
		color:#000814;;
		border-radius:20px;
		cursor:pointer;
	}
  .todo .filters > button.active {
		background:#ffc300;
		color:#f5f5f5;
	}
</style>

<!-- Html structure -->

<div class="container1">
  <h1>ToDo App + Svelte </h1>
  <div class="container">
	<div class="todo">
		<div class="form">
			<input type="text" bind:value={task}/>
			<button on:click={addTask}>
				Add
			</button>
		</div>
		<div class="tasks">
			{#each todos as todo, i}
				{#if filter=='all'}
					<div class="task">
						<div>
							{todo.task}
						</div>
						<button class="{todo.status=='completed'?'active':''}" on:click={()=>{markComplete(i)}}>
							&#10004;
						</button>
						<button on:click={()=>{removeTask(i)}}>
							&#10006;
						</button>
					</div>
				{:else if filter=='completed'}
					{#if todo.status=='completed'}
						<div class="task">
							<div>
								{todo.task}
							</div>
							<button on:click={()=>{removeTask(i)}}>
								&#10006;
							</button>
						</div>
					{/if}
				{:else}
					{#if todo.status=='pending'}
						<div class="task">
							<div>
								{todo.task}
							</div>
							<button class="{todo.status=='completed'?'active':''}" on:click={()=>{markComplete(i)}}>
								&#10004;
							</button>
						</div>
					{/if}
				{/if}
			{/each}
		</div>
		<div class="filters">
			<button class="{filter=='all'?'active':''}" on:click={()=>{filter='all'}}>
				All
			</button>
			<button class="{filter=='completed'?'active':''}" on:click={()=>{filter='completed'}}>
				Completed
			</button>
			<button class="{filter=='incomplete'?'active':''}" on:click={()=>{filter='incomplete'}}>
				Incomplete
			</button>
		</div>
	</div>
</div>
  </div>

