<template>
    <div class="rowBorder">
        <el-row class="fontWeight">
            A组件
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
    }
</script>
<style>
    .rowBorder{
        margin-bottom: 20px;
        padding: 20px;
        border:1px solid #2c3e50;
        background: rgba(0,0,0,0.2);
    }
    .fontWeight{
        font-size: 20px;
        color: #ff6400;
        font-weight: 700;
    }

    .el-col {
        margin-bottom: 10px;
    }

    .grid-content {
        border-radius: 4px;
        min-height: 36px;
        background: green;
    }

</style>
