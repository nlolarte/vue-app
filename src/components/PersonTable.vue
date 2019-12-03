<template>
  <div id="person-table">
    <p v-if="persons.length < 1" class="empty-table">
      No famous persons
    </p>
    <table v-else>
      <thead>
        <tr>
          <th>Name</th>
          <th>Bio</th>
          <th>Date of birth</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="person in persons" :key="person.id">
          <td v-if="editing === person.id">
            <input type="text" v-model="person.name" />
          </td>
          <td v-else>{{ person.name }}</td>
          <td v-if="editing === person.id">
            <input type="text" v-model="person.bio" />
          </td>
          <td v-else>{{ person.bio }}</td>
          <td v-if="editing === person.id">
            <input type="text" v-model="person.dob" />
          </td>
          <td v-else>{{ person.dob }}</td>
          <td v-if="editing === person.id">
            <button @click="editPerson(person)">Save</button>
            <button class="muted-button" @click="cancelEdit(person)">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(person)">Edit</button>
            <button @click="$emit('delete:person', person.name)">Delete</button>
          </td>
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
    data() {
      return {
        editing: null,
      }
    },
    methods: {
      editMode(person) {
        this.cachedPerson = Object.assign({}, person)
        this.editing = person.id
      },

      cancelEdit(person) {
        Object.assign(person, this.cachedPerson)
        this.editing = null;
      },

      editPerson(person) {
        if (person.name === '' || person.bio === '' || person.dob === '') return
        this.$emit('edit:person', person.name, person)
        this.editing = null
      }
    }
  }
</script>

<style scoped>
  button {
    margin: 0 0.5rem 0 0;
  }
</style>
