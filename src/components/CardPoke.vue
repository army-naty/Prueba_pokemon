<script>
export default {
  name: 'CardPoke',
  props: {
    namePokemon: {
      type: String
    },
    imageUrl: {
      type: String
    }
  },
  data() {
    return {
      inputUser: '',
      correct: false
    }
  },
  methods: {
    sendName() {
      console.log(this.namePokemon)
      if (this.inputUser.toLowerCase().trim() == this.namePokemon.toLowerCase()) {
        this.correct = true
        this.$emit('send-name', this.namePokemon)
      } else {
        alert('Siga intentando')
      }
    }
  }
}
</script>
<template>
  <div class="card col-3 border border-0">
    <img :class="!correct ? 'filter' : ''" :src="imageUrl" :alt="namePokemon" />
    <div v-if="correct">
      <p class="name">{{ namePokemon }}</p>
    </div>
    <form v-else @submit.prevent="sendName">
      <input class="col-12 form-control mb-2" v-model="inputUser" />
      <button class="col-12 btn btn-light">Descubrir</button>
      <p class="incorrect" v-show="correct == false">Incorrecto, intentalo de nuevo</p>
    </form>
  </div>
</template>
<style scoped>
.filter {
  filter: blur(5px) grayscale(100%);
}
</style>
