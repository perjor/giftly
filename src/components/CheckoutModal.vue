<template>
  <div class="modal fade right" :id="`checkoutModal${i}`" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h4 class="modal-title">Checkout: {{ category.name }}</h4>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        </div>
        <div class="modal-body">
          <template v-if="$store.state.currentBox">
            <Card :name="$store.state.currentBox.name" :info="$store.state.currentBox.info" class="col-6"></Card>
            <form>
              <div class="form-group">
                <label class="display-2">€ {{ price }}</label>
                <input type="range" class="form-control-range" id="formControlRange" v-model="price">
              </div>
            </form>
            <button type="button" class="btn" data-toggle="modal" data-target="#exampleModal">Nu kopen</button>
            <button type="button" class="btn" data-dismiss="modal" aria-label="Close">Annuleren</button>
            <PayModal />
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from "@/components/Card";
import PayModal from "@/components/PayModal";

export default {
  props: {
    category: Object,
    i: Number
  },
  components: {
    PayModal,
    Card
  },
  computed: {
    price: {
      get () {
        return this.$store.state.price
      },
      set (value) {
        this.$store.commit('updatePrice', value)
      }
    }
  }
}
</script>