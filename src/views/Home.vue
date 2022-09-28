<template>
	<div>
		<Banner />
		<div id="main-container" class="m-14">
			<h1 class="text-center text-5xl mb-10 text-gray-600">Make Your Burguer</h1>
			<BurgerForm/>
		</div>
	</div>
</template>



<script>
import Banner from '@/components/Banner.vue'
import BurgerForm from '@/components/BurgerForm.vue'
export default {
	name: 'Home',
	components: {
		Banner,
		BurgerForm
	}
}
</script>