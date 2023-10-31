<template>
	<h1>Counter App</h1>
	<div>{{ count }}</div>
	<button v-on:click="increaseCount()">Increment</button>
	<button v-on:click="decreaseCount()">Decrement</button>
	<button v-on:click="resetCount()">Reset to 0</button>
	<div>
		<label for="">Skip to
			<input type="number" v-on:change="setCount($event)">
		</label>
	</div>		
</template>

<script setup lang="ts">
import { ref } from "vue";

let count = ref(0);

function increaseCount(incrementAmount = 1): void {
	count.value += incrementAmount;
}

function decreaseCount(decrementAmount = 1): void {
	count.value -= decrementAmount;
}

function resetCount() {
	count.value = 0;
}

function countClasses():string {
	if (count.value % 5 === 0) {
		return "green";
	} else {
		return ""
	}
}

function setCount(event:Event) {
	// see https://freshman.tech/snippets/typescript/fix-value-not-exist-eventtarget/
	// for why the 'as' part is needed
	const target = event.target as HTMLInputElement;
	if (target != null) {
		count.value = Number(target.value);
		target.value = "";
	}
}
</script>
