<template>
    <div>
        <el-row>
            <el-col :span="12">
                <el-button>123</el-button>
                <el-button>456</el-button>
            </el-col>
            <el-col :span="12">
                <el-input v-model="input" placeholder="请输入内容"></el-input>
            </el-col>
            <el-col :span="12" v-for="item in colors" :key="item.text">{{item.text}}</el-col>
        </el-row>
        <el-row :gutter="10">
            <el-col :span="12">
                <div class="grid-content"></div>
            </el-col>
            <el-col :span="12">
                <div class="grid-content"></div>
            </el-col>
            <el-col :span="12">
                <div class="grid-content"></div>
            </el-col>
            <el-col :span="12">
                <div class="grid-content"></div>
            </el-col>
        </el-row>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                input: '',
                colors: [
                    {
                        text: "Erimson",
                    },
                    {
                        text: "Elueviolet",
                    },
                    {
                        text: "Eightblue",
                    },
                    {
                        text: "Eornflowerblue",
                    },
                    {
                        text: "Ekyblue",
                    },
                    {
                        text: "Eurlywood",
                    }
                ]
            }
        }
    }
</script>
<style>
    .el-col {
        margin-bottom: 10px;
    }

    .grid-content {
        border-radius: 4px;
        min-height: 36px;
        background: #ff8900;
    }

</style>