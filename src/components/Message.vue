<template>
	<div class="text-blue-800 bg-indigo-200 rounded p-2 border-solid border-blue-900 border-2 max-w-sm mb-7 m-auto">
		<p> {{ message }} </p> 
	</div>
</template>

<script>

export default {
	name: "Message",
	props: {
		msg: String,
	}
}
</script>

