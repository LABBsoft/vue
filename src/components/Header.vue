<template>
    <nav>
        <div class="title">luciano</div>
        <div>
            <button><span class="material-icons-outlined">add</span></button>
        </div>
    </nav>
</template>

<script lang="ts">
import { ref, defineComponent } from 'vue'
export default defineComponent({
  name: 'Header',
  props: {},
  setup: () => {
  }
})
</script>

<style scoped lang="scss">
@import "../styles/_variables.scss";

nav {
    position: fixed;
    top: 0;
    width: 100%;
    height: 55px;

    display: flex;
    justify-content: space-between;
    align-items: center;
    
    background-color: $bg-light;
    border-bottom: 1px solid $border;
}

.title {
    font-family: "Roboto";
    padding-left: 1em;
}

.material-icons-outlined {
    font-size: 36px;
    
}

a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
