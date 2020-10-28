<template>
    <div class="watermark">
        <el-button class="excel_button" type="primary" @click="ExportToExcel">Excel-Export</el-button>
        <div :style="`color:${color};transform: rotate(${rotate}deg);width:${wm_w}%;height:${wm_h}%;opacity: ${opacity}`"
             class="wm" v-for="(i,index) in watermarkNum"
             :key="index"
        >{{watermarkText}}</div>
    </div>
</template>

<script>
    export default {
        name: "ExportToExcel",
        data(){
            return{
                //死数据，实际项目中需要调用api中的数据
                tableData:[
                    {id: '1',name: 'json',username: 'json数据',sex: '男',email: 'json@wyy.com'},
                    {id: '2',name: 'api',username:  'api接口',sex: '男',email: 'api@wyy.com'},
                    {id: '3',name: 'vue-cli3',username: 'vue.js',sex: '男',email: 'vue@wyy.com'},
                    {id: '4',name: 'elementUI',username: 'elementUI模板',sex: '男',email: 'elementUI@wyy.com'}
                ],
                watermarkNum: 0, //水印数量
                watermarkRow: 2, //列数
                watermarkLine:2, //行数
                rotate: -30,     //文字旋转角度
                color: '#ccc',   //文字颜色
                watermarkText: '仅供测试使用',    //水印文本
                wm_w: 0,          //水印宽度百分比
                wm_h: 0,           //水印高度百分比
                opacity:0.2        //水印透明度
            }
        },
        created(){},
        mounted(){
            //在挂载后载入水印
            this.setwaterMark();
        },
        methods: {
            //Excel导出
            ExportToExcel(){
                const {export_json_to_excel} = require('../assets/js/ExportExcel');
                const tHeader = ['序号','姓名','用户名','性别','邮箱'];
                const filterVal = ['id','name','username','sex','email'];
                const list = this.tableData;
                const data = this.formatJson(filterVal,list);
                export_json_to_excel(tHeader,data,'测试Excel导出');
            },
            //Excel导出函数
            formatJson(filterVal,jsonData){
                return jsonData.map(v => filterVal.map(j => v[j]))
            },
            //创建水印
            setwaterMark(){
                let that = this;
                that.watermarkNum = that.watermarkRow * that.watermarkLine;
                that.wm_w = 100 / that.watermarkRow;
                that.wm_h = 100 / that.watermarkLine;
            }

        }
    }
</script>

<style lang="less" scoped>
    .watermark{
        width: 100%;
        height: auto;
        display: flex;
        .excel_button{
            margin-top: 120px;
        }
    }
</style>
