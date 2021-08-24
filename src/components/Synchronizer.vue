<template>
  <div class="main">
    <div class="containerFlex">
      <img class="blobImg" alt1="Blob" src="../assets/Blob.svg" />
    </div>
    <div class="containerFlex">
      <SyncButton :state="state" @click="this.handleButton()" />
      <SyncText :state="state" :ammountSynced="ammountSynced" />
    </div>
  </div>
  <div class="loadingContainer" v-if="syncing">
    <div class="containerFlex">
      <Loader />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SyncButton from "./SyncButton";
import SyncText from "./SyncText.vue";
import Loader from "./Loader.vue";

export default {
  name: "Synchronizer",
  components: {
    SyncButton,
    SyncText,
    Loader,
  },
  data() {
    return {
      state: "NOT_SYNCED",
      stateList: {
        NOT_SYNCED: "NOT_SYNCED",
        SYNCED: "SYNCED",
      },
      ammountSynced: 0,
      syncing: false,
    };
  },
  methods: {
    handleButton() {
      switch (this.state) {
        case this.stateList.NOT_SYNCED:
          this.syncContacts();
          break;
        case this.stateList.SYNCED:
          this.resetView();
          break;
      }
    },
    changeState(state) {
      if (state in this.stateList) {
        this.state = state;
      }
    },
    async syncContacts() {
      this.syncing = true;
      const REQUEST_URL = "http://localhost:3000/sync";
      const { data } = await axios.put(REQUEST_URL);
      this.syncing = false;
      this.ammountSynced = data.sent;
      this.changeState(this.stateList.SYNCED);
    },
    resetView() {
      this.changeState(this.stateList.NOT_SYNCED);
    },
  },
};
</script>

<style scoped>
.main {
  position: relative;
  height: 100vh;
  width: 100vw;
}
.blobImg {
  width: 522px;
  height: 539px;
  z-index: -10;
}
.containerFlex {
  position: absolute;
  display: flex;
  flex-direction: column;
  height: 66vh;
  width: 100vw;
  align-items: center;
  justify-content: center;
}
.loadingContainer {
  position: absolute;
  left: 0px;
  top: 0px;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.3);
  z-index: 100;
}
</style>