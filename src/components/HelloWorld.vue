<template>
  <div class="hello">
    <div id="main" style="width: 1200px;height:400px; margin-top: 25px"></div>
  </div>
</template>

<script>
import $ from "jquery";
import echarts from "echarts";

let _data = [];
let myChart = null;

export default {
  name: "HelloWorld",
  data() {
    return {
      data: [],
    };
  },

  mounted (){
    myChart = echarts.init(document.getElementById("main"));
    const _this = this;
    $.post(
      "http://127.0.0.1:8000/initialize",
      {},
      function (res){
        let resObj = JSON.parse(res);
        console.log(resObj);
        _this.data = resObj.data;
        _data = resObj.data
        let option = {
          tooltip: {
            trigger: "item"
            //triggerOn: 'mousemove'
          },
          series: [
            {
              type: "tree",
              data: [_data],
              left: "5%",
              right: "5%",
              top: "8%",
              bottom: "20%",
              symbol: "emptyCircle",
              orient: "vertical",
              expandAndCollapse: true,
              label: {
                normal: {
                  position: "top",
                  rotate: 0,
                  verticalAlign: "middle",
                  align: "left",
                  fontSize: 14
                }
              },
              leaves: {
                label: {
                  normal: {
                    position: "bottom",
                    rotate: 0,
                    verticalAlign: "middle",
                    align: "center"
                  }
                }
              },
              animationDurationUpdate: 750
            }
          ]
        };

        // 使用刚指定的配置项和数据显示图表。
        myChart.setOption(option);
      }
    )
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
