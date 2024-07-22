<template>
  <nav class="navbar mb-5" role="navigation" aria-label="main navigation">
    <div class="navbar-menu">
      <div class="navbar-start">
        <a class="navbar-item is-size-5 is-uppercase">A-Simple-Todo-Manager</a>
      </div>

      <div class="navbar-end">
        <div class="navbar-item">
          <div class="buttons">
            <a class="button is-primary" @click.prevent="$emit('add')">
              <strong>Add Task</strong>
            </a>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {};
</script>
