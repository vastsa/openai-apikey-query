<script setup lang="ts">
import { ref } from 'vue';
import axios from "axios";
const result: any = ref([]);
const keys = ref('');
const baseUrl = 'https://ai.mdzx.me/';

function formatDate(today: Date) {
  let year:any = today.getFullYear();
  let month:any = today.getMonth() + 1;
  let day:any = today.getDate();
  if (month < 10) {
    month = "0" + month;
  }
  if (day < 10) {
    day = "0" + day;
  }
  return  year + "-" + month + "-" + day;
}
function select() {
  const now = new Date();
  const old: any = new Date();
  old.setDate(now.getDate() - 90);
  keys.value.split('\n').forEach((key) => {
    if (key) {
      axios.get(`${baseUrl}dashboard/billing/usage?end_date=${formatDate(now)}&start_date=${formatDate(old)}`,{
        headers: {
          'Authorization': `Bearer ${key}`
        }
      }).then((res:any)=>{
        result.value.push({
          key,
          quota:res.data.total_usage,
          status: '正常'
        })
      }).catch((err:any)=>{
        result.value.push({
          key,
          quota:err.statusCode,
          status: '异常'
        })
      })
    }
  });
}
</script>

<template>
  <div style="margin-top: 1rem">
    <div style="position: relative">
      <textarea v-model="keys" class="textarea" :rows="5" placeholder="一行一个，请输入你的APIKeys"/>
      <button @click="select" class="submit">查询</button>
    </div>
    <table v-if="result.length>0">
      <tr>
        <td>Key</td>
        <td>使用额度</td>
        <td>状态</td>
      </tr>
      <tr v-for="row in result" :key="row.key">
        <td style="width: 50%">{{ row.key }}</td>
        <td >{{ row.quota }}</td>
        <td >{{ row.status }}</td>
      </tr>
    </table>
  </div>
</template>

<style>
.textarea {
  width: 100%;
  border: none;
  background: rgba(0, 0, 0, 0.1);
  resize: vertical;
  border-radius: 16px;
  padding: 1rem
}

.submit {
  width: 100px;
  height: 2rem;
  border: none;
  right: 0;
  bottom: 0.4rem;
  position: absolute;
  border-radius: 16px 0 16px 0;
  background-image: linear-gradient(-56deg, #0773ff 5%, #797eff);
  cursor: pointer;
}

.submit:hover {
  border: #282828 1px solid;
}

table {
  border-collapse: collapse;
  width: 100%;
  max-width: 80vw;
  font-size: 16px;
  margin: 1rem auto;
  word-wrap: break-word;
  text-align: center;
  color: #333;
}

th, td {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

th {
  background-color: #f2f2f2;
  font-weight: bold;
}

tr:hover {
  background-color: #f5f5f5;
}
</style>