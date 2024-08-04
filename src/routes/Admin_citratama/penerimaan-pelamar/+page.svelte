<script>
	import Sidebar from '../../../components/Sidebar.svelte';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import Button from '../../../components/Button.svelte';
	import axios from 'axios';
	import { onMount } from 'svelte';
	import { CheckCircle, XCircle } from 'svelte-bootstrap-icons';
	import { fly } from 'svelte/transition';
	import Swal from 'sweetalert2';

	let data, name, id_user;
	let user = {};
	let status = false;
	let recruitment = {};

	async function recruitUser(id, status) {
		try {
			const response = await axios.post(
				`https://sinaker.pocari.id/api/admin/approve/penerimaan/${id}`,
				{
					status
				}
			);
			fetchRecruit();
			if (response.status === 200) {
				Swal.fire({
					title: 'Success!',
					text: 'Pelamar berhasil ',
					icon: 'success',
					confirmButtonText: 'OK'
				});
			}
			console.log('Recruitment successful:', response.data);
			data.sort((a, b) => {
				return new Date(b.updated_at) - new Date(a.updated_at); // Sorting descending by updated_at
			});
			// Handle success (optional)
		} catch (error) {
			console.error('Recruitment failed:', error);
			// Handle error response here (e.g., show error message)
		}
	}

	const fetchRecruit = () => {
		axios
			.get('https://sinaker.pocari.id/api/admin/recruitment', {})
			.then((response) => {
				console.log('Response dari API:', response); // Tambahkan log untuk melihat response lengkap
				status = true;
				data = response.data;

				data.sort((a, b) => {
					return new Date(b.updated_at) - new Date(a.updated_at); // Sorting descending by updated_at
				});
				console.log(data);
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};
	onMount(() => {
		fetchRecruit();
	});

	const handleSilang = async (ID_user, action) => {
		const result = await Swal.fire({
			title: 'Apakah kamu yakin?',
			text: 'Kamu tidak bisa mengembalikan proses ini!',
			icon: 'warning',
			showCancelButton: true,
			confirmButtonText: 'Iya, Tolak Rekrutkmen!',
			cancelButtonText: 'Tidak, batalkan!',
			reverseButtons: true
		});

		if (result.isConfirmed) {
			await recruitUser(ID_user, action);
		} else if (result.dismiss === Swal.DismissReason.cancel) {
			Swal.fire('Dibatalkan', 'Proses rekrutmen dibatalkan', 'error');
		}
	};
	const handleCentang = async (ID_user, action) => {
		const result = await Swal.fire({
			title: 'Apakah kamu yakin?',
			text: 'Kamu tidak bisa mengembalikan proses ini!',
			icon: 'warning',
			showCancelButton: true,
			confirmButtonText: 'Iya, rekrut!',
			cancelButtonText: 'Tidak, batalkan!',
			reverseButtons: true
		});

		if (result.isConfirmed) {
			await recruitUser(ID_user, action);
		} else if (result.dismiss === Swal.DismissReason.cancel) {
			Swal.fire('Dibatalkan', 'Proses rekrutmen dibatalkan', 'error');
		}
	};
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
							<div class="flex flex-gap-small flex-center-vertical w-15">
								<div class="text-drop-card">Status</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-15">
								<div class="text-drop-card">Aksi</div>
							</div>
						</div>
					</div>
					{#if status}
						{#each data as d}
							{#if d.status === 'menunggu'}
								<div class="card w-100 height-fit">
									<div class="flex flex-direction-col flex-gap-regular">
										<div class="flex flex-gap-regular">
											<div class="flex flex-gap-small flex-center-vertical w-10">
												<div class="text-drop-card">{d.user.info.name}</div>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-15">
												<div class="text-drop-card">{d.user.info.klasifikasi_pilihan}</div>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-20">
												<div class="text-drop-card">{d.user.info.sub_klasifikasi_pilihan}</div>
											</div>

											<div class="flex flex-gap-small flex-center-vertical w-20">
												<div class="text-drop-card">{d.perusahaan_mitra.info.name}</div>
											</div>

											<div class="flex flex-gap-regular flex-center-vertical w-10">
												<a
													href={`/Admin_mitra/detail-pelamar?id=${d.user.ID_user}`}
													class="text-blue">Detail</a
												>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-15">
												<Button classList="btn-pending">{d.info_penerimaan}</Button>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-15">
												{#if d.info_penerimaan === 'menunggu'}
													<div
														class="check-circle"
														on:click={() => handleCentang(d.ID_recruitment, 'centang')}
													>
														<CheckCircle style="width: 18px; height: 18px;" />
													</div>
													<div
														class="x-circle"
														on:click={() => handleSilang(d.ID_recruitment, 'silang')}
													>
														<XCircle style="width: 18px; height: 18px;" />
													</div>
												{:else}
													<div>Successful</div>
												{/if}
											</div>
										</div>
									</div>
								</div>
							{:else if d.info !== 'ditolak'}
								<div class="card w-100 height-fit">
									<div class="flex flex-direction-col flex-gap-regular">
										<div class="flex flex-gap-regular">
											<div class="flex flex-gap-small flex-center-vertical w-10">
												<div class="text-drop-card">{d.user.info.name}</div>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-15">
												<div class="text-drop-card">{d.user.info.klasifikasi_pilihan}</div>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-20">
												<div class="text-drop-card">{d.user.info.sub_klasifikasi_pilihan}</div>
											</div>

											<div class="flex flex-gap-small flex-center-vertical w-20">
												<div class="text-drop-card">{d.perusahaan_mitra.info.name}</div>
											</div>

											<div class="flex flex-gap-regular flex-center-vertical w-10">
												<a
													href={`/Admin_mitra/detail-pelamar?id=${d.user.ID_user}`}
													class="text-blue">Detail</a
												>
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-15">
												{#if d.info_penerimaan === 'ditolak'}
													<Button classList="btn-danger">{d.info_penerimaan}</Button>
												{:else if d.info_penerimaan === 'diterima'}
													<Button classList="btn-success">{d.info_penerimaan}</Button>
												{:else}{/if}
											</div>
											<div class="flex flex-gap-small flex-center-vertical w-15">
												{#if d.info_penerimaan === 'menunggu'}
													<div
														class="check-circle"
														on:click={() => recruitUser(d.ID_recruitment, 'centang')}
													>
														<CheckCircle style="width: 18px; height: 18px;" />
													</div>
													<div
														class="x-circle"
														on:click={() => recruitUser(d.ID_recruitment, 'silang')}
													>
														<XCircle style="width: 18px; height: 18px;" />
													</div>
												{:else}
													<div>Successful</div>
												{/if}
											</div>
										</div>
									</div>
								</div>
							{/if}
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

<style>
	.check-circle {
		color: #198754;
		cursor: pointer;
	}
	.x-circle {
		color: #dc3545;
		cursor: pointer;
	}
</style>
