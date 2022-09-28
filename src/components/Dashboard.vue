<template>
	<div id="burger-table" v-if="burgers">
		<div>
			<div id="burger-table-heading">
				<div class="order-id">#:</div>
				<div>Client</div>
				<div>Bread</div>
				<div>Meat</div>
				<div>Options</div>
				<div>Actions</div>
			</div>
		</div>
		<div id="burger-table-rows">
			<div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
				<div class="order-number">{{ burger.id }}</div>
				<div>{{ burger.name }}</div>
				<div>{{ burger.bread }}</div>
				<div>{{ burger.meat }}</div>
				<div>
					<ul v-for="(additional, index) in burger.additional" :key="index">
						<li>{{ additional }}</li>
					</ul>
				</div>
				<div>
					<select name="status" class="mr-3 pb-3 pl-1.5" @change="updateBurger($event, burger.id)">
						<option :value="s.type" v-for="s in status" :key="s.id" :selected="burger.status == s.type">
							{{ s.type }}
						</option>
					</select>

					<button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 border border-red-700 rounded" @click="deleteBurger(burger.id)">
						Cancel
					</button>
				</div>
			</div>
		</div>
	</div>
	<div v-else>
		<h2>No orders at the moment!</h2>
	</div>
</template>
	<!-- <div class="" v-if="burgers">
		<div>
			<div class="font-bold p-3 border-solid divide-orange-800">
				<div class="order-id">#:</div>
				<div>Client</div>
				<div>Bread</div>
				<div>Meat</div>
				<div>Additional</div>
				<div>Actions</div>
			</div>
		</div>
		<div id="burger-table-rows">
			<div class="w-full p-3 border-solid divide-orange-800" v-for="burger in burgers" :key="burger.id">
				<div class="order-number">{{ burger.id }}</div>
				<div>{{ burger.name }}</div>
				<div>{{ burger.bread }}</div>
				<div>{{ burger.meat }}</div>
				<div>
					<ul v-for="(opcional, index) in burger.opcionais" :key="index">
						<li>{{ opcional }}</li>
					</ul>
				</div>
				<div>
					<select class="mr-3 pb-3 pl-1.5" name="status" @change="updateBurger($event, burger.id)">
						<option :value="s.type" v-for="s in status" :key="s.id" :selected="burger.status == s.type">
							{{ s.type }}
						</option>
					</select>
					<button
						class="bg-red-500 hover:bg-red-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-red-500 rounded"
						@click="deleteBurger(burger.id)" >
						Cancel
					</button>
				</div>
			</div>
		</div>
	</div>
	<div v-else>
		<h2>No orders at the moment!</h2>
	</div> -->
<!-- </template> -->

<script>
import api from '@/services/Base.js'

export default {
	name: "Dashboard",
	data() {
		return {
			burgers: null,
			burger_id: null,
			status: [],
			msg: ""
		}
	},
	methods: {
		getOrders() {
			return api.get("burgers").then((response) => {
				console.log(response.data)
				this.burgers = response.data
				this.getStatus()
			});
		},
		getStatus() {
			return api.get("status").then((response) => {
				this.status = response.data
			})
		},
		deleteBurger(id) {
			let response = api.delete(`burgers/${id}`)

			this.getOrders()

			return response
		},
	},
	mounted() {
		this.getOrders()
	}
}
</script>
<style scoped>

#burger-table {
	max-width: 1200px;
	margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
	display: flex;
	flex-wrap: wrap;
}

#burger-table-heading {
	font-weight: bold;
	padding: 12px;
	border-bottom: 3px solid #333;
}

.burger-table-row {
	width: 100%;
	padding: 12px;
	border-bottom: 1px solid #CCC;
}

#burger-table-heading div,
.burger-table-row div {
	width: 19%;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
	width: 5%;
}

</style>