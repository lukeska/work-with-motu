<script setup>
import { defineProps } from "vue";

let props = defineProps({
	active: Boolean,
});
</script>

<template>
	<div
		:class="[
			active ? 'opacity-100' : 'opacity-0 group-hover:opacity-100',
			'w-[3px] h-[3px] bg-[#393956] rounded-full absolute transition duration-500',
		]"
	></div>
</template>
