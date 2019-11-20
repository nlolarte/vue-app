<template>
  <div id="app" class="small-container">
    <h1>Famous Persons</h1>

    <person-form />
    <person-table :persons="persons" />
  </div>
</template>

<script>
  import PersonTable from '@/components/PersonTable.vue'
  import PersonForm from '@/components/PersonForm.vue'

  export default {
    name: 'app',
    components: {
      PersonForm,
      PersonTable,
    },
    data() {
      return {
        persons: [
          {
            id: 1,
            name: 'Kobe Bryant',
            bio: 'NBA Player',
            dob: '8/23/1978',
          },
          {
            id: 2,
            name: 'Barack Obama',
            bio: 'US President',
            dob: '8/4/1961',
          },
          {
            id: 3,
            name: 'Bill Gates',
            bio: 'Programmer',
            dob: '10/28/1955',
          },
        ],
      }
    },
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
