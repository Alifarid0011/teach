<template>
  <div class="container" >
    <h1>
      Component B
    </h1>
    <div class="mb-3" >
      <label for="address" class="form-label">address</label>
      <input type="text" class="form-control" id="address" v-model="address" placeholder="آدرس محل سكونت">
    </div>
    <div class="mb-3" >
      <label for="email" class="form-label">email</label>
      <input type="email" class="form-control" id="email" v-model="email" placeholder="ايميل" >
    </div>
    <button type="submit" class="btn btn-primary" @click.prevent="sendData()">صفحه ي بعد</button>
    <button type="submit" class="btn btn-danger" @click.prevent="sendBack()">صفحه ي قبل</button>
  </div>
</template>

<script>
import {reactive, toRefs} from '@vue/reactivity';

export default {
  name: 'B',
  setup(props, context) {
    const form = reactive({
      address: '',
      email: ''
    });
    function sendBack(){
      let formData = {
        goToPage: 'Back'
      };
      context.emit('childData', formData);
    }
    function sendData() {
      let formData = {
        address: form.address,
        email: form.email,
        goToPage: 3
      };
      context.emit('childData', formData);
    }
    return{
      ...toRefs(form),
      sendData,
      sendBack
    }
    }

};
</script>

<style scoped>
h1{
  background: #7fedb4;
}
</style>