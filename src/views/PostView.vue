<template>
  <div class="home">
    <Header v-if="this.token == null" />
    <HeaderLogged v-if="this.token != null" />
    <PostView  v-bind:titre="this.titre" v-bind:theme="this.theme" v-bind:auteur="this.auteur" v-bind:date="this.date" v-bind:contenu="this.contenu"/>
     <router-link to="/NewCommentInput">
          <NewComment />
      </router-link>
    
    <Comment v-for="comment in comments" v-bind:key="comment.id" v-bind:auteur="comment.auteur" v-bind:contenu="comment.contenu" v-bind:date="comment.date" />
  </div>
</template>

<script>
// @ is an alias to /src
import PostView from "@/components/PostView.vue";
import Header from "@/components/Header.vue";
import Comment from "@/components/Comment.vue";
import NewComment from "@/components/NewComment.vue";
import HeaderLogged from "@/components/HeaderLogged.vue";
const axios = require('axios');

export default {
  name: "Home",
  components: {
    PostView,
    Header,
    Comment,
    NewComment,
    HeaderLogged
  },
  data: () => {
    return {
      id: "",
      titre: "",
      theme: "",
      auteur: "",
      date: "",
      contenu: "",
      comments: [],
      token: "",
      countLike: 0,
    };
  },
  mounted() {
    this.id = localStorage.getItem('id');
    this.titre = localStorage.getItem('titre');
    this.theme = localStorage.getItem('theme');
    this.auteur = localStorage.getItem('auteur');
    this.date = localStorage.getItem('date');
    this.contenu = localStorage.getItem('contenu');
    this.token = localStorage.getItem('myToken');
    this.countLike = localStorage.getItem('like');
    axios.get(process.env.VUE_APP_BASE_URL+'api/comment/')
    .then((response) => {
      console.log(response.data);
      response.data.forEach(result => {
        if (result.id_post == this.id){
          console.log(result);
          console.log(result.id_post);
          this.comments.push({id: result.id, auteur: result.auteur, date: result.date, contenu: result.contenu});
        }
      })
    })
    .catch((error) => {
      console.log(error);
    })
  },
  methods:{
    like() {
      this.countLike += 1;
      this.countLike = localStorage.setItem('like');
    },
  }
};
</script>
