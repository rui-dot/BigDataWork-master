<template>
    <div class="centreRight1">

        <div class="bg-color-black">
            <!-- 总共高为820 -->
            <div style="height: 820px">
              <div id="container" style="height: 100%"></div>
            </div>

        </div>
    </div>
</template>

<script>

    import { onMounted, ref } from 'vue'
    import * as echarts from 'echarts'
    export default {
        name: "Right1",
        components: {},
        setup() {

          const drawLine = () =>{
            const myChart = echarts.init(document.getElementById('container'), 'dark', {
              renderer: 'canvas',
              useDirtyRect: false
            });
            var option = {
                legend:{},
                tooltip:{
                  //折线图显示框，待添加
                  trigger: 'axis',
                },
                dataset: {
                  source:[
                    ['year', '2013', '2014', '2015', '2016', '2017', '2018'],
                    //测试数据
                    ['CO', 56.5, 82.1, 88.7, 70.1, 53.4, 85.1],
                    ['NO2', 51.1, 51.4, 55.1, 53.3, 73.8, 68.7],
                    ['O3', 40.1, 62.2, 69.5, 36.4, 45.2, 32.5],
                    ['PM2.5', 25.2, 37.1, 41.2, 18, 33.9, 49.1],
                    ['PM10',38.2, 45.1, 22.7, 57.7, 33.9, 11.8],
                    ['SO2', 10.2, 30.1, 22.2, 11, 8.8, 11.7]
                  ]
                },
                xAxis: { type: 'category' },
                yAxis: { gridIndex : 0 },
                grid: { top: '55%' },
                series: [
                  {
                    type: "line",
                    smooth: true,
                    seriesLayoutBy: 'row',
                    emphasis: { focus: 'series'}
                  },
                  {
                    type: "line",
                    smooth: true,
                    seriesLayoutBy: 'row',
                    emphasis: { focus: 'series'}
                  },
                  {
                    type: "line",
                    smooth: true,
                    seriesLayoutBy: 'row',
                    emphasis: { focus: 'series'}
                  },
                  {
                    type: "line",
                    smooth: true,
                    seriesLayoutBy: 'row',
                    emphasis: { focus: 'series'}
                  },
                  {
                    type: "line",
                    smooth: true,
                    seriesLayoutBy: 'row',
                    emphasis: { focus: 'series'}
                  },
                  {
                    type: "line",
                    smooth: true,
                    seriesLayoutBy: 'row',
                    emphasis: { focus: 'series'}
                  },
                  {
                    type: 'pie',
                    id: 'pie',
                    radius : '40%',
                    center: ['50%', '25%'],
                    emphasis: {
                      focus: 'self'
                    },
                    label: {
                      formatter: '{b}: {@2013} ({d}%)'
                    },
                    encode: {
                      itemName: 'year',
                      value: '2013',
                      tooltip: '2013'
                    }
                  }
                ]
              };
            myChart.on('updateAxisPointer', function (event) {
                const xAxisInfo = event.axesInfo[0];
                if(xAxisInfo){
                  const dimension = xAxisInfo.value + 1;
                  myChart.setOption({

                    series: {
                      id : 'pie',
                      label: {
                        formatter: '{b}: {@[' + dimension +']} ({d}%)'
                      },
                      encode: {
                        value: dimension,
                        tooltip: dimension
                      }
                    }
                  })
                }
              });

            if (option && typeof option === 'object') {
              myChart.setOption(option);
            }
            window.addEventListener('resize', myChart.resize());
          }
          onMounted(() =>{
            drawLine()
          })
        }
    }


</script>

<style lang="scss" scoped>
    /*$box-width: 300px;*/
    $box-width: 100%;
    $box-height: 900px;

    .centreRight1 {
        padding: 16px;
        height: $box-height;
        width: $box-width;
        border-radius: 10px;
        .bg-color-black {
            height: $box-height - 30px;
            border-radius: 10px;
        }
        .text {
            color: #c3cbde;
        }
        .dv-dec-3 {
            position: relative;
            width: 100px;
            height: 20px;
            top: -3px;
        }

        .bottom-data {
            .item-box {
                & > div {
                    padding-right: 5px;
                }
                font-size: 14px;
                float: right;
                position: relative;
                width: 50%;
                color: #d3d6dd;
                .dv-digital-flop {
                    width: 120px;
                    height: 30px;
                }
                i {
                    font-size: 20px;
                    line-height: 30px;
                    margin-left: 20px;
                }
                .colorYellow {
                    color: yellowgreen;
                }
                p {
                    text-align: center;
                }
            }
        }
    }
</style>
