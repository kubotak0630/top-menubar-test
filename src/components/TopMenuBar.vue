<template>
  <div class="menu-wrapper">
    <input type="checkbox" id="openSidebarMenu" v-model="menuChecked" @change="clickMunu" />
    <label for="openSidebarMenu" class="sidebarIconToggle">
      <div class="spinner diagonal part-1"></div>
      <div class="spinner horizontal"></div>
      <div class="spinner diagonal part-2"></div>
    </label>
    <div class="sidemenu-content">
      <ul>
        <li @click="onClick1">レジスタSummary</li>
        <li>IPC情報</li>
        <li>RP情報</li>
        <li>FWログ</li>
        <li>レジスタ詳細</li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'TopMenuBar',
  emits: ['emit-topmenu-on'],
  setup(props, context) {
    const menuChecked = ref(false);

    const clickMunu = () => {
      console.log(`call clickMenu, ${menuChecked.value}`);
      context.emit('emit-topmenu-on', menuChecked.value);
    };

    const onClick1 = () => {
      console.log('hoge');
    };

    return { menuChecked, clickMunu, onClick1 };
  },
});
</script>

<style lang="scss" scoped>
.sidemenu-content {
  position: fixed;
  top: 0px;
  left: 0px;
  // width: 200px;
  width: 100%;
  // height: 100vh;
  height: 50px;

  background: linear-gradient(180deg, #e0e0e0 0%, #c2cbf0 100%);
  transform: translateY(-50px);
  transition: transform 0.25s ease-in-out;
}

#openSidebarMenu {
  display: none; /* ラベルは消しておく */
}

.sidebarIconToggle {
  transition: all 0.3s;
  box-sizing: border-box;
  cursor: pointer;
  position: absolute;
  position: fixed;
  z-index: 2;
  height: 100%;
  width: 100%;
  top: 15px;
  right: 15px;
  height: 22px;
  width: 22px;

  .spinner {
    transition: all 0.3s;
    box-sizing: border-box;
    position: absolute;
    height: 3px;
    width: 100%;
    // background-color: #fff;
    background-color: gray;
  }
  .horizontal {
    transition: all 0.3s;
    box-sizing: border-box;
    position: relative;
    float: left;
    margin-top: 3px;
  }
  .diagonal.part-1 {
    position: relative;
    transition: all 0.3s;
    box-sizing: border-box;
    float: left;
  }
  .diagonal.part-2 {
    transition: all 0.3s;
    box-sizing: border-box;
    position: relative;
    float: left;
    margin-top: 3px;
  }
}

/* チェック時のハンバーガーメニューアイコン動作 */
// input[type='checkbox']:checked {
#openSidebarMenu:checked {
  & ~ .sidebarIconToggle {
    .horizontal {
      transition: all 0.3s;
      box-sizing: border-box;
      opacity: 0;
    }
    .diagonal.part-1 {
      transition: all 0.3s;
      box-sizing: border-box;
      transform: rotate(135deg);
      margin-top: 8px;
    }
    .diagonal.part-2 {
      transition: all 0.3s;
      box-sizing: border-box;
      transform: rotate(-135deg);
      margin-top: -9px;
    }
  }

  /* サイドメニュー出現 */
  & ~ .sidemenu-content {
    transform: translateX(0px);
    transition: transform 0.25s ease-in-out;
  }
}

.sidemenu-content {
  ul {
    list-style-type: none;
    width: 100%;
  }
  li {
    display: inline-block;
    margin-right: 50px;
    // margin-left: 50px;
    cursor: pointer;
    font-weight: bold;
  }
}
</style>
