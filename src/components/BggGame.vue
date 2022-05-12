<template>
  <section>
    <h2>BGG ID: {{ id }}</h2>
    <figure v-if="imageUrl">
      <img :src="imageUrl" :alt="imageAlt">
      <figcaption>
        <a :href="bggPageUrl" target="_blank">
          {{ name }} ({{ year }})
        </a>
      </figcaption>
    </figure>
  </section>
</template>

<script>
const xmlParser = new window.DOMParser()

export default {
  name: 'BggGame',
  props: {
    id: {
      type: Number,
      required: true
    }
  },
  data () {
    return {
      imageUrl: '',
      name: '',
      year: ''
    }
  },
  created () {
    this.loadGame(this.id)
  },
  computed: {
    bggPageUrl () {
      return `https://boardgamegeek.com/boardgame/${this.id}`
    },
    imageAlt () {
      return `Cover art for ${this.name}`
    }
  },
  methods: {
    loadGame (id) {
      fetch(`https://api.geekdo.com/xmlapi2/thing?type=boardgame&id=${id}`)
        .then(response => response.text())
        .then(xml => xmlParser.parseFromString(xml, 'text/xml'))
        .then(gameDom => {
          const item = gameDom.getElementById(id)
          this.imageUrl = item.querySelector('image').textContent
          this.name = item.querySelector('name[type="primary"]').getAttribute('value')
          this.year = item.querySelector('yearpublished').getAttribute('value')
        })
    }

  },
  watch: {
    id (newId) {
      this.loadGame(newId)
    }
  }
}
</script>

<style scoped lang="scss">
figure {
  img {
    height: 200px;
    border: 1px solid var(--green-light);
    border-radius: 3px;
    padding: 3px;
  }
}
</style>
