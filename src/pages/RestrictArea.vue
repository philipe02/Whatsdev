<template>
  <q-page class="container full-height">
    <div>
      <ConversationArea />
    </div>

    <div class="column" v-if="1 === 2"></div>
    <Empty v-else />
  </q-page>
</template>

<script>
import Empty from "src/components/Empty/Index";
import ConversationArea from "src/components/ConversationArea/Index";

export default {
  name: "MainLayout",
  data() {
    return {};
  },
  components: {
    Empty,
    ConversationArea,
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  overflow: hidden;
  min-width: 1200px;
}
</style>