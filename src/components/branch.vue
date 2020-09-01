<template>
  <div>
      <h1>
      <span>旅游申请管理</span>
    </h1>
    <div class="island">
      <h3>
        <span>旅游申请一览</span>
      </h3>
      <div>
        <button type="button" id="button_1">
          <span>新建申请</span>
        </button>
      </div>
      <table id="table">
        <thead>
          <th>状态</th>
          <th>部门</th>
          <th>组别</th>
          <th>识别ID</th>
          <th>人数</th>
          <th>申请日</th>
          <th>申请人</th>
          <th>审批日</th>
          <th>审批人</th>
          <th>备注</th>
        </thead>
        <tbody>
          <tr>
            <td>
              <span>待审批</span>
            </td>
            <td>
              <span>D1</span>
            </td>
            <td>
              <span>T1</span>
            </td>
            <td>
              <a href="#">
                <span>00000015</span>
              </a>
            </td>
            <td>
              <span>10</span>
            </td>
            <td>
              <span>2020-07-05</span>
            </td>
            <td>
              <span>张三</span>
            </td>
            <td></td>
            <td></td>
            <td></td>
          </tr>
          <tr>
            <td>
              <span>已审批</span>
            </td>
            <td>
              <span>D1</span>
            </td>
            <td>
              <span>T2</span>
            </td>
            <td>
              <a href="#">
                <span>00000013</span>
              </a>
            </td>
            <td>
              <span>8</span>
            </td>
            <td>
              <span>2020-07-15</span>
            </td>
            <td>
              <span>张四</span>
            </td>
            <td>
              <span>2020-07-18</span>
            </td>
            <td>
              <span>李三</span>
            </td>
            <td></td>
          </tr>
          <tr>
            <td>
              <span>终了</span>
            </td>
            <td>
              <span>D1</span>
            </td>
            <td>
              <span>T1</span>
            </td>
            <td>
              <a href="#">
                <span>00000005</span>
              </a>
            </td>
            <td>
              <span>9</span>
            </td>
            <td>
              <span>2020-07-20</span>
            </td>
            <td>
              <span>张四</span>
            </td>
            <td>
              <span>2020-07-21</span>
            </td>
            <td>
              <span>李三</span>
            </td>
            <td>无</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "branchVue",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
