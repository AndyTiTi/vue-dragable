<template>
    <div class="rowBorder">
        <el-row class="fontWeight">D组件</el-row>
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
    }
</script>
