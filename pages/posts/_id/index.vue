<template>
    <div class="single-post-page">
        <section class="post">
            <img class="post-thumbnail" :src="loadedPost.thumbnail" alt="">
            <h1 class="post-title">{{ loadedPost.title }}</h1>
            <div class="post-details">
                <div class="post-detail">updated on {{ loadedPost.updatedDate }}</div>
                <div class="post-detail">Post By: {{ loadedPost.author }}</div>
            </div>
            <p>{{ loadedPost.content }}</p>
        </section>
        <div class="post-feedback">
            <p>Let me know what you think about the post. Send the mail on <a href="mailto:dongoamuza@gmail.com">dongoamuza@gmail.com</a></p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    asyncData(context){
      return axios.get('https://nuxtblog-9d5f2-default-rtdb.firebaseio.com/posts/' + context.params.id + '.json')
      .then(res => {
          return {
              loadedPost: res.data
          }
      })
      .catch(e => context.error(e))
    },
};
</script>

<style scoped>

    .post-thumbnail {
        width: 100%;
        height: 300px;
        background-position: center;
        background-size: cover;
    }
    .single-post-page {
    padding: 30px;
    text-align: center;
    box-sizing: border-box;
    }

    .post {
    width: 100%;
    }

    @media (min-width: 768px) {
    .post {
        width: 600px;
        margin: auto;
    }
    }

    .post-title {
    margin: 0;
    padding: 15px 0;
    }

    .post-details {
    padding: 10px;
    box-sizing: border-box;
    border-bottom: 3px solid #ccc;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    }

    @media (min-width: 768px) {
    .post-details {
        flex-direction: row;
    }
    }

    .post-detail {
    color: rgb(88, 88, 88);
    margin: 0 10px;
    }

    .post-feedback a {
    color: red;
    text-decoration: none;
    }

    .post-feedback a:hover,
    .post-feedback a:active {
    color: salmon;
    }
</style>