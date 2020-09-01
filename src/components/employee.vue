<template>
  <div>
      <h1>
      <span>旅游申请管理</span>
    </h1>
    <div class="island">
      <h3>
        <span>旅游申请一览</span>
      </h3>
      <table id="table">
        <thead>
          <th></th>
          <th>组别</th>
          <th>识别ID</th>
          <th>人数</th>
          <th>备注</th>
        </thead>
        <tbody>
          <tr>
            <td>
              <input type="button" value="情报入力" id="t_button_1" />
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
            <td></td>
          </tr>
          <tr>
            <td>
              <input type="button" value="情报入力" id="t_button_1" />
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
            <td></td>
          </tr>
          <tr>
            <td></td>
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
            <td>无</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "employeeVue",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
