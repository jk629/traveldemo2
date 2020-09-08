<template>
  <div>
    <div class="island">
      <h3>
        <span>旅游申请一览</span>
      </h3>
      <div>
        <a-button type="primary" @click="newDrawer">
          <a-icon type="plus" />新建申请
        </a-button>
      </div>

      <detail
        :visible="isVisible"
        :department="departmentValue"
        :departmentlb="departmentStr"
        :travelstartday="travelstartdayValue"
        :travelendday="travelenddayValue"
        :destination="destinationValue"
        :count="countValue"
        :amount="amountValue"
        :remaks="remaksValue"
        :index="index"
        :userType="false"
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
    title: "部门&组别",
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
    department: "D1/T2",
    departmentid: ['0', '02'],
    id: "1000001",
    count: "10",
    applydate: "2019-11-30",
    applicant: "张三",
    approvedate: "2019-12-03",
    approver: "李四",
    remaks: "同意",
    travelstartday: "2019-12-03",
    travelendday: "2020-09-06",
    destination: null,
    amount: "",
  },
  {
    index: 1,
    status: "终了",
    department: "D2/T3",
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
      departmentStr: "",
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
      this.departmentStr = this.dateSource[id].department;
      this.travelstartdayValue = this.dateSource[id].travelstartday;
      this.travelenddayValue = this.dateSource[id].travelendday;
      this.destinationValue = this.dateSource[id].destination;
      this.countValue = this.dateSource[id].count;
      this.amountValue = this.dateSource[id].amount;
      this.remaksValue = this.dateSource[id].remaks;
      this.showDrawer();
    },
    // updTableData(tbd) {
    //   this.tableData = tbd;
    // },
    newDrawer() {
      this.index = null;
      this.departmentValue = null;
      this.departmentStr = null;
      this.travelstartdayValue = null;
      this.travelenddayValue = null;
      this.destinationValue = null;
      this.countValue = null;
      this.amountValue = null;
      this.remaksValue = null;
      this.showDrawer();
    },
    showDrawer() {
      this.isVisible = true;
    },
    closeDrawer() {
      this.isVisible = false;
      console.log("branch close !!!!!!!!!");
    },
    submitDrawer(data) {
      if (data.index) {
        this.dateSource[data.index].departmentid = data.departmentid;
        this.dateSource[data.index].department = data.department;
        this.dateSource[data.index].travelstartday = data.travelstartday;
        this.dateSource[data.index].travelendday = data.travelendday;
        this.dateSource[data.index].destination = data.destination;
        this.dateSource[data.index].count = data.count;
        this.dateSource[data.index].amount = data.amount;
        this.dateSource[data.index].remaks = data.remaks;
      } else {
        data.index = this.dateSource.length;
        (data.status = "待审批"),
          (data.id =
            Number.parseInt(this.dateSource[this.dateSource.length - 1].id) +
            1);
        data.applydate =
          new Date().getFullYear() +
          "-0" +
          new Date().getMonth() +
          "-0" +
          new Date().getDate();
        data.applicant = "张三";
        this.dateSource.push(data);
      }

      this.closeDrawer();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
