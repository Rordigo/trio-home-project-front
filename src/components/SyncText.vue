<template>
  <div class="syncText">{{ templateContactsSynced() }}</div>
</template>

<script>
export default {
  name: "SyncText",
  props: {
    state: String,
    ammountSynced: Number,
  },
  methods: {
    templateContactsSynced() {
      switch (this.state) {
        case "NOT_SYNCED":
          return "Sync Contacts";
        case "SYNCED":
          return `${this.ammountSynced} contacts were synced!`;
        default:
          return "Sync Contacts";
      }
    },
  },
};
</script>

<style scoped>
.syncText {
  height: 24px;

  font-family: Noto Sans;
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 25px;
  text-align: center;
  margin-bottom: auto;

  color: #374a5e;
}
</style>