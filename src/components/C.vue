<template>
  <div>
    <div class="container">
      <h1>
        Component C
      </h1>
      <div class="mb-3">
        <label for="explanations" class="form-label">explanations</label>
        <textarea class="form-control" id="explanations" v-model="explanations" placeholder="توضيحات"/>
      </div>
    </div>
    <button type="submit" class="btn btn-success" @click.prevent="sendData()">نمايش داده ها</button>
    <button type="submit" class="btn btn-danger" @click.prevent="sendBack()">صفحه ي قبل</button>
  </div>

</template>

<script>
import {reactive, toRefs} from '@vue/reactivity';

export default {
  name: 'C',
  setup(props, context) {
    const form = reactive({
      explanations:''
    });
    function sendBack() {
      let formData = {
        goToPage: 'Back'
      };
      context.emit('childData', formData);
    }

    function sendData() {
      let formData = {
        explanations: form.explanations,
        goToPage: 'Send'
      };
      context.emit('childData', formData);
    }

    return {
      ...toRefs(form),
      sendData,
      sendBack
    };
  }
};
</script>

<style scoped>
h1{
  background: #c8aaf3;
}
</style>