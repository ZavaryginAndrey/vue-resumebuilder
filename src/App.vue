<template>
  <div class="container column">
    <app-form
      @add="addBlock"
      :options="options"
    ></app-form>
    <app-resume
      :blocks="blocks"
    ></app-resume>
  </div>

  <app-comments-block
    :url="commentUrl"
  ></app-comments-block>
</template>

<script>
import AppCommentsBlock from '@/components/AppCommentsBlock'
import AppForm from '@/components/AppForm'
import AppResume from '@/components/AppResume'

export default {
  data() {
    return {
      commentUrl: 'https://jsonplaceholder.typicode.com/comments?_limit=42',
      block: null,
      value: '',
      blocks: [],
      options: [
        {
          type: 'title',
          text: 'Заголовок'
        },
        {
          type: 'subtitle',
          text: 'Подзаголовок'
        },
        {
          type: 'avatar',
          text: 'Аватар'
        },
        {
          type: 'text',
          text: 'Текст'
        }
      ]
    }
  },
  methods: {
    addBlock(type, value) {
      if (value.length > 3) {
        this.blocks.push({type, value})
      }
      else {
        console.log('Значение блока должно быть минимум 4 символа.')
      }
    }
  },
  components: {
    AppCommentsBlock,
    AppForm,
    AppResume
  }
}
</script>
