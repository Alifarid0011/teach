<template>
  <div class="container">
    <form>
      <h1>
        component A
      </h1>

      <div class="mb-3">
        <label for="name" class="form-label">name</label>
        <input type="text" class="form-control" id="name" v-model="name" placeholder="نام">
      </div>
      <div class="mb-3">
        <label for="family" class="form-label">family</label>
        <input type="text" class="form-control" id="family" v-model="family" placeholder="نام خانوادگي">
      </div>
    </form>
    <button class="btn btn-primary" @click.prevent="sendData()">صفحه ي بعد</button>
  </div>
</template>

<script>
import {reactive, toRefs} from '@vue/reactivity';

export default {
  name: 'A',
  setup(props, context) {
    const form = reactive({
      name: '',
      family: ''
    });

    function sendData() {
      let formData = {
        name: form.name,
        family: form.family,
        goToPage: 2
      };
      context.emit('childData', formData);
    }

    return {
      ...toRefs(form),
      sendData
    };
  }
};
</script>

<style scoped>
h1{
  background: cornflowerblue;
}
</style>