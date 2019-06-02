<template>
    <div>
        <!-- 选择屏幕框 -->
        <select v-model="selected">
            <option v-for="option in layouts" :value="option.value" :key="option.value">
                {{ option.name }}
            </option>
        </select>
        <span style="padding: 0 20px;" class="field-label">方块选择</span>
        <el-select v-model="selected" placeholder="请选择">
            <el-option
                    v-for="option in layouts"
                    :key="option.value"
                    :label="option.label"
                    :value="option.value"
            >
            </el-option>
        </el-select>
        <el-main v-model="selected">
            <div class="block" style="height:350px;">
                <!-- {{selected}} -->
                <div style="height:100%;width:100%" v-if="selected==0">
                    <!-- 1*1布局 -->
                    <el-row
                            :gutter="10"
                            type="flex"
                            class="grid-one-contentheight"
                            justify="center"
                    >
                        <el-col :span="24"></el-col>
                    </el-row>
                </div>
                <!-- 2*1布局 -->
                <div style="height:100%;width:100%" v-else-if="selected==1">
                    <el-row
                            :gutter="10"
                            type="flex"
                            class="row-bg el-row-two"
                            justify="space-between"
                    >
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                    </el-row>
                </div>
                <!-- 2*2 -->
                <div style="height:100%;width:100%" v-else-if="selected==2">
                    <el-row :gutter="10" type="flex" class="row-bg" justify="center">
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                    </el-row>
                    <br />
                    <el-row :gutter="10" type="flex" class="row-bg" justify="center">
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                    </el-row>
                </div>
                <!-- 3*2布局 -->
                <div style="height:100%;width:100%" v-else-if="selected==3">
                    <el-row :gutter="10" type="flex" class="row-bg" justify="center">
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                    </el-row>
                    <br />
                    <el-row :gutter="10" type="flex" class="row-bg" justify="center">
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                        <el-col :span="12"><div class="grid-content "></div></el-col>
                    </el-row>
                </div>
                <!-- 3*3模式 -->
                <div style="height:100%;width:100%" v-else-if="selected==4">
                    <el-row :gutter="10" type="flex" class="row-bg" justify="center">
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                    </el-row>
                    <br />
                    <el-row :gutter="10" type="flex" class="row-bg" justify="center">
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                    </el-row>
                    <br />
                    <el-row :gutter="10" type="flex" class="row-bg" justify="center">
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                    </el-row>
                </div>
                <!-- 模式 -->
                <div style="height:100%;width:100%" v-else>
                    <el-row :gutter="10" type="flex" class="row-bg" justify="start">
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                        <el-col :span="8"><div class="grid-a-contentWidth"></div></el-col>
                    </el-row>
                    <br />
                    <el-row :gutter="10" type="flex" class="row-bg" justify="start">
                        <el-col :span="8">
                            <div class="grid-a-contentWidth"></div>
                            <br />
                            <div class="grid-a-contentWidth"></div>
                        </el-col>
                        <el-col :span="16"
                        ><div class="grid-a-content-a-Width"></div
                        ></el-col>
                    </el-row>
                </div>
            </div>
        </el-main>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        selected: 0,
        layouts: [
          { name: '1x1模式', value: '0', label: '1x1模式' },
          { name: '2x1模式', value: '1', label: '2x1模式' },
          { name: '2x2模式', value: '2', label: '2x2模式' },
          { name: '3x2模式', value: '3', label: '3x2模式' },
          { name: '3x3模式', value: '4', label: '3x3模式' },
          { name: '1+5模式', value: '5', label: '1+5模式' }
        ]
      };
    },
  };
</script>

<style>
    .block {
        padding: 30px 24px;
        background-color: rgb(27, 16, 16);
    }
    .grid-content {
        background-color: rgb(44, 143, 121);
        border-radius: 4px;
        min-height: 150px;
        min-width: 100px;
    }
    .grid-a-contentWidth {
        background-color: rgb(44, 143, 121);
        border-radius: 4px;
        min-height: 100px;
    }
    .grid-a-content-a-Width {
        background-color: rgb(44, 143, 121);
        border-radius: 4px;
        min-height: 220px;
    }

    .grid-one-contentheight {
        background-color: rgb(44, 143, 121);
        border-radius: 4px;
        min-height: 100%;
    }

    .el-row-two {
        margin-bottom: 80px;
        margin-top: 80px;
    }
</style>
