<template>
  <teleport to="body">
    <transition name="fade">
      <div class="notification" v-if="show">
        <p class="notification__message">{{ message }}</p>
        <span class="notification__btn" @click="$emit('close')">&#10005;</span>
      </div>
    </transition>
  </teleport>
</template>

<script>
export default {
  name: "BaseNotification",
  emits: ["close"],
  props: ["show", "message"],
};
</script>

<style lang="scss" scoped>
.notification {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: space-between;
  top: 5%;
  right: 5%;
  width: 20rem;
  height: 4rem;
  background: rgb(240, 255, 240);
  padding: 0 2rem;
  border: 1px solid #d6d6d6;
  border-radius: 9px;

  &__message {
    font-size: 1.4rem;
  }

  &__btn {
    cursor: pointer;
    font-size: 1.6rem;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
