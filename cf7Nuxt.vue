<template>
    <form @submit.prevent="submitForm">
      <div>
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="name" required>
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" required>
      </div>
      <div>
        <label for="message">Message:</label>
        <textarea id="message" v-model="message" required></textarea>
      </div>
      <div>
        <label for="file">File:</label>
        <input type="file" id="file" ref="file" @change="onFileChange">
      </div>
      <button type="submit">Submit</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        message: '',
        file: null
      }
    },
    methods: {
      onFileChange() {
        this.file = this.$refs.file.files[0]
      },
      async submitForm() {
        const formData = new FormData()
        formData.append('your-name', this.name)
        formData.append('your-email', this.email)
        formData.append('your-message', this.message)
        if (this.file) {
          formData.append('your-file', this.file, this.file.name)
        }
        const response = await this.$axios.$post('http://nuxtwp.local/wp-json/contact-form-7/v1/contact-forms/124/feedback', formData, {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        })
        console.log(response)
      }
    }
  }
  </script>
  
