<template>
  <div class="cate-container">
    <van-sidebar v-model="active" class="sidebar">
      <template v-for="item in cateList" :key="item">
        <van-sidebar-item :title="item.cate_title"/>
      </template>
    </van-sidebar>
    <div class="shop-content">
      <template v-for="cateItem in cateList[active].cate_data" :key="cateItem.title">
        <h4 class="cate-title">{{ cateItem.title }}</h4>
        <van-grid :column-num="3" :gutter="10" :border="false">
          <template v-for="shopItem in cateItem.list" :key="shopItem.title">
            <van-grid-item :icon="shopItem.imgUrl" :text="shopItem.title"/>
          </template>
        </van-grid>
      </template>
    </div>
  </div>
</template>

<script lang="ts">
import {ref, watch} from 'vue';
import {cateList} from './cateList'

console.log(cateList, '分类数据')

export default {
  name: 'category',
  setup() {
    const active = ref(0);

    watch(() => active.value, () => document.querySelector('.shop-content').scrollTop = 0)

    return {active, cateList};
  },
};
</script>

<style lang="scss" scoped>
.cate-container {
  display: flex;

  .sidebar {
    height: var(--container-height);
    overflow-y: auto;
  }

  ::v-deep(.shop-content) {
    flex: 1;
    height: var(--container-height);
    overflow-y: auto;

    .cate-title {
      padding-left: px2rem(20);
      font-size: px2rem(14);
    }
    .van-grid-item__icon {
      .van-icon__image {
        font-size: px2rem(120);
      }
    }
  }
}
</style>
