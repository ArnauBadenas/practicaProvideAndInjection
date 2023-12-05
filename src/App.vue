<template>
  <header>
  </header>
  <main>
    <section id="restaurant">
      <article class="orders">
        <h1>Tom's Dinner</h1>
      </article>
      <img
        src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/19d15c51-f7c6-4914-838c-06e5599f84b6/dfrv9yk-d36c8c4e-9502-43b0-b41a-6077aa7378bf.gif?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzE5ZDE1YzUxLWY3YzYtNDkxNC04MzhjLTA2ZTU1OTlmODRiNlwvZGZydjl5ay1kMzZjOGM0ZS05NTAyLTQzYjAtYjQxYS02MDc3YWE3Mzc4YmYuZ2lmIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.uCioa3ijsWL19j-TA8qJm1cUMBTO1lBYbOfV8j0geSw"
        alt="">
    </section>
    <section id="order">
      <h2>{{ orderTitle || "Your order" }}</h2>
      <input type="text" name="order-title" id="order-title" v-model="orderTitle" placeholder="Write your order's name!">
      <div>
        <button type="submit">Place Order</button>
      </div>
      <fieldset id="currency">
        <label>Currency</label>
        <select v-model="currency">
          <option value="€" selected>€</option>
          <option value="$">$</option>
        </select>
      </fieldset>
      <fieldset>
        <order @submit-order="submitOrder(order)" v-for="order in orders" :key="order.name" :order="order"></order>
      </fieldset>

    </section>
    <section id="cart">
      <h2>Current order</h2>
      <table>
        <tr v-for="item in cart">
          <td>{{ item.name }} </td>
          <td>{{ item.price }}€</td>
        </tr>
        <br />
        <tr>
          <td>Subtotal</td>
          <td>{{ totalPrice() }}€</td>
        </tr>
        <tr>
          <td>TOTAL</td>
          <td>{{ totalPrice() + ((totalPrice() / 100) * 21) }}€</td>         
        </tr>
      </table>
    </section>
  </main>
  <footer>

  </footer>
</template>

<script setup lang="ts">
import { type Ref, ref, provide } from 'vue';
import type { Order } from './types/Order';
import order from './components/order.vue';
import type { Currency } from './types/Currency';
const orders: Ref<Order[]> = ref([{ name: "Hamburger 🍔.", price: 5 },
{ name: "Cheeseburger 🧀", price: 6 },
{ name: "Impossible Burger 🥕", price: 7 },
{ name: "Fries 🍟", price: 2 }])

const orderTitle: Ref<string> = ref("")

const cart: Ref<Order[]> = ref([])

function submitOrder(order: Order) {
  cart.value.push(order)
}
function totalPrice(): number {
  let total = 0
  for (let item of cart.value) {
    total += item.price
  }
  return total
}

//provide currency
let currency: Ref<Currency> = ref("€")
provide<Ref<Currency>>('currency', currency) //TODO type
</script>

<style scoped>
.orders {
  position: relative;
  top: 50px;
  left: 10px;
  margin-top: -56px;
}

main {
  display: grid;
  align-items: start;
  grid-template-rows: auto auto;
  grid-template-columns: auto auto;
}

#restaurant {
  grid-column: span 2;

}

img {
  width: 100vw;
  height: 300px;
  object-fit: cover;

}

#order {
  display: flex;
  flex-direction: column;
  align-items: center;
}

#currency {
  width: 200px;
  display: flex;
  justify-content: space-between;
}
</style>
