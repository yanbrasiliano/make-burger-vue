<template>
	<div id="burger-table" v-if="burgers">
		<div>
			<div id="burger-table-heading">
				<div class="order-id">#</div>
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
					<button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 border border-red-700 rounded"
						@click="deleteBurger(burger.id)">
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

		updateBurger(event, id) {
			const option = event.target.value;
			const dataJson = JSON.stringify({ status: option });
			const req = fetch(`http://localhost:5001/burgers/${id}`, {
				method: "PATCH",
				headers: { "Content-Type": "application/json" },
				body: dataJson
			});
			window.location.reload();
			return req;
		}
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