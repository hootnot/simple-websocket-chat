<template>
  <div class="login">
    <span class="login__description">Choose a nickname to start:</span>
    <div class="login__row">
      <form @submit="enterName">
        <input
          class="login__input"
          v-model="username"
        />
        <button
          class="login__button"
          type="submit"
        >
          Start
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import WS from '../ws';

export default {
  data() {
    return {
      username: this.loadUsername(),
    };
  },
  computed: {
    userId() {
      return this.$store.getters.userId;
    },
  },
  methods: {
    enterName(event) {
      event.preventDefault();
      if (this.username) {
        WS.sendSubscribe(
          this.$socket,
          this.userId,
          this.username,
          this.$route.meta.admin,
        );
        localStorage.setItem('sc_userName', this.username);
      }
    },
    loadUsername() {
      const oldUserName = localStorage.getItem('sc_userName');
      if (oldUserName) {
        return oldUserName;
      }
      return this.$route.meta.admin ? 'SJ - ' : '';
    },
  },
};
</script>

<style lang="scss" scoped>
  @import "@/assets/defaults.scss";

  .login {
    margin: 100px auto;
    width: fit-content;
    height: fit-content;
    background-color: $c_white;
    padding: $sp_lg;
    border-radius: $br_md;
    box-shadow: $bs_md;

    &__description {}

    &__row {
      @extend .row;
      margin-top: 10px;
    }

    &__input {
      @extend .input;
      font-weight: 600;
    }

    &__button {
      @extend .button;
      background-color: $c_red;
      color: $c_white;
      margin: 0 10px;
      font-weight: 500;
    }
  }
</style>
