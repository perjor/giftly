<template>
  <section>
    <div class="categories container mb-5">
      <h1 class="page-title pb-4">Categorieën</h1>
      <div class="row justify-content-around">
        <div v-for="(category, key, i) in this.$store.state.data.categories" :key="i" class="col-12 col-md-6">
          <Card :key="i" :boxImg="category.img">
            <div class="d-flex justify-content-between mb-2">
              <h3 class="card-title">{{ category.name }}</h3>
              <button type="button" class="btn btn-lg btn-red" data-toggle="modal" :data-target="`#checkoutModal${i}`" @click="selectBox(category, key)">Ik wil deze</button>
            </div>
            <p class="card-text">{{ category.info }}</p>
            <a href="#" class="text-red mt-2" data-toggle="modal" :data-target="`#categoryModal${i}`">Meer info</a>
            <CheckoutModal :i="i" :category="category" />
            <InfoModal :i="i" :category="category" />
          </Card>
        </div>
      </div>
    </div>
    <Footer></Footer>
  </section>
</template>

<script>
import Card from '@/components/Card'
import InfoModal from '@/components/InfoModal'
import CheckoutModal from '@/components/CheckoutModal'
import Footer from '@/components/Footer'
import { mapMutations } from 'vuex'

export default {
  components: {
    Card,
    InfoModal,
    CheckoutModal,
    Footer
  },
  methods: {
    ...mapMutations(['showAlert', 'clearCurrentBox']),
    selectBox(category, type) {
      this.clearCurrentBox()

      category = {
        type,
        ...category,
      }
      this.$store.commit('changeBox', category)
    },
  },
}
</script>

<style lang="scss" scoped>
.card {
  min-height: 400px;
}
</style>
