<template>
  <form @submit="onSubmit">
    <input
      type="text"
      v-model="username"
      name="text"
      placeholder="Username do Github"
    />
    <button type="submit">Pesquisar</button>
    <User :user="user" :userRepos="userRepos" v-show="visible" />
  </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';
import User from './User.vue';

export default defineComponent({
  name: 'Main',
  components: {
    User,
  },
  data() {
    return {
      username: '',
      user: Object,
      userRepos: Array,
      visible: false,
    };
  },
  methods: {
    onSubmit(e: Event) {
      interface userReposInterface {
        created_at: string;
      }
      this.visible = false;

      e.preventDefault();

      if (this.username === '') {
        alert('Por gentileza, preencha o campo');
        return;
      }

      axios
        .get(`https://api.github.com/users/${this.username}`)
        .then((response) => {
          const user = response.data;
          this.user = user;
          console.log(user);
          axios
            .get(user.repos_url)
            .then((res) => {
              res.data.sort((a: userReposInterface, b: userReposInterface) => {
                if (a.created_at < b.created_at) {
                  return 1;
                }
                if (a.created_at > b.created_at) {
                  return -1;
                }
                return 0;
              });

              this.userRepos = res.data.slice(0, 4);
            });
          this.visible = !this.visible;
        })
        .catch(() => {
          alert('Ops! ocorreu um erro na consulta');
        });
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
form {
  max-width: 1170px;
  margin: 0 auto;
  padding: 50px 10px;

  input {
    padding: 10px;
    border: none;
    max-width: 200px;
    width: 100%;
  }

  button {
    padding: 10px;
    background: var(--header-bg);
    color: var(--text-body);
    border: none;
  }
}
</style>
