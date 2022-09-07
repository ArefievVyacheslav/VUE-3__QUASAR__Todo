<template>
  <q-page padding>
    <Container>
      <div class="row items-center justify-between">
        <h3>Your notes</h3>
        <q-btn round color="positive" icon="add" to="/new"></q-btn>
      </div>
      <NoteCard
        v-for="({ title, description }, idx) in notes"
        :key="idx"
        :title="title"
        :description="description"
        @click="router.push(`/note/${idx}`)"
      />
      <div v-if="notes.length === 0">You have not created any notes</div>
    </Container>
  </q-page>
</template>

<script>
import Container from "src/components/Container";
import NoteCard from "src/components/NoteCard";
import { useLocalNotes } from "src/helpers";
import { useRouter } from "vue-router";
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  components: { Container, NoteCard },
  setup() {
    const notes = useLocalNotes();
    const router = useRouter();
    return { notes, router };
  }
});
</script>
