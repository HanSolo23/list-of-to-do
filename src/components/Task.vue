<template>
  <div 
    :key="task.id" 
    class="task__list__column">
    <p class="row">{{ task.public_date }}</p>
    <p class="row">{{ task.description }}</p>
    <p class="row">{{ task.note }}</p>
    <div class="task__buttons">
      <button @click="showEditWindow(); id = task.id" class="button_1"></button>
      <button @click="showDeleteWindow(); id = task.id" class="button_2"></button>
    </div>
    <transition name="modal-animation">
      <ModalForEdit v-if="isEditWindowVisible">
        <template #form>
          <form>
            <div class="edit__first__field">
              <label for="edit__first__field">Описание:</label>
              <input id="edit__first__field" type="text" v-model="description">
            </div>
            <div class="edit__second__field">
              <label for="edit__second__field">Примечание:</label>
              <input id="edit__second__field" type="text" v-model="note">
            </div>
            <div class="modal__buttons">
              <div class="modal__button_1">
                <button 
                  class="btn__edit" 
                  type="submit"
                  @click="submit">
                  Редактировать!
                </button>
              </div>
              <div class="modal__button_2">
                <button  @click.prevent="closeEditWindow" class="btn__no">Назад</button>
              </div>
            </div>
          </form>
        </template>
      </ModalForEdit>
    </transition>
    <transition name="modal-animation">
      <ModalForDelete v-if="isDeleteWindowVisible">
        <template #deleteWindow>
          <div class="modal">
            <div class="modal__text">
              <div name="modalText">
                Вы действительно хотите удалить эту запись?
              </div>
            </div>
            <div class="modal__buttons">
              <div class="modal__button_1">
                <button @click="deleteTask" class="btn__yes">Да</button>
              </div>
              <div class="modal__button_2">
                <button @click="closeDeleteWindow" class="btn__no">Нет</button>
              </div>
            </div>
          </div>
        </template>
      </ModalForDelete>
    </transition> 
  </div>
</template>

<script>
import ModalForEdit from '../components/ModalForEdit.vue';
import ModalForDelete from '../components/ModalForDelete.vue';
import gql from "graphql-tag";

const EDIT_TODO = gql`
  mutation editTask (
    $id: uuid!
    $description: String!
    $note: String!
  ) {
    update_todo_by_pk  (
      pk_columns: {id: $id}
      _set: {
        description: $description
        note: $note
      }
    ) {
      id
      description
      note
    }
  }
`;

const DELETE_TODO = gql`
  mutation deleteTask (
    $id: uuid!
  ) {
    delete_todo_by_pk (
      id: $id
    ) {
      id
      description
      note
      public_date
      done
    }
  }
`;

export default {
  name: 'Task',
  props: ['task', 'index'],
  components: {
    ModalForEdit,
    ModalForDelete
  },
  data() {
    return {
      taskIndex: this.index,
      nameOfEditImage: '3',
      nameOfDeleteImage: '4',
      isEditWindowVisible: false,
      isDeleteWindowVisible: false,
      id: '',
      description: '',
      note: '',
    }
  },
  computed: {

  },
  apollo: {},
  methods: {
    showImage(name) {
      return require(`../assets/${name}.png`);
    },
    showEditWindow() {
      this.isEditWindowVisible = true;
    },
    submit(e) {
      e.preventDefault();
      const { id, description, note } = this.$data;
      this.$apollo.mutate({
        mutation: EDIT_TODO,
        variables: {
          id,
          description,
          note
        },
        refetchQueries: ["getTasks"]
      });
      this.isEditWindowVisible = false;
    },
    showDeleteWindow() {
      this.isDeleteWindowVisible = true;
    },
    deleteTask() {
      const { id } = this.$data;
      this.$apollo.mutate({
        mutation: DELETE_TODO,
        variables: {
          id
        },
        refetchQueries: ["getTasks"]
      });
      this.isDeleteWindowVisible = false;
    },
    closeEditWindow() {
      this.isEditWindowVisible = false;
    },
    closeDeleteWindow() {
      this.isDeleteWindowVisible = false;
    },
  }
}
</script>


<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Russo+One&display=swap');
.task__list__column {
  display: flex;
  flex-direction: column;
  border: 1px solid black;
  text-align: center;
  margin-right: 20px;
  width: 300px;
  background: url('../assets/2.jpg') 0 0 / cover no-repeat;
  margin-bottom: 20px;
  padding: 20px;
  box-shadow: 5px 5px 15px 0px;
  .modal-animation-enter-active {
    transition: all .5s ease;
  }
  .modal-animation-leave-active {
    transition: all .5s ease;
  }
  .modal-animation-enter, .modal-animation-leave-to {
    opacity: 0;
  }
  .row {
    font-family: 'Russo One', sans-serif;
  } 
  .task__buttons {
    .button_1 {
      background: url('../assets/3.png') 0 0 / cover no-repeat rgba(235, 182, 83, 0);
      margin-right: 10px;
    }
    .button_2 {
      background: url('../assets/4.png') 0 0 / cover no-repeat rgba(235, 182, 83, 0);
    }
    button {
      border-radius: 50%;
      border: none;
      outline: none;
      cursor: pointer;
      width: 50px;
      height: 50px;
      transition: all 0.2s ease;
      // &:nth-child(1) {
      //   margin-right: 70px;
      // }
      &:hover {
        transform: scale(1.2);
        transition: all 0.2s ease;
      }
      img {
        width: 50px;
        height: 50px;
      }
    }
  }
}
</style>
