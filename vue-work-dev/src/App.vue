<script setup>
import {computed, ref} from "vue";

const array = ref([
  {
    name: 'Задача по умолчанию',
    done: false
  },
  {
    name: 'Вторая по умолчанию',
    done: false
  },
  {
    name: 'Третья по умолчанию',
    done: false
  },
  {
    name: 'Четвертая по умолчанию',
    done: false
  }
]);

const arrayRadio = ref([
  {
    name: 'Задача по умолчанию',
    done: false
  },
  {
    name: 'Вторая по умолчанию',
    done: false
  },
  {
    name: 'Третья по умолчанию',
    done: false
  },
  {
    name: 'Четвертая по умолчанию',
    done: false
  }
]);

const arrayReady = ref([
  '',
]);

const selected = ref('')
const selected2 = ref([])
const text = ref('')

const picked = ref('')

const completed = computed(() => {
  return array.value.filter(item => item.done)
})

const unCompleted = computed(() => {
  return array.value.filter(item => !item.done)
})
const arrayTask = ref([])

const addTask = () => {
  array.value.push({name: textTask.value, done: false});
  textTask.value = ''
}
const textTask = ref('')

</script>

<template>
  <header>
    <h1>Первый блок</h1>
    <div>
      <h2>Задача 1</h2>
      <label :for="i" v-for="(item, i) in unCompleted" :key="item">
        {{ item.name }}
        <input :id="i" type="checkbox" v-model="item.done">
      </label>
    </div>
    <h3>Выполненные</h3>
    <div style="margin-bottom: 10px;" class="output" v-for="(item, i) in completed" :key="i">
      {{ item.name }}
    </div>
    <h2>Задача 2</h2>
    <select v-model="selected">
      <option disabled value="">выбрать</option>
      <option v-for="(item, i) in array" :key="i">{{ item.name }}</option>
    </select>
    <h3>{{ selected }}</h3>
    <div>
      <h2>Задача 3</h2>

    </div>
    <input type="text" v-model="text">
    <h3>Вывод: {{ text }}</h3>

    <h2>Задача 4 </h2>
    <div v-for="(item, i) in arrayRadio" :key="i">
      <label :for="i">
        {{ item.name }}
        <input type="radio" :id="i" :value="item" v-model="picked"/>
      </label>
    </div>
    <div>Выбрано: {{ picked.name }}</div>

    <h2>Задача 5</h2>
    <select v-model="selected2" multiple>
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <h3>{{ selected2 }}</h3>
  </header>

  <main>
  <h1>Второй блок</h1>
    <form @submit.prevent="addTask()">
      <input type="text" placeholder="Введите текст задачи" v-model="textTask">
      <button>Добавить</button>
    </form>
    <ul>
      <h3 v-if="unCompleted.length">Надо сделать</h3>
      <h2 v-else>Все выполнил!</h2>
      <li v-for="(item, i) in unCompleted" :key="item">
        <label>
          <input type="checkbox" v-model="item.done">
          {{ item.name}}
        </label>
      </li>
    </ul>
    <ul>
      <h2 v-if="unCompleted.length === 0">хорошо потрудился</h2>
      <h2 v-else-if="completed.length >= 1">Пошло дело!</h2>
      <h3 v-else >Пусто, простой!</h3>
      <li v-for="(item, i) in completed" :key="item">
        <label>
          <input type="checkbox" v-model="item.done">
          {{ item.name}}
        </label>
      </li>
    </ul>
  </main>
</template>

<style scoped>
header, main {
  padding: 20px;
  border-radius: 10px;
  background-color: #eee;
}

select {
  min-width: 200px;
}

h2 {
  margin-bottom: 20px;
}

h2 {
  margin-bottom: 10px;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

label {
  display: flex;
}

@media (min-width: 1024px) {


  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
