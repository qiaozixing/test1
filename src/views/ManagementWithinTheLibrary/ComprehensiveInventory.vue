<template>
    <div>
        <Card dis-hover>
            <Row>
                <Col :span="6">
                    移动日期: <DatePicker style="width: 200px" split-panels type="daterange"></DatePicker>
                </Col>
                <Col :span="6">
                    库存类型: <Input type="text" style="width:200px"/>
                </Col>
                <Col :span="6">
                    储位: <Input type="text" style="width:150px;margin-left: 9%"/>
                </Col>
                <Col :span="6">
                    托盘: <Input type="text" style="width:150px;margin-left: 9%"/>
                </Col>
            </Row>
            <Row style="margin-top: 5px">
                <Col :span="6">
                    货主: <Input type="text" style="width: 200px;margin-left: 9%"/>
                </Col>
                <Col :span="6">
                    货主名称: <Input type="text" style="width:200px"/>
                </Col>
                <Col :span="6">
                    商品编码: <Input type="text" style="width:150px"/>
                </Col>
                <Col :span="6">
                    商品数量: <Input type="text" style="width:150px"/>
                </Col>
            </Row>
            <Row style="margin-top: 5px">
                <Col :span="6">
                    商品名称: <Input type="text" style="width:200px"/>
                </Col>
                <Col :span="6">
                    生产日期:  <DatePicker style="width: 200px" split-panels type="daterange"></DatePicker>
                </Col>
            </Row>
            <Row style="margin-top: 5px">
                <Button>批量生产</Button>
                <Button icon="md-search" style="margin-left: 70%">查询</Button>
                <Button icon="md-refresh" style="margin-left: 5px">重置</Button>
            </Row>
        </Card>
        <Card dis-hover>
            <Table :columns="columns" :data="comdata"></Table>
        </Card>
    </div>
</template>

<script>
    import * as ComperApi from '@/api/ManagementWithinTheLibrary/ComprehensiveInventory.js'
    export default {
        name: "ComprehensiveInventory",
        data(){
            return {
                columns:this.comcolumns(),
                comdata:[],
                comresquestparams:{
                    page:1,
                    size:10,
                    total:0
                }
            }
        },
        methods:{
            comcolumns(){
                let comarr = [
                    {title:'移动日期',key:'lastMove',align:'center'},
                    {title:'库存类型',key:'kuctype',align:'center'},
                    {title:'储位',key:'kuWeiBianMa',align:'center'},
                    {title:'托盘',key:'binId',align:'center'},
                    {title:'货主',key:'cusCode',align:'center'},
                    {title:'货主名称',key:'zhongWenQch',align:'center'},
                    {title:'商品编码',key:'goodsId',align:'center'},
                    {title:'商品数量',key:'goodsQua',align:'center'},
                    {title:'商品名称',key:'shpMingCheng',align:'center'},
                    {title:'生产日期',key:'goodsProData',align:'center'},
                    {title:'保质期',key:'bzhiQi',align:'center'},
                    {title:'单位',key:'goodsUnit',align:'center'},
                    {title:'状态',key:'sttSta',align:'center'},
                ];
                return comarr;
            },
            ComperTestDate(){
                ComperApi.CompreList(this.comresquestparams).then(res=>{
                    this.comdata = res.data.data.rows;
                    this.comresquestparams.total = res.data.data.total;
                })
            }
        },
        created() {
            this.ComperTestDate()
        }
    }
</script>

<style scoped>

</style>