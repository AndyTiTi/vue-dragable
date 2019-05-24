<template>
    <div>
        <el-row>
            <el-col :span="8" v-for="item in colors" :key="item.text">{{item.text}}</el-col>
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
                colors: [
                    {
                        text: "Aquamarine",
                    },
                    {
                        text: "Aotpink",
                    },
                    {
                        text: "Aold",
                    },
                    {
                        text: "Arimson",
                    },
                    {
                        text: "Alueviolet",
                    },
                    {
                        text: "Aightblue",
                    }
                ]
            }
        }
    }
</script>
<style>
    .el-row{
        margin-bottom: 10px;
    }
</style>