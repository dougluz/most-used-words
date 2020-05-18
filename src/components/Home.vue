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
import { ipcRenderer } from 'electron'
import WordPill from './WordPill'

export default {
  data: () => ({
    files: [],
    groupedWords: []
  }),
  methods: {
    processSubtitles () {
      const paths = this.files.map(f => f.path)
      ipcRenderer.send('process-subtitles', paths)
      ipcRenderer.on('process-subtitles', (event, response) => {
        console.log('responmse')
        this.groupedWords = response
      })
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