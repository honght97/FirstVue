<script setup>
import Test from './components/Test.vue';
import Header from './components/Header.vue';
import Modal from './components/Modal.vue';
</script>

<template>
  <Header/>
  <Test ref="test"/>
  <div>
    <button @click="onChange">Change me</button>
  </div>
  <div>
    <button @click="onToogleModal">Toogle Modal</button>
  </div>
  <teleport to="body">
    <base-modal 
      v-if="isShowModal"
      title="This is title app component"
        content="This is content app component"
        theme="example"
        @cancel="onToogleModal"
      >
        <template #header>
          <p>Test slot for header</p>
        </template>
        <p>Test slot for default</p>
        <template #footer>
          <p>Test slot for footer</p>
          <button type="button" @click="onToogleModal">Close</button>
          <button type="button" >Save changes</button>
        </template>
      </base-modal>
  </teleport>
</template>
<script>
  export default {
    data() {
      return {
        isShowModal: false,
      }
    },
    components: {
      baseModal: Modal,
    },
    methods: {
      onChange() {
        console.log(this.$refs.test);
       console.log(this.$refs.test.firsName);
      },
      onToogleModal() {
        this.isShowModal = !this.isShowModal;
      }
    }
  }
</script>