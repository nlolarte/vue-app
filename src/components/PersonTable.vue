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
            <button @click="$emit('delete:person', person.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  // import axios from 'axios'

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

        // axios({
        //   method: "PUT",
        //   url: "http://127.0.0.1:3000/famouspersons/".concat(person.name),
        //   params: {
        //     name: person.name
        //   },
        //   data: {
        //     name: person.name,
        //     bio: person.bio,
        //     dob: person.dob
        //   },
        //   headers: {
        //     "content-type": "text/plain"
        //   }
        // });

        this.$emit('edit:person', person.id, person)
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
