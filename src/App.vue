<template>
  <div id="app" class="small-container">
    <h1>Famous Persons</h1>

    <person-form @add:person="addPerson" />
    <person-table
      :persons="persons"
      @delete:person="deletePerson"
      @edit:person="editPerson"
    />
  </div>
</template>

<script>
  import PersonTable from '@/components/PersonTable.vue'
  import PersonForm from '@/components/PersonForm.vue'
  import axios from 'axios'

  export default {
    name: 'app',
    components: {
      PersonForm,
      PersonTable,
    },
    data() {
      return {
        persons: [],
      }
    },
    mounted() {
      this.getPersons()
    },
    methods: {
      getPersons() {
        try {
          axios.get('http://localhost:8080/famouspersons')
            .then((response) => {
              /* eslint-disable no-console */
              console.log(response.data);
              console.log(response.status);
              console.log(response.statusText);
              console.log(response.headers);
              console.log(response.config);
              /* eslint-enable no-console */
              this.persons = response.data;
            });
        } catch (error) {
          /* eslint-disable no-console */
          console.error(error)
          /* eslint-enable no-console */
        }
      },

      addPerson(person) {
        try {
          axios.post("http://localhost:8080/famouspersons", person)
            .then((response) => {
            /* eslint-disable no-console */
            console.log(response.data);
            console.log(response.status);
            console.log(response.statusText);
            console.log(response.headers);
            console.log(response.config);
            /* eslint-enable no-console */
            this.persons = [...this.persons, response.data];
          });
        } catch (error) {
          /* eslint-disable no-console */
          console.error(error)
          /* eslint-enable no-console */
        }
      },

      editPerson(name, updatedPerson) {
        try {
          /* eslint-disable no-console */
          console.log(name);
          /* eslint-enable no-console */
          axios.put(`http://localhost:8080/famouspersons/${name}`, {
            name: updatedPerson.name,
            bio: updatedPerson.bio,
            dob: updatedPerson.dob,
          })
            .then((response) => {
            /* eslint-disable no-console */
            console.log(response.data);
            console.log(response.status);
            console.log(response.statusText);
            console.log(response.headers);
            console.log(response.config);
            /* eslint-enable no-console */
            this.persons = this.persons.map(person => person.name === name ? response.data : person)
          });
        } catch (error) {
          /* eslint-disable no-console */
          console.error(error)
          /* eslint-enable no-console */
        }
      },

      deletePerson(name) {
        try {
          axios.delete(`http://localhost:8080/famouspersons/${name}`)
            .then((response) => {
            /* eslint-disable no-console */
            console.log(response.data);
            console.log(response.status);
            console.log(response.statusText);
            console.log(response.headers);
            console.log(response.config);
            /* eslint-enable no-console */
            this.persons = this.persons.filter(person => person.name !== name)
          });
        } catch (error) {
          /* eslint-disable no-console */
          console.error(error)
          /* eslint-enable no-console */
        }
      },

    }
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>
