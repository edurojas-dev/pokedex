<template>
  <div class="card">
    <div class="card-image">
      <figure>
        <img :src="currentImg" alt="Placeholder image" />
      </figure>
    </div>
    <div class="card-content">
      <h1 class="title is-1">{{ num }}. {{ name }}</h1>
      <h3 class="title is-5">Tipo: {{ pokemon.tipo }}</h3>
    </div>
    <div class="card-footer">
      <div class="card-footer-item">
        <button class="button is-link is-medium is-fullwidth" @click="mudarImg">
          Mudar Sprite
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      front: true,
      currentImg: "",
      pokemon: {
        tipo: "",
        imgFront: "",
        imgBack: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  created() {
    axios.get(this.url).then((r) => {
      this.pokemon.tipo = r.data.types[0].type.name;
      this.currentImg = r.data.sprites.front_default;
      this.pokemon.imgFront = r.data.sprites.front_default;
      this.pokemon.imgBack = r.data.sprites.back_default;
    });
  },
  methods: {
    mudarImg() {
      if (this.front) {
        this.front = false;
        this.currentImg = this.pokemon.imgBack;
      } else {
        this.front = true;
        this.currentImg = this.pokemon.imgFront;
      }
    },
  },
};
</script>
<style scoped>
.card {
  width: 38rem;
  margin: auto;
}
.card-image {
  display: flex;
  align-items: center;
  justify-content: center;
}
h1 {
  text-transform: capitalize;
}

@media (max-width: 800px) {
  .card {
    width: 400px !important;
    margin: auto;
  }

  a {
    font-size: 22px !important;
  }
}
</style>
