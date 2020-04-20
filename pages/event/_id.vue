<template>
  <h1>{{ event.title }}</h1>
</template>
<script>
import EventService from '@/services/EventService.js'
export default {
  async asyncData({ error, params }) {
    try {
      const { data } = await EventService.getEvent(params.id)
      return {
        event: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: `Unable to fetch event # ${params.id}.`
      })
    }
  },

  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `What you need to know about ${this.event.title}`
        }
      ]
    }
  }
}
</script>
