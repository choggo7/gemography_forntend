<template>
  <div class="repos">
      <b-container>
      <ul >
        <li v-for="(value, index) in repos" :key="index">
          <img :src="value.owner.avatar_url">
          <div class="repo-content">
            <h4>{{ value.name }}</h4>
            <p class="repo-discription">
              {{ value.description }}
            </p>
            <div class="repo-action">
                <div class="repo-badge">
                  Stars <span class="badge bg-secondary"> {{ value.stargazers_count }} </span>
                </div>
                <div class="repo-badge">
                  Issues <span class="badge bg-secondary"> {{ value.open_issues }} </span>
                </div>
                <span> Submitted {{ value.pushed_at | moment("from") }} by {{ value.owner.login }}</span>
            </div>
          </div>
        </li>
      </ul>

      <div v-if="repos.length" v-observe-visibility="handleScrolledToBottom"> </div>
      </b-container>
      
      <hr width="100%" />
  </div>

</template>

<script>
import axios from "axios";
export default {
  name: "Repos",
  data: () => ({
    repos : [],
    errors : [],
    page : 1,
  }),

  methods:{
    async fetch(){
      axios
      .get(`https://api.github.com/search/repositories?q=created:>2017-10-22&sort=stars&order=desc&page=${this.page}`)
      .then((Response) => {
        this.repos.push(...Response.data.items);
      })
      .catch((e) => {
        this.errors.push(e);
      });
    },
    handleScrolledToBottom (isVisible){
      if(!isVisible){return}
      console.log('hola');
      this.page++;
      this.fetch();
    }
  },
  mounted(){
    this.fetch();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li{
  position: relative;
  display: flex;
justify-content: flex-start;
align-items: center;
gap: 1rem;
margin-bottom: 1rem;
height: 8rem;
}
li img{height: 100%;width: auto;}
li .repo-content{
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-direction: column;
}
li .repo-action{
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 1rem;
}
li .repo-badge{
  border: 3px solid #5D5D5D;
  padding: .2rem .6rem;
}
</style>
