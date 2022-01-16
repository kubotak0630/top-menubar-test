<template>
  <div class="main-container">
    <TopMenuBar @emit-topmenu-on="topMenuOn" />
    <ContentV class="main-content" :style="{ 'padding-top': topPos }" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import TopMenuBar from '@/components/TopMenuBar.vue';
import ContentV from '@/components/ContentV.vue';

export default defineComponent({
  name: 'Home',
  components: { TopMenuBar, ContentV },
  setup() {
    const topPos = ref('0px');

    const topMenuOn = (isOn: boolean) => {
      topPos.value = isOn ? '50px' : '0px';
    };

    return { topMenuOn, topPos };
  },
});
</script>

<style lang="scss" scoped>
// .main-container {
//   position: relative;
// }

.main-content {
  transition: padding-top 0.25s ease-in-out;
}
</style>
