<template>
  <div class="conteiner" style="overflow-x:hidden">
    <b-navbar type="dark" variant="dark">
      <b-navbar-nav>
        <transition name="fade">
          <div v-show="alert" :class="[`alert-${colorAlert}`, 'alert']">Added</div>
        </transition>
        <b-nav-item-dropdown right>
          <template #button-content>
            {{ basketAllItemCount }} &#128722;
          </template>
          <b-dropdown-item v-show="basket.length === 0">
            sepet boş
          </b-dropdown-item>
          <b-dropdown-item
            v-for="(el, i) in basket"
            :key="i"
            style="width: 400px"
          >
            {{ el.item.color }} ({{ el.size }}) -
            {{ (parseInt(el.price) * el.count).toFixed(2) }}$
            <b-button
              class="mx-2"
              @click="productCal({ value: el, type: '-' })"
              variant="dark"
              size="sm"
              >-</b-button
            >
            <b-button
              class="mx-2"
              @click="productCal({ value: el, type: '+' })"
              variant="success"
              size="sm"
              >+</b-button
            >
            <b-button
              @click="productCal({ value: el, type: 'del' })"
              variant="danger"
              size="sm"
              >X</b-button
            >
          </b-dropdown-item>
          <b-dropdown-item> Total : {{ getTotal }} $ </b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-navbar>
    <b-row class="mt-2">
      <Card
        v-for="(item, i) in cardList"
        :key="i"
        :info="item"
        @addShoe="productCal({ value: $event, type: 'add' })"
      />
    </b-row>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  name: "Cards",
  components: {
    Card,
  },
  computed: {
    basketAllItemCount() {
      let count = 0;
      for (let i = 0; i < this.basket.length; i++) {
        count += this.basket[i].count;
      }
      return count;
    },
    getTotal() {
      let total = 0;
      for (let i = 0; i < this.basket.length; i++) {
        total += this.basket[i].price * this.basket[i].count;
      }
      return total.toFixed(2);
    },
  },
  methods: {
    productCal(val) {
      this.colorAlert = val.value.item.color;
      let index = this.basket.findIndex(
        (el) =>
          el.item.color == val.value.item.color && el.size == val.value.size
      );
      console.log(index);
      switch (val.type) {
        case "add":
          if (index >= 0) {
            this.basket[index].count++;
          } else {
            this.basket.unshift({ ...val.value, count: 1 });
          }
          this.alert = true;
          setTimeout(() => {
            this.alert = false;
          }, 3000);
          break;
        case "+":
          this.basket[index].count++;
          break;
        case "-":
          if (this.basket[index].count > 1) {
            this.basket[index].count--;
          } else {
            this.basket.splice(index, 1);
          }
          break;
        case "del":
          this.basket.splice(index, 1);
          break;
        default:
      }
    },
  },
  data() {
    return {
      colorAlert: "white",
      alert: false,
      basket: [],
      cardList: [
        {
          id: 1,
          slogan: "WOMEN'S RUNNİNG SHOE",
          title: "NIKE EPIC REACT FLYKNIT",
          color: "pink",
          img: "src/assets/pink.jpg",
          content:
            "Lorem ipsum dolor, sit amet conste dolore illum. Amet quibusdam nisi perferendis sapiente iure eveniet cumque, re eveniet cumqueveniet cumque, eenim tempore reprehenderit dolor.",
          props: [
            {
              shoeSize: 33,
              price: "150",
              width: "86%",
            },
            {
              shoeSize: 34,
              price: "151",
              width: "88%",
            },
            {
              shoeSize: 35,
              price: "152",
              width: "90%",
            },
            {
              shoeSize: 36,
              price: "153",
              width: "92%",
            },
            {
              shoeSize: 37,
              price: "154",
              width: "94%",
            },
            {
              shoeSize: 38,
              price: "155",
              width: "96%",
            },
            {
              shoeSize: 39,
              price: "156",
              width: "98%",
            },
            {
              shoeSize: 40,
              price: "157",
              width: "100%",
            },
          ],
        },
        {
          id: 2,
          slogan: "MAN'S RUNNİNG SHOE",
          title: "NIKE EPIC REACT FLYKNIT",
          color: "blue",
          img: "src/assets/blue.png",
          content:
            "Lorem ipsum dolor, sit amet conste dolore illum. Amet quibusdam nisi perferendis sapiente iure eveniet cumque, re eveniet cumqueveniet cumque, eenim tempore reprehenderit dolor.",
          props: [
            {
              shoeSize: 31,
              price: "131",
              width: "86%",
            },
            {
              shoeSize: 32,
              price: "132",
              width: "88%",
            },
            {
              shoeSize: 33,
              price: "133",
              width: "90%",
            },
            {
              shoeSize: 34,
              price: "134",
              width: "92%",
            },
            {
              shoeSize: 35,
              price: "135",
              width: "94%",
            },
            {
              shoeSize: 36,
              price: "136",
              width: "96%",
            },
            {
              shoeSize: 37,
              price: "137",
              width: "98%",
            },
            {
              shoeSize: 38,
              price: "138",
              width: "100%",
            },
          ],
        },
        {
          id: 3,
          slogan: "WOMEN'S RUNNİNG SHOE",
          title: "NIKE EPIC REACT FLYKNIT",
          color: "red",
          img: "src/assets/red.png",
          content:
            "Lorem ipsum dolor, sit amet conste dolore illum. Amet quibusdam nisi perferendis sapiente iure eveniet cumque, re eveniet cumqueveniet cumque, eenim tempore reprehenderit dolor.",
          props: [
            {
              shoeSize: 35,
              price: "200",
              width: "86%",
            },
            {
              shoeSize: 36,
              price: "201",
              width: "88%",
            },
            {
              shoeSize: 37,
              price: "202",
              width: "90%",
            },
            {
              shoeSize: 38,
              price: "203",
              width: "92%",
            },
            {
              shoeSize: 39,
              price: "204",
              width: "94%",
            },
            {
              shoeSize: 40,
              price: "205",
              width: "96%",
            },
            {
              shoeSize: 41,
              price: "206",
              width: "98%",
            },
            {
              shoeSize: 42,
              price: "207",
              width: "100%",
            },
          ],
        },
        {
          id: 4,
          slogan: "MAN'S RUNNİNG SHOE",
          title: "NIKE EPIC REACT FLYKNIT",
          color: "green",
          img: "src/assets/green.png",
          content:
            "Lorem ipsum dolor, sit amet conste dolore illum. Amet quibusdam nisi perferendis sapiente iure eveniet cumque, re eveniet cumqueveniet cumque, eenim tempore reprehenderit dolor.",
          props: [
            {
              shoeSize: 37,
              price: "330",
              width: "86%",
            },
            {
              shoeSize: 38,
              price: "331",
              width: "88%",
            },
            {
              shoeSize: 39,
              price: "332",
              width: "90%",
            },
            {
              shoeSize: 40,
              price: "333",
              width: "92%",
            },
            {
              shoeSize: 41,
              price: "334",
              width: "94%",
            },
            {
              shoeSize: 42,
              price: "335",
              width: "96%",
            },
            {
              shoeSize: 43,
              price: "336",
              width: "98%",
            },
            {
              shoeSize: 44,
              price: "337",
              width: "100%",
            },
          ],
        },
      ],
    };
  },
};
</script>

<style>
.container {
  margin-top: 1rem;
}
.alert {
  height: 1rem;
  width: fit-content;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
   color:white;
  top: 5rem;
  left: 0px;
}
.alert-pink {
  background-color: #e0c9cc;
}
.alert-blue {
  background-color: #2596be;
}
.alert-red {
  background-color: #da5966;
}
.alert-green {
  background-color: #8bc595;
}
</style>