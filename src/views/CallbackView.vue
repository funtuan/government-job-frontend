<template>
  <div class="page">
    <div class="loading" v-if="!error && !id">
      綁定中
    </div>
    <div class="success" v-if="!error && id">
      <div>
        綁定成功！
      </div>
      <div class="back" @click="$router.push('/')">
        回首頁
      </div>
    </div>
    <div class="loading" v-if="error">
      <div>
        綁定失敗
      </div>
      <div class="back" @click="$router.push('/')">
        回首頁
      </div>
    </div>
  </div>
</template>

<style>
a {
  text-decoration: none;
  color: #000;

}

.page {
  margin: 0 auto;
  max-width: 600px;
  margin-bottom: 80px;
  padding-left: 5px;
  padding-right: 5px;

  text-align: center;
  font-size: 20px;
}


.back {
  margin-top: 20px;
  color: #fff;
  background: rgb(15, 82, 82);
  padding: 10px 20px;
  border-radius: 5px;
  display: inline-block;
}


</style>

<script>
  export default {
    data:() => ({
      id: null,
      error: null,
    }),
    methods: {
      // 綁定通知
      async bind() {
        const {
          code,
          state,
        } = this.$route.query;
        if (!code || !state) {
          this.error = true;
          return;
        }

        const stateObj = JSON.parse(decodeURIComponent(state));

        // eslint-disable-next-line
        void Tinybird.trackEvent('bind_notify', {
          condition: stateObj.condition,
        })
        // curl -X POST -H "Content-Type: application/json" -d '{"authorizationCode": "YOUR_AUTHORIZATION_CODE", "redirectUri": "YOUR_REDIRECT_URI", "condition": {"sysnams": ["綜合行政", "文教行政"]}}' http://localhost:8787/notifyConfig
        const res = await this.axios.post(process.env.VUE_APP_BACKEND_HOST + 'notifyConfig', {
          authorizationCode: code,
          redirectUri: window.location.origin + '/callback',
          condition: stateObj.condition,
        })

        this.id = res.data.id;
      }
    },
    mounted() {
      this.bind();
    },
  }
</script>