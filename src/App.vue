<template>
  <div class="box">
    <div class="card">
      <div class="t1">
        <el-select placeholder="请选择张数">
          <el-option label="1张" :value="1">1张</el-option>
          <el-option label="2张" :value="2">2张</el-option>
          <el-option label="3张" :value="3">3张</el-option>
          <el-option label="4张" :value="4">4张</el-option>
          <el-option label="5张" :value="5">5张</el-option>
        </el-select>
      </div>
      <div class="t2">
        <el-button type="primary" style="height: 42px; width: 125px;">提交</el-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      tickets: []
    }
  },
  mounted: function () {
    const a = ['A', 'B', 'C', 'D']
    for (let i = 0; i < 4; i++) {
      const firstChar = a[i]
      for (let j = 1; j <= 1875; j++) {
        this.tickets.push(firstChar + j)
      }
    }
    console.log(this.tickets)
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}
.box {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
  background: #f5f5f5;
  .card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 650px;
    height: 350px;
    border-radius: 8px;
    box-shadow: 0px 1px 6px 0px #e6e6e6;
    background: #ffffff;
    .t1 {
      display: flex;
      margin-top: 30px;
      width: 350px;
      height: 70px;
      flex-direction: column;
    }
    .t2 {
      display: flex;
      width: 350px;
      justify-content: space-around;
      height: 100px;
      justify-content: space-around;
      align-items: center;
    }
  }
}
</style>
