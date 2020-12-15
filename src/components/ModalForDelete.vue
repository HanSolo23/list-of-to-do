<template>
  <div class="modal__background">
    <slot name="deleteWindow"></slot>
  </div>
  
</template>

<script>
export default {
  name: 'ModalForContactsList',
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
    background: url('../assets/6.jpg') 0 0px / cover no-repeat;
    box-shadow: 2px 2px 20px 1px black;
    overflow-x: auto;
    padding: 20px;
    display: flex;
    flex-direction: column;
    font-family: 'Russo One', sans-serif;
    color: white;
    .modal__text {
      padding: 20px
    }
    .modal__buttons {
      display: flex;
      justify-content: center;
      margin-top: 20px;
      padding: 20px;
      .modal__button_1 {
        margin-right: 50px;
        .btn__yes {
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

</style>
