<template>
	<div id="main-banner" class="bg-no-repeat h-96 flex items-center justify-start pb-5 pl-10 text-gray-800 text-stone-300">
		<h1 class="text-gray-900 text-center text-6xl">Make Your Burger</h1>
	</div>
</template>

<script>
export default {
	name: "Banner"
}
</script>



<style scoped>
#main-banner {
	background-image: url('/public/img/burger1.jpg');
	background-position: right top;
}
</style>