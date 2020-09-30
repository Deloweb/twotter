<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ user.username }}</h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile__follower-count">
          <strong>Followers: </strong> {{ followers }}
        </div>
      </div>
      <CreateTwootPanel @add-twoot="addTwoot" />
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from './TwootItem';
import CreateTwootPanel from './CreateTwootPanel';

export default {
  name: 'UserProfile',
  components: { CreateTwootPanel, TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'Deloweb',
        firstName: 'Lucien',
        lastName: 'Delohen',
        email: 'lucien.delohen@gmail.com',
        isAdmin: true,
        twoots: [
          { id: 1, content: 'Twotter is Amazing!' },
          { id: 2, content: "Don't forget to drink water!" },
        ],
      },
    };
  },
  methods: {
    addTwoot(twoot) {
      this.user.twoots.unshift({
        id: this.user.twoots.length + 1,
        content: twoot,
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding: 50px, 5%;
  padding: 50px;

  &__sidebar {
    margin-right: 50px;
  }

  &__user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;

    h1 {
      margin: 0;
    }
  }

  &__admin-badge {
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    padding: 0 10px;
    font-weight: bold;
    margin: 10px auto 10px 0;
  }

  &__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}
</style>
