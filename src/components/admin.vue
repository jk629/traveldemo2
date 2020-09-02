<template>
  <a-form :form="form" @submit="handleSubmit">
    <h1><span>旅游申请管理</span></h1>
    <a-form-item label="部门&组别">
      <a-cascader
        style="width:20%"
        v-decorator="[
          'residence',
          {
            initialValue: ['ALL', '', ''],
            rules: [
              { type: 'array', message: 'xxxxxxxxxxxxxx!' },
            ],
          },
        ]"
        :options="residences"
      />
    </a-form-item>
    <a-form-item label="状态">
      <a-select default-value="ALL" style="width:20%">
        <a-select-option value="0">ALL</a-select-option>
        <a-select-option value="1">待审批</a-select-option>
        <a-select-option value="2">已审批</a-select-option>
        <a-select-option value="3">终了</a-select-option>
      </a-select>
    </a-form-item>
    <a-form-item label="申请日">
      <a-date-picker />
    </a-form-item>
    <a-form-item label="审批日">
      <a-date-picker />
    </a-form-item>
    <a-form-item label="识别ID">
      <a-input-number :min="1000000" :max="9999999" :step="1" style="width:20%" />
    </a-form-item>
    <a-form-item>
      <a-space size="large">
        <a-button type="primary">检索</a-button>
        <a-button type="reset">重置</a-button>
      </a-space>
    </a-form-item>
    <div class="island">
      <h3>
        <span>旅游申请一览</span>
      </h3>
    </div>
    <div class="island">
      <div style="margin-bottom: 16px">
        <a-space size="large">
          <a-button :disabled="!hasSelected">批准</a-button>
          <a-button :disabled="!hasSelected">驳回</a-button>
        </a-space>
        <span style="margin-left: 8px">
          <template v-if="hasSelected">{{ `Selected ${selectedRowKeys.length} items` }}</template>
        </span>
      </div>
      <a-table
        :row-selection="{ selectedRowKeys : selectedRowKeys , onChange: onSelectChange }"
        :columns="tableData.columns"
        :data-source="tableData.dateSource"
        :rowKey="record=>record.id"
      >
        <a slot="link" slot-scope="id" @click="handleEdit(id)">{{id}}</a>
      </a-table>
    </div>
  </a-form>
</template>

<script>
// selection
const residences = [
  {
    value: "ALL",
    label: "ALL",
  },
  {
    value: "0",
    label: "D1",
    children: [
      {
        value: "01",
        label: "T1",
      },
      {
        value: "02",
        label: "T2",
      },
    ],
  },
  {
    value: "1",
    label: "D2",
    children: [
      {
        value: "03",
        label: "T3",
      },
    ],
  },
];
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
      checked: false,
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
      checked: false,
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
  name: "admin",
  props: {},
  data() {
    return {
      residences,
      // formItemLayout: {
      //   labelCol: {
      //     xs: { span: 24 },
      //     sm: { span: 8 },
      //   },
      //   wrapperCol: {
      //     xs: { span: 24 },
      //     sm: { span: 16 },
      //   },
      // },
      tableData,
      loading: false,
      selectedRowKeys: [],
    };
  },
  beforeCreate() {
    this.form = this.$form.createForm(this, { name: "search" });
  },
  computed: {
    hasSelected() {
      return this.selectedRowKeys.length > 0;
    },
  },
  methods: {
    start() {
      //   this.loading = true;
      //   // ajax request after empty completing
      //   setTimeout(() => {
      //     this.loading = false;
      //     this.tableData.selectedRowKeys = [];
      //   }, 1000);
    },
    onSelectChange(selectedRowKeys) {
      console.log("selectedRowKeys changed: ", selectedRowKeys);
      this.selectedRowKeys = selectedRowKeys;
    },
    handleSubmit(e) {
      e.preventDefault();
      this.form.validateFieldsAndScroll((err, values) => {
        if (!err) {
          console.log("Received values of form: ", values);
        }
      });
    },
    handleEdit(key) {
      console.log(key + "!!!!!!!!!");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
