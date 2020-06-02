<template>
  <div class="searchBar">
    <input @keypress.enter="onInput" type="text">
  </div>
</template>

<script>
    export default {
        name: "SearchBar",
        methods: {
            onInput(event) {
                // 1. 부모로 커스텀 이벤트를 날린다.
                this.$emit('input-change',event.target.value)
                this.$router.push({name:'Home'})
            }
        }
    }
</script>

<style scoped>
  .searchBar {
    text-align: center;
    margin: 10px;
  }
  .searchBar > input {
    width: 75%;
  }
</style>