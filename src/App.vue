<template>
  <!-- <HelloWorld msg="Welcome To Neko Frontend" /> -->

  <div class="common-layout">
    <el-container>
      <!-- 头部 -->
      <el-header>Welcome to Neko Frontend</el-header>

      <el-container>
        <!-- 菜单 -->
        <el-aside width="200px">
          <el-row class="tac">
            <el-col>
              <h5 class="mb-2">Default colors</h5>
              <el-menu
                default-active="2"
                class="el-menu-vertical-demo"
                @open="handleOpen"
                @close="handleClose"
              >
                <el-sub-menu index="1">
                  <template #title>
                    <el-icon><location /></el-icon>
                    <span>Navigator One</span>
                  </template>
                  <el-menu-item-group title="Group One">
                    <el-menu-item index="1-1">item one</el-menu-item>
                    <el-menu-item index="1-2">item two</el-menu-item>
                  </el-menu-item-group>
                  <el-menu-item-group title="Group Two">
                    <el-menu-item index="1-3">item three</el-menu-item>
                  </el-menu-item-group>
                  <el-sub-menu index="1-4">
                    <template #title>item four</template>
                    <el-menu-item index="1-4-1">item one</el-menu-item>
                  </el-sub-menu>
                </el-sub-menu>
                <el-menu-item index="2">
                  <el-icon><icon-menu /></el-icon>
                  <span>Navigator Two</span>
                </el-menu-item>
                <el-menu-item index="3" disabled>
                  <el-icon><document /></el-icon>
                  <span>Navigator Three</span>
                </el-menu-item>
                <el-menu-item index="4">
                  <el-icon><setting /></el-icon>
                  <span>Navigator Four</span>
                </el-menu-item>
              </el-menu>
            </el-col>
          </el-row>
        </el-aside>

        <el-main>
          <!-- 页面 -->

          <!-- 查询框 -->
          <div class="query-box">
            <el-input
              v-model="input1"
              class="w-50 m-2"
              size="large"
              placeholder="请输入需要查询的姓名"
              :suffix-icon="Search"
            />
            <el-button type="primary">查询</el-button>
            <el-button type="primary" @click="handleAdd">新增</el-button>
          </div>

          <!-- 表单 -->
          <div class="table-box">
            <el-table
            border
            ref="multipleSelection" 
            @selection-change="handleSelectionChange"
            :data="tableData" 
            style="width: 100%">
              <el-table-column type="selection" width="55"></el-table-column>
              <el-table-column fixed prop="date" label="Date" width="150" />
              <el-table-column prop="name" label="Name" width="120" />
              <el-table-column prop="state" label="State" width="120" />
              <el-table-column prop="city" label="City" width="120" />
              <el-table-column prop="address" label="Address" width="600" />
              <el-table-column prop="zip" label="Zip" width="120" />
              <el-table-column fixed="right" label="操作" width="120">
                <template #default>
                  <el-button
                    link
                    type="primary"
                    size="small"
                    @click="handleClick"
                    >编辑</el-button
                  >
                  <el-button link type="danger" size="small">删除</el-button>
                </template>
              </el-table-column>
            </el-table>


          </div>

          <!-- Dialog -->
          <el-dialog v-model="dialogFormVisible" title="用户信息">
            <el-form :model="tableForm">
              <el-form-item label="请输入姓名" :label-width="100">
                <el-input v-model="tableForm.name" autocomplete="off" />
              </el-form-item>
              <el-form-item label="请输入年龄" :label-width="100">
                <el-input v-model="tableForm.age" autocomplete="off" />
              </el-form-item>
              <el-form-item label="请输入部门" :label-width="100">
                <el-input v-model="tableForm.apartment" autocomplete="off" />
              </el-form-item>
              <el-form-item label="请输入权限" :label-width="100">
                <el-input v-model="tableForm.permission" autocomplete="off" />
              </el-form-item>
      
            </el-form>
            <template #footer>
              <span class="dialog-footer">
                <el-button @click="dialogFormVisible = false">Cancel</el-button>
                <el-button type="primary" @click="dialogFormVisible = false">
                  Confirm
                </el-button>
              </span>
            </template>
          </el-dialog>

          <!-- 页面 -->
        </el-main>
      </el-container>
    </el-container>


  </div>
</template>

<style scoped>
/* 表单 */
.table-box {
  width: 80%;
  position: absolute;
  top: 20%;
  left: 20%;
  transform: translateX(-30%, -30%);
}

/* 输入框 */
.query-box {
  width: 300px;
  position: absolute;
  left: 20%;
}
</style>

<script lang="ts" setup>
// 菜单样式引入
import {
  Delete,
  Document,
  Menu as IconMenu,
  Location,
  Setting,
  Search,
} from "@element-plus/icons-vue";
const handleOpen = (key: string, keyPath: string[]) => {
  console.log(key, keyPath);
};
const handleClose = (key: string, keyPath: string[]) => {
  console.log(key, keyPath);
};

// 引入ref
import { ref } from 'vue';

//输入框
let input1 = ref('') 
// 选择项
let multipleSelection = ref([])
// 数据
let tableData = ref([
  {
    date: "2016-05-03",
    name: "Tom",
    state: "California",
    city: "Los Angeles",
    address: "No. 189, Grove St, Los Angeles",
    zip: "CA 90036",
    tag: "Home",
  },
  {
    date: "2016-05-02",
    name: "Tom",
    state: "California",
    city: "Los Angeles",
    address: "No. 189, Grove St, Los Angeles",
    zip: "CA 90036",
    tag: "Office",
  },
  {
    date: "2016-05-04",
    name: "Tom",
    state: "California",
    city: "Los Angeles",
    address: "No. 189, Grove St, Los Angeles",
    zip: "CA 90036",
    tag: "Home",
  },
  {
    date: "2016-05-01",
    name: "Tom",
    state: "California",
    city: "Los Angeles",
    address: "No. 189, Grove St, Los Angeles",
    zip: "CA 90036",
    tag: "Office",
  },
]);
let dialogFormVisible = ref(false)

let tableForm = ref ({
  name:'桜桃喵',
  age: 20,
  apartment: 1,
  permission: 0,
})

// 方法
const handleClick = () => {
  console.log("click");
};

// 新增
const handleAdd = () => {
  dialogFormVisible.value = true

}

// 多选
const handleSelectionChange = (val) => {
  multipleSelection.value = val
  console.log(val);
}
</script>
