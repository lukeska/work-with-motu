<script setup>
import { defineProps } from "vue";
import GrayDot from "./GrayDot.vue";
import ColorfulDot from "./ColorfulDot.vue";

let props = defineProps({
	active: Boolean,
	img: String,
});
</script>
<template>
	<div class="relative w-16 md:w-32 lg:w-40">
		<button
			:class="[
				active
					? 'button-gradient-border gradient-border border-transparent text-white'
					: 'border-slate-800 text-[#8c8fb4] hover:text-gray-400 hover:border-slate-700',
				'relative group block w-full h-12 border font-semibold rounded-xl transition duration-300',
			]"
		>
			<div
				class="relative z-30 flex items-center justify-center h-full space-x-2"
			>
				<div
					:class="[
						active ? '' : 'grayscale',
						'w-7 h-7 overflow-hidden rounded-full',
					]"
				>
					<img :src="img" alt="" />
				</div>
				<div class="hidden md:block">
					<slot></slot>
				</div>
			</div>

			<!-- Gray dots -->
			<GrayDot :active="active" class="-top-4 left-6"></GrayDot>
			<GrayDot :active="active" class="-top-8 left-8"></GrayDot>
			<GrayDot :active="active" class="top-0 -left-6"></GrayDot>
			<GrayDot :active="active" class="top-6 -left-4"></GrayDot>
			<GrayDot :active="active" class="-bottom-4 left-6"></GrayDot>
			<GrayDot :active="active" class="-top-4 right-6"></GrayDot>
			<GrayDot :active="active" class="-top-7 right-3"></GrayDot>
			<GrayDot :active="active" class="top-6 -right-3"></GrayDot>
			<GrayDot :active="active" class="top-8 -right-5"></GrayDot>
			<GrayDot :active="active" class="-top-5 -right-6"></GrayDot>

			<template v-if="active">
				<!-- Colorful dots -->
				<ColorfulDot
					class="bg-[#c17b79] bottom-3 -left-8"
				></ColorfulDot>
				<ColorfulDot
					class="bg-[#b998d4] -bottom-2 -left-2"
				></ColorfulDot>
				<ColorfulDot class="bg-[#b998d4] -top-4 -left-2"></ColorfulDot>
				<ColorfulDot class="bg-[#c3a0c7] -top-3 left-12"></ColorfulDot>
				<ColorfulDot
					class="bg-[#b998d4] -bottom-4 right-6"
				></ColorfulDot>
				<ColorfulDot class="bg-[#b998d4] -top-4 -right-6"></ColorfulDot>
				<ColorfulDot
					class="bg-[#c17b79] -bottom-3 -right-4"
				></ColorfulDot>
			</template>
		</button>
		<div
			:class="[
				active ? 'z-20' : 'z-10',
				'absolute top-0 -left-[640px] xl:left-0 xl:-top-[300px] svg-container',
			]"
		></div>
	</div>
</template>
