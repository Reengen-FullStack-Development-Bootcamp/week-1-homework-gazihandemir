<template>
  <b-col cols="6">
    <b-card tag="article" :class="[`card-${color}`, 'mb-2 card mx-auto']">
      <b-row>
        <b-col cols="7" class="p-3">
          <img :src="info.img" :style="{ width: width }" alt="" />
        </b-col>

        <b-col cols="5" class="text-left">
          <b-row>
            <b-col cols="12">
              <h6 :class="[`${color}-color`, 'info']">
                {{ info.slogan }}
              </h6>
            </b-col>
            <b-col cols="12">
              <h5>{{ info.title }} ({{ size }})</h5>
            </b-col>
            <b-col cols="12">
              <h3 :class="`h3-${color}`" :id="`h3-${info.id}`">${{ price }}</h3>
            </b-col>
            <b-col cols="12">
              <p class="lorem">
                {{ info.content }}
              </p></b-col
            >
          </b-row>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <small :class="`${color}-color`" style="font-size: 0.75rem"
            >CHOOSE SIZE</small
          >
          <div class="btn-group">
            <b-button
              variant="outline-light"
              :class="[`button-outline-${color}`, 'btn-sm']"
              :id="`btn-${info.id}-${info.props[i].shoeSize}`"
              v-for="(shoe, i) in info.props.length"
              :key="i"
              @click="
                changeShoeSize(
                  i,
                  info.id,
                  info.props[i].shoeSize,
                  info.props[i].price,
                  info.props[i].width
                )
              "
            >
              {{ info.props[i].shoeSize }}
            </b-button>
          </div>
        </b-col>
        <b-col>
          <div class="btn-group">
            <b-button
              @click="addToBasket(info, size, price)"
              variant="outline-light"
              :class="[`button-${color}`, 'btn-sm mt-4']"
              >ADD TO CART</b-button
            ><b-button
              variant="outline-light"
              :class="[`button-${color}`, 'btn-sm mt-4']"
              >&hearts;</b-button
            >
          </div>
        </b-col>
      </b-row>
    </b-card>
  </b-col>
</template>

<script>
export default {
  name: "Card",
  props: {
    info: Object,
  },
  data() {
    return {
      color: this.info.color,
      price: this.info.props[0].price,
      width: this.info.props[0].width,
      size: this.info.props[0].shoeSize,
    };
  },
  computed: {},
  methods: {
    changeShoeSize(i, id, size, priceP, wh) {
      this.price = priceP;
      this.width = wh;
      this.size = size;
    },
    addToBasket(val, size, price) {
      this.$emit("addShoe", { item: val, size: size, price: parseInt(price) });
    },
  },
};
</script>

<style>
.card-pink {
  width: 32rem;
  height: 20rem;
  background-color: #f5f5f5;
}
.card-blue {
  width: 32rem;
  height: 20rem;
  background-color: #ebf9fa;
}
.card-green {
  width: 32rem;
  height: 20rem;
  background-color: #ebfaf3;
}
.card-red {
  width: 32rem;
  height: 20rem;
  background-color: #faebeb;
}
img {
  max-width: 100%;
}
.info {
  font-size: 0.75rem;
  text-align: left;
}
span {
  font-weight: bold;
}

.lorem {
  font-size: 0.7rem;
  text-align: left;
}
h5 {
  text-align: left;
  font-weight: bold;
  font-size: 0.9rem;
}
h3 {
  text-align: left;
  font-weight: bold;
}

/* ---------------------PINK--------------------- */
.button-pink {
  margin-left: 2px;
  margin-right: 2px;
  color: white !important;
  background-color: #e0c9cc;
  border-color: #e0c9cc !important;
}
.button-outline-pink {
  margin-left: 2px;
  margin-right: 2px;
  color: #e0c9cc !important;
  border-color: #e0c9cc !important;
}

.button-outline-pink:hover {
  color: white !important;
  background-color: #e0c9cc !important;
}
.button-pink:hover {
  color: #e0c9cc !important;
  background-color: white !important;
}

.h3-pink {
  color: #e0c9cc;
}

.pink-color {
  color: #e0c9cc;
  font-weight: bold;
}
.pink-bg-color {
  background-color: #e0c9cc;
}
/* ---------------------RED--------------------- */
.button-red {
  margin-left: 2px;
  margin-right: 2px;
  color: white !important;
  background-color: #da5966;
  border-color: #da5966 !important;
}
.button-outline-red {
  margin-left: 2px;
  margin-right: 2px;
  color: #da5966 !important;
  border-color: #da5966 !important;
}

.button-outline-red:hover {
  color: white !important;
  background-color: #da5966 !important;
}
.button-red:hover {
  color: #da5966 !important;
  background-color: white !important;
}

.h3-red {
  color: #da5966;
}

.red-color {
  color: #da5966;
  font-weight: bold;
}
.red-bg-color {
  background-color: #da5966;
}
/* ---------------------GREEN--------------------- */
.button-green {
  margin-left: 2px;
  margin-right: 2px;
  color: white !important;
  background-color: #8bc595;
  border-color: #8bc595 !important;
}
.button-outline-green {
  margin-left: 2px;
  margin-right: 2px;
  color: #8bc595 !important;
  border-color: #8bc595 !important;
}

.button-outline-green:hover {
  color: white !important;
  background-color: #8bc595 !important;
}
.button-green:hover {
  color: #8bc595 !important;
  background-color: white !important;
}

.h3-green {
  color: #8bc595;
}

.green-color {
  color: #8bc595;
  font-weight: bold;
}
.green-bg-color {
  background-color: #8bc595;
}

/* ---------------------BLUE--------------------- */

.button-blue {
  margin-left: 2px;
  margin-right: 2px;
  color: white !important;
  background-color: #2596be;
  border-color: #2596be !important;
}
.button-outline-blue {
  margin-left: 2px;
  margin-right: 2px;
  color: #2596be !important;
  border-color: #2596be !important;
}

.button-outline-blue:hover {
  color: white !important;
  background-color: #2596be !important;
}
.button-blue:hover {
  color: #2596be !important;
  background-color: white !important;
}
.h3-blue {
  color: #2596be;
}
.blue-color {
  color: #2596be;
  font-weight: bold;
}
.blue-bg-color {
  background-color: #2596be;
}
</style>