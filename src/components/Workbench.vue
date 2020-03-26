<template>
  <div id="work_bench">
    <div>
      <el-row>
        <el-col class="col_s18" :span="18">
          <el-row>
            <el-col class="drap_bl" :span="8">
              <!-- 左侧可拖拉组件 -->
              <draggable
                class="drap_bl drap_bl_left"
                v-model="listReft"
                v-bind="dragOptions"
                dragable="true"
                :move="onMove"
                @start="draggableStart"
                @end="draggableEnd"
              >
                <el-row class="col_p10" v-for="(i, k) in listReft" :key="k">
                  <el-col>
                    <el-card class="box-card">
                      <div class="box_top">
                        <div class="box_top_t">
                          <span>{{ i.name }}</span>
                        </div>
                        <div class="box_top_r">
                          <div class="box_top_rshow" v-show="editable">
                            <el-tooltip class="item" effect="dark" content="隐藏卡片" placement="top">
                              <span class="i_hide" @click="setEdit(i.id)">
                                <i class="el-icon-view"></i>
                              </span>
                            </el-tooltip>
                            <el-tooltip class="item" effect="dark" content="调整顺序" placement="top">
                              <span class="i_adjust">
                                <i class="el-icon-rank"></i>
                              </span>
                            </el-tooltip>
                          </div>
                          <el-dropdown trigger="click" v-show="!editable" @command="setEdit">
                            <span class="el-dropdown-link">
                              <i class="el-icon-more"></i>
                            </span>
                            <el-dropdown-menu slot="dropdown">
                              <el-dropdown-item command="adjust">调整顺序</el-dropdown-item>
                              <el-dropdown-item :command="i.id">隐藏卡片</el-dropdown-item>
                            </el-dropdown-menu>
                          </el-dropdown>
                        </div>
                      </div>
                      <div class="box_body">
                        <div></div>
                      </div>
                    </el-card>
                  </el-col>
                </el-row>
              </draggable>
            </el-col>
            <el-col class="drap_bl" :span="16">
              <!-- 中间可拖拉组件 -->
              <draggable
                class="drap_bl drap_bl_center"
                v-model="listCenter"
                v-bind="dragOptions"
                dragable="true"
                :move="onMove"
              >
                <el-row class="col_p10" v-for="(i, k) in listCenter" :key="k">
                  <el-col>
                    <el-card class="box-card">
                      <div class="box_top">
                        <div class="box_top_t">
                          <span>{{ i.name }}</span>
                        </div>
                        <div class="box_top_r">
                          <div class="box_top_rshow" v-show="editable">
                            <el-tooltip class="item" effect="dark" content="隐藏卡片" placement="top">
                              <span class="i_hide" @click="setEdit(i.id)">
                                <i class="el-icon-view"></i>
                              </span>
                            </el-tooltip>
                            <el-tooltip class="item" effect="dark" content="调整顺序" placement="top">
                              <span class="i_adjust">
                                <i class="el-icon-rank"></i>
                              </span>
                            </el-tooltip>
                          </div>
                          <el-dropdown trigger="click" v-show="!editable" @command="setEdit">
                            <span class="el-dropdown-link">
                              <i class="el-icon-more"></i>
                            </span>
                            <el-dropdown-menu slot="dropdown">
                              <el-dropdown-item command="adjust">调整顺序</el-dropdown-item>
                              <el-dropdown-item :command="i.id">隐藏卡片</el-dropdown-item>
                            </el-dropdown-menu>
                          </el-dropdown>
                        </div>
                      </div>
                      <div class="box_body">
                        <div></div>
                      </div>
                    </el-card>
                  </el-col>
                </el-row>
              </draggable>
            </el-col>
          </el-row>
        </el-col>
        <el-col class="col_s06" :span="6">
          <el-row>
            <el-col class="drap_bl">
              <!-- 右侧可拖拉组件 -->
              <draggable
                class="drap_bl drap_bl_right"
                v-model="listRight"
                v-bind="dragOptions"
                dragable="true"
                :move="onMove"
                @start="draggableStart"
                @end="draggableEnd"
              >
                <el-row class="col_p10" v-for="(i, k) in listRight" :key="k">
                  <el-col>
                    <el-card class="box-card">
                      <div class="box_top">
                        <div class="box_top_t">
                          <span>{{ i.name }}</span>
                        </div>
                        <div class="box_top_r">
                          <div class="box_top_rshow" v-show="editable">
                            <el-tooltip class="item" effect="dark" content="隐藏卡片" placement="top">
                              <span class="i_hide" @click="setEdit(i.id)">
                                <i class="el-icon-view"></i>
                              </span>
                            </el-tooltip>
                            <el-tooltip class="item" effect="dark" content="调整顺序" placement="top">
                              <span class="i_adjust">
                                <i class="el-icon-rank"></i>
                              </span>
                            </el-tooltip>
                          </div>
                          <el-dropdown trigger="click" v-show="!editable" @command="setEdit">
                            <span class="el-dropdown-link">
                              <i class="el-icon-more"></i>
                            </span>
                            <el-dropdown-menu slot="dropdown">
                              <el-dropdown-item command="adjust">调整顺序</el-dropdown-item>
                              <el-dropdown-item :command="i.id">隐藏卡片</el-dropdown-item>
                            </el-dropdown-menu>
                          </el-dropdown>
                        </div>
                      </div>
                      <div class="box_body">
                        <div></div>
                      </div>
                    </el-card>
                  </el-col>
                </el-row>
              </draggable>
            </el-col>
          </el-row>
        </el-col>
      </el-row>
      <el-row>
        <div v-show="!editable" class="box_work_set">
          <!-- 工作台 -->
          <el-card class="box-card box_work_t">
            <div class="poi" @click="setEdit('adjust')">
              <i class="el-icon-setting"></i>
              <span>工作台设置</span>
            </div>
          </el-card>
        </div>
        <div v-show="editable" style="min-height: 120px;">
          <el-row>
            <div class="work_hide_t">
              <div>
                <span>以下卡片将在工作台不显示</span>
              </div>
            </div>
            <el-col class="drap_bl work_hide_ls">
              <el-row>
                <!-- 底部 隐藏可拖拉组件 -->
                <draggable
                  class="drap_bl"
                  v-model="listHide"
                  v-bind="dragOptions"
                  dragable="true"
                  :move="onMove"
                  @start="draggableStart"
                  @end="draggableEnd"
                >
                  <el-col class="col_p10" :span="8" v-for="(i, k) in listHide" :key="k">
                    <el-card class="box-card">
                      <div class="box_top">
                        <div class="box_top_t">
                          <span>{{ i.name }}</span>
                        </div>
                        <div class="box_top_r">
                          <div class="box_top_rshow">
                            <el-tooltip class="item" effect="dark" content="显示卡片" placement="top">
                              <span class="i_hide" @click="showCard(i.id)">
                                <i class="el-icon-view"></i>
                              </span>
                            </el-tooltip>
                            <el-tooltip class="item" effect="dark" content="调整顺序" placement="top">
                              <span class="i_adjust">
                                <i class="el-icon-rank"></i>
                              </span>
                            </el-tooltip>
                          </div>
                        </div>
                      </div>
                      <div class="box_body">
                        <div></div>
                      </div>
                    </el-card>
                  </el-col>
                </draggable>
              </el-row>
            </el-col>
          </el-row>
        </div>
        <div v-show="editable" class="box_work_save">
          <div class="box_work_btn">
            <el-button type="primary" @click="drapCancel" style="border-color: #FFF;">取消</el-button>
            <el-button plain @click="drapSave">保存</el-button>
          </div>
        </div>
      </el-row>
    </div>
  </div>
</template>

<script>
// 引入组件 vue-draggable
import draggable from "vuedraggable";
import Sortable from "sortablejs";
import init from "./init.json";
import $ from "jquery";
export default {
  name: "work_bench",
  data() {
    return {
      ///////////////////////////////
      /// 拖拽
      ///////////////////////////////
      editable: false,
      isDragging: false, // 是否拖动
      delayedDragging: false,
      dragLists: [], // 全部数据
      dragListsBefore: [], // 取消前数据
      HeightBefore: {},
      listReft: [], // 左边数据
      listCenter: [], // 中间数据
      listRight: [], // 右边数据
      listHide: [] // 隐藏数据
      ///////////////////////////////
    };
  },
  components: {
    draggable,
    Sortable
  },
  computed: {
    dragOptions() {
      return {
        animation: 0, // 动画时间
        group: "description", // 分组拖动
        disabled: !this.editable, // 是否拖动
        ghostClass: "ghost" // 拖动样式
      };
    }
  },
  methods: {
    /// 拖动开始事件
    draggableStart() {
      this.isDragging = true;
    },
    /// 拖动结束事件
    draggableEnd() {
      this.isDragging = false;
    },
    /// 初始化 卡片数据
    initCardData() {
      let that = this;
      this.dragLists = init.res;
      this.loadCardData(init.res);
    },
    /// 加载 卡片数据
    loadCardData(e) {
      this.listReft = e.filter(i => {
        return i.pos == "l";
      });
      this.listCenter = e.filter(i => {
        return i.pos == "c";
      });
      this.listRight = e.filter(i => {
        return i.pos == "r";
      });
      this.listHide = e.filter(i => {
        return i.pos == "h";
      });
    },
    /// 隐藏卡片
    setEdit(e) {
      if (e == "adjust") {
        this.dragListsBefore = JSON.parse(JSON.stringify(this.dragLists));
        console.log(this.dragLists, "dragLists");
        this.editable = true;
      } else {
        let select = this.dragLists.filter(d => {
          return d.id == e;
        });
        if (select[0].pos == "l") {
          let index = this.listReft.findIndex(d => {
            return d.id == e;
          });
          this.listReft.splice(index, 1);
          this.listHide.push(select[0]);
        } else if (select[0].pos == "c") {
          let index = this.listCenter.findIndex(d => {
            return d.id == e;
          });
          this.listCenter.splice(index, 1);
          this.listHide.push(select[0]);
        } else if (select[0].pos == "r") {
          let index = this.listRight.findIndex(d => {
            return d.id == e;
          });
          this.listRight.splice(index, 1);
          this.listHide.push(select[0]);
        }
        let h = 200;
        $("#work_bench .drap_bl_left").css("min-height", h);
        $("#work_bench .drap_bl_center").css("min-height", h);
        $("#work_bench .drap_bl_right").css("min-height", h);
        setTimeout(() => {
          this.filterHeightBlock();
        }, 100);
      }
    },
    /// 显示卡片
    showCard(e) {
      let select = this.dragLists.filter(d => {
        return d.id == e;
      });
      let index = this.listHide.findIndex(d => {
        return d.id == e;
      });
      this.listHide.splice(index, 1);
      this.listCenter.push(select[0]);
    },
    /// 工作台 取消事件
    drapCancel() {
      this.dragLists = JSON.parse(JSON.stringify(this.dragListsBefore));
      this.loadCardData(this.dragLists);
      this.dragListsBefore = [];
      $("#work_bench .drap_bl_left").css("min-height", this.HeightBefore.l);
      $("#work_bench .drap_bl_center").css("min-height", this.HeightBefore.c);
      $("#work_bench .drap_bl_right").css("min-height", this.HeightBefore.r);
      this.HeightBefore = {};
      this.editable = false;
    },
    /// 工作台 保存事件
    drapSave() {
      let saveList = []
        .concat(this.listReft)
        .concat(this.listCenter)
        .concat(this.listRight)
        .concat(this.listHide);
      let saveData = []; // 保存的数据
      this.editable = false;
    },
    /// 移动事件
    onMove({ relatedContext, draggedContext }) {
      let h = 200;
      $("#work_bench .drap_bl_left").css("min-height", h);
      $("#work_bench .drap_bl_center").css("min-height", h);
      $("#work_bench .drap_bl_right").css("min-height", h);
      setTimeout(() => {
        this.filterHeightBlock();
      }, 50);
      const relatedElement = relatedContext.element;
      const draggedElement = draggedContext.element;
      return (
        (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
      );
    },
    /////////////////////////////
    /// filter 过滤块
    /////////////////////////////
    /// 过滤高度数字 (px)
    filterHeightPX(e) {
      if (typeof e == "string") {
        let es = e.replace("px", "");
        let re = Number(es);
        if (!isNaN(re)) {
          return re;
        }
      }
      return e;
    },
    /// 自适应页面布局事件
    filterHeightBlock(e) {
      let lot = $("#work_bench .drap_bl_left").offset().top || 0;
      let cot = $("#work_bench .drap_bl_center").offset().top || 0;
      let rot = $("#work_bench .drap_bl_right").offset().top || 0;
      let lh = $("#work_bench .drap_bl_left").css("height") || 0;
      let ch = $("#work_bench .drap_bl_center").css("height") || 0;
      let rh = $("#work_bench .drap_bl_right").css("height") || 0;
      lh = this.filterHeightPX(lh);
      ch = this.filterHeightPX(ch);
      rh = this.filterHeightPX(rh);
      this.MathAdaptiveHeight({ lot, cot, rot, lh, ch, rh, status: e });
    },
    /// 自适应页面布局
    MathAdaptiveHeight(e) {
      let ls = e.lot + e.lh;
      let cs = e.cot + e.ch;
      let rs = e.rot + e.rh;
      let res = ls > cs ? (ls > rs ? ls : rs) : cs > rs ? cs : rs;
      if (e.status) {
        this.HeightBefore.l = res - e.lot;
        this.HeightBefore.c = res - e.cot;
        this.HeightBefore.r = res - e.rot;
      }
      $("#work_bench .drap_bl_left").css("min-height", res - e.lot);
      $("#work_bench .drap_bl_center").css("min-height", res - e.cot);
      $("#work_bench .drap_bl_right").css("min-height", res - e.rot);
    }
  },
  mounted() {
    this.initCardData();
  },
  watch: {
    /// 是否拖动
    isDragging(n) {
      if (n) {
        this.delayedDragging = true;
        return;
      }
      this.$nextTick(() => {
        this.delayedDragging = false;
      });
    },
    editable() {
      if (this.editable == true) {
        this.filterHeightBlock(true);
      }
    },
    dragLists: {
      handler() {
        setTimeout(() => {
          this.filterHeightBlock();
        }, 50);
      },
      deep: true
    },
    listReft(n) {
      console.log(n, "---listReft");
      this.listReft.forEach(e => {
        e.pos = "l";
      });
    },
    listCenter(n) {
      console.log(n, "---listCenter");
      this.listCenter.forEach(e => {
        e.pos = "c";
      });
    },
    listRight(n) {
      console.log(n, "---listRight");
      this.listRight.forEach(e => {
        e.pos = "r";
      });
    },
    listHide(n) {
      console.log(n, "---listHide");
      this.listHide.forEach(e => {
        e.pos = "h";
      });
    }
  }
};
</script>

<style>
#work_bench {
  font-size: 14px;
  min-width: 1366px;
}
#work_bench .col_s18 {
  padding: 6px 0px 6px 6px;
}
#work_bench .col_s06 {
  padding: 6px 0px 6px 0px;
}
#work_bench .col_p10 {
  padding: 6px;
}
#work_bench .box_body > div {
  height: 120px;
  width: 200px;
}
/* 卡片 头部 */
#work_bench .box-card .box_top {
  display: flex;
  justify-content: space-between;
  cursor: pointer;
}
#work_bench .box-card .box_top .box_top_t {
  display: inline-block;
  font-size: 16px;
}
#work_bench .box-card .box_top .box_top_r {
  display: inline-block;
  width: 60px;
  text-align: right;
}
#work_bench .box-card .box_top .box_top_r .box_top_rshow i {
  padding: 4px;
  color: #fff;
  background-color: rgb(24, 155, 228);
}
#work_bench .box_top .r_job_enter i {
  font-size: 20px;
  color: #409eff;
  padding: 0px 4px;
}
#work_bench .r_job_enter,
#work_bench .r_job_mg {
  height: 30px;
  line-height: 30px;
}
#work_bench .box_top .r_job_enter span {
  font-size: 20px;
}
#work_bench .box_top .r_job_mg span {
  font-size: 16px;
  display: inline-block;
  border-left: 1px solid #c0c4cc;
  text-align: right;
  width: 60px;
}
/* 模块 中间 */
#work_bench .box_center {
  padding-top: 12px;
  padding-bottom: 8px;
}
#work_bench .box_center .box_card_ul {
  width: 33%;
  display: inline-block;
  text-align: center;
  line-height: 150%;
  padding: 8px 0px;
}
/* 模块 范围 */
#work_bench .drap_bl_left {
  min-height: 200px;
}
#work_bench .drap_bl_center {
  min-height: 200px;
}
#work_bench .drap_bl_right {
  min-height: 200px;
}
#work_bench .drap_bl {
  min-height: 200px;
}
/* 模块 工作台 */
#work_bench .box_work_set {
  height: 60px;
  padding-bottom: 60px;
  display: flex;
  justify-content: center;
}
#work_bench .box_work_set .box_work_t {
  width: 200px;
  text-align: center;
  font-size: 16px;
  color: #c0c4cc;
}
#work_bench .i_hide:hover {
  cursor: pointer;
}
#work_bench .i_adjust:hover {
  cursor: move;
}
#work_bench .poi:hover {
  color: #409eff;
  cursor: pointer;
}
#work_bench .box_work_save {
  display: flex;
  justify-content: center;
  position: fixed;
  width: 100%;
  bottom: 0;
  height: 60px;
  line-height: 60px;
  z-index: 999;
  background-color: rgb(24, 155, 228);
}
#work_bench .box_work_save .box_work_btn {
  width: 400px;
  text-align: center;
  font-size: 16px;
}
#work_bench .work_hide_t {
  padding: 20px;
  font-size: 20px;
}
#work_bench .work_hide_t div {
  padding-bottom: 20px;
  border-bottom: 1px solid #dcdfe6;
}
#work_bench .work_hide_t span {
  padding-left: 20px;
  border-left: 5px solid #409eff;
}
/* 模块 隐藏 */
#work_bench .work_hide_ls {
  margin-bottom: 60px;
  padding: 6px;
}
#work_bench .box_bottom {
  border-top: 1px solid #ebeef5;
  padding-top: 10px;
  display: flex;
  justify-self: center;
  justify-content: space-between;
}
#work_bench .box_bottom div {
  display: inline-block;
  height: 36px;
  line-height: 36px;
  padding: 5px;
}
#work_bench .box_bottom .box_bl {
  min-width: 60px;
}
#work_bench .box_bottom .box_br {
  min-width: 36px;
}
#work_bench .box_bottom .box_bottomBtn {
  padding: 0px;
  height: 36px;
  width: 36px;
  margin: 0px;
  border-radius: 50%;
}
</style>