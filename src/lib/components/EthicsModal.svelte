<script lang="ts">
	import { enhance } from "$app/forms";
	import { base } from "$app/paths";
	import { PUBLIC_VERSION } from "$env/static/public";
	import Logo from "$lib/components/icons/Logo.svelte";
	import Modal from "$lib/components/Modal.svelte";
	import type { LayoutData } from "../../routes/$types";

	export let settings: LayoutData["settings"];
</script>

<Modal>
	<div
		class="flex w-full flex-col items-center gap-6 bg-gradient-to-t from-yellow-500/40 via-yellow-500/10 to-yellow-500/0 px-4 pb-10 pt-9 text-center"
	>
		<h2 class="flex items-center text-2xl font-semibold text-gray-800">
			<Logo classNames="text-3xl mr-1.5" />HuggingChat
			<div
				class="ml-3 flex h-6 items-center rounded-lg border border-gray-100 bg-gray-50 px-2 text-base text-gray-400"
			>
				v{PUBLIC_VERSION}
			</div>
		</h2>
		<p class="px-4 text-lg font-semibold leading-snug text-gray-800 sm:px-12">
			This application is for demonstration purposes only.
		</p>
		<p class="text-gray-800">
			AI is an area of active research with known problems such as biased generation and
			misinformation. Do not use this application for high-stakes decisions or advice.
		</p>
		<p class="px-2 text-sm text-gray-500">
			Your conversations will be shared with model authors unless you disable it from your settings.
		</p>
		<form action="{base}/settings" use:enhance method="POST">
			<input type="hidden" name="ethicsModalAccepted" value={true} />
			{#each Object.entries(settings) as [key, val]}
				<input type="hidden" name={key} value={val} />
			{/each}
			<button
				type="submit"
				class="mt-2 rounded-full bg-black px-5 py-2 text-lg font-semibold text-gray-100 transition-colors hover:bg-yellow-500"
			>
				Start chatting
			</button>
		</form>
	</div>
</Modal>
