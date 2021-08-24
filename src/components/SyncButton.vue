<template>
  <div :class="getButtonClass()">
    <img alt="Elipse" src="../assets/SyncButton.svg" />
  </div>
</template>

<script>
export default {
  name: "SyncButton",
  data() {
    return {
      stateClass: {
        NOT_SYNCED: "NOT_SYNCED",
        SYNCED: "SYNCED",
      },
    };
  },
  props: {
    state: String,
  },
  methods: {
    getButtonClass() {
      switch (this.state) {
        case this.stateClass.NOT_SYNCED:
          return "syncButton notSyncButton";
        case this.stateClass.SYNCED:
          return "syncButton syncedButton";
        default:
          return "syncButton notSyncButton";
      }
    },
  },
};
</script>

<style scoped>
.syncButton {
  position: relative;
  width: 132px;
  height: 133px;
  margin: auto;
  margin-bottom: 9px;
  transition: all 1s;
}

.syncedButton {
  transform: rotate(-180deg);
}

.notSyncButton {
  transform: rotate(0deg);
}
</style>