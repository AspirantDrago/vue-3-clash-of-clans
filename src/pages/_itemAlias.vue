<template>
  <div class="wrapper-person">
    <div v-if="item">
      <img :src="item.img" :alt="item.descr" />
      <h1 style="color: #ffffff;" class="title">{{ item.title }}</h1>
      <p>{{ item.descr }}</p>
      <CardFooterVue :info="item.info" />
      <div>
        <router-link to="/" class="btn btnWhite">Back to home</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import items from '@/seeders/items.js'
import CardFooterVue from '@/components/UI/CardFooter.vue'

export default {
  components: {
    CardFooterVue,
  },
  data() {
    return {
      item: null
    }
  },
  created() {
    const alias = this.$route.params.itemAlias
    const item = items.find(el => el.alias === alias)
    if (item == undefined) {
      this.$router.push({name: '404'})
      return
    }
    this.item = item
  }
}
</script>

<style lang="scss">
.wrapper-person {
  text-align: center;
  .card-stats {
    margin: 30px 0;
    border-radius: 14px;
  }
}
</style>
