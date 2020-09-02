<template>
  <div>
    <div class="island">
      <h3>
        <span>旅游申请一览</span>
      </h3>
      <div>
        <a-button type="primary" @click="showDrawer"><a-icon type="plus"/>新建申请</a-button>
      </div>
      <a-drawer
      title="Create a new account"
      :width="720"
      :visible="visible"
      :body-style="{ paddingBottom: '80px' }"
      @close="onClose"
    >
    <detail/>
      </a-drawer>
      <a-table
        :columns="tableData.columns"
        :data-source="tableData.dateSource"
        :rowKey="record=>record.id"
      >
        <a slot="link" slot-scope="id" @click="handleEdit(id)">{{id}}</a>
      </a-table>
    </div>
  </div>
</template>

<script>
import detail from './detail'
// table
var tableData = {
  columns: [
    {
      title: "状态",
      dataIndex: "status",
    },
    {
      title: "部门",
      dataIndex: "department",
    },
    {
      title: "识别ID",
      dataIndex: "id",
      scopedSlots: { customRender: "link" },
    },
    {
      title: "人数",
      dataIndex: "count",
    },
    {
      title: "申请日",
      dataIndex: "applydate",
    },
    {
      title: "申请人",
      dataIndex: "applicant",
    },
    {
      title: "审批日",
      dataIndex: "approvedate",
    },
    {
      title: "审批人",
      dataIndex: "approver",
    },
    {
      title: "备注",
      dataIndex: "remaks",
    },
  ],
  dateSource: [
    {
      status: "终了",
      department: "D1",
      id: "1000001",
      count: "10",
      applydate: "2019-11-30",
      applicant: "张三",
      approvedate: "2019-12-03",
      approver: "李四",
      remaks: "同意",
    },
    {
      status: "待审批",
      department: "D2",
      id: "1000004",
      count: "15",
      applydate: "2019-11-15",
      applicant: "王五",
      approvedate: "2019-12-10",
      approver: "朱六",
      remaks: "",
    },
  ],
};
export default {
  name: "branch",
  props: {
  },
  components: {
    detail
  },
  data() {
    return {
            tableData,
            visible:false,
    }
  },
  methods: {
    handleEdit(key) {
      console.log(key + "!!!!!!!!!");
    },
    showDrawer() {
      this.visible = true;
    },
    onClose() {
      this.visible = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
