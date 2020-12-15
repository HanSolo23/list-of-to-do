<template>
  <div class="modal__background">
    <div class="modal">
      <div class="modal__text">
        <slot name="modalText">Редактирование поля:</slot>
      </div>
      <div class="modal__form">
        <slot name="form"></slot>
      </div>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'ModalForEdit',
  data() {
    return {

    }
  },
  methods: {

  }
}
</script>


<style scoped lang="scss">
.modal__background {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
  .modal {
    background: url('../assets/5.jpg') 0 0 / cover no-repeat;
    box-shadow: 2px 2px 20px 1px black;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
    font-family: 'Russo One', sans-serif;
    padding: 20px;
    color: white;
    .modal__text {
      padding: 20px
    }
    .modal__form {
      .edit__first__field {
        margin-bottom: 10px;
        label {
          margin-right: 27px;
        }
      }
      .edit__second__field {
        label {
          margin-right: 5px;
        }
      }
      .modal__buttons {
        display: flex;
        justify-content: center;
        margin-top: 20px;
        padding: 20px;
        .modal__button_1 {
          margin-right: 50px;
          .btn__edit {
            text-decoration: none;
            outline: none;
            padding: 10px 20px;
            color: black;
            border: 1px solid rgba(255,255,255,.4);
            background: rgba(187, 52, 52, 0.856);
            font-family: 'Russo One', sans-serif;
            text-transform: uppercase;
            letter-spacing: 2px;
            transition: all 1s ease;
            &:hover {
              border: 1px solid black;
              background: rgb(255, 255, 255);
              color: rgb(0, 0, 0);
              transition: all 1s ease;
            }
          }
        }
        .modal__button_2 {
          .btn__no {
            text-decoration: none;
            outline: none;
            padding: 10px 20px;
            color: black;
            border: 1px solid rgba(255,255,255,.4);
            background: rgba(255,255,255,.4);
            font-family: 'Russo One', sans-serif;
            text-transform: uppercase;
            letter-spacing: 2px;
            transition: all 1s ease;
            &:hover {
              border: 1px solid black;
              background: black;
              color: white;
              transition: all 1s ease;
            }
          }
        }
      }
    }
  }
}

</style>
