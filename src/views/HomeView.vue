<template>
	<h1>Messages</h1>

	<ul>
		<li v-for="(message, key) in messages" :key="key">{{ message }}</li>
	</ul>
</template>

<script setup lang="ts">
	import Echo from 'laravel-echo'
	import Pusher from 'pusher-js'
	import { ref } from 'vue'

	const messages = ref([])

	window.Pusher = Pusher

	window.Echo = new Echo({
		broadcaster: 'pusher',
		key: '11111111',
		encrypted: true,
		wsHost: 'localhost',
		cluster: 'ap1',
		wsPort: 6001,
		// wssPort: 6001,
		forceTLS: false,
		// enabledTransports: ['ws', 'wss'],
		// disableStats: true,
	})

	window.Echo.channel('sample-channel').listen('NewMessage', (data: any) => {
		// messages.value.push(data.message)
		console.log(data)
	})
</script>
