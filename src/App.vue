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
    <br />
    <a-popover title="Title">
      <a-button>Hover</a-button>
      <template #content>
        <p>Here is the text content</p>
        <p>Here is the text content</p>
      </template>
    </a-popover>
    <br />
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
    <br />
    <!-- 表格 -->
    <a-space direction="vertical" size="large" fill>
      <div>
        <span>OnlyCurrent: </span>
        <a-switch v-model="rowSelection.onlyCurrent" />
      </div>
      <a-table
        row-key="name"
        :columns="columns"
        :data="data"
        :row-selection="rowSelection"
        v-model:selectedKeys="selectedKeys"
        :pagination="pagination"
      />
    </a-space>
    <br />
    <a-space>
      <a-tag closable>Tag</a-tag>
      <a-tag closable>
        <!-- 表示插入的字体图标的数据 -->
        <template #icon>
          <icon-star />
        </template>
        Tag
      </a-tag>
    </a-space>
    <!-- 时间轴 -->
    <a-timeline>
      <a-timeline-item label="2017-03-10" dotColor="#00B42A">
        The first milestone
      </a-timeline-item>
      <a-timeline-item label="2018-05-22">The second milestone</a-timeline-item>
      <a-timeline-item label="2020-06-22" dotColor="#F53F3F">
        The third milestone
        <IconExclamationCircleFill
          :style="{ color: 'F53F3F', fontSize: '12px', marginLeft: '4px' }"
        />
      </a-timeline-item>
      <a-timeline-item label="2020-09-30" dotColor="#C9CDD4">
        The fourth milestone
      </a-timeline-item>
    </a-timeline>
  </div>
</template>
<script>
import { ref, reactive } from 'vue';
import { IconExclamationCircleFill } from '@arco-design/web-vue/es/icon';
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
    // table
    const selectedKeys = ref(['1', '2']);

    const rowSelection = reactive({
      type: 'checkbox',
      showCheckedAll: true,
      onlyCurrent: false,
    });
    const pagination = { pageSize: 5 };

    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
      },
      {
        title: 'Salary',
        dataIndex: 'salary',
      },
      {
        title: 'Address',
        dataIndex: 'address',
      },
      {
        title: 'Email',
        dataIndex: 'email',
      },
    ];
    const data = reactive([
      {
        key: '1',
        name: 'Jane Doe',
        salary: 23000,
        address: '32 Park Road, London',
        email: 'jane.doe@example.com',
      },
      {
        key: '2',
        name: 'Alisa Ross',
        salary: 25000,
        address: '35 Park Road, London',
        email: 'alisa.ross@example.com',
      },
      {
        key: '3',
        name: 'Kevin Sandra',
        salary: 22000,
        address: '31 Park Road, London',
        email: 'kevin.sandra@example.com',
        disabled: true,
      },
      {
        key: '4',
        name: 'Ed Hellen',
        salary: 17000,
        address: '42 Park Road, London',
        email: 'ed.hellen@example.com',
      },
      {
        key: '5',
        name: 'William Smith',
        salary: 27000,
        address: '62 Park Road, London',
        email: 'william.smith@example.com',
      },
      {
        key: '6',
        name: 'Jane Doe 2',
        salary: 15000,
        address: '32 Park Road, London',
        email: 'jane.doe@example.com',
      },
      {
        key: '7',
        name: 'Alisa Ross 2',
        salary: 28000,
        address: '35 Park Road, London',
        email: 'alisa.ross@example.com',
      },
      {
        key: '8',
        name: 'Kevin Sandra 2',
        salary: 26000,
        address: '31 Park Road, London',
        email: 'kevin.sandra@example.com',
      },
      {
        key: '9',
        name: 'Ed Hellen 2',
        salary: 18000,
        address: '42 Park Road, London',
        email: 'ed.hellen@example.com',
      },
      {
        key: '10',
        name: 'William Smith 2',
        salary: 12000,
        address: '62 Park Road, London',
        email: 'william.smith@example.com',
      },
    ]);

    return {
      align,
      start,
      like,
      star,
      onLikeChange,
      onStarChange,
      /*table 数据*/
      rowSelection,
      columns,
      data,
      selectedKeys,
      pagination,
    };
  },
  components: { IconExclamationCircleFill }, // 引入组件
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
