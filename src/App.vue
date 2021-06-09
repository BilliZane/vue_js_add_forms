<template>
  <div class="container">
    <form class="card" @submit.prevent="submitHandler">
      <h1>Анкета соискателя</h1>

      <app-input
        placeholder="Введите имя"
        :error="errors.name"
        label="Как тебя зовут"
        v-model="name"
      ></app-input>

      <div class="form-control">
        <label for="age">Выбери возраст</label>
        <input type="number" id="age" min="18" max="45" v-model.number="age" />
      </div>

      <div class="form-control">
        <label for="city">Твой город</label>
        <select id="city" v-model="city">
          <option value="kyiv">Киев</option>
          <option value="kharkov">Харьков</option>
          <option value="dnepr">Днепр</option>
          <option value="odessa">Одесса</option>
        </select>
      </div>

      <div class="form-checkbox">
        <span class="label">Готов к переезду?</span>
        <div class="checkbox">
          <label
            ><input type="radio" v-model="relocate" name="trip" value="Yes" />
            Да</label
          >
        </div>

        <div class="checkbox">
          <label
            ><input type="radio" v-model="relocate" name="trip" value="No" />
            Нет</label
          >
        </div>
      </div>

      <div class="form-checkbox">
        <span class="label">Ваш опыт разработки</span>

        <div class="checkbox">
          <label>
            <input
              type="checkbox"
              v-model="skills"
              name="skills"
              value="without-experience"
            />
            без опыта
          </label>
        </div>
        <div class="checkbox">
          <label
            ><input
              type="checkbox"
              v-model="skills"
              name="skills"
              value="less-than-a-year"
            />
            менее года</label
          >
        </div>
        <div class="checkbox">
          <label
            ><input
              type="checkbox"
              v-model="skills"
              name="skills"
              value="1-2-years"
            />
            1 - 2 года</label
          >
        </div>
      </div>

      <div class="form-checkbox">
        <span class="label">Согласие на обработку персональных данных</span>

        <div class="checkbox">
          <label>
            <input type="checkbox" name="politics" required v-model="agree" />
            Согласен</label
          >
        </div>
      </div>

      <button type="submit" class="btn primary">Отправить</button>
    </form>
  </div>
</template>

<script>
import AppInput from './AppInput.vue'

export default {
  data () {
    return {
      name: '',
      age: 21,
      city: 'kyiv',
      relocate: null,
      skills: [],
      agree: false,
      errors: {
        name: null
      }
    }
  },
  methods: {
    formIsValid () {
      let isValid = true

      if (this.name.length === 0) {
        this.errors.name = 'Имя не может быть пустым'
        isValid = false
      } else {
        this.errors.name = null
      }

      return isValid
    },
    submitHandler () {
      if (this.formIsValid()) {
        console.group('Form Data')
        console.log('name:', this.name)
        console.log('age:', this.age)
        console.log('city', this.city)
        console.log('ready to move', this.relocate)
        console.log('skills', this.skills)
        console.log('agree', this.agree)
        console.groupEnd()
      }
    }
  },
  components: { AppInput }
}
</script>

<style>
.form-control small {
  background-color: yellow;
}

.form-control.invalid input {
  border: solid 1px yellow;
}
</style>
