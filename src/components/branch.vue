<template>
  <div>
    <div class="island">
      <h3>
        <span>旅游申请一览</span>
      </h3>
      <div>
        <a-button type="primary" @click="showDrawer">
          <a-icon type="plus" />新建申请
        </a-button>
        <detail />
      </div>

      <detail
        :visible="isVisible"
        :department="departmentValue"
        :travelstartday="travelstartdayValue"
        :travelendday="travelenddayValue"
        :destination="destinationValue"
        :count="countValue"
        :amount="amountValue"
        :remaks="remaksValue"
        :index="index"
        @closeDrawer="closeDrawer"
        @submitDrawer="submitDrawer"
      />
      <a-table :columns="columns" :data-source="dateSource" :rowKey="record=>record.index">
        <a slot="link" slot-scope="id,record" @click="handleEdit(record.index)">{{id}}</a>
      </a-table>
    </div>
  </div>
</template>

<script>
import detail from "./detail";
// table
var columns = [
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
];
var dateSource = [
  {
    index: 0,
    status: "终了",
    department: "D1",
    departmentid: ["0", "02"],
    id: "1000001",
    count: "10",
    applydate: "2019-11-30",
    applicant: "张三",
    approvedate: "2019-12-03",
    approver: "李四",
    remaks: "同意",
    travelstartday: "2019-12-03",
    travelendday: "",
    destination: null,
    amount: "",
  },
  {
    index: 1,
    status: "终了",
    department: "D1",
    departmentid: ["1", "03"],
    id: "1000002",
    count: "10",
    applydate: "2019-11-30",
    applicant: "张三",
    approvedate: "2019-12-03",
    approver: "李四",
    remaks: "同意",
    travelstartday: "",
    travelendday: "",
    destination: null,
    amount: "",
  },
];

export default {
  name: "branch",
  components: {
    detail,
  },
  data() {
    return {
      columns,
      dateSource,
      departmentValue: "",
      travelstartdayValue: "",
      travelenddayValue: "",
      destinationValue: "",
      countValue: "",
      amountValue: "",
      remaksValue: "",
      isVisible: false,
      index: null,
    };
  },
  methods: {
    handleEdit(id) {
      //通过key取得当前行数据
      // const currentData = this.dateSource.filter(item => key === item.id)[0];
      this.index = id;
      this.departmentValue = this.dateSource[id].departmentid;
      this.travelstartdayValue = this.dateSource[id].travelstartday;
      this.travelenddayValue = this.dateSource[id].travelendday;
      this.destinationValue = this.dateSource[id].destination;
      this.countValue = this.dateSource[id].count;
      this.amountValue = this.dateSource[id].amount;
      this.remaksValue = this.dateSource[id].remaks;
      this.isVisible = true;
    },
    // updTableData(tbd) {
    //   this.tableData = tbd;
    // },
    showDrawer() {
      this.isVisible = true;
      console.log("branch open !!!!!!!!!");
    },
    closeDrawer() {
      this.isVisible = false;
      console.log("branch close !!!!!!!!!");
    },
    submitDrawer(data, index) {
      this.dateSource[index].departmentid = data.departmentid;
      this.dateSource[index].travelstartday = data.travelstartday;
      this.dateSource[index].travelendday = data.travelendday;
      this.dateSource[index].destination = data.destination;
      this.dateSource[index].count = data.count;
      this.dateSource[index].amount = data.amount;
      this.dateSource[index].remaks = data.remaks;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
