<template>
  <div class="message" :class="message.self?'message--self':''">

    <div v-if="message.self && !hideDot" class="message__row message__row--self">
      <div class="message__profile">
        <div class="message__profile__circle message__profile__circle--self" />
      </div>
      <div class="message__username">
        {{message.userName}}
      </div>
    </div>

    <div  class="message__row" v-if="!message.self && !hideDot">
      <div class="message__username">
        {{message.userName}}
      </div>
      <div class="message__profile">
        <div class="message__profile__circle" />
      </div>
    </div>
    <div class="message__text" :class="message.self?'message__text--self':''">
      <span>{{message.text}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    message: Object,
    hideDot: Boolean,
  },
};
</script>

<style lang="scss" scoped>
  @import "@/assets/defaults.scss";
  .message {
    margin-left: auto;
    margin-right: 10px;
    width: fit-content;

    &--self {
      margin-left: 10px;
      margin-right: auto;
    }

    &__username {
      padding: 0 10px;
      color: $c_grey;
    }

    &__profile {
      box-shadow: $bs_md;
      border-radius: 50%;
      padding: $sp_sm;
      &__circle {
        height: $sp_md;
        width: $sp_md;
        border-radius: 50%;
        background-color: $c_red;

        &--self {
          background-color: $c_orange;
        }
      }
    }

    &__text {
      padding: $sp_sm;
      border: 1px solid $c_grey;
      border-radius: $br_md;
      margin: 0 $sp_lg;
      margin-top: 4px;
      border-top-right-radius: 0;

      &--self {
        border-radius: $br_md;
        border-top-left-radius: 0;
      }
    }

    &__row {
      @extend .row;
      justify-content: right;

      &--self {
        justify-content: left;
      }
    }
  }
</style>
