<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import Navbar from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import { fly, scale } from 'svelte/transition';
	import { each } from 'svelte/internal';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import Chatbot from '../../../components/Chatbotwidget.svelte';
	let active = 0;

	
	let countNup = null;
	let countPemberkasan = null;
	let countPengajuan = null;
	let countGriya = null;
	let countUnit = null;
	let yearlySale = null;



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
	<Chatbot/>
	<NavbarAdmin />
	<div class="flex">
		<Sidebar active="Dashboard" pagePointer="ams" />
		<div class="w-100 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="title-content">Dashboard</div>
				<div class="flex flex-direction-col flex-gap-semi-large">
					<div class="sub-title-content">Ringkasan</div>
					<div class="flex flex-gap-large">
						<div class="card flex flex-center-horizontal flex-center-vertical flex-gap-semi-small">
							<div class="box-icon flex flex-center-horizontal flex-center-vertical">
								<svg
									width="24"
									height="24"
									viewBox="0 0 24 24"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<path
										d="M12 12C14.4853 12 16.5 9.98528 16.5 7.5C16.5 5.01472 14.4853 3 12 3C9.51472 3 7.5 5.01472 7.5 7.5C7.5 9.98528 9.51472 12 12 12ZM15 7.5C15 9.15685 13.6569 10.5 12 10.5C10.3431 10.5 9 9.15685 9 7.5C9 5.84315 10.3431 4.5 12 4.5C13.6569 4.5 15 5.84315 15 7.5Z"
										fill="black"
									/>
									<path
										d="M21 19.5C21 21 19.5 21 19.5 21H4.5C4.5 21 3 21 3 19.5C3 18 4.5 13.5 12 13.5C19.5 13.5 21 18 21 19.5ZM19.5 19.4948C19.4978 19.1246 19.2693 18.0157 18.2518 16.9982C17.2734 16.0198 15.4336 15 12 15C8.56632 15 6.72653 16.0198 5.74815 16.9982C4.73063 18.0157 4.50214 19.1246 4.5 19.4948H19.5Z"
										fill="black"
									/>
								</svg>
							</div>
							<div class="flex flex-direction-col">
								<div class="title-small-card-dashboard">Total Pelamar</div>
								<div class="flex flex-center-vertical flex-gap-small">
									<div class="value-small-card-dashboard">{countNup == null ? 0 : countNup}</div>
									<div class="unit-small-card-dashboard">Orang</div>
								</div>
							</div>
						</div>
						<div class="card flex flex-center-horizontal flex-center-vertical flex-gap-semi-small">
							<div class="box-icon flex flex-center-horizontal flex-center-vertical">
								<svg
									width="24"
									height="24"
									viewBox="0 0 48 50"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<rect width="47.5572" height="24" rx="8" fill="#F5F6FD" />
									<path
										d="M16 25.3535L20.9497 30.3033L31.5572 19.6968"
										stroke="#172426"
										stroke-width="2"
										stroke-linecap="round"
										stroke-linejoin="round"
									/>
								</svg>
							</div>
							<div class="flex flex-direction-col">
								<div class="title-small-card-dashboard">Diterima</div>
								<div class="flex flex-center-vertical flex-gap-small">
									<div class="value-small-card-dashboard">
										{countPemberkasan == null ? 0 : countPemberkasan}
									</div>
									<div class="unit-small-card-dashboard">Orang</div>
								</div>
							</div>
						</div>
						<div class="card flex flex-center-horizontal flex-center-vertical flex-gap-semi-small">
							<div class="box-icon flex flex-center-horizontal flex-center-vertical">
								<svg
									width="56"
									height="50"
									viewBox="0 0 56 50"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<rect width="56" height="50" rx="8" fill="#F5F6FD" />
									<path
										d="M28.7724 14.5284C28.516 14.5095 28.2584 14.5 28 14.5V13C28.2953 13 28.5897 13.0109 28.8828 13.0325L28.7724 14.5284ZM31.7789 15.2036C31.2978 15.018 30.8037 14.8681 30.3006 14.7551L30.6292 13.2916C31.2042 13.4207 31.7689 13.592 32.3187 13.8041L31.7789 15.2036ZM33.8335 16.2696C33.6187 16.126 33.3991 15.9908 33.1754 15.8641L33.9148 14.559C34.1705 14.7038 34.4213 14.8583 34.6668 15.0224C34.9123 15.1864 35.1511 15.359 35.3828 15.5398L34.4599 16.7224C34.2572 16.5642 34.0483 16.4131 33.8335 16.2696ZM36.5846 18.954C36.2877 18.5324 35.9602 18.1333 35.6046 17.7598L36.691 16.7255C37.0973 17.1523 37.4717 17.6085 37.811 18.0903L36.5846 18.954ZM37.7007 20.9818C37.6019 20.7431 37.4945 20.5087 37.3789 20.2791L38.7187 19.6047C38.8508 19.8671 38.9736 20.135 39.0866 20.4078C39.1995 20.6806 39.3022 20.9568 39.3943 21.2358L37.9701 21.7063C37.8894 21.4622 37.7996 21.2205 37.7007 20.9818ZM38.4968 24.7423C38.4842 24.2268 38.4336 23.713 38.3454 23.2049L39.8233 22.9485C39.9241 23.5291 39.9819 24.1164 39.9964 24.7055L38.4968 24.7423ZM38.2982 27.0484C38.3487 26.795 38.3896 26.5405 38.421 26.2853L39.9098 26.4689C39.8738 26.7606 39.827 27.0515 39.7694 27.3411C39.7118 27.6307 39.6437 27.9173 39.5653 28.2006L38.1197 27.8005C38.1882 27.5527 38.2478 27.3019 38.2982 27.0484ZM36.871 30.6175C37.1468 30.1818 37.3902 29.7264 37.5992 29.255L38.9705 29.8629C38.7317 30.4016 38.4535 30.9221 38.1382 31.42L36.871 30.6175ZM35.4246 32.4246C35.6073 32.2419 35.7828 32.053 35.9507 31.8583L37.0865 32.8381C36.8946 33.0606 36.6941 33.2765 36.4853 33.4853L35.4246 32.4246Z"
										fill="black"
									/>
									<path
										d="M28 14.5C26.2733 14.5 24.5732 14.9258 23.0503 15.7398C21.5275 16.5538 20.2289 17.7308 19.2696 19.1665C18.3102 20.6022 17.7198 22.2524 17.5506 23.9708C17.3813 25.6892 17.6385 27.4229 18.2993 29.0182C18.9601 30.6135 20.0041 32.0212 21.3389 33.1166C22.6737 34.212 24.258 34.9614 25.9516 35.2982C27.6451 35.6351 29.3956 35.5491 31.048 35.0479C32.7004 34.5466 34.2036 33.6456 35.4246 32.4246L36.4853 33.4853C35.0899 34.8807 33.3719 35.9104 31.4834 36.4833C29.595 37.0561 27.5944 37.1544 25.6589 36.7694C23.7234 36.3844 21.9127 35.528 20.3873 34.2761C18.8618 33.0242 17.6686 31.4154 16.9134 29.5922C16.1583 27.769 15.8644 25.7877 16.0578 23.8238C16.2512 21.8599 16.926 19.974 18.0224 18.3332C19.1187 16.6923 20.6028 15.3472 22.3432 14.4169C24.0836 13.4867 26.0266 13 28 13V14.5Z"
										fill="black"
									/>
									<path
										d="M27.25 17.5C27.6642 17.5 28 17.8358 28 18.25V26.0648L32.8721 28.8488C33.2317 29.0543 33.3567 29.5125 33.1512 29.8721C32.9457 30.2317 32.4875 30.3567 32.1279 30.1512L26.8779 27.1512C26.6442 27.0177 26.5 26.7691 26.5 26.5V18.25C26.5 17.8358 26.8358 17.5 27.25 17.5Z"
										fill="black"
									/>
								</svg>
							</div>
							<div class="flex flex-direction-col">
								<div class="title-small-card-dashboard">Ditunda</div>
								<div class="flex flex-center-vertical flex-gap-small">
									<div class="value-small-card-dashboard">
										{countPengajuan == null ? 0 : countPengajuan}
									</div>
									<div class="unit-small-card-dashboard">Orang</div>
								</div>
							</div>
						</div>
						<div class="card flex flex-center-horizontal flex-center-vertical flex-gap-semi-small">
							<div class="box-icon flex flex-center-horizontal flex-center-vertical">
								<svg
									width="56"
									height="50"
									viewBox="0 0 56 50"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<rect width="56" height="50" rx="8" fill="#F5F6FD" />
									<path
										d="M28 35.5C22.201 35.5 17.5 30.799 17.5 25C17.5 19.201 22.201 14.5 28 14.5C33.799 14.5 38.5 19.201 38.5 25C38.5 30.799 33.799 35.5 28 35.5ZM28 37C34.6274 37 40 31.6274 40 25C40 18.3726 34.6274 13 28 13C21.3726 13 16 18.3726 16 25C16 31.6274 21.3726 37 28 37Z"
										fill="black"
									/>
									<path
										d="M22.9697 19.9697C23.2626 19.6768 23.7374 19.6768 24.0303 19.9697L28 23.9393L31.9697 19.9697C32.2626 19.6768 32.7374 19.6768 33.0303 19.9697C33.3232 20.2626 33.3232 20.7374 33.0303 21.0303L29.0607 25L33.0303 28.9697C33.3232 29.2626 33.3232 29.7374 33.0303 30.0303C32.7374 30.3232 32.2626 30.3232 31.9697 30.0303L28 26.0607L24.0303 30.0303C23.7374 30.3232 23.2626 30.3232 22.9697 30.0303C22.6768 29.7374 22.6768 29.2626 22.9697 28.9697L26.9393 25L22.9697 21.0303C22.6768 20.7374 22.6768 20.2626 22.9697 19.9697Z"
										fill="black"
									/>
								</svg>
							</div>
							<div class="flex flex-direction-col">
								<div class="title-small-card-dashboard">Cancel</div>
								<div class="flex flex-center-vertical flex-gap-small">
									<div class="value-small-card-dashboard">
										{countGriya == null ? 0 : countGriya}
									</div>
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
											<span class="text-notif-bold"
												>Pelamar a/n Reza Astari Putra telah di approve</span
											>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold"
												>Pelamar a/n Reza Astari Putra telah di approve</span
											>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold"
												>Pelamar a/n Reza Astari Putra telah di approve</span
											>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold"
												>Pelamar a/n Reza Astari Putra telah di approve</span
											>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold"
												>Pelamar a/n Reza Astari Putra telah di approve</span
											>
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
												<span class="text-notif">Dari HO</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold">Pelamar a/n Reza Astari Putra telah di approve</span>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold">Pelamar a/n Reza Astari Putra telah di approve</span>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold">Pelamar a/n Reza Astari Putra telah di approve</span>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold">Pelamar a/n Reza Astari Putra telah di approve</span>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold">Pelamar a/n Reza Astari Putra telah di approve</span>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
										<div class="card flex flex-direction-col flex-gap-small w-100">
											<div class="flex flex-between-horizontal">
												<span class="text-notif">Dari Sistem</span>
												<span class="text-notif">08 : 00</span>
											</div>
											<span class="text-notif-bold">Pelamar a/n Reza Astari Putra telah di approve</span>
											<div class="text-notif-desc">
												Pelamar a/n Reza Astari Putra telah di approve oleh PT. Citratama Indonesia.
												Silahkan masukkan jadwal untuk pelamar dan jika jadwal masih belum
												diketahui, tinggalkan catatan untuk pelamar.
											</div>
										</div>
									</div>
								{/if}
							</div>
							<div class="card w-100 height-fit">
								<div class="flex flex-between-horizontal">
									<div class="flex flex-gap-regular flex-center-vertical">
										<div class="text-display-sort">Menampilkan</div>
										<select class="select-sort">
											<option>10</option>
										</select>
										<div class="text-display-sort">
											dari <span class="bold-number">3</span> Notifikasi
										</div>
									</div>
									<div class="flex flex-gap-regular flex-center-vertical">
										<div class="flex flex-center-vertical flex-center-horizontal border-pagination">
											<img src="/images/icons/Arrow_Left.svg" />
										</div>
										<div class="flex flex-center-vertical flex-center-horizontal border-pagination">
											<div class="text-display-sort bold-number">1</div>
										</div>
										<div class="flex flex-center-vertical flex-center-horizontal border-pagination">
											<img src="/images/icons/Arrow_Right.svg" />
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
					<div class="flex flex-gap-regular">
						<div class="card w-50">
							<div class="title-card-dashboard">Piechart disini</div>
							<div style="width: 100%;"><canvas id="myChart"></canvas></div>
						</div>
						<div class="flex flex-direction-col flex-gap-semi-large w-50">
							<div class="flex flex-direction-col flex-gap-regular">
								<div class="card w-100 height-fit">
									<div class="flex flex-gap-regular">
										<div class="flex flex-gap-small flex-center-vertical w-10">
											<div class="text-drop-card">NPK</div>
											<img src="/images/icons/Arrow.svg" />
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-15">
											<div class="text-drop-card">Nama</div>  
											<img src="/images/icons/Arrow.svg" />
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-10">
											<div class="text-drop-card">Detail</div>
											<img src="/images/icons/Arrow.svg" />
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">Perusahaan</div>
											<img src="/images/icons/Arrow.svg" />
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">Aksi</div>
										</div>
									</div>
								</div>
								<div class="card w-100 height-fit">
									<div class="flex flex-direction-col flex-gap-regular">
										<div class="flex flex-gap-regular">
											<div class="flex flex-gap-small flex-center-vertical w-10">
												<div class="text-drop-card">30001</div>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-15">
												<div class="text-drop-card">Suryadi</div>
											</div>
											
											<div class="flex flex-gap-regular flex-center-vertical w-15">
												<a href="" class="text-blue">Detail</a>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-15">
												<div class="text-drop-card">PT. Air Kampar</div>
											</div>
											<div class="flex flex-gap-regular flex-center-vertical w-15">
												<svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
													<path d="M8 15C4.13401 15 1 11.866 1 8C1 4.13401 4.13401 1 8 1C11.866 1 15 4.13401 15 8C15 11.866 11.866 15 8 15ZM8 16C12.4183 16 16 12.4183 16 8C16 3.58172 12.4183 0 8 0C3.58172 0 0 3.58172 0 8C0 12.4183 3.58172 16 8 16Z" fill="#A8B6F7"/>
													<path d="M10.9697 4.96967C10.9626 4.97674 10.9559 4.98423 10.9498 4.9921L7.4774 9.41674L5.38388 7.32322C5.09098 7.03033 4.61611 7.03033 4.32322 7.32322C4.03032 7.61612 4.03032 8.09099 4.32322 8.38388L6.96966 11.0303C7.26256 11.3232 7.73743 11.3232 8.03032 11.0303C8.03685 11.0238 8.043 11.0169 8.04876 11.0097L12.041 6.01947C12.3232 5.72582 12.3196 5.25897 12.0303 4.96967C11.7374 4.67678 11.2626 4.67678 10.9697 4.96967Z" fill="#A8B6F7"/>
													</svg>
													<svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
														<path d="M8 15C4.13401 15 1 11.866 1 8C1 4.13401 4.13401 1 8 1C11.866 1 15 4.13401 15 8C15 11.866 11.866 15 8 15ZM8 16C12.4183 16 16 12.4183 16 8C16 3.58172 12.4183 0 8 0C3.58172 0 0 3.58172 0 8C0 12.4183 3.58172 16 8 16Z" fill="#E7515A"/>
														<path d="M4.64645 4.64645C4.84171 4.45118 5.15829 4.45118 5.35355 4.64645L8 7.29289L10.6464 4.64645C10.8417 4.45118 11.1583 4.45118 11.3536 4.64645C11.5488 4.84171 11.5488 5.15829 11.3536 5.35355L8.70711 8L11.3536 10.6464C11.5488 10.8417 11.5488 11.1583 11.3536 11.3536C11.1583 11.5488 10.8417 11.5488 10.6464 11.3536L8 8.70711L5.35355 11.3536C5.15829 11.5488 4.84171 11.5488 4.64645 11.3536C4.45118 11.1583 4.45118 10.8417 4.64645 10.6464L7.29289 8L4.64645 5.35355C4.45118 5.15829 4.45118 4.84171 4.64645 4.64645Z" fill="#E7515A"/>
														</svg>
																											
											</div>
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
