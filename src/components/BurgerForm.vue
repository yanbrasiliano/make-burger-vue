<template>
	<Message :msg="msg" v-show="msg" />
	<div class="flex justify-center items-center">
		<form class="max-w-xl m-4 p-10 bg-white rounded shadow-xl">

			<div class="">
				<label class="text-lg block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400"
					for="name">Name</label>
				<input
					class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
					id="name" name="name" type="text" required="" placeholder="Your Name" aria-label="Name">
			</div>

			<label class="text-lg block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400 mt-5"
				for="bread">Bread</label>
			<select
				class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
				name="bread" v-model="bread">
				<option class="text-lg block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400 mt-5">Select your bread</option>
				<option v-for="bread in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
			</select>

			<label class="text-lg block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400 mt-5" for="pao">Meat</label>
			<select
				class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
				name="meat" v-model="meat">
				<option class="text-lg block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400 mt-5">Select your meat</option>
				<option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
			</select>

			<label class="text-lg block mb-4 text-sm font-medium text-gray-900 dark:text-gray-400 mt-10"
				for="pao">Additional</label>
			<div class="flex items-center mb-4">
				<input id="default-checkbox" type="checkbox" value=""
					class="w-4 h-4 text-blue-600 bg-gray-100 rounded border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
				<label for="default-checkbox" class="ml-1 mr-2 text-sm font-medium text-gray-900 dark:text-gray-300">Default
					checkbox</label>

			</div>


			<div class="flex justify-center items-center">
				<button
					class="hover:shadow-form rounded-md bg-[#6A64F1] py-3 px-8 text-center text-base font-semibold text-white outline-none mt-6">
					Submit
				</button>
			</div>
		</form>
	</div>
</template>

<script>
import Message from '@/components/Message.vue'

export default {
	name: "BurgerForm",
	components: {
		Message
	}
}
</script>