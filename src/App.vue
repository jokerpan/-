<template>
  <div>
    <el-row :gutter="21">
      <el-col :span="9"><div class="grid-content bg-purple">
        <el-table
          ref="saleTable"
          :data="saleTable"
          highlight-current-row
          @current-change="handleSaleCurrent">
          </el-table-column>
          <el-table-column
            property="name"
            label="货物">
          </el-table-column>
          <el-table-column
            property="price"
            label="价格">
          </el-table-column>
        </el-table>
      </div></el-col>
      <el-col :span="6"><div class="grid-content bg-purple">
          <div style="width: 100%;text-align: center;">
            <el-button type="primary" class="myBtn" @click="buy">购买</el-button><br>
            <el-button type="primary" class="myBtn" @click="sale">卖出</el-button>
          </div>
      </div></el-col>
      <el-col :span="9"><div class="grid-content bg-purple">
        <el-table
          ref="myTable"
          :data="myTable"
          highlight-current-row
          @current-change="handleMyCurrent">
          </el-table-column>
          <el-table-column
            property="name"
            label="货物">
          </el-table-column>
          <el-table-column
            property="num"
            label="数量">
          </el-table-column>
          <el-table-column
            property="price"
            label="价格">
          </el-table-column>
        </el-table>
      </div></el-col>
    </el-row>
    <el-dialog :title="title" :visible.sync="dialogFormVisible">
      <el-form>
        <el-form-item :label="label">
          <el-input-number v-model="num" @change="handleChange" :min="0" :max="max"></el-input-number>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>

  
  </div>
</template>

<script>
export default {
  data() {
    const total = [
      {
        id: 1,
        name: '盗版VCD，游戏',
        price: 20
      },
      {
        id: 2,
        name: '假白酒（剧毒）',
        price: 2000
      },
      {
        id: 3,
        name: '《上海小宝贝》（禁书）',
        price: 7500
      },
      {
        id: 4,
        name: '进口玩具',
        price: 300
      },
      {
        id: 5,
        name: '水货手机',
        price: 900
      },
      {
        id: 6,
        name: '伪劣化妆品',
        price: 200
      },
      {
        id: 7,
        name: '走私汽车',
        price: 20000
      }
    ];
    return {
      saleTable: total,
      myTable: total,
      day: 1,
      useSpace: 0,//使用空间
      totalSpace: 100,//总空间
      saleCurrent: null,
      myCurrent: null,
      cash: 2000,
      save: 0,
      debt: 4500,
      dialogFormVisible: false,
      title: '',
      max: 0,
      num: 0,
      label: ''
    }
  },
  methods: {
    initData() {

    },
    handleSaleCurrent(val) {
      this.saleCurrent =  val;
    },
    handleMyCurrent(val) {
      this.myCurrent = val;
    },
    buy() {
      if (this.saleCurrent) {
        this.dialogFormVisible = true;
        this.title = `购买`;
        let x = this.totalSpace-this.useSpace;
        let y = Math.floor(this.cash/this.saleCurrent.price);
        this.max = (x>y) ? y : x;
        this.num = this.max;
        this.label = this.saleCurrent.name;
      }
    },
    sale() {
      if (this.myCurrent) {
        this.dialogFormVisible = true;
        this.title = `出售`;
        this.max = this.myCurrent.num;
        this.num = this.max;
        this.label = this.myCurrent.name;
      }
    }
  },
  created() {

  }
}
</script>
<style scope>
  .myBtn{
    margin-bottom: 20px;
  }
</style>