<script setup lang="ts">
import { ref } from 'vue';
type Item = {
	id: string;
	isChecked: boolean;
	name: string;
};

const data: Item[] = [
	{
		id: 'todo-001',
		isChecked: false,
		name: 'Apples',
	},
	{
		id: 'todo-002',
		isChecked: true,
		name: 'Bananies',
	},
	{
		id: 'todo-003',
		isChecked: false,
		name: 'Avocåëdos',
	},
];
const items = ref(data);
const name = ref('');

const onInput = (evt: Event) => {
	const target = evt.target as HTMLInputElement;
	name.value = target.value;
};

const onSubmit = () => {
	items.value.push({
		name: name.value,
		id: `todo-${name.value}-${items.value.length + 1}`,
		isChecked: false,
	});
	name.value = '';
};

const onChange = (itemId: string) => {
	const updatedItem = items.value.find(({ id }) => id === itemId) as Item;
	updatedItem.isChecked = !updatedItem.isChecked
}
</script>

<template>
  <h1>Hewwo</h1>
  <form @submit.prevent="onSubmit">
    <label for="todo-name">Name</label>
    <input
      id="todo-name"
      type="text"
      :value="name"
      @input="onInput"
    >
    <button type="submit">
      Submit
    </button>
  </form>
  <ul>
    <li
      v-for="item of items"
      :key="item.id"
    >
      <input
        :id="'todo-' + item.id"
        :checked="item.isChecked"
        type="checkbox"
        @change="onChange(item.id)"
      >
      <label :for="'todo-' + item.id">{{ item.name }}</label>
    </li>
  </ul>
</template>

<style>
*,
*::after,
*::before {
	box-sizing: border-box;
}

html {
	font-size: 62.5%;
}

body {
	font-family: sans-serif;
	font-size: 1.6rem;
	line-height: 1.15;
}

#app {
	padding: 2rem;
}
</style>
