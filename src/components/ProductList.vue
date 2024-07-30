<template>
  <transition-group
    name="fade"
    tag="div"
    @before-enter="before"
    @enter="enter"
    @leave="leave"
  >
    <div
      class="row d-none mb-3 align-items-center"
      v-for="(item, index) in showItem"
      :key="index">
        <div class="col-1 m-auto">
            <button class="btn btn-info" @click="$emit('add',item)">+</button>
        </div>
        <div class="col-sm-4">
            <img :src="item.image" :alt="item.name" class="img-fluid d-block">
        </div>
        <div class="col">
            <h3 class="text-info">{{ item.name }}</h3>
            <p class="h5 float-right"></p>
            <price-component  :value="Number(item.price)"></price-component>
        </div>
    </div>
  </transition-group>
</template>

<script>
import PriceComponent from './PriceComponent.vue';

export default {
    name: "product-list",
    comments: {
        PriceComponent,
    },
    props: ["product", "maximum"],
    computed: {
        showItem: function() {
            let max = this.maximum;
            return this.products.filter(function(item) {
                return item.price <= max;
            });
        }
    },
    methods: {
        before: function (el) {
            el.className = 'd-none'
        },
        enter: function (el) {
            var delay = el.dataset.index * 100;
            setTimeout(function () {
                el.className = 'row d-flex mb-3 align-items-center'
            }, delay)
        },
        leave: function (el) {
      var delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className = "row d-flex mb-3 align-items-center ";
            }, delay)
        },
    }
}
</script>
