<template>
  <q-page padding>
    <Container>
      <h3>New Note</h3>
      <form @submit.prevent="submit">
        <q-input v-model="note.title" class="q-mt-sm" outlined label="Title" />
        <q-input v-model="note.description" class="q-mt-sm" outlined label="Description" dense />
        <q-card flat bordered class="q-mt-sm">
          <q-editor v-model="note.content" min-height="5rem" />
        </q-card>
        <div class="q-mt-md">
          <q-btn to="/" color="negative" type="reset">Cancel</q-btn>
          <q-btn color="positive" class="q-ml-sm" type="submit">Create</q-btn>
        </div>
      </form>
    </Container>
  </q-page>
</template>

<script>
import Container from "components/Container";
import { useRouter } from "vue-router";
import { useLocalNotes } from "src/helpers";
import { reactive } from "vue";

export default {
  name: "PageNew",
  components: { Container },
  setup() {
    const notes = useLocalNotes();
    const router = useRouter();
    const note = reactive({
      title: "",
      description: "",
      content: ""
    });
    const submit = () => {
      notes.value.unshift({
        ...note,
        createdAt: Date.now(),
        updatedAt: Date.now()
      });
      router.push("/");
      note.title = "";
      note.description = "";
      note.content = "";
    };
    return { note, submit };
  }
};
</script>
