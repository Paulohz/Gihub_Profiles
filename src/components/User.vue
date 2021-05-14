<template>
  <div class="container">
    <div>
      <img :src="user?.avatar_url" alt="" />
    </div>
    <div class="user_personal_information">
      <p><span>Name:</span> {{ user?.name }}</p>
      <p><span>Username:</span> {{ user?.login }}</p>
      <p><span>Followers:</span> {{ user?.followers }} </p>
      <p><span>Repos count:</span> {{ user?.public_repos }} </p>
    </div>
    <div class="user_repositories">
      <p>Newest Repositories:</p>
      <div :key="userRepo.id" v-for="userRepo of userRepos">
        {{ userRepo.name }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue';

export default defineComponent({
  name: 'User',
  props: {
    user: Object,
    userRepos: Object,
  },
});

</script>

<style scoped lang="scss">
  .container {
    display: flex;
    margin-top: 50px;
    gap: 50px;
    color: var(--text-body);

    img {
      max-width: 364px;
      width: 100%;
    }
    @media (max-width: 1024px) {
      flex-direction: column;
    }
  }

</style>
