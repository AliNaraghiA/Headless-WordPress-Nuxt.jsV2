<!-- pages/contact.vue -->
<template>
  <div>
    <form @submit.prevent="submitForm">
      <!-- Form fields go here -->
      <button type="submit">Send Message</button>
    </form>
    <div v-if="successMessage" class="success-message">{{ successMessage }}</div>
  </div>
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
      successMessage: '',
    }
  },
  methods: {
    handleAttachment(event) {
      this.attachment = event.target.files[0]
    },
    async submitForm() {
      const apiUrl = '/wp-json/contact-form-7/v1/contact-forms/your_contact_form_id/feedback'

      const formData = new FormData()
      formData.append('your-name', this.name)
      formData.append('your-subject', this.subject)
      formData.append('your-email', this.email)
      formData.append('your-message', this.message)
      formData.append('your-attachment', this.attachment)

      try {
        const response = await axios.post(apiUrl, formData, {
          headers: { 'Content-Type': 'multipart/form-data' },
        })

        if (response.data.status === 'mail_sent') {
          this.successMessage = 'Your message was sent successfully!'
        } else {
          this.successMessage = 'Failed to send your message. Please try again.'
        }
      } catch (error) {
        console.error(error)
        this.successMessage = 'Failed to send your message. Please try again.'
      }
    },
  },
}
</script>
