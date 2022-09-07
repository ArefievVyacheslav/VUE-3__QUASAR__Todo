<template>
  <q-page padding>
    <Container>
      <div v-if="editing">
        <form>
          <q-input v-model="note.title" label="Title" filled />
          <q-input v-model="note.description" label="Description" filled class="q-mt-sm" dense />
          <q-card flat bordered class="q-mt-sm">
            <q-editor v-model="note.content" min-height="5rem" />
          </q-card>
          <div class="q-mt-md">
            <q-btn color="positive" class="q-ml-sm" type="submit">Done</q-btn>
          </div>
        </form>
      </div>
      <div v-else>
        <div class="row items-center justify-between">
          <h3 class="q-mb-md q-mt-md">{{ note.title }}</h3>
          <div>
            <q-btn @click="editing = true" round color="secondary" icon="edit"></q-btn>
            <q-btn @click="remove" round color="negative" icon="delete" class="q-ml-sm"></q-btn>
          </div>
        </div>
        <div>{{ note.description }}</div>
        <div v-html="note.content" class="q-mt-md" />
      </div>
    </Container>
  </q-page>
</template>

<script>
import { computed, ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import { useLocalNotes } from "src/helpers";
import Container from "components/Container";

export default {
  name: "PageNote",
  components: { Container },
  setup() {
    const notes = useLocalNotes();
    const route = useRoute();
    const router = useRouter();
    const noteId = computed(() => +route.params.id)
    const note = computed(() => notes.value[noteId.value])
    const remove = () => {
      notes.value.splice(noteId.value, 1)
      router.push('/')
    }
    const editing = ref(false)
    return { note, editing, remove }
  }
};
</script>
