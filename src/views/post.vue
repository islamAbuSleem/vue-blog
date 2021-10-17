<template>
  <div class="container">
    <button @click="goToHome">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-chevron-double-left"
        viewBox="0 0 16 16"
      >
        <path
          fill-rule="evenodd"
          d="M8.354 1.646a.5.5 0 0 1 0 .708L2.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z"
        />
        <path
          fill-rule="evenodd"
          d="M12.354 1.646a.5.5 0 0 1 0 .708L6.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z"
        />
      </svg>
      Back
    </button>
    <div class="post">
      <h2 class="title">{{ post.title }}</h2>
      <p class="post-body">{{ post.body }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      post: null,
    };
  },
  created() {
    this.getSinglePost();
  },
  methods: {
    async getSinglePost() {
      try {
        const data = await axios.get(
          `https://jsonplaceholder.typicode.com/posts/${this.id}`
        );
        this.post = data.data;
      } catch (e) {
        console.log(e);
      }
    },
    goToHome() {
      this.$router.push({ name: "Home" });
    },
  },
};
</script>

<style lang="scss" scoped>
button {
  margin-top: 3%;
  padding: 6px;
  color: #5f5c5c;
  display: flex;
  align-items: center;
  cursor: pointer;
  background-color: #eee;
  border: 1px solid #ddd;
  box-shadow: 0px 2px 3px #ccc;
  transition: all 0.3s ease-in-out;
  &:hover {
    box-shadow: 0px 2px 7px rgb(177, 248, 218);
    background-color: rgb(236, 236, 236);
  }
}
.post {
  margin-top: 5%;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 5px;
  position: relative;

  .title {
    position: absolute;
    top: -36px;
    padding: 0 10px;
    background: white;
    color: #333;
  }
  .post-body {
    font-size: 1.5rem;
    color: rgb(71, 71, 71);
  }
}
</style>