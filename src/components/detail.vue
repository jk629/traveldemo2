<template>
  <a-drawer
    title="旅游情报"
    :width="720"
    :visible="visible"
    :body-style="{ paddingBottom: '80px' }"
    @close="onClose"
  >
    <div>
      <a-form :form="form" layout="vertical" :hide-required-mark="isHideRequired">
        <a-row :gutter="16">
          <a-col :span="12">
            <a-form-item label="部门&组别">
              <a-cascader
                :options="residences"
                :allowClear="false"
                :disabled="userType"
                @change="onChangeDepartment"
                v-decorator="[
                  'department',
                  { 
                    initialValue:department,
                  },
                ]"
              />
            </a-form-item>
          </a-col>
        </a-row>
        <a-row :gutter="16">
          <a-col :span="12">
            <a-form-item label="旅游开始日">
              <a-date-picker
                v-decorator="[
                  'travelstartday',
                  {
                    initialValue:travelstartday,
                    rules: [{ required: true, message: 'Please select a travelstartday' }],
                  },
                ]"
                :disabled="userType"
              />
            </a-form-item>
          </a-col>
          <a-col :span="12">
            <a-form-item label="旅游结束日">
              <a-date-picker
                v-decorator="[
                  'travelendday',
                  {
                    initialValue:travelendday,
                    rules: [{ required: true, message: 'Please select a travelendday' }],
                  },
                ]"
                :disabled="userType"
              />
            </a-form-item>
          </a-col>
        </a-row>
        <a-row :gutter="16">
          <a-col :span="24">
            <a-form-item label="目的地">
              <a-space size="large">
                <a-cascader
                  :options="district"
                  @change="onChangeDistrict"
                  v-decorator="[
                  'destination',
                  {
                    initialValue:destination,
                    rules: [{ required: true, message: 'Please select a destination' }],
                  },
                ]"
                  :disabled="userType"
                >
                  <a href="#" :disabled="userType">选择</a>
                </a-cascader>
                {{ destinationStr }} &nbsp;
              </a-space>
            </a-form-item>
          </a-col>
        </a-row>
        <a-row :gutter="16">
          <a-col :span="24">
            <a-form-item label="人数">
              <a-space size="large">
                {{totalCount}}
                <a-button @click="showModal" :disabled="userType">详细</a-button>
              </a-space>
            </a-form-item>
          </a-col>
        </a-row>
        <a-row :gutter="16">
          <a-col :span="24">
            <a-form-item label="预算">
              <a-space size="large">
                <a-input-number
                  v-decorator="[
                  'amount',
                  {
                    initialValue:amount,
                    rules: [{ required: true, message: 'Please input a number' }],
                  },
                ]"
                  :disabled="userType"
                />
                {{amount}} $
              </a-space>
            </a-form-item>
          </a-col>
        </a-row>
        <a-row :gutter="16">
          <a-col :span="24">
            <a-form-item label="备注">
              <a-textarea
                v-decorator="[
                  'remaks',
                  {
                    initialValue:remaks,
                    rules: [{ required: true, message: 'Please enter something' }],
                  },
                ]"
                :disabled="userType"
                :rows="4"
                placeholder="please enter url description"
              />
            </a-form-item>
          </a-col>
        </a-row>
      </a-form>
      <div
        :style="{
          position: 'absolute',
          right: 0,
          bottom: 0,
          width: '100%',
          borderTop: '1px solid #e9e9e9',
          padding: '10px 16px',
          background: '#fff',
          textAlign: 'right',
          zIndex: 1,
        }"
      >
        <a-space size="large">
          <a-button @click="onClose" size="large">Cancel</a-button>
          <a-button type="primary" size="large" @click="onSave" :disabled="userType">save</a-button>
        </a-space>
      </div>
      <a-modal title="员工信息" :visible="isModal" @ok="handleOk" @cancel="handleCancel">
        <a-table
          :row-selection="{ selectedRowKeys : selectedRowKeys , onChange: onSelectChange }"
          :columns="columns"
          :data-source="dateSource"
          :rowKey="record=>record.index"
        ></a-table>
      </a-modal>
    </div>
  </a-drawer>
</template>
<script>
// selection
const residences = [
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
const district = [
  {
    value: "0",
    label: "国内",
    children: [
      {
        value: "01",
        label: "北京",
      },
      {
        value: "02",
        label: "上海",
      },
      {
        value: "03",
        label: "山东",
        children: [
          {
            value: "030",
            label: "济南",
          },
          {
            value: "031",
            label: "青岛",
          },
        ],
      },
    ],
  },
  {
    value: "1",
    label: "国外",
    children: [
      {
        value: "10",
        label: "日本",
        children: [
          {
            value: "100",
            label: "东京",
          },
          {
            value: "101",
            label: "北海道",
            children: [
              {
                value: "1010",
                label: "x1",
              },
              {
                value: "1011",
                label: "x2",
              },
            ],
          },
        ],
      },
    ],
  },
];
// table
var columns = [
  {
    title: "员工ID",
    dataIndex: "id",
  },
  {
    title: "员工姓名",
    dataIndex: "name",
  },
  {
    title: "家属",
    dataIndex: "fanmily",
  },
  {
    title: "人数",
    dataIndex: "count",
  },
  {
    title: "备注",
    dataIndex: "remaks",
  },
];
var dateSource = [
  {
    index: 0,
    id: "000001",
    count: "1",
    name: "张三",
    fanmily: "",
    remaks: "",
  },
  {
    index: 1,
    id: "000002",
    count: "3",
    name: "李四",
    fanmily: "有",
    remaks: "小孩",
  },
  {
    index: 2,
    id: "000003",
    count: "5",
    name: "王五",
    fanmily: "有",
    remaks: "小孩和老人",
  },
];
export default {
  name: "detail",
  props: [
    "visible",
    "datasource",
    "department",
    "departmentlb",
    "travelstartday",
    "travelendday",
    "destination",
    "count",
    "amount",
    "remaks",
    "index",
    "userType",
  ],
  data() {
    return {
      form: this.$form.createForm(this),
      residences,
      district,
      destinationStr: "",
      departmentStr: "",
      isHideRequired: true,
      isModal: false,
      dateSource,
      columns,
      selectedRowKeys: [],
      totalCount: 0,
    };
  },
  computed: {
    hasSelected() {
      return this.selectedRowKeys.length > 0;
    },
  },
  methods: {
    onClose() {
      console.log("index!!!" + this.index);
      this.$emit("closeDrawer");
    },
    onSelectChange(selectedRowKeys) {
      console.log("selectedRowKeys changed: ", selectedRowKeys);
      this.selectedRowKeys = selectedRowKeys;
    },
    onSave() {
      this.form.validateFieldsAndScroll((err, values) => {
        if (!err) {
          console.log("Received values of form: ", values);
        }
      });
      let data = {
        index: this.index,
        departmentid: this.form.getFieldValue("department"),
        department: this.departmentStr ? this.departmentStr : this.departmentlb,
        travelstartday: this.form.getFieldValue("travelstartday"),
        travelendday: this.form.getFieldValue("travelendday"),
        destination: this.form.getFieldValue("destination"),
        count: this.totalCount,
        amount: this.form.getFieldValue("amount"),
        remaks: this.form.getFieldValue("remaks"),
      };
      this.$emit("submitDrawer", data);
      // console.log("form" + this.form.getFieldValue("destination"));
    },
    onChangeDistrict(value, selectedOptions) {
      this.destinationStr = selectedOptions.map((o) => o.label).join(", ");
    },
    onChangeDepartment(value, selectedOptions) {
      this.departmentStr = selectedOptions.map((o) => o.label).join("/");
      // console.log("selectedOptions:" + selectedOptions);
    },
    showModal() {
      this.isModal = true;
    },
    handleOk() {
      this.totalCount = this.selectedRowKeys.length;
      this.isModal = false;
    },
    handleCancel() {
      this.isModal = false;
    },
  },
};
</script>