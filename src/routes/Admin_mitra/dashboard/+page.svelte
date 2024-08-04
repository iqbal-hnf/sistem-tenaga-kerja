<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { Check, People, X, Clock } from 'svelte-bootstrap-icons';
	import axios from 'axios';

	let active = 0;

	let countNup = 0;
	let countPemberkasan = 0;
	let countPengajuan = 0;
	let countGriya = 0;
	let yearlySale = [];

	let getDashboard = () => {
		axios.get('/api/recruitments') // Ubah endpoint sesuai API recruitments Anda
			.then((response) => {
				let data = response.data;

				// Inisialisasi total pelamar
				countNup = data.length;

				// Hitung berdasarkan status
				data.forEach(item => {
					if (item.status === 'diterima') {
						countPemberkasan++;
					} else if (item.status === 'menunggu') {
						countPengajuan++;
					} else if (item.status === 'cancel') {
						countGriya++;
					}
				});

				// Jika ada data penjualan tahunan, set ke yearlySale
				if (data.penjualan_tahunan) {
					yearlySale = data.penjualan_tahunan;
					setChart(yearlySale);
				}
			})
			.catch((error) => {
				console.error("There was an error fetching the dashboard data!", error);
			});
	};

	let randomRGBA = () => {
		let r = Math.floor(Math.random() * 256);
		let g = Math.floor(Math.random() * 256);
		let b = Math.floor(Math.random() * 256);
		return 'rgba(' + r + ',' + g + ',' + b;
	};

	let setChart = (data) => {
		let preparedLabel = [];
		let preparedData = [];
		let preparedBgColor = [];
		let preparedBorderColor = [];

		data.forEach((d, i) => {
			let curColor = randomRGBA();
			const date = new Date();
			date.setMonth(i);
			preparedLabel.push(date.toLocaleString('en-US', { month: 'long' }));
			preparedData.push(d.views);
			preparedBgColor.push(curColor + ', 0.2)');
			preparedBorderColor.push(curColor + ', 0.8)');
		});

		var ctx = document.getElementById('myChart').getContext('2d');
		ctx.canvas.width = 300;
		ctx.canvas.height = 200;
		var myChart = new Chart(ctx, {
			type: 'bar',
			data: {
				labels: preparedLabel,
				datasets: [
					{
						label: 'Total penjualan',
						data: preparedData,
						backgroundColor: preparedBgColor,
						borderColor: preparedBorderColor,
						borderWidth: 1
					}
				]
			},
			options: {
				scales: {
					yAxes: {
						ticks: {
							beginAtZero: true
						}
					}
				}
			}
		});
	};

	onMount(() => {
		getDashboard();
	});
</script>

<div id="after-login-layout">
	<NavbarAdmin />
	<div class="flex">
		<Sidebar statusPointer="Dashboard" pagePointer="mitra" />
		<div class="w-100 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="title-content">Dashboard</div>
				<div class="flex flex-direction-col flex-gap-semi-large">
					<div class="sub-title-content">Ringkasan</div>
					<div class="flex flex-gap-large">
						<div class="card flex flex-center-horizontal flex-center-vertical flex-gap-semi-small">
							<div class="box-icon flex flex-center-horizontal flex-center-vertical">
								<People />
							</div>
							<div class="flex flex-direction-col">
								<div class="title-small-card-dashboard">Total Pelamar</div>
								<div class="flex flex-center-vertical flex-gap-small">
									<div class="value-small-card-dashboard">{countNup}</div>
									<div class="unit-small-card-dashboard">Orang</div>
								</div>
							</div>
						</div>
						<div class="card flex flex-center-horizontal flex-center-vertical flex-gap-semi-small">
							<div class="box-icon flex flex-center-horizontal flex-center-vertical">
								<Check />
							</div>
							<div class="flex flex-direction-col">
								<div class="title-small-card-dashboard">Diterima</div>
								<div class="flex flex-center-vertical flex-gap-small">
									<div class="value-small-card-dashboard">{countPemberkasan}</div>
									<div class="unit-small-card-dashboard">Orang</div>
								</div>
							</div>
						</div>
						<div class="card flex flex-center-horizontal flex-center-vertical flex-gap-semi-small">
							<div class="box-icon flex flex-center-horizontal flex-center-vertical">
								<Clock />
							</div>
							<div class="flex flex-direction-col">
								<div class="title-small-card-dashboard">Ditunda</div>
								<div class="flex flex-center-vertical flex-gap-small">
									<div class="value-small-card-dashboard">{countPengajuan}</div>
									<div class="unit-small-card-dashboard">Orang</div>
								</div>
							</div>
						</div>
						<div class="card flex flex-center-horizontal flex-center-vertical flex-gap-semi-small">
							<div class="box-icon flex flex-center-horizontal flex-center-vertical">
								<X />
							</div>
							<div class="flex flex-direction-col">
								<div class="title-small-card-dashboard">Cancel</div>
								<div class="flex flex-center-vertical flex-gap-small">
									<div class="value-small-card-dashboard">{countGriya}</div>
									<div class="unit-small-card-dashboard">Griya</div>
								</div>
							</div>
						</div>
					</div>
					<div class="flex flex-gap-regular">
						<div class="card w-50">
							<div class="title-card-dashboard">Penjualan Tahun Ini</div>
							<div style="width: 100%;"><canvas id="myChart"></canvas></div>
						</div>
						<div class="flex flex-direction-col flex-gap-semi-large w-50">
							<div class="flex flex-direction-col flex-gap-small">
								<div class="title-card-dashboard">Notifikasi</div>
								<div class="flex flex-gap-regular">
									<span
										class={active == 0 ? 'active-notif-button' : 'unactive-notif-button'}
										on:click={() => {
											active = 0;
										}}>Belum Dibaca</span
									>
									<span
										class={active == 1 ? 'active-notif-button' : 'unactive-notif-button'}
										on:click={() => {
											active = 1;
										}}>Sudah Dibaca</span
									>
								</div>
							</div>
							<div class="scroll-notif">
								{#if active == 0}
									<div
										class="flex flex-direction-col flex-gap-regular"
										in:fly={{ y: -20, duration: 600 }}
									>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold">
												Pelamar a/n Reza Astari Putra telah di approve
											</span>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
									</div>
								{:else}
									<div
										class="flex flex-direction-col flex-gap-regular"
										in:fly={{ y: -20, duration: 600 }}
									>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold">
												Pelamar a/n Reza Astari Putra telah di approve
											</span>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
									</div>
								{/if}
							</div>
						</div>
					</div>
					<div class="flex flex-gap-regular">
						<div class="card w-50">
							<div class="title-card-dashboard">Penjualan Tahun Ini</div>
							<div style="width: 100%;"><canvas id="myChart"></canvas></div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	#after-login-layout {
		display: flex;
		flex-direction: column;
		width: 100%;
	}

	.title-content {
		font-size: 24px;
		font-weight: bold;
	}

	.sub-title-content {
		font-size: 20px;
		font-weight: bold;
	}

	.card {
		background: #fff;
		border-radius: 8px;
		padding: 16px;
		width: 125px;
		height: 125px;
		box-shadow: 0 1px 2px rgba(0, 0, 0, 0.01);
	}

	.box-icon {
		width: 40px;
		height: 40px;
		background-color: #e0e0e0;
		border-radius: 50%;
	}

	.title-small-card-dashboard,
	.value-small-card-dashboard,
	.unit-small-card-dashboard,
	.text-notif,
	.text-notif-bold,
	.text-notif-desc,
	.title-card-dashboard {
		font-size: 14px;
	}

	.title-small-card-dashboard {
		font-weight: bold;
	}

	.value-small-card-dashboard {
		font-size: 24px;
		font-weight: bold;
	}

	.unit-small-card-dashboard {
		font-size: 14px;
	}

	.text-notif {
		color: #757575;
	}

	.text-notif-bold {
		font-weight: bold;
	}

	.text-notif-desc {
		color: #616161;
	}

	.title-card-dashboard {
		font-size: 18px;
		font-weight: bold;
	}

	.flex {
		display: flex;
	}

	.flex-direction-col {
		flex-direction: column;
	}

	.flex-gap-large {
		gap: 32px;
	}

	.flex-gap-semi-large {
		gap: 16px;
	}

	.flex-gap-regular {
		gap: 24px;
	}

	.flex-gap-small {
		gap: 8px;
	}

	.flex-center-horizontal {
		justify-content: center;
	}

	.flex-center-vertical {
		align-items: center;
	}

	.flex-between-horizontal {
		justify-content: space-between;
	}

	.w-50 {
		width: 50%;
	}

	.w-100 {
		width: 100%;
	}

	.content {
		padding: 16px;
	}

	.scroll-notif {
		overflow-y: auto;
		max-height: 400px;
	}

	.active-notif-button,
	.unactive-notif-button {
		cursor: pointer;
		padding: 8px 16px;
		border-radius: 16px;
		font-size: 14px;
	}

	.active-notif-button {
		background-color: #007bff;
		color: #fff;
	}

	.unactive-notif-button {
		background-color: #e0e0e0;
		color: #616161;
	}
</style>
