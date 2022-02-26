<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
    
    <FormToDo @addComment="add"></FormToDo>

    <div class="list-group mt-3">
      <p v-if="!comments.length">Sem comentários...</p>
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
import FormToDo from './FormToDo.vue';

export default {
  components: {
    FormToDo
  },
  data() {
    return {
      comments: [],
    };
  },
  methods: {
    add(comment) {
      console.log({ comment });
      this.comments.push(comment);
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
        name: comment.author.trim() ? comment.author : "Anônimo",
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
