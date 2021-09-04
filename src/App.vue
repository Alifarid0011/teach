<template>
  <div>
    <keep-alive>
      <component :is="nameOfComponent" @childData="childData"></component>
    </keep-alive>
  </div>
</template>

<script>
import A from '@/components/A.vue';
import B from '@/components/B.vue';
import C from '@/components/C.vue';
import {reactive, ref, toRefs} from '@vue/reactivity';

export default {
  name: 'App',
  setup() {
    const form = reactive({
      name: '',
      family: '',
      address: '',
      email: ''
    });
    const nameOfComponent = ref('A');

    function childData(data) {
      switch (data.goToPage) {
        case 'Back':
          if (nameOfComponent.value === 'B')
            nameOfComponent.value = 'A';
          else if (nameOfComponent.value === 'C')
            nameOfComponent.value = 'B';
          break;
        case 2:
          nameOfComponent.value = 'B';
          form.name = data.name;
          form.family = data.family;
          break;
        case 3:
          nameOfComponent.value = 'C';
          form.address = data.address;
          form.email = data.email;
          break;
        case 'Send':
          form.explanations = data.explanations;
          alert(`
     نام :
     ${form.name}
     نام خانوادگي :
      ${form.family}
ايميل :
     ${form.email}
     آدرس :
     ${form.address}
توضيحات :
     ${form.explanations}
    `
          );
          break;
      }
      console.log(form);
    }

    return {
      nameOfComponent,
      childData,
      ...toRefs(form)
    };
  },
  components: {
    A, B, C
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
