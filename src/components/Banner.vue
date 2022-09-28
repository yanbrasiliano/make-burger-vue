<template>
	<div id="main-banner" class="bg-no-repeat h-96 flex items-center justify-start pb-5 pl-10">
		<h1 class="text-slate-200 text-center text-6xl"></h1>
	</div>
</template>

<script>
export default {
	name: "Banner"
}
</script>



<style scoped>
#main-banner {
	background-image: url('/public/img/burger.jpg');
	background-position: right bottom -290px;
}
</style>