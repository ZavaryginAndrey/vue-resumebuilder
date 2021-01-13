<template>
  <form class="card card-w30">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" @change="selectValue">
        <option
          v-for="option in options"
          :key="option.type"
          :value="option.type"
          :selected="selected"
        >{{option.text}}</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea
        id="value"
        rows="3"
        @input="inputValue"
        :value="value"
      ></textarea>
    </div>

    <button
      class="btn primary"
      @click.prevent="addBlock"
      :disabled="addButtonDisabled"
    >Добавить</button>
  </form>
</template>

<script>

export default {
  data() {
    return {
      selected: 0,
      type: 'title',
      value: '',
    }
  },
  emits: ['add'],
  props: {
    options: {
      type: Object
    }
  },
  methods: {
    inputValue(event) {
      this.value = event.target.value
    },
    selectValue(event) {
      this.type = event.target.value
    },
    addBlock() {
      this.$emit('add', this.type, this.value)
      this.value = ''
    }
  },
  computed: {
    addButtonDisabled() {
      return this.value.length < 4
    }
  }
}
</script>

<style scoped>

</style>