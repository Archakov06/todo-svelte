<link rel="stylesheet" href="/app.css">

<script>
  import ListItem from './components/ListItem.svelte';
  import TaskField from './components/TaskField.svelte';

  let tasks = [
    {
      text: 'Изучить Svelte',
      completed: true,
    },
    {
      text: 'Разработать ToDo на Svelte',
      completed: false,
    },
  ];

  const onAddTask = text => {
    tasks = [...tasks, {
      text,
      completed: false
    }];
  }

  const onToggleCompleted = index => {
    tasks[index].completed = !tasks[index].completed;
  }

  const onRemoveTask = index => {
    if (confirm("Вы действительно хотите удалить?")) {
      tasks = tasks.filter((_, curIdx) => index !== curIdx);
    }
  }
</script>

<div class="todo">
  <div class="todo__header">
    <h4>Список задач</h4>
  </div>
  <TaskField onAddTask={onAddTask} />
  <div class="todo__list">
    {#each tasks as task, index}
    <ListItem index={index} onRemoveTask={onRemoveTask} onToggleCompleted={onToggleCompleted} text={task.text} completed={task.completed} />
    {/each}
  </div>
</div>

