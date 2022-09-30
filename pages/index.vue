<template>
  <div>
    <h1>Index page</h1>
    <div>
      <button :disabled="fetching" @click="callFunction">
        {{
          fetching
            ? 'Fetch data from serverless function'
            : 'Call serverless function'
        }}
      </button>
    </div>
    <div>
      <h4>Response:</h4>
      <code>{{ response || 'click the button above' }}</code>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      response: null,
      fetching: false,
    }
  },
  methods: {
    async callFunction() {
      this.fetching = true
      try {
        const { data } = await this.$axios.get(
          `${window.location.href}api/test`
        )
        this.response = data
      } catch (e) {
        this.response = e
      } finally {
        this.fetching = false
      }
    },
  },
}
</script>
