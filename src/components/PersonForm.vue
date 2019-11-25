<template>
  <div id="person-form">
    <form @submit.prevent="handleSubmit">
      <label>Name</label>
      <input
        ref="first"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="person.name"
        @focus="clearStatus"
        @keypress="clearStatus"
      />
      <label>Bio</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidBio }"
        v-model="person.bio"
        @focus="clearStatus"
      />
      <label>Date of Birth</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidDob }"
        v-model="person.dob"
        @focus="clearStatus"
      />
      <p v-if="error && submitting" class="error-message">
        ❗Please fill out all required fields
      </p>
      <p v-if="success" class="success-message">
        ✅ Employee successfully added
      </p>
      <button>Add Famous Person</button>
    </form>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'person-form',
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        person: {
          name: '',
          bio: '',
          dob: '',
        },
      }
    },
    methods: {
      handleSubmit() {
        this.submitting = true
        this.clearStatus()

        if (this.invalidName || this.invalidBio || this.invalidDob) {
          this.error = true
          return
        }

        this.$emit('add:person', this.person)
        this.$refs.first.focus()

        axios({
          method: "POST",
          url: "http://127.0.0.1:3000/famouspersons",
          data: this.person,
          headers: {
            "content-type": "text/plain"
          }
        });

        this.person = {
          name: '',
          bio: '',
          dob: '',
        }
        this.error = false
        this.success = true
        this.submitting = false
      },
      clearStatus() {
        this.success = false
        this.error = false
      }
    },
    computed: {
      invalidName() {
        return this.person.name === ''
      },

      invalidBio() {
        return this.person.bio === ''
      },

      invalidDob() {
        return this.person.dob === ''
      },
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>
