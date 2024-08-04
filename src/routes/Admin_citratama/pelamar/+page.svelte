<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import Navbar from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import { fly, scale } from 'svelte/transition';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import axios from 'axios';
	import Button from '../../../components/Button.svelte';
	
	let data, name, id_user;
	let user = {};
	let status = false;
	let recruitment = {};

	const sortUserByUpdateDate = (users) =>{
		return users.sort((a,b) => new Date(b.updated_at) - new Date(a.updated_at))
	}

	onMount(() => {
		axios
			.get('https://sinaker.pocari.id/api/userStatus ', {})
			.then((response) => {
				console.log('Response dari API:', response); // Tambahkan log untuk melihat response lengkap
				status = true;
				data = response.data;
				user = sortUserByUpdateDate(data.users);
				console.log('User:', user);
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	});
</script>

<div id="after-login-layout">
	<NavbarAdmin />
	<div class="flex">
		<Sidebar statusPointer="Nup" pagePointer="ams" />
		<div class="w-100 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="flex flex-between-horizontal w-100">
					<div class="title-content">Daftar Semua Pelamar Kerja</div>
					<div class="flex flex-gap-regular">
						<button class="btn-outline flex flex-center-vertical flex-gap-small">
							<span>Download Data Pelamar</span>
							<img src="/images/icons/File_Download.svg" />
						</button>
					</div>
				</div>
				<div class="flex flex-gap-regular">
					<button class="btn-outline flex flex-center-vertical flex-gap-small">
						<span>Tambah Pelamar Kerja</span>
					</button>
				</div>
				<div class="flex flex-direction-col flex-gap-regular">
					<div class="card w-100 height-fit">
						<div class="flex flex-gap-regular">
							<div class="flex flex-gap-small flex-center-vertical w-10">
								<div class="text-drop-card">Nama</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-15">
								<div class="text-drop-card">Kualifikasi Pilihan</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Sub Kualifikasi Pilihan</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Perusahaan</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-10">
								<div class="text-drop-card">Info</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-10">
								<div class="text-drop-card">Status</div>
							</div>
						</div>
					</div>
					{#if status}
						{#each user as d}
							<div class="card w-100 height-fit">
								<div class="flex flex-direction-col flex-gap-regular">
									<div class="flex flex-gap-regular">
										<div class="flex flex-gap-small flex-center-vertical w-10">
											<div class="text-drop-card">{d.info.name}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-15">
											<div class="text-drop-card">{d.info.klasifikasi_pilihan}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">{d.info.sub_klasifikasi_pilihan}</div>
										</div>

										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">{d.recruitments.perusahaanmitra}</div>
										</div>
										<div class="flex flex-gap-regular flex-center-vertical w-10">
											<a href={`/Admin_mitra/detail-pelamar?id=${d.ID_user}`} class="text-blue"
												>Detail</a
											>
										</div>
										<div class="flex flex-gap-regular flex-center-vertical w-10">
											{#if d.recruitments.length > 0}
												{#if d.recruitments[0].status === "menunggu"}
													<Button classList="btn-pending">Menunggu</Button>
													{:else if d.recruitments[0].status ==="tersedia"}
													<Button classList="btn-success">Tersedia</Button>
													{:else if d.recruitments[0].status ==="tidak tersedia"}
													<Button classList="btn-danger">Tidak Tersedia</Button>
												{/if}
											{/if}
										</div>
									</div>
								</div>
							</div>
						{/each}
					{/if}

					<div class="card w-100 height-fit">
						<div class="flex flex-between-horizontal">
							<div class="flex flex-gap-regular flex-center-vertical">
								<div class="text-display-sort">Menampilkan</div>
								<select class="select-sort">
									<option>10</option>
								</select>
								<div class="text-display-sort">dari <span class="bold-number">28</span> NUP</div>
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
		</div>
	</div>
</div>
