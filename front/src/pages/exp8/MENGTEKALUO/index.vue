<template>
    <!-- <span> {{ test }}</span> -->
    <!-- <h2>一、实验目的  </h2>
    <p class="content">理解软件项目规模度量功能点法原理，通过实验操作掌握功能点法。 学生应以小组为单位，根据本小组“软件工程管理与经济”课程设计项目架构及组件等设计成果，以功能点方法测量该项目的规模(功能点数量)。 建议选用某一种功能点方法度量课程设计项目的功能点，并采用另外一种功能点方法或其他的软件规模度量方法对前一种方法的度量结果进行验证。 本实验为课内设计性实验项目，实验学时 1 学时，完成实验报告 1 学时。
    </p> -->
    <h2>一、实验步骤 </h2>
    <!-- <p class="content" > -->
    <p class="secondtitle">第一步：确定平均工期、标准差和估计工期</p>
    <p class="content">假设该软件项目共有三个WBS要素，分别是设计、建造和测试。假设这三个WBS要素的
        预估的工期概率分布都呈标准正态分布，请填写各自的平均工期、标准差以及最悲观、最可能和最乐观的
        估计工期。
        <br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实验操作：将项目平均工期、标准差以及最悲观、最可能和最乐观的估计工期填入表中。
    </p>
    <h2 style="text-align: center">工期估计表</h2>
    <a-table :pagination="false" :columns="columns1" :data-source="tableData1" bordered size="middle"
        style="word-break: break-all;" />
    <br>

    <p class="secondtitle">第二步：绘制工期的正态分布图</p>
    <p class="content">以三个WBS要素的工期的分布为输入，模拟得到整个项目的工期概率分布图。
        由于设计、建造和测试这三个要素都是呈标准正态分布，可以根据上面表格中的各自的均值
        和标准差数据大致画出三要素工期的正态分布图。<br />
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实验操作：绘制三阶段工期的概率分布图。</p>

    <p class="secondtitle">第三步：随机生成工期值</p>
    <p class="content">蒙特卡洛模拟定量分析整个项目的工期进度风险，可以用计算机来模拟项目的实施。
        需要为每个WBS要素随机生成400次工期值，此工期值满足该工期规定均值、标准差的正态分布。模拟结束后，
        得到总计400*3=1200个呈正态分布的随机工期值，并计算出三个要素相加的总工期。
        <br />
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实验操作：随机生成每个要素的工期值并计算总工期。
    </p>
    <a-button type="primary" @click="createRandomData">生成随机工期值</a-button>
    <h2 style="text-align: center">随机工期值</h2>
    <a-table :pagination="{ pageSize: 50 }" :columns="columns2" :data-source="tableData2" :scroll="{ y: 240 }" bordered
        size="middle" style="word-break: break-all;">
    </a-table>
    <p>总工期最大值: {{ maxSum }} &nbsp;&nbsp;&nbsp;&nbsp; 总工期最小值: {{ minSum }}</p>
    <br>

    <p class="secondtitle">第四步：统计总工期的概率和累积概率分布</p>
    <p class="content">计算得出总工期的最小值与最大值作为范围，统计该范围内每个总工期值的概率和累积概率。 <br />
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实验操作：统计总工期值的概率和累积概率</p>
    <!-- <a-button type="primary" @click="printMinMaxValues">计算最小值与最大值</a-button> -->
    
    <br>

    <p class="secondtitle">第五步：绘制总工期的概率和累积概率分布图</p>
    <p class="content">结合上面表格的数据，以分组数据为X轴，出现概率和累积概率的值为Y轴，
        绘制总工期的概率和累积概率分布图。红色柱状图是整个项目估计刚好多少天完工的概率数据，
        蓝线是整个项目在多少天内完工的概率，也就是蒙特卡洛模拟的结果。<br />
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实验操作：绘制总工期的概率和累积概率分布图。 </p>


    <p class="secondtitle">第六步：合理规划项目进度</p>
    <p class="content">通过累积概率分布图，可以得出项目进度规划为x天时，项目按时完工的概率。
        (1)假设最低允许30%不能按时完工的风险，得出项目应规划为多少日内完成。
        (2)假设最低允许15%不能按时完工的风险，得出项目应规划为多少日内完成。<br />
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;实验操作：计算项目进度规划。 </p>



    <h2 style="text-align: center">EO 和 EQ 复杂度认定表</h2>
    <a-table :pagination="false" :columns="columns3" :data-source="tableData3" bordered size="middle"
        style="word-break: break-all;" />
    <br>

    <h2 style="text-align: center">每个组件复杂度等级与功能点数对应关系表 </h2>
    <a-table :pagination="false" :columns="columns4" :data-source="tableData4" bordered size="middle"
        style="word-break: break-all;" />
    <br>



    <h2>二、实验参数 </h2>

    <h2 style="text-align: center;">表1：未调整功能点计算表 </h2>
    <a-table :pagination="false" :columns="columns" :data-source="tableData" bordered size="middle"
        style="word-break: break-all;">
        <template #bodyCell="{ column, record, index }">
            <template v-if="column.dataIndex === 'A' && tableData !== undefined">
                <a-input v-model:value="record.A" style="width:100px; " />
            </template>
            <template v-if="column.dataIndex === 'D' && tableData !== undefined">
                <a-input v-model:value="record.D" style="width:100px;" />
            </template>
            <template v-if="column.dataIndex === 'G' && tableData !== undefined">
                <a-input v-model:value="record.G" style="width:100px;" />
            </template>
            <template v-if="column.dataIndex === 'C' && tableData !== undefined">
                {{ c(index) }}
            </template>
            <template v-if="column.dataIndex === 'F' && tableData !== undefined">
                {{ f(index) }}
            </template>
            <template v-if="column.dataIndex === 'I' && tableData !== undefined">
                {{ i(index) }}
            </template>
            <template v-if="column.dataIndex === 'number' && tableData !== undefined">
                {{ number(index) }}
            </template>
            <template v-if="column.dataIndex === 'unchanged' && tableData !== undefined">
                {{ unchanged(index) }}
            </template>
        </template>
    </a-table>
    <br>

    <div style="width:100%;text-align:right">
        <span style="width:30%;display:inline-block" class="secondtitle">本实验未调整功能点总计为 </span>
        <span style="display:inline-block;font-size:20px;">{{ SUM }}</span>
    </div>
    <br>
    <br>

    <h2 style="text-align: center;">表2：系统特征因子表及计算表 </h2>
    <a-table :columns="columnsadjust" :pagination="false" :data-source="dataadjust" bordered size="middle"
        style="word-break: break-all;">
        <template #bodyCell="{ column, record }">
            <template v-if="column.dataIndex === 'grade'">
                <a-input-group compact>
                    <a-select v-model:value="record.grade">
                        <a-select-option value="0">0</a-select-option>
                        <a-select-option value="1">1</a-select-option>
                        <a-select-option value="2">2</a-select-option>
                        <a-select-option value="3">3</a-select-option>
                        <a-select-option value="4">4</a-select-option>
                        <a-select-option value="5">5</a-select-option>
                    </a-select>

                </a-input-group>

            </template>
        </template>
    </a-table>
    <br>
    <div style="width:100%;text-align:right">
        <span style="width:30%;display:inline-block" class="secondtitle">合计数 </span>
        <span style="display:inline-block;font-size:20px;">{{ SUM_A }}</span>
    </div>
    <br>
    <br>

    <span class="secondtitle">功能点调整因子(VAF)为 </span>
    <span style="font-size:20px">{{ VAF }}</span>
    <br /><br />
    <span class="secondtitle">本实验案例的功能点为</span>
    <span style="font-size:20px">{{ ALL }}</span>
    <br /><br />
</template>



<script lang="ts">
import { reactive } from 'vue'
import { defineComponent } from 'vue'
export default {
    name: 'Exp1_IFPUG',
    data() {
        return {
            test: '21111',
            SUM: 0,
            VAF: 0,
            SUM_A: 0,
            maxSum: 0,
            minSum: 0,
            columns3: [
                {
                    title: '引用的文件类型个数(FTR) ',
                    dataIndex: 'FTR',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },
                {
                    title: '数据元素类型(DET)',
                    children: [
                        {
                            title: '1-5',
                            dataIndex: 'left',
                            key: 'type',
                            align: 'center'
                            // width: 30,
                            // fixed: 'left',
                        },
                        {
                            title: '6-19',
                            dataIndex: 'mide',
                            key: 'type',
                            align: 'center'
                            // width: 30,
                            // fixed: 'left',
                        },
                        {
                            title: '>19',
                            dataIndex: 'right',
                            key: 'type',
                            align: 'center'
                            // width: 30,
                            // fixed: 'left',
                        },
                    ]
                }
            ],
            columns4: [
                {
                    title: '类型 ',
                    dataIndex: 'type',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },
                {
                    title: '复杂度级别',
                    children: [
                        {
                            title: '简单',
                            dataIndex: 'easy',
                            key: 'type',
                            align: 'center'
                            // width: 30,
                            // fixed: 'left',
                        },
                        {
                            title: '平均',
                            dataIndex: 'mide',
                            key: 'type',
                            align: 'center'
                            // width: 30,
                            // fixed: 'left',
                        },
                        {
                            title: '复杂',
                            dataIndex: 'complex',
                            key: 'type',
                            align: 'center'
                            // width: 30,
                            // fixed: 'left',
                        },
                    ]
                }
            ],
            columns1: [
                {
                    title: '',
                    dataIndex: 'stage',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },
                {
                    title: '最乐观',
                    dataIndex: 'optimistic',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },
                {
                    title: '最可能',
                    dataIndex: 'probably',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },
                {
                    title: '最悲观',
                    dataIndex: 'pessimistic',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },
                {
                    title: '平均工期',
                    dataIndex: 'average',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },
                {
                    title: '标准差',
                    dataIndex: 'sd',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },
                {
                    title: '分布',
                    dataIndex: 'distribution',
                    key: 'type',
                    align: 'center',
                    width: 400,
                    // fixed: 'left',
                },

            ],
            columns2: [
                {
                    title: '设计',
                    dataIndex: 'design',
                    width: 150,
                },
                {
                    title: '建造',
                    dataIndex: 'build',
                    width: 150,
                },
                {
                    title: '测试',
                    dataIndex: 'test',
                },
                {
                    title: '总工期',
                    dataIndex: 'sum',
                },

            ],
            columns: [
                {
                    title: '组件',
                    dataIndex: 'component',
                    key: 'component',
                    align: 'center'
                    // width: 30,
                    // fixed: 'left',
                },
                {
                    title: '数量',
                    dataIndex: 'number',
                    key: 'number',
                    align: 'center'
                    // width: 30,
                    // fixed: 'left',
                },
                {
                    title: '复杂度',
                    children: [
                        {
                            title: '简单',
                            align: 'center',
                            children: [{
                                title: '计数',
                                align: 'center',
                                children: [{
                                    title: 'A',
                                    // width: 30,
                                    dataIndex: 'A',
                                    align: 'center'
                                }],
                            },
                            {
                                title: '权重',
                                align: 'center',
                                children: [{
                                    title: 'B',
                                    dataIndex: 'B',
                                    align: 'center',
                                    // width: 30,
                                }],
                            },
                            {
                                title: '功能点数',
                                align: 'center',
                                children: [{
                                    title: 'C=A*B',
                                    align: 'center',
                                    dataIndex: 'C',
                                    // width: 30,
                                }],
                            }
                            ],
                        },
                        {
                            title: '平均',
                            align: 'center',
                            children: [{
                                title: '计数', children: [{
                                    align: 'center',
                                    dataIndex: 'D',
                                    title: 'D',
                                    // width: 30,
                                }],
                            },
                            {
                                title: '权重',
                                align: 'center',
                                children: [{
                                    dataIndex: 'E',
                                    align: 'center',
                                    title: 'E',
                                    // width: 30,
                                }],
                            },
                            {
                                title: '功能点数',
                                align: 'center',
                                children: [{
                                    dataIndex: 'F',
                                    title: 'F=D*E',
                                    align: 'center',
                                    // width: 30,
                                }],
                            }],
                        },
                        {
                            title: '复杂',
                            align: 'center',
                            children: [{
                                title: '计数',
                                align: 'center',
                                children: [{
                                    dataIndex: 'G',
                                    align: 'center',
                                    title: 'G',
                                    // width: 30,
                                }],
                            },
                            {
                                title: '权重',
                                align: 'center',
                                children: [{
                                    dataIndex: 'H',
                                    align: 'center',
                                    title: 'H',
                                    // width: 30,
                                }],
                            },
                            {
                                title: '功能点数',
                                align: 'center',
                                children: [{
                                    dataIndex: 'I',
                                    title: 'I=G*H',
                                    align: 'center',
                                    // width: 30,
                                }],
                            }],
                        },

                    ]
                },
                {
                    title: '未调整功能点数',
                    dataIndex: 'unchanged',
                    key: 'unchanged',
                    align: 'center',
                    // width: 800,
                    // fixed: 'right',
                },
            ],
            columnsadjust: [
                {
                    title: '序号',
                    dataIndex: 'index',
                    key: 'component',
                    align: 'center',
                    width: 100
                    // fixed: 'left',
                },
                {
                    title: '因子',
                    dataIndex: 'title',
                    key: 'component',
                    align: 'center',
                    width: 900,
                    // fixed: 'left',
                },
                {
                    title: '等级',
                    dataIndex: 'grade',
                    key: 'component',
                    align: 'center'
                    // width: 30,
                    // fixed: 'left',
                },
            ],
            tableData1: [
                {
                    stage: '设计',
                    optimistic: '8',
                    probably: '14',
                    pessimistic: '20',
                    average: '14',
                    sd: '2',
                    distribution: '正态分布',
                },
                {
                    stage: '开发',
                    optimistic: '14',
                    probably: '23',
                    pessimistic: '32',
                    average: '23',
                    sd: '3',
                    distribution: '正态分布',
                },
                {
                    stage: '测试',
                    optimistic: '10',
                    probably: '22',
                    pessimistic: '34',
                    average: '22',
                    sd: '4',
                    distribution: '正态分布',
                },
            ],
            tableData2: [],
            tableData3: [
                {
                    FTR: '0~1',
                    left: '简单',
                    mide: '简单',
                    right: '平均'
                },
                {
                    FTR: '2~3',
                    left: '简单',
                    mide: '平均',
                    right: '复杂'
                },
                {
                    FTR: '>3',
                    left: '平均',
                    mide: '复杂',
                    right: '复杂'
                }
            ],
            tableData4: [
                {
                    type: 'ILF',
                    easy: 'X7',
                    mide: 'X10',
                    complex: 'X15'
                },
                {
                    type: 'EIF',
                    easy: 'X5',
                    mide: 'X7',
                    complex: 'X10'
                },
                {
                    type: 'EI',
                    easy: 'X3',
                    mide: 'X4',
                    complex: 'X6'
                },
                {
                    type: 'EO',
                    easy: 'X4',
                    mide: 'X5',
                    complex: 'X7'
                },
                {
                    type: 'EQ',
                    easy: 'X3',
                    mide: 'X4',
                    complex: 'X6'
                }
            ],
            tableData: [
                {
                    component: 'EI',
                    number: '',
                    A: '',
                    B: '3',
                    C: '',
                    D: '',
                    E: '4',
                    F: '',
                    G: '',
                    H: '6',
                    I: '',
                    unchanged: '',
                },
                {
                    component: 'EO',
                    number: '',
                    A: '',
                    B: '4',
                    C: '',
                    D: '',
                    E: '5',
                    F: '',
                    G: '',
                    H: '7',
                    I: '',
                    unchanged: '',
                },
                {
                    component: 'EQ',
                    number: '',
                    A: '',
                    B: '3',
                    C: '',
                    D: '',
                    E: '4',
                    F: '',
                    G: '',
                    H: '6',
                    I: '',
                    unchanged: '',
                },
                {
                    component: 'ILF',
                    number: '',
                    A: '',
                    B: '7',
                    C: '',
                    D: '',
                    E: '10',
                    F: '',
                    G: '',
                    H: '15',
                    I: '',
                    unchanged: '',
                },
                {
                    component: 'EIF',
                    number: '',
                    A: '',
                    B: '5',
                    C: '',
                    D: '',
                    E: '7',
                    F: '',
                    G: '',
                    H: '10',
                    I: '',
                    unchanged: '',
                },
            ],
            dataadjust: [
                {
                    index: '1',
                    title: 'Requirement for reliable backup and recovery ',
                    grade: ''

                },
                {
                    index: '2',
                    title: 'Requirement for data communication',
                    grade: ''

                },
                {
                    index: '3',
                    title: 'Extent of distributed processing ',
                    grade: ''

                },
                {
                    index: '4',
                    title: 'Performance requirements ',
                    grade: ''

                },
                {
                    index: '5',
                    title: 'Expected operational environment ',
                    grade: ''

                },
                {
                    index: '6',
                    title: 'Extent of online data entries ',
                    grade: ''

                },
                {
                    index: '7',
                    title: 'Extent of multi-screen or multi-operation online data input ',
                    grade: ''

                },
                {
                    index: '8',
                    title: 'Extent of online updating of master files ',
                    grade: ''

                },
                {
                    index: '9',
                    title: 'Extent of complex inputs, outputs, online queries and files ',
                    grade: ''

                },
                {
                    index: '10',
                    title: 'Extent of complex data processing ',
                    grade: ''

                },
                {
                    index: '11',
                    title: 'Extent that currently developed code can be designed for reuse ',
                    grade: ''

                },
                {
                    index: '12',
                    title: 'Extent of conversion and installation included in the design ',
                    grade: ''

                },
                {
                    index: '13',
                    title: 'Extent of multiple installations in an organization and variety of customer organizations ',
                    grade: ''

                },
                {
                    index: '14',
                    title: 'Extent of change and focus on ease of use ',
                    grade: ''

                },
            ]
        }
    },
    computed: {
        c: function () {
            return (index) => {
                if (this.tableData.length > 0) {
                    this.tableData[index].C = (parseInt(this.tableData[index].A) ? parseInt(this.tableData[index].A) : 0) * parseInt(this.tableData[index].B)
                    return this.tableData[index].C
                }
            }
        },
        f: function () {
            return (index) => {
                if (this.tableData.length > 0) {
                    this.tableData[index].F = (parseInt(this.tableData[index].D) ? parseInt(this.tableData[index].D) : 0) * parseInt(this.tableData[index].E)
                    return this.tableData[index].F
                }
            }
        },
        i: function () {
            return (index) => {
                if (this.tableData.length > 0) {
                    this.tableData[index].I = (parseInt(this.tableData[index].G) ? parseInt(this.tableData[index].G) : 0) * parseInt(this.tableData[index].H)
                    return this.tableData[index].I
                }
            }
        },
        number: function () {
            return (index) => {
                if (this.tableData.length > 0) {
                    this.tableData[index].number = (parseInt(this.tableData[index].A) ? parseInt(this.tableData[index].A) : 0) + (parseInt(this.tableData[index].D) ? parseInt(this.tableData[index].D) : 0) + (parseInt(this.tableData[index].G) ? parseInt(this.tableData[index].G) : 0)
                    return this.tableData[index].number
                }
            }
        },
        unchanged: function () {
            return (index) => {
                if (this.tableData.length > 0) {
                    this.tableData[index].unchanged = (parseInt(this.tableData[index].C) ? parseInt(this.tableData[index].C) : 0) + (parseInt(this.tableData[index].F) ? parseInt(this.tableData[index].F) : 0) + (parseInt(this.tableData[index].I) ? parseInt(this.tableData[index].I) : 0)

                    var sum = 0
                    for (var i = 0; i < 5; i++)
                        sum += (parseInt(this.tableData[i].unchanged) ? parseInt(this.tableData[i].unchanged) : 0)
                    this.$data.SUM = sum

                    return this.tableData[index].unchanged
                }
            }
        },
        VAF() {
            var vaf = 0
            // console.log('111',this.$data.tableData)
            for (var i = 0; i < 14; i++)
                vaf += (parseInt(this.dataadjust[i].grade) ? parseInt(this.dataadjust[i].grade) : 0)

            vaf = vaf * 0.01 + 0.65
            this.$data.VAF = vaf.toFixed(2)
            return vaf
        },
        SUM_A() {
            var sum = 0
            for (var i = 0; i < 14; i++)
                sum += (parseInt(this.dataadjust[i].grade) ? parseInt(this.dataadjust[i].grade) : 0)
            return sum
        },
        ALL() {
            return (this.$data.SUM * this.$data.VAF).toFixed(2)
        }
    },
    methods: {
        created() {
            this.gettableData()
        },
        updated() {
            // 用于防止表格合计行不显示
            this.$nextTick(() => {
                this.$refs['detailTable'].doLayout();
            })
        },
        pdfHandle() {
            window.open('/#/show', "_blank")
        },
        pdfHandle2() {
            window.open('/#/show', "_blank")
        },
        getSummaries(param, val) {
            const { columns, data } = param;
            const sums = [];
            columns.forEach((column, index) => {
                if (index === 0) {
                    sums[index] = (() => {
                        // let el=<p>未调整功能点</p>
                    })();
                    return;
                }
                if (index === 11) {
                    sums[index] = (() => {
                        // let num=<p >￥{this.tableData[val].nonum.toFixed(2)}</p>
                        // return num;
                    })();
                    return;
                }
            });
            return sums;
        },
        count() {
        },
        createRandomData() {
            this.tableData2 = Array(400).fill(undefined).map((item) => ({
                design: Math.round(this.normalDistribution(14, 2)),
                build: Math.round(this.normalDistribution(23, 3)),
                test: Math.round(this.normalDistribution(22, 4)),
            }));

            let max = Number.MIN_SAFE_INTEGER;
            let min = Number.MAX_SAFE_INTEGER;
            for (var i = 0; i < 400; i++) {
                this.tableData2[i].sum = this.tableData2[i].design + this.tableData2[i].build + this.tableData2[i].test
                if (this.tableData2[i].sum > max) {
                    max = this.tableData2[i].sum;
                }
                if (this.tableData2[i].sum < min) {
                    min = this.tableData2[i].sum;
                }
            }
            this.maxSum = max;
            this.minSum = min;
        },
        normalDistribution(mean, std) {
            let u = 0;
            let v = 0;
            let s = 0;
            let val = 0;

            do {
                u = Math.random() * 2 - 1;
                v = Math.random() * 2 - 1;
                s = u * u + v * v;
            } while (s >= 1);

            val = u * Math.sqrt((-2 * Math.log(s)) / s);

            return mean + std * val;
        },
    }
}
</script>

<style scoped>
.title {
    text-align: center;
    font-family: sans-serif;
    font-size: 30px;
}

.secondtitle {
    text-indent: 2em;
    font-weight: bold;
    margin-left: 30px;
    margin-right: 30px;
}

.maintable {
    text-align: center;
    font-family: sans-serif;
    font-size: 30px;
}

.button1 {
    margin-left: 25px;
}

.button2 {
    margin-left: 15px;
}

.button3 {

    float: right;
    margin-top: 10px;
    margin-right: 50px;

}

.button4 {

    margin-left: 250px;

}

.content {
    text-indent: 2em;
    margin-left: 20px;
    margin-right: 20px;
}

.guidance {
    position: absolute;
    right: 50px;
    font-weight: bold;
}

:deep(.ant-table .ant-table-thead > tr > th) {
    border-width: 1px;
}
</style> 
