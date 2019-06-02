<template>
    <div>
        <el-row class="dynamic" style="margin-bottom: 100px;">
            <transition-group appear>
                <component :is="item.com" v-for="(item,i) in Components" :key="item.name"
                           @click.native="del(i)"></component>
            </transition-group>
            <el-table
                    :data="Components"
                    highlight-current-row
                    style="width: 96%;border-top: 1px dashed gray;margin: 0 auto;"
                    @selection-change="handleSelectionChange">
                <el-table-column
                        type="selection"
                        width="55px">
                </el-table-column>
                <el-table-column
                        prop="comId"
                        label="组件ID"
                        width="100">
                </el-table-column>
                <el-table-column
                        prop="name"
                        label="组件名称" width="100">
                </el-table-column>
                <el-table-column label="操作">
                    <template slot-scope="scope">
                        <el-button
                                size="mini"
                                :disabled="scope.$index===0"
                                @click="moveUp(scope.$index,scope.row)"><i class="el-icon-arrow-up"></i></el-button>
                        <el-button
                                size="mini"
                                :disabled="scope.$index===(Components.length-1)"
                                @click="moveDown(scope.$index,scope.row)"><i class="el-icon-arrow-down"></i></el-button>
                        <el-button type="info" size="mini" round v-if="scope.$index===0">默认</el-button>
                    </template>

                </el-table-column>
            </el-table>
        </el-row>
        <hr>
        <el-row style="margin: 100px 0;">
            <el-col :span="12">
                <draggable v-model="colors" @update="datadragEnd">
                    <transition-group>
                        <div v-for="element in colors" :key="element.text" class="drag-item">
                            {{element.text}}
                        </div>
                    </transition-group>
                </draggable>
            </el-col>
            <el-col :span="12">
                <p v-for="item in colors" :key="item.text">
                    {{item}}
                </p>
            </el-col>
        </el-row>
        <hr>
        <el-row>
            <dynamic-layout/>
        </el-row>
        <hr>
        <el-row style="margin: 100px 0;">
            <trans-group/>
            <p>{{currentView}}</p>

            <button @click="changeView('A')">切换到A</button>

            <button @click="changeView('B')">切换到B</button>

            <button @click="changeView('C')">切换到C</button>
        </el-row>
    </div>
</template>

<script>
  import draggable from 'vuedraggable'
  import A from './A'
  import B from './B'
  import C from './C'
  import D from './D'
  import E from './E'
  import transGroup from './transition-group'
  import dynamicLayout from './dynamic-layout'

  export default {
    data() {
      return {
        sort: [2, 3, 1, 4, 5],
        Components: [{
          comId: '1',
          name: 'A',
          com: A
        }, {
          comId: '2',
          name: 'B',
          com: B
        }, {
          comId: '3',
          name: 'C',
          com: C
        }, {
          comId: '4',
          name: 'D',
          com: D
        }, {
          comId: '5',
          name: 'E',
          com: E
        }],
        currentView: 'comA',
        msg: "这是测试组件",
        colors: [
          {
            text: "Aquamarine",
          },
          {
            text: "Hotpink",
          },
          {
            text: "Gold",
          },
          {
            text: "Crimson",
          }
        ],
        multipleSelection: [],
      }
    },
    components: {
      A, B, C, D, E,
      transGroup,
      dynamicLayout,
      draggable
    },
    methods: {
      //选择复选框数据
      handleSelectionChange(val) {
        this.multipleSelection = val;
      },
      //上移
      moveUp(index, row) {
        var that = this;
        // console.log('上移', index, row);
        if (index > 0) {
          let upDate = that.Components[index - 1];
          that.Components.splice(index - 1, 1);
          that.Components.splice(index, 0, upDate);
        } else {
          alert('已经是第一条，不可上移');
        }
      },

      //下移
      moveDown(index, row) {
        var that = this;
        // console.log('下移', index, row);
        if ((index + 1) === that.Components.length) {
          alert('已经是最后一条，不可下移');
        } else {
          console.log(index);
          let downDate = that.Components[index + 1];
          that.Components.splice(index + 1, 1);
          that.Components.splice(index, 0, downDate);
        }
      },
      changeView: function (data) {
        this.currentView = data//动态地改变currentView的值就可以动态挂载组件了。
      },
      datadragEnd(evt) {
        evt.preventDefault();
        console.log('拖动前的索引 :' + evt.oldIndex)
        console.log('拖动后的索引 :' + evt.newIndex)
      },
      del: function (index) {
        this.Components.splice(index, 1)
      },
      sortComponents() {
        this.Components = this.sort.map(sItem => {
          return this.Components.filter(item => {
            return item.comId == sItem
          })[0]
        })
      }
    },
    mounted() {
      this.sortComponents();
      //为了防止火狐浏览器拖拽的时候以新标签打开，此代码真实有效
      document.body.ondrop = function (event) {
        event.preventDefault();
        event.stopPropagation();
      }
    },
    watch: {
      Components(newName, oldName) {
        this.sort = []
        newName.forEach((i, k) => {
          this.sort.push(i.comId)
        })
        console.log(this.sort)
      }
    }
  }
</script>

<style>
    .dynamic .grid-content {
        border-radius: 4px;
        min-height: 36px;
        background: green;
    }
    li {
        list-style: none;
        border: 1px dashed #999999;
        margin: 5px;
        line-height: 35px;
        padding-left: 5px;
        font-size: 12px;
        width: 100%;
    }

    li:hover {
        background-color: hotpink;
        transition: all 0.8s ease;
    }

    .v-enter, .v-leave-to {
        opacity: 0;
        transform: translateY(80px);
    }

    .v-enter-active,
    .v-leave-active {
        transition: all 0.6s ease;
    }

    .drag-item {
        width: 200px;
        height: 50px;
        line-height: 50px;
        margin: auto;
        position: relative;
        background: #ddd;
        margin-top: 20px;
    }
</style>
