<template>
  <div class="modal" @click="onsCloseModal">
      <div class="modal-dialog">
        <div class="modal-content" :class="{'bg-purple': theme === 'example'}">
          <div class="modal-header">
            <h5 class="modal-title">
              {{title}}
            </h5>
             <slot name="header"></slot>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <p>{{content}}</p>
            <slot></slot>
          </div>
          <div class="modal-footer">
            <slot name="footer"></slot>
          </div>
      </div>
  </div>
</div>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    content: {
      type: String,
      default: "",

    },
    theme: {
      type: String,
       default: "example",
      validator(value) {
        // The value must match one of these strings
        return ['example', 'sales', 'contact'].includes(value)
      },
     
    }
  },
  methods: {
    onsCloseModal() {
      this.$emit("cancel");
    }
  },
  data() {
    return{}
  }
}
</script>
<style lang="css" scoped>
.modal-content.bg-purple {
  background-color: purple;
}
.modal {
  position: fixed;
  top:0;
  left:0;
  right: 0;
  background: rgba(0, 0, 0, .2);
  bottom: 0;
}
  .modal-dialog {
    position: relative;
    width: auto;
    margin: 1.75rem;
    pointer-events: none;
    margin-right: auto;
    margin-left: auto;
}
.modal-content {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 100%;
    color: #d00;
    pointer-events: auto;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ddd;
    border-radius: 10px;
    outline: 0;
}
.modal-header {
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: space-between;
    padding: 2rem;
    border-bottom: 1px solid #ddd;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}
.modal-body {
    position: relative;
    flex: 1 1 auto;
    padding: 2rem;
}
.modal-footer {
    display: flex;
    flex-shrink: 0;
    flex-wrap: wrap;
    align-items: center;
    justify-content: flex-end;
    padding: 2rem;
    background-color: #ccc;
    border-top: 1px solid #ddd;
    border-bottom-right-radius: 10px;
    border-bottom-left-radius: 10px;
}
</style>