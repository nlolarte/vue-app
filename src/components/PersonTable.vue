<template>
  <div id="person-table">
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Bio</th>
          <th>Date of birth</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="person in persons" :key="person.id">
          <td>{{ person.name }}</td>
          <td>{{ person.bio }}</td>
          <td>{{ person.dob }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'person-table',
    props: {
      persons: Array,
    },
  }
</script>

<style scoped></style>
