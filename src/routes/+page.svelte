<script lang="ts">
	import { Toaster, toast } from 'svelte-sonner';

	let email = $state('');
</script>

<div class="absolute w-screen h-screen bg-stone-100 -z-10"></div>
<div class="w-full max-w-5xl mx-auto pt-20 z-10 px-2">
	<div>
		<h1 class="text-5xl font-semibold tracking-tight py-5">Introducing Eyeballs</h1>
		<p class="text-xl text-stone-700 text-pretty">
			A useful file manager designed to be used with a keyboard
		</p>
	</div>

	<div transition:fade class="mx-auto max-w-lg w-full bg-stone-200 rounded-lg flex p-2 mt-20">
		<input
			type="text"
			placeholder="Enter your email address"
			class="grow focus-visible:outline-none px-2"
			bind:value={email}
		/>
		<button
			onclick={() => {
				if (!email) return;

				fetch('https://api.devmatter.app/forms/7', {
					method: 'POST',
					headers: {
						'Content-Type': 'application/json'
					},
					body: JSON.stringify({
						email: email
					})
				})
					.then((res) => res.json())
					.then((data) => {
						toast.success('You are on the waitlist! I will notify you when the app is ready.');
					});
			}}
			class="bg-stone-800 transition active:scale-95 text-stone-50 font-medium rounded-lg px-4 py-2"
			>Join the waitlist</button
		>
	</div>

	<enhanced:img src="../lib/assets/preview.png" alt="Screenshot of Eyeballs app" />
</div>

<Toaster />
