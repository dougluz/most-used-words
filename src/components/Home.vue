<template>
  <v-container fluid="">
    <v-form>
      <v-file-input 
        multiple 
        chips 
        v-model="files" 
        label="Selecione as legendas"
        prepend-icon="mdi-message-text"
        outlined
        append-icon="mdi-send"
        @click:append="processSubtitles"
      />
    </v-form>
    <div class="pills">
      <WordPill v-for="word in groupedWords" :key="word.name"
        :name="word.name"
        :amount="word.amount"
      />
    </div>
  </v-container>
</template>

<script>
import WordPill from './WordPill'

export default {
  data: () => ({
    files: [],
    groupedWords: [
      { name: 'you', amount: 900 },
      { name: 'he', amount: 300 },
      { name: 'hi', amount: 525 },
      { name: 'i', amount: 879 },
    ]
  }),
  methods: {
    processSubtitles () {
      console.log(this.files)
    }
  },
  components: {
    WordPill
  }
}
</script>

<style>
  .pills {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
</style>