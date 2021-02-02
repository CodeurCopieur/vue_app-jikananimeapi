<template lang="pug">
.card
  a(href="#" target="_blank")
    img(:src="anime.image_url", :alt="anime.title + ' Poster'")
    h3 {{ anime.title }}
</template>

<script>
 export default {
   props: ['anime']
  }
</script>

<style lang="scss" scoped>

.card {
  flex: 1 1 33%;
  width: 33%;
  max-width: 33%;
  padding: 0 8px;
  margin-bottom: 16px;

  a {
    width: 100%;
  }

  img {
    width: 100%;
    height: 300px;
    object-fit: fill;
    border-radius: 16px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, .15);
    transition: .4s;
  }
  h3 {
    padding: 16px;
    color: #313131;
  }

  &:hover {
    img {
      transform: scale(1.05);
    }

    h3 {
      color:#2E51A2;
    }
  }
}
</style>