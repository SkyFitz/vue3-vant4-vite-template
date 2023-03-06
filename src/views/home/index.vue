<script setup lang="ts">
import {ref} from "vue"
const operate = ref(0)
const currentDate = ref(['2021', '01', '01'])
const startTime = ref('')
const endTime = ref('')
const showPicker = ref(false)
const onDateClick = (index) =>{
  const value = (index === 1 ? startTime.value : endTime.value) || '2021-12-12'
  console.log(value)
  currentDate.value = value.split('-')
  showPicker.value = true
  operate.value = index
  console.log(currentDate.value)
}
const onConfirm = ({ selectedValues }) => {
  operate.value === 1 ? startTime.value = selectedValues.join('-') : endTime.value = selectedValues.join('-')
  showPicker.value = false;
};
</script>
<template>
  <div class="home-container">
    <van-form>
      <van-field
        v-model="startTime"
        is-link
        readonly
        name="datePicker"
        label="开始时间"
        placeholder="点击选择开始时间"
        @click="onDateClick(1)"
      />
      <van-field
        v-model="endTime"
        is-link
        readonly
        name="datePicker"
        label="结束时间"
        placeholder="点击选择开始时间"
        @click="onDateClick(2)"
      />
      <van-popup v-model:show="showPicker" position="bottom">
        <van-date-picker v-model="currentDate" @confirm="onConfirm" @cancel="showPicker = false" />
      </van-popup>

    </van-form>
  </div>
</template>

