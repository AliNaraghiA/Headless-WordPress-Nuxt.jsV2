<template>
  <form @submit.prevent="submitForm">
    <input type="text" name="name" v-model="name" />
    <input type="text" name="subject" v-model="subject" />
    <input type="email" name="email" v-model="email" />
    <textarea name="message" v-model="message"></textarea>
    <input type="file" ref="attachment" @change="handleAttachment" />
    <button type="submit">Send Message</button>
  </form>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      name: '',
      subject: '',
      email: '',
      message: '',
      attachment: null,
    }
  },
  methods: {
    handleAttachment(event) {
      this.attachment = event.target.files[0]
    },
    async submitForm() {
      const apiUrl = 'http://graph.local/wp-json/contact-form-7/v1/contact-forms/23/feedback'

      const formData = new FormData()
      formData.append('your-name', this.name)
      formData.append('your-subject', this.subject)
      formData.append('your-email', this.email)
      formData.append('your-message', this.message)
      formData.append('your-file', this.attachment)

      try {
        const response = await axios.post(apiUrl, formData, {
          headers: { 'Content-Type': 'multipart/form-data' },
        })
        console.log(response)
      } catch (error) {
        console.error(error)
      }
    },
  },
}
</script>
