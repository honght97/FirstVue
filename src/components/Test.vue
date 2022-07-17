<template>
  <div>
    <!-- first learn -->
    <div class="hello">
      Hello from {{ lastName }} and {{ isHello ? `${firsName} ${lastName}` : '' }}
      <button @click="onChangeName">Change Name</button>
      <div class="modal" v-if="isShowModal">
        <p>Modal content</p>
      </div>
    </div>
    <!-- mouse event -->
    <div class="card-container">
      <div class="card" @mouseover="onLogEvent">Mouse over (Enter)</div>
      <div class="card" @mouseleave="onLogEvent">Mouse leave </div>
      <div class="card" @dblclick="onLogEvent($event, 150, 100)">Double click</div>
      <div class="card" @mousemove="onMouseMove">Mouse Move {{ `x= ${x}; y= ${y}` }}</div>
    </div>
    <!-- list rendering -->
    <div class="products" :class="classTesting">
      <div class="products__item" v-for="product in products" :class="{ cart: product.isCart }"
        @dblclick="onToogleCart($event, product)">
        <img v-bind:src="product.img" alt="" class="products__thumb">
        <h3>{{ product.name }}</h3>
        <p>{{ product.price }}</p>
      </div>
    </div>
    <!-- computed property -->
    <div>
      <button @click="onSortPriceLow">Giá từ thấp tới cao</button>
      <button @click="onSortPriceHigh">Giá từ cao xuống thấp</button>

    </div>
    <p>there are products price lower 1200</p>
    <div class="products" :class="classTesting">
      <div class="products__item" v-for="product in productsComputed" :class="{ cart: product.isCart }"
        @dblclick="onToogleCart($event, product)">
        <img v-bind:src="product.img" alt="" class="products__thumb">
        <h3>{{ product.name }}</h3>
        <p>{{ product.price }}</p>
      </div>
    </div>
  </div>
</template>
<script>
import { computed } from '@vue/runtime-core';
export default {
  data() {
    return {
      firsName: "Hoang",
      lastName: "Hong",
      isHello: true,
      isShowModal: false,
      x: 0,
      y: 0,
      classTesting: "flex",
      products: [
        {
          name: "san A",
          price: 1200,
          img: "src/assets/img/cat-1.jpg",
          isCart: true,
        }, {
          name: "san b",
          price: 1500,
          img: "src/assets/img/cat-2.avif",
          isCart: false,
        },
        {
          name: "san c",
          price: 1000,
          img: "src/assets/img/cat-3.avif",
          isCart: false,
        },
      ],
    }
  },
  methods: {
    onChangeName() {
      this.firsName = "Thao";
      this.isShowModal = !this.isShowModal;
    },
    onLogEvent(event, newX, newY) {
      console.log("Running event...", event);
      this.x = newX;
      this.y = newY;
    },
    onMouseMove(event) {
      console.log(event);
      this.x = event.offsetX;
      this.y = event.offsetY;


    },
    onToogleCart(event, product) {
      product.isCart = !product.isCart;
    },
    onSortPriceLow() {
      this.products.sort((a, b) => {
        return a.price - b.price;
      })
    },
    onSortPriceHigh() {
      this.products.sort((a, b) => {
        return b.price - a.price;
      })
    },
  },
  computed: {
    productsComputed() {
      return this.products.filter((product) => {
        return product.price < 1200;
      })
    }
  }
}
</script>
<style scoped>
.flex {
  display: flex;
  column-gap: 30px;
}

.card {
  width: 180px;
  height: 180px;
  background: #eee;
  margin-bottom: 30px;
  color: orangered;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 20px;
}

.card-container {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  column-gap: 30px;
  margin-top: 30px;

}

.products__item {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
  flex-direction: column;
}

.products__item.cart {
  background: orchid;
  color: black;
  box-shadow: 0 10px 10px;
}

.products__thumb {
  width: 100px;
  height: 100px;
  object-fit: cover;
}
</style>