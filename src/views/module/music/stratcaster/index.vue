<template>
  <page-view :title="title">
    <a-card
      style="margin-top: 24px"
      :bordered="false"
      title="电吉他练习曲">

      <div slot="extra">
        <a-radio-group v-model="status">
          <a-radio-button value="all">全部</a-radio-button>
          <a-radio-button value="processing">进行中</a-radio-button>
          <a-radio-button value="waiting">等待中</a-radio-button>
        </a-radio-group>
        <a-input-search style="margin-left: 16px; width: 272px;" />
      </div>

      <!--      <div class="operate">-->
      <!--        <a-button type="dashed" style="width: 100%" icon="plus" @click="add">添加</a-button>-->
      <!--      </div>-->

      <a-list size="large" :pagination="{showSizeChanger: true, showQuickJumper: true, pageSize: 5, total: 50}">
        <a-list-item :key="index" v-for="(item, index) in data">
          <a-list-item-meta :description="item.description">
            <a-avatar slot="avatar" size="large" shape="square" :src="item.avatar"/>
            <a slot="title">{{ item.title }}</a>
          </a-list-item-meta>
          <div slot="actions">
            <a @click="edit(item)">详情</a>
          </div>
          <div slot="actions">
            <a-dropdown>
              <a-menu slot="overlay">
                <a-menu-item><a>编辑</a></a-menu-item>
                <a-menu-item><a>删除</a></a-menu-item>
              </a-menu>
              <a>更多<a-icon type="down"/></a>
            </a-dropdown>
          </div>
          <div class="list-content">
            <div class="list-content-item">
              <span>Owner</span>
              <p>{{ item.owner }}</p>
            </div>
            <div class="list-content-item">
              <span>开始时间</span>
              <p>{{ item.startAt }}</p>
            </div>
            <div class="list-content-item">
              <a-progress :percent="item.progress.value" :status="!item.progress.status ? null : item.progress.status" style="width: 180px" />
            </div>
          </div>
        </a-list-item>
      </a-list>
    </a-card>
  </page-view>
</template>

<script>
import { PageView } from '@/layouts'
import { STable } from '@/components'
import RoleModal from './modal'
const data = []
data.push({
  title: 'Ten word',
  avatar: 'http://localhost:8000/avatar.jpg',
  description: 'Joe Satriani,为了纪念9.11事件',
  owner: '魏其森',
  startAt: '2019-07-26 22:44',
  progress: {
    value: 85
  }
})
data.push({
  title: 'Where We Started',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/zOsKZmFRdUtvpqCImOVY.png',
  description: 'Guthrie Govan，柔情电吉他抒情曲目',
  owner: '魏其森',
  startAt: '2018-07-26 22:44',
  progress: {
    value: 54
  }
})
data.push({
  title: 'Ant Design',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/dURIMkkrRFpPgTuzkwnB.png',
  description: '生命就像一盒巧克力，结果往往出人意料',
  owner: '林东东',
  startAt: '2018-07-26 22:44',
  progress: {
    value: 66
  }
})
data.push({
  title: 'Ant Design Pro',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/sfjbOqnsXXJgNCjCzDBL.png',
  description: '城镇中有那么多的酒馆，她却偏偏走进了我的酒馆',
  owner: '周星星',
  startAt: '2018-07-26 22:44',
  progress: {
    value: 30
  }
})
data.push({
  title: 'Bootstrap',
  avatar: 'https://gw.alipayobjects.com/zos/rmsportal/siCrBXXhmvTQGWPNLBow.png',
  description: '那时候我只会想自己想要什么，从不想自己拥有什么',
  owner: '吴加好',
  startAt: '2018-07-26 22:44',
  progress: {
    status: 'exception',
    value: 100
  }
})

export default {
  name: 'UpgradeIndex',
  components: {
    PageView,
    STable,
    RoleModal
  },
  data () {
    return {
      data,
      status: 'all',
      columns: [
        {
          title: '编号',
          dataIndex: 'key'
        },
        {
          title: '学生',
          dataIndex: 'studentName'
        },
        {
          title: '老师',
          dataIndex: 'teacherName',
          scopedSlots: { customRender: 'online' }
        },
        {
          title: '课时费',
          dataIndex: 'lessonMoney'
        },
        {
          title: '类型',
          dataIndex: 'type'
        },
        {
          title: '上课时间',
          dataIndex: 'lessonTime'
        },
        {
          title: '课程内容',
          dataIndex: 'lessonContent'
        },

        {
          title: '操作',
          dataIndex: 'action',
          width: '150px',
          scopedSlots: { customRender: 'action' }
        }
      ],
      selectedRowKeys: [],
      selectedRows: []
    }
  },
  filters: {
  },
  computed: {
    title () {
      return this.$route.meta.title
    }
  },
  created () {
  },
  mounted () {

  },
  methods: {
  }
}
</script>
<style lang="less" scoped>
.ant-avatar-lg {
  width: 48px;
  height: 48px;
  line-height: 48px;
}

.list-content-item {
  color: rgba(0, 0, 0, .45);
  display: inline-block;
  vertical-align: middle;
  font-size: 14px;
  margin-left: 40px;
  span {
    line-height: 20px;
  }
  p {
    margin-top: 4px;
    margin-bottom: 0;
    line-height: 22px;
  }
}
</style>
