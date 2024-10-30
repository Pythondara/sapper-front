<script>
import axios from 'axios'
export default {
  data () {
    return {
      username: '',
      error: '',
      responseStatus: ''
    }
  },
  computed: {
    computedUsername() {
      return 'Вас зовут' + ' ' + this.username
    }
  },
  methods: {
    async createUser() {
      let res

      try {
      res = await axios.post('http://localhost:8000/user', {username: this.username})
      } catch (e) {
        this.error = 'Ошибка создания пользователя'
        return e
      }

      if(res.data.username) {
        console.log('pledge')
        console.log('res', this.responseStatus)
        this.responseStatus = 'Пользователь успешно создан'
        console.log('res', this.responseStatus)

        this.username = res.data.username
      }
      this.error = ''

      return this.username


    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Игра в сапера(в алмазы (сапер наоборот))</h1>
    <p>{{ username === '' ? 'Создать пользователя' :  computedUsername }}</p>
    <input type="text" v-model="username" placeholder="Введите username">
    <button v-if="username !== ''" @click="createUser()">Отправить</button>
    <button disabled v-else >Отправить</button>
    <p class="responseStatus">{{responseStatus}}</p>
    <p class="error">{{error}}</p>
    <p>Сначала создайте пользователя потом нажмите "Начать игру"</p>
    <button>Начать игру</button>
  </div>
</template>

<style scoped>


.error {
  color: #d03939
}

.responseStatus {
  color: #fff
}

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background: #1f0f24;
  text-align: center;
  color: #f8f8f8;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

::placeholder {
  color: #f8f8f8;
}

.wrapper input:focus {
  border-bottom-color: #6e2d7d;
}

.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:disabled {
  background: #746027;
  cursor: not-allowed;

}

.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}

</style>
