<template>
	<div>
		<div class="flex justify-end items-center bg-slate-900 border-solid divide-orange-800 py-3.5 pl-14  ">
			<router-link class="ml-0 m-auto" id="logo-url" to="/">
				<img class="w-10 h-10" id="logo" :src="logo" :alt="alt">
			</router-link>
			<router-link class="text-amber-500 m-3 text-4xl transition ease-in-out delay-150 hover:-translate-y-2 hover:scale-120 duration-300 " to="/">Home</router-link>
			<router-link class="text-amber-500 m-3 text-4xl ease-in duration-300 transition ease-in-out delay-150 hover:-translate-y-2 hover:scale-120 duration-300" to="/order">Orders</router-link>
		</div>
	</div>
</template>


<script>
export default {
	name: "Navbar",
	props: ["logo", "alt"]
}
</script>