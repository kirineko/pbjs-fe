<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        pbjsfe
      </h1>
      <h2 class="subtitle">
        My bee&#39;s knees Nuxt.js project
      </h2>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
      <div>
        <button @click="getpb">
          getData
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import awesome from '@/proto/test_pb'

export default {
  components: {
    Logo
  },

  methods: {
    async getpb() {
      await this.$axios({
        method: 'get',
        url: '/proto/get',
        headers: { 'contentType': 'application/x-protobuf' } })
        .then((res) => {
          const pm = awesome.Test.deserializeBinary(res.data.data)
          const protoBuf = pm.toObject()
          // eslint-disable-next-line no-console
          console.log('protoBuf: ', protoBuf) // 打印出来是一个对象
        })
        .catch((error) => {
          // eslint-disable-next-line no-console
          console.log(error)
        })
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
