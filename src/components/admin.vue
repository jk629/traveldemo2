<template>
  <div>
            <h1><span>旅游申请管理</span></h1>
            <form>
                <div class="island">
                    <table id="table_1">
                        <tr>
                            <th><span>部门</span></th>
                            <td><select id="select_1">
                                <option value="0"></option>
                                <option value="1">D1</option>
                                <option value="2">D2</option>
                            </select></td>
                        </tr>
                        <tr>
                            <th><span>组别</span></th>
                            <td><select id="select_2">
                                <option value="0">T1</option>
                                <option value="1">T2</option>
                            </select></td>
                        </tr>
                        <tr>
                            <th><span>状态</span></th>
                            <td><select id="select_3">
                                <option value="0">所有</option>
                                <option value="1">待审批</option>
                                <option value="2">已审批</option>
                                <option value="3">终了</option>
                            </select></td>
                        </tr>
                        <tr>
                            <th><span>申请日</span></th>
                            <td><input type="date" id="date_1"/></td>
                        </tr>
                        <tr>
                            <th><span>审批日</span></th>
                            <td><input type="date" id="date_2"/></td>
                        </tr>
                        <tr>
                            <th><span>识别ID</span></th>
                            <td><input type="number" id="text_1"/></td>
                        </tr>
                    </table>
                    <div class="search">
                        <input type="button" value="检索">
                        <input type="reset" value="重置">
                    </div>
                </div>
                <div class="island">
                    <h3><span>旅游申请一览</span></h3>
                    <div>
                        <button type="button" id="button_1"><span>批准</span></button>
                        <button type="button" id="button_2"><span>驳回</span></button>
                    </div>
                    <table id="table">
                        <thead>
                            <th></th>
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
                                <td><input type="checkbox" value="详细" id="checkbox_1" ></td>
                                <td><span>待审批</span></td>
                                <td><span>D1</span></td>
                                <td><span>T1</span></td>
                                <td><a href="#"><span>00000015</span></a></td>
                                <td><span>10</span></td>
                                <td><span>2020-07-05</span></td>
                                <td><span>张三</span></td>
                                <td></td>
                                <td></td>
                                <td></td>
                            </tr>
                            <tr>
                                <td><input type="checkbox" value="详细" id="checkbox_1" ></td>
                                <td><span>已审批</span></td>
                                <td><span>D1</span></td>
                                <td><span>T2</span></td>
                                <td><a href="#"><span>00000013</span></a></td>
                                <td><span>8</span></td>
                                <td><span>2020-07-15</span></td>
                                <td><span>张四</span></td>
                                <td><span>2020-07-18</span></td>
                                <td><span>李三</span></td>
                                <td></td>
                            </tr>
                            <tr>
                                <td></td>
                                <td><span>终了</span></td>
                                <td><span>D2</span></td>
                                <td><span>T1</span></td>
                                <td><a href="#"><span>00000005</span></a></td>
                                <td><span>9</span></td>
                                <td><span>2020-07-20</span></td>
                                <td><span>张四</span></td>
                                <td><span>2020-07-21</span></td>
                                <td><span>李三</span></td>
                                <td>无</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </form>
        </div>
</template>

<script>
export default {
  name: "adminVue",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
