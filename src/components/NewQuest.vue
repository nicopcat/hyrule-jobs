<template>
  <div>
    <div class="container">
      <header>
        <div class="text-add">新  增</div>
        <div>
      <MyButton text="X" :size="12"  class="close" @click="closeModal" myPadding="4px 6px" />
         </div>
      </header>
      <div class="content">
        <label for="">标题</label>
        <input type="text" v-model="title">
        <label for="" >地点</label>
        <input type="text" v-model="location">
        <label for="">报酬</label>
        <input type="number" v-model="salary">
        <label for="">任务详情</label>
        <textarea name="" id="" cols="30" rows="10"  v-model="content"></textarea>
        <MyButton text="发 送" :size="14"  @click="addQuest" myPadding="6px"/>
        <!-- <button @click="addQuest">发 送</button> -->
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive , toRefs} from 'vue'
import { v4 as uuidv4 } from 'uuid';
import MyButton from './MyButton.vue'

export default defineComponent({
  components: {
    MyButton
  },
  emits: ['close-modal', 'add-quest'],
  setup (props, ctx) {
    const closeModal = () => {
      ctx.emit('close-modal');
    }

    const newQuest = reactive({
      title: undefined,
      location: undefined,
      id: uuidv4(),
      salary: undefined,
      content: undefined
    })

    

    const addQuest = () => {
      ctx.emit('add-quest', newQuest);
      closeModal();
    }

    return { closeModal, addQuest, ...toRefs(newQuest)}
  }
})
</script>

<style lang="less" scoped>
.container{
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 800px;
  height:600px;
  background-color: #ffffff;
  border-radius: 8px;
  border: 6px solid bisque;
  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 40px;
    background-color: bisque;
    div{
      margin:0  0 0 10px;
      .text-add{
        font-weight: bold;
      }
      .close{
        text-align: center;
        // width: 30px;
        // height: 30px;
      //  background-color: #fff;
    }
    }
   
  }

  .content {
  margin: 30px 60px;
  display: flex;
  flex-direction: column;
  gap: 10px; // 控制 input 和 label 之间的间距
  label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px; // 控制 label 和 input 的间距
  }
  input[type="text"],input[type="number"],textarea {
    min-height: 25px;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 3px;
    &:focus {
      outline: none;
      border-color: #007bff;
      box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
    }
  }
}
}
</style>