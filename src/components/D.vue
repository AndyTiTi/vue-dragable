<template>
    <div>
        <el-row>
            <el-col :span="12" v-for="item in colors" :key="item.text">{{item.text}}</el-col>
        </el-row>
        <el-row :gutter="10">
            <el-col :span="18">
                <div class="grid-content"></div>
            </el-col>
            <el-col :span="6">
                <div class="grid-content"></div>
            </el-col>
            <el-col :span="6">
                <div class="grid-content"></div>
            </el-col>
            <el-col :span="18">
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
                        text: "Dold",
                    },
                    {
                        text: "Drimson",
                    },
                    {
                        text: "Dornflowerblue",
                    },
                    {
                        text: "Dkyblue",
                    },
                    {
                        text: "Durlywood",
                    }
                ]
            }
        }
    }
</script>