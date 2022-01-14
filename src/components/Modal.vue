
<!-- template for the modal component -->
<template>
    <ShowModal @show-modal="showModal"/>
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
              <h3>Login</h3>
          </div>

          <div class="modal-body">
            <slot name="body">
              Para confirmar o seu pedido, é necessário fazer o login.
            </slot>
          </div>

          <div id = "container-buttons"> 
              <button class = "modal-button" id = "login">Entrar</button>
          </div>

          <!-- <div class="modal-footer">
            <slot name="footer">
              <button class="modal-default-button" @click="$emit('close')">
                OK
              </button>
            </slot>
          </div> -->
        </div>
      </div>
    </div>
</template>

<script>

import ShowModal from './ShowModal.vue'

export default{
    nome: 'Modal',
    components: {
        ShowModal
    },
    data(){
        return{
            showModal: false
        }
    },
    methods:{
        showModal(){
            this.ShowModal = true;
        }
    }
}

</script>

<style scoped>

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: rgb(132, 181, 28, 1);
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  display: block;
  margin-top: 1rem;
}

#login{
   background-color: #4C2D51; 
   color: #fff;
   font-weight: bold;
   border: 2px solid #4C2D51;
   padding: 10px;
   font-size: 12px;
   margin: 0 auto;
   cursor: pointer;
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}


</style>

