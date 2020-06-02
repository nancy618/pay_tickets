<template>
  <div class="box" v-loading="loading">
    <div class="card">
      <div class="t1">
        <el-select placeholder="请选择张数" v-model="payNumber">
          <el-option label="1张" :value="1">1张</el-option>
          <el-option label="2张" :value="2">2张</el-option>
          <el-option label="3张" :value="3">3张</el-option>
          <el-option label="4张" :value="4">4张</el-option>
          <el-option label="5张" :value="5">5张</el-option>
        </el-select>
      </div>
      <div>
        <span class="item" v-for="(item, index) of paidArray" :key="index">{{item}}</span>
      </div>
      <div class="t2">
        <el-button type="primary" style="height: 42px; width: 125px;" @click="pay">提交</el-button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
const host = 'http://localhost:8888'
export default {
  data: function () {
    return {
      tickets: [],
      loading: true,
      payNumber: undefined,
      paidArray: []
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
    axios.get(`${host}/api/getPaidTickets`)
      .then(res => {
        console.log(res)
        let arr = []
        if (res.data.data) {
          arr = res.data.data.split(',')
        }
        for (let i = 0; i < arr.length; i++) {
          this.tickets.splice(this.tickets.indexOf(arr[i]), 1)
        }
        this.loading = false
        console.log(this.tickets)
      })
    console.log(this.tickets)
  },
  methods: {
    pay: function () {
      this.paidArray = []

      if (!this.payNumber) {
        this.$message({ type: 'error', message: '请选择至少一张' })
        return
      }
      console.log(this.payNumber) // 2
      for (let i = 0; i < this.payNumber; i++) {
        const index = Math.floor(Math.random() * this.tickets.length)
        this.paidArray.push(this.tickets[index])
        this.tickets.splice(index, 1)
      }
      this.loading = true
      axios.get(`${host}/api/setPaidTickets?paidStr=${this.paidArray.join(',')}`)
        .then(res => {
          this.loading = false
          this.$message({ type: 'success', message: '购票成功' })
        })
    }
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
  background: url(/images/bg.jpg) center no-repeat;
  background-size: cover;
  .card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 450px;
    height: 300px;
    border-radius: 8px;
    box-shadow: 0px 1px 6px 0px rgba(0, 0, 0, .1);
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
  .item {
    margin: 6px;
    color: #004eaf;
  }
}
</style>
