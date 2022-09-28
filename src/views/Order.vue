<template>
	<div>
		<div id="main-container" class="m-14">
			<h1 class="text-center text-5xl mb-10 text-gray-600">Manage Orders</h1>
			<Dashboard />
		</div>
	</div>
</template>


<script>
import Dashboard from '@/components/Dashboard.vue'
export default {
	name: 'Order',
	components: {
		Dashboard
	}
}

</script>