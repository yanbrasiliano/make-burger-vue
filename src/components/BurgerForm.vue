<template>
	<Message :msg="msg" v-show="msg" />
	<div class="flex justify-center items-center">
		<form method="POST" class="max-w-xl m-4 p-10 bg-white rounded shadow-xl" @submit="createBurger">

			<label class="text-xl block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400" for="name">Name</label>
			<input
				class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
				id="name" name="name" type="text" required v-model="name" placeholder="Your Name">

			<label class="text-xl block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400 mt-5"
				for="bread">Bread</label>
			<select
				class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
				name="bread" v-model="bread">
				<option class="text-lg block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400 mt-5" disabled>Select
					your bread
				</option>
				<option v-for="bread in breadLocal" :key="bread.id" :value="bread.type">{{ bread.type }}</option>
			</select>

			<label class="text-xl block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400 mt-5"
				for="meat">Meat</label>
			<select
				class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
				name="meat" v-model="meat">
				<option class="text-lg block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400 mt-5" disabled>Select
					your meat
				</option>
				<option v-for="meat in meatLocal" :key="meat.id" :value="meat.type">{{ meat.type }}</option>
			</select>

			<label class="text-xl block mb-4 text-sm font-medium text-gray-900 dark:text-gray-400 mt-10"
				for="additional">Additional</label>
			<div class="flex items-center mb-4" v-for="options in additionalLocal" :key="options.id">
				<input class="w-4 h-4 text-blue-600 bg-gray-100 rounded border-gray-300
					 focus:ring-blue-500 
					 dark:focus:ring-blue-600 
					 dark:ring-offset-gray-800 
					 focus:ring-2 
					 dark:bg-gray-700 
					 dark:border-gray-600" type="checkbox" name="opcionais" v-model="additional" :value="options.type">
				<span class="ml-1 mr-2 text-sm font-medium text-gray-900 dark:text-gray-300">{{ options.type }}</span>
			</div>


			<div class="flex justify-center items-center">
				<button
					class="hover:shadow-form rounded-md bg-[#6A64F1] py-3 px-8 text-center text-base font-semibold text-white outline-none mt-6">
					Create Burger
				</button>
			</div>
		</form>
	</div>
</template>

<script>
import Message from '@/components/Message.vue'
import api from '@/services/Base.js'

export default {
	name: "BurgerForm",
	data() {
		return {
			breadLocal: null,
			mealLocal: null,
			additionalLocal: null,
			name: null,
			bread: null,
			meat: null,
			additional: [],
			status: "Requested",
			msg: "",

		}
	},
	methods: {
		getIngredients() {
			return api.get("ingredients").then((response) => {
				this.breadLocal = response.data.breads;
				this.meatLocal = response.data.meat;
				this.additionalLocal = response.data.optional;
			});
		},

		createBurger(e) {
			e.preventDefault();

			const data = {
				name: this.name,
				meat: this.meat,
				bread: this.bread,
				additional: Array.from(this.additional),
				status: "Requested"
			}

			const response = api.post("burgers", data).then((response) => {
				return response.data;
			});

			this.successMessage();
			this.clearForm();

			return response;
		},
		successMessage(){
			return this.msg = "Order successfully completed!";
		},
		clearForm() {

			setTimeout(() => this.msg = "", 3000)

			this.name = ""
			this.meat = ""
			this.bread = ""
			this.additional = []

		}
	},
	mounted() {
		this.getIngredients();
	},
	components: {
		Message
	}
}
</script>