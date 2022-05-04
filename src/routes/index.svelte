<script lang="ts" context="module">
	import type { Load } from '@sveltejs/kit';
	export const load: Load = async ({ fetch }) => {
		const valueRequest = await fetch('https://www.mercadobitcoin.net/api/BTC/ticker/');
		const valueResponse = await valueRequest.json();

		return {
			props: {
				btcValue: valueResponse.ticker.last,
				btcHigh: valueResponse.ticker.high,
				btcLow: valueResponse.ticker.low
			}
		};
	};
</script>

<script>
	export let btcValue = 0;
	export let btcHigh = 0;
	export let btcLow = 0;

	const currencyFormatter = new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' });
</script>

<div class="min-h-screen flex justify-center items-center flex-col">
	<div class="border border-neutral-200 shadow-sm p-8 rounded-md text-5xl text-center space-y-5">
		<h1 class="font-bold">{currencyFormatter.format(btcValue)}</h1>
		<h1 class="text-green-500">{currencyFormatter.format(btcHigh)}</h1>
		<h1 class="text-red-700">{currencyFormatter.format(btcLow)}</h1>
	</div>
</div>
