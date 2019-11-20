<template>
  <div id="person-form">
    <form>
      <label>Name</label>
      <input v-model="person.name" type="text" />
      <label>Bio</label>
      <input v-model="person.bio" type="text" />
      <label>Date of Birth</label>
      <input v-model="person.dob" type="text" />
      <button>Add Famous Person</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'person-form',
    data() {
      return {
        person: {
          name: '',
          bio: '',
          dob: '',
        },
      }
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>
