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
                v-decorator="[
                  'department',
                  {
                    initialValue:department,
                    rules: [{ required: true, message: 'Please select a department' }],
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
                    rules: [{ required: true, message: 'Please select a department' }],
                  },
                ]"
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
                    rules: [{ required: true, message: 'Please select a department' }],
                  },
                ]"
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
                >
                  <a href="#">选择</a>
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
                <a-input-number
                  v-decorator="[
                  'count',
                  {
                    initialValue:count,
                    rules: [{ required: true, message: 'Please input a number' }],
                  },
                ]"
                />
                <a-button>详细</a-button>
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
          <a-button type="primary" size="large" @click="onSave">save</a-button>
        </a-space>
      </div>
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
export default {
  name: "detail",
  props: [
    "visible",
    "datasource",
    "department",
    "travelstartday",
    "travelendday",
    "destination",
    "count",
    "amount",
    "remaks",
    "index",
  ],
  data() {
    return {
      form: this.$form.createForm(this),
      residences,
      district,
      destinationStr: "",
      isHideRequired: true,
      cdatasource: this.datasource,
      indexValue: this.index,
    };
  },
  methods: {
    onClose() {
      console.log("index!!!" + this.indexValue);
      this.$emit("closeDrawer");
    },
    onSave() {
      let data = {
        departmentid: this.form.getFieldValue("department"),
        // department: this.form.getFieldLabel("department"),
        travelstartday: this.form.getFieldValue("travelstartday"),
        travelendday: this.form.getFieldValue("travelendday"),
        destination: this.form.getFieldValue("destination"),
        count: this.form.getFieldValue("count"),
        amount: this.form.getFieldValue("amount"),
        remaks: this.form.getFieldValue("remaks"),
      };
      this.$emit("submitDrawer", data, this.index);
      // console.log("form" + this.form.getFieldValue("destination"));
      this.onClose();
    },
    onChangeDistrict(value, selectedOptions) {
      this.destinationStr = selectedOptions.map((o) => o.label).join(", ");
    },
  },
};
</script>