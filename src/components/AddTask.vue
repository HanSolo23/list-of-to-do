<template>
  <div class="add__task__form">
    <form @submit="submit">
      <div class="form__fields">
        <div class="add__first__field">
          <label for="add__field">Описание:</label>
          <input id="add__field" type="text" v-model="description">
        </div>
        <div class="add__second__field">
          <label for="add__field">Примечание:</label>
          <input id="add__field" type="text" v-model="note">
        </div>
      </div>
      <div class="buttons">
        <div class="button_1">
          <input 
            class="btn__add" 
            type="submit"
            value="Добавить задачу!">
        </div>
      </div>
    </form>
  </div>
  
</template>

<script>
import gql from "graphql-tag";

const ADD_TASK = gql`
  mutation addTask (
    $description: String!
    $note: String!
  ) {
    insert_todo (
      objects: [
        {
          description: $description,
          note: $note
        }
      ]
    ) {
      returning {
        id
        public_date
        done
      }
    }
  }
`;

export default {
  name: 'AddTask',
  data() {
    return {
      description: '',
      note: '',
    }
  },
  apollo: {},
  methods: {
    submit(e) {
      e.preventDefault();
      const { description, note } = this.$data;
      this.$apollo.mutate({
        mutation: ADD_TASK,
        variables: {
          description,
          note
        },
        refetchQueries: ["getTasks"]
      })
    },
  }
}
</script>


<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Russo+One&display=swap');
.add__task__form {
  display: flex;
  justify-content: center;
  margin-top: 100px;
  border: 1px solid black;
  max-width: 700px;
  padding: 20px;
  margin: 20px auto;
  font-family: 'Russo One', sans-serif;
  background: url('../assets/2.jpg') 0 0 / cover no-repeat;
  box-shadow: 5px 5px 15px 0px;
  .form__fields {
    display: flex;
    margin-bottom: 20px;
    .add__first__field {
      margin-right: 20px;
      label {
        margin-right: 10px;
      }
    }
    .add__second__field {
      label {
        margin-right: 10px;
      }
    }
  }
  .buttons {
    display: flex;
    justify-content: center;
    .button_1 {
      input {
        text-decoration: none;
        outline: none;
        padding: 10px 20px;
        color: white;
        border: 1px solid rgba(255,255,255, .4);
        background: rgba(0, 0, 0, 0.9);
        font-family: 'Russo One', sans-serif;
        text-transform: uppercase;
        letter-spacing: 2px;
        transition: all 1s ease;
        &:hover {
          border: 1px solid black;
          background: rgba(255,255,255, .9);
          color: black;
          transition: all 1s ease;
        }
      }
      
    }
  }
}

</style>
