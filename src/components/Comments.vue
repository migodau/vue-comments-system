<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
    <div class="form-todo form-group">
      <p>
        <input
          v-model="name"
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

    <div class="list-group mt-3">
      <div class="list-group-item" v-for="(comment, index) in allComments" :key="index">
        <span class="comment__author">
          Author(a): <strong>{{ comment.name }}</strong>
        </span>
        <p>
          {{ comment.message }}
        </p>
        <div>
          <a href="#" @click.prevent="removeComment(index)" title="Excluir"
            >Excluir</a
          >
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  data() {
    return {
      comments: [],
      name: "",
      message: "",
    };
  },
  methods: {
    addComment() {
      if (!this.message.trim()) {
        alert("Preencha o comentário");
        return;
      }
      this.comments.push({ name: this.name, message: this.message });
      this.name = "";
      this.message = "";
    },
    removeComment(index) {
      this.comments.splice(index, 1);
    },
    rightClick() {
      alert("right click!");
    },
  },
  computed: {
    allComments() {
      return this.comments.map((comment) => ({
        ...comment,
        name: comment.name.trim() ? comment.name : "Anônimo",
      }));
    },
  },
  watch: {
    // comments: {
    //   handler(newValue, oldValue) {
    //     console.log({ newValue, oldValue });
    //   },
    //   deep: true,
    // },
    name(newValue, oldValue) {
      console.log({ newValue, oldValue });
    },
  },
};
</script>
