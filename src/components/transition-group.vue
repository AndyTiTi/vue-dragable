<template>
    <div class="fluid container">
        <div class="form-group form-group-lg panel panel-default">
            <div class="panel-heading">
                <h3 class="panel-title">Sortable control</h3>
            </div>
            <div class="panel-body">
                <div class="checkbox">
                    <label><input type="checkbox" v-model="editable">允许拖放</label>
                </div>
                <button type="button" class="btn btn-default" @click="orderList">元素排序</button>
            </div>
        </div>

        <el-row>
            <el-col :span="12">
                <draggable class="list-group" tag="ul" v-model="list" v-bind="dragOptions" :move="onMove"
                           @start="isDragging=true" @end="isDragging=false">
                    <transition-group type="transition" :name="'flip-list'">
                        <li class="list-group-item" v-for="element in list" :key="element.order">
                            <i :class="element.fixed? 'fa fa-anchor' : 'glyphicon glyphicon-pushpin'"
                               @click=" element.fixed=! element.fixed" aria-hidden="true"></i>
                            {{element.name}}
                            <span class="badge">{{element.order}}</span>
                        </li>
                    </transition-group>
                </draggable>
                <div class="list-group">
                    <pre>{{listString}}</pre>
                </div>
            </el-col>
            <el-col :span="1" class="vertical">左右拖放</el-col>
            <el-col :span="11">
                <draggable v-model="list2" v-bind="dragOptions" :move="onMove">
                    <transition-group name="no" class="list-group" tag="ul">
                        <li class="list-group-item" v-for="element in list2" :key="element.order">
                            <i :class="element.fixed? 'fa fa-anchor' : 'glyphicon glyphicon-pushpin'"
                               @click=" element.fixed=! element.fixed" aria-hidden="true"></i>
                            {{element.name}}
                            <span class="badge">{{element.order}}</span>
                        </li>
                    </transition-group>
                </draggable>
                <div class="list-group">
                    <pre>{{list2String}}</pre>
                </div>
            </el-col>

        </el-row>


    </div>
</template>

<script>
  import draggable from "vuedraggable";

  const message = [
    "vue.draggable",
    "draggable",
    "component",
    "for",
    "vue.js 2.0",
    "based",
    "on",
    "Sortablejs"
  ];

  export default {
    name: "hello",
    components: {
      draggable
    },
    data() {
      return {
        list: message.map((name, index) => {
          return {name, order: index + 1, fixed: false};
        }),
        list2: [],
        editable: true,
        isDragging: false,
        delayedDragging: false
      };
    },
    methods: {
      orderList() {
        this.list = this.list.sort((one, two) => {
          return one.order - two.order;
        });
        this.list2 = this.list2.sort((one, two) => {
          return one.order - two.order;
        });
      },
      onMove({relatedContext, draggedContext}) {
        const relatedElement = relatedContext.element;
        const draggedElement = draggedContext.element;
        console.log(relatedElement)
        console.log(draggedElement)
        return (
          (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
        );
      }
    },
    computed: {
      dragOptions() {
        return {
          animation: 0,
          group: "description",
          disabled: !this.editable,
          ghostClass: "ghost"
        };
      },
      listString() {
        return JSON.stringify(this.list, null, 2);
      },
      list2String() {
        return JSON.stringify(this.list2, null, 2);
      }
    },
    watch: {
      isDragging(newValue) {
        if (newValue) {
          this.delayedDragging = true;
          return;
        }
        this.$nextTick(() => {
          this.delayedDragging = false;
        });
      }
    }
  };
</script>

<style>
    .flip-list-move {
        transition: transform 0.5s;
    }

    .no-move {
        transition: transform 0s;
    }

    .ghost {
        opacity: 0.5;
        background: #c8ebfb;
    }
    .vertical{
        width: 20px!important;
        margin: 220px auto 0;
        line-height: 30px;
        color: #ff6400;
        font-size: 20px;
        word-wrap: break-word;
    }
    .badge{
        background: gray;
        height: 30px;
        line-height: 30px;
        margin: 10px 20px 0 0;
        width: 30px;
        color: #fff;
        border-radius: 15px;
        display: inline-block;
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
        float: right;
    }
    .list-group {
        padding: 40px;
        margin: 10px;
        border: 1px dotted;
        box-sizing: border-box;
        background: rgba(0,0,0,0.06);
    }
    ul.list-group{
        min-height: 560px;
    }
    .list-group-item {
        overflow: hidden;
        cursor: move;
        height: 50px;
        line-height: 50px;
    }

    .list-group-item i {
        cursor: pointer;
    }
</style>
