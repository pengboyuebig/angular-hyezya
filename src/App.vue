<template>
  <div>
    <a-space direction="vertical" fill>
      <a-button type="primary" small>Item1</a-button>
      <a-button type="primary" long>Item2</a-button>
      <a-button type="primary" long>Item3</a-button>
    </a-space>
    <div>
      <div style="marginbottom: 20px">
        <a-radio-group v-model="align" type="button">
          <a-radio value="start">start</a-radio>
          <a-radio value="center">center</a-radio>
          <a-radio value="end">end</a-radio>
          <a-radio value="baseline">baseline</a-radio>
        </a-radio-group>
      </div>
      <a-space
        :align="align"
        style="backgroundcolor: var(--color-fill-2); padding: 10px"
      >
        <a-typography-text>Space:</a-typography-text>
        <a-button type="primary">Item2</a-button>
        <a-card title="Card"> Card content </a-card>
      </a-space>
    </div>
    <a-collapse :default-active-key="['1', 2]">
      <a-collapse-item header="Beijing Toutiao Technology Co., Ltd." key="1">
        <div>Beijing Toutiao Technology Co., Ltd.</div>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
        <div>Beijing Toutiao Technology Co., Ltd.</div>
      </a-collapse-item>
    </a-collapse>
    <a-comment
      author="Socrates"
      content="Comment body content."
      datetime="1 hour"
    >
      <template #actions>
        <span class="action" key="heart" @click="onLikeChange">
          <span v-if="like">
            <IconHeartFill :style="{ color: '#f53f3f' }" />
          </span>
          <span v-else>
            <IconHeart />
          </span>
          {{ 83 + (like ? 1 : 0) }}
        </span>
        <span class="action" key="star" @click="onStarChange">
          <span v-if="star">
            <IconStarFill
              style="
                 {
                  color: '#ffb400';
                }
              "
            />
          </span>
          <span v-else>
            <IconStar />
          </span>
          {{ 3 + (star ? 1 : 0) }}
        </span>
        <span class="action" key="reply"> <IconMessage /> Reply </span>
      </template>
      <template #avatar>
        <a-avatar>
          <img
            alt="avatar"
            src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp"
          />
        </a-avatar>
      </template>
    </a-comment>
    <a-list :gridProps="{ gutter: 0, span: 6 }" :bordered="true">
      <a-list-item>
        <a-list>
          <template #header>Platform</template>
          <a-list-item>iOS</a-list-item>
          <a-list-item>iOS</a-list-item>
          <a-list-item>iOS</a-list-item>
        </a-list>
      </a-list-item>
    </a-list>
    <a-popover title="Title">
      <a-button>Hover</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <a-space size="large">
      <a-statistic title="New Users" :value="125670" show-group-separator>
        <template #suffix>
          <icon-arrow-rise />
        </template>
      </a-statistic>
      <a-statistic
        title="User Growth Rate"
        :value="50.52"
        :precision="2"
        :value-style="{ color: '#0fbf60' }"
      >
        <template #prefix>
          <icon-arrow-rise />
        </template>
        <template #suffix>%</template>
      </a-statistic>
    </a-space>
    <br />
    <a-statistic
      title="User Growth Rate"
      :value="50.52"
      :precision="2"
      :value-from="0"
      :start="start"
      animation
    >
      <template #prefix>
        <icon-arrow-rise />
      </template>
      <template #suffix>%</template>
    </a-statistic>
    <a-button @click="start = true">Start</a-button>
  </div>
</template>
<script>
import { ref } from 'vue';
import {
  IconHeart,
  IconMessage,
  IconStar,
  IconStarFill,
  IconHeartFill,
} from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconHeart,
    IconMessage,
    IconStar,
    IconStarFill,
    IconHeartFill,
  },
  setup() {
    const like = ref(false);
    const star = ref(false);
    const onLikeChange = () => {
      like.value = !like.value;
    };
    const onStarChange = () => {
      star.value = !star.value;
    };
    const align = ref(false);
    const start = ref(false);
    return {
      // align
      start
      like,
      star,
      onLikeChange,
      onStarChange,
    };
  },
};
</script>
<style scoped>
.action {
  display: inline-block;
  padding: 0 4px;
  color: var(--color-text-1);
  line-height: 24px;
  background: transparent;
  border-radius: 2px;
  cursor: pointer;
  transition: all 0.1s ease;
}
.action:hover {
  background: var(--color-fill-3);
}
</style>
