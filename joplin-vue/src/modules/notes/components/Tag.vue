<template>
  <div>
    <b-link v-for="tag in parent_folder" :key="tag.id" :to="{ name: 'myTag', params: { id: tag.title } }"
        replace
        v-slot="{ href, route, navigate, isActive, isExactActive }">
      <b-button :key="tag.id"
        variant="outline-success"
        size="sm"
        href="#" title="display notes by this tag"
        @click="notesByTag(tag)"><i class="fas fa-tag"></i> {{ tag.title }}</b-button>
    </b-link>
  </div>
</template>

<script>
import { createNamespacedHelpers } from 'vuex'

import getters from '../getters'

import typesTag from '../../tags/types'
import types from '../types'
import typesFolder from '../../folders/types'

const namespace = 'tags'
const { mapGetters } = createNamespacedHelpers(namespace)

export default {
  name: 'Tag',
  props: {
    parent_folder: Object
  },
  methods: {
    notesByTag (tag) {
      this.$store.dispatch('folders/' + typesFolder.FOLDER_FETCH, {})
      this.$store.dispatch('tags/' + typesTag.TAG_FETCH, tag)
      this.$store.dispatch('notes/' + types.NOTE_FETCH_TAG, tag)
    }
  },
  computed: {
    ...mapGetters(Object.keys(getters))
  }
}

</script>
