<template>
  <div class="card card-w70">
    <h3 v-if="noBlocks">{{noBlocksMessage}}</h3>
    <component
      v-else
      v-for="block in blocks"
      :is="'app-'+block.type"
      :value="block.value"
    ></component>
  </div>
</template>

<script>
import AppAvatar from '@/components/AppAvatar'
import AppTitle from '@/components/AppTitle'
import AppSubtitle from '@/components/AppSubtitle'
import AppText from '@/components/AppText'

export default {
  data() {
    return {
      noBlocksMessage: 'Добавьте первый блок, чтобы увидеть результат'
    }
  },
  props: ['blocks'],
  computed: {
    noBlocks() {
      return this.blocks.length === 0
    }
  },
  components: {
    AppText,
    AppAvatar,
    AppTitle,
    AppSubtitle
  }
}
</script>

<style scoped>

</style>