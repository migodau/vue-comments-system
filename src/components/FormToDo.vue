<template>
  <div class="form-todo form-group">
    <p>
      <input
        v-model="author"
        placeholder="nome"
        type="text"
        name="author"
        class="form-control"
      />
    </p>
    <p>
      <textarea
        v-model="message"
        placeholder="comentário"
        name="message"
        class="form-control"
      >
      </textarea>
    </p>
    <button
      @click="addComment"
      @click.right.prevent="rightClick"
      type="submit"
      class="btn btn-primary"
    >
      Comentar
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      author: "",
      message: "",
    };
  },
  methods: {
    addComment() {
      if (!this.message.trim()) {
        alert("Preencha o comentário");
        return;
      }

      this.$emit('addComment', {
        author: this.author,
        message: this.message 
      });

      this.author = "";
      this.message = "";
    },
  },
};
</script>