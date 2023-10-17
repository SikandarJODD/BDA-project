<script>
	import { onMount } from 'svelte';
	import Chart from 'chart.js/auto';
	import { fade, scale } from 'svelte/transition';
	let fruitsData = [
		{
			name: 'Orange',
			quantity: 12
		},
		{
			name: 'Mango',
			quantity: 19
		},
		{
			name: 'Grapes',
			quantity: 3
		},
		{
			name: 'Banana',
			quantity: 5
		},
		{
			name: 'Apple',
			quantity: 2
		},
		{
			name: 'Pineapple',
			quantity: 3
		}
	];
	let values = [12, 19, 3, 5, 2, 3];

	let diagramFruits = (/** @type {number[]} */ vas) => {
		let ctx = document.getElementById('myChart').getContext('2d');
		let chartStatus = Chart.getChart('myChart'); // <canvas> id
		if (chartStatus != undefined) {
			chartStatus.destroy();
		}

		// myChartCode.destroy();
		let myChartCode = new Chart(ctx, {
			type: 'bar',
			data: {
				labels: ['Orange', 'Mango', 'Grapes', 'Banana', 'Apple', 'Pineapple'],
				datasets: [
					{
						label: 'Fruits Data',
						data: vas,
						backgroundColor: [
							'rgba(255, 99, 132, 0.2)',
							'rgba(54, 162, 235, 0.2)',
							'rgba(255, 206, 86, 0.2)',
							'rgba(75, 192, 192, 0.2)',
							'rgba(153, 102, 255, 0.2)',
							'rgba(255, 159, 64, 0.2)'
						],
						borderColor: [
							'rgba(255, 99, 132, 1)',
							'rgba(54, 162, 235, 1)',
							'rgba(255, 206, 86, 1)',
							'rgba(75, 192, 192, 1)',
							'rgba(153, 102, 255, 1)',
							'rgba(255, 159, 64, 1)'
						],
						borderWidth: 1
					}
				]
			},
			options: {
				scales: {
					y: {
						beginAtZero: true
					}
				},
				animation: {
					duration: 0
				}
			}
		});
	};
	onMount(() => {
		diagramFruits(values);
	});
</script>

<div class="flex justify-center items-center h-screen flex-wrap">
	<div class="m-20  p-5 border flex gap-4 flex-col rounded-xl bg-gray-50 w-full md:w-fit">
		<h1 class="text-4xl font-bold">Real Time Data Analysis</h1>
		<div class="box rounded-md">
			<div class="mt-8 flow-root">
				<div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
					<div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
						<div class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:rounded-lg">
							<table class="min-w-full divide-y divide-gray-300">
								<thead class="bg-gray-50">
									<tr>
										<th
											scope="col"
											class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
											>Product Name</th
										>
										<th
											scope="col"
											class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Quantity</th
										>
										<th
											scope="col"
											class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Buy</th
										>
										<th
											scope="col"
											class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Sell</th
										>
									</tr>
								</thead>
								<tbody class="divide-y divide-gray-200 bg-white">
									{#each fruitsData as item, i}
										<tr>
											<td
												class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6"
												>{item.name}</td
											>

											{#key values[i]}
												<td in:fade class="whitespace-nowrap px-3 py-4 text-sm text-gray-700"
													>{values[i]}</td
												>
											{/key}
											<td
												class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-6"
											>
												<button
													class="text-indigo-600 hover:text-indigo-900 border-none outline-none"
													on:click={() => {
														if (values[i] >= 20) {
															values[i] = 20;
														} else {
															values[i] += 1;
														}
														diagramFruits(values);
													}}
												>
													<svg
														xmlns="http://www.w3.org/2000/svg"
														width="24"
														height="24"
														viewBox="0 0 24 24"
														fill="none"
														stroke="currentColor"
														stroke-width="1.3"
														stroke-linecap="round"
														stroke-linejoin="round"
														class="lucide lucide-plus-circle"
														><circle cx="12" cy="12" r="10" /><path d="M8 12h8" /><path
															d="M12 8v8"
														/></svg
													>
												</button>
											</td>
											<td
												class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-6"
											>
												<button
													class="text-indigo-600 hover:text-indigo-900 border-none outline-none"
													on:click={() => {
														if (values[i] <= 2) {
															values[i] = 2;
														} else {
															values[i] -= 1;
														}
														diagramFruits(values);
													}}
												>
													<svg
														xmlns="http://www.w3.org/2000/svg"
														width="24"
														height="24"
														viewBox="0 0 24 24"
														fill="none"
														stroke="currentColor"
														stroke-width="1.3"
														stroke-linecap="round"
														stroke-linejoin="round"
														class="lucide lucide-minus-circle"
														><circle cx="12" cy="12" r="10" /><path d="M8 12h8" /></svg
													>
												</button>
											</td>
										</tr>
									{/each}
								</tbody>
							</table>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
	<div>
		<div>
			<h1 class="text-4xl font-bold text-blue-500">Chart</h1>
			<div class="border rounded-md my-3 p-2 flex justify-end px-5 border-gray-400 bg-gray-100">
				Total Product Quantity :
				{values.reduce((a, b) => a + b, 0)}
			</div>
		</div>
		<div class="border w-full  md:w-[500px] rounded-lg shadow-md my-10 md:my-0 lg:p-2">
			<canvas id="myChart" />
		</div>
	</div>
</div>
