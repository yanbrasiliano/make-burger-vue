<template>
	<div>
		<Banner />
		<div class="m-12 min-h-full">
			<h1 class="text-center text-5xl mb-10 text-gray-600">Make Your Burguer</h1>
			<BurgerForm />
		</div>
	</div>
</template>


<script>
import Banner from '@/components/Banner.vue'

export default {
	name: 'Home',
	components: {
		Banner,
	}
}
</script>