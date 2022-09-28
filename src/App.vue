<template>
	<div>
		<Navbar :logo="logo_src" :alt="app_name" />
		<router-view />
		<Footer />

	</div>
</template>

<script>
import Navbar from "@/components/Navbar.vue"
import Footer from "@/components/Footer.vue"


export default {
	name: "Home",
	data() {
		return {
			logo_src: ("/img/logo.png"),
			app_name: "Make Your Burguer"
		}
	},
	components: {
		Navbar,
		Footer
	}
}
</script>

<style>
#main-container {
	min-height: 400px;
}
</style>