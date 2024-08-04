<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import axios from 'axios';
	import Button from '../../../components/Button.svelte';
	import { CheckCircle, XCircle } from 'svelte-bootstrap-icons';
	import Swal from 'sweetalert2';
	let status = false;
	let data = [];

	async function recruitUser(id, action) {
		let token = localStorage.getItem('token');
		let status = action === 'check' ? 'centang' : 'silang';
		try {
			const response = await axios.post(
				`https://sinaker.pocari.id/api/recruit/confirm/${id}`,
				{ status },
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			);
			fetchRecruitment();
			console.log('Recruitment successful:', response.data);
			if (response.status === 200) {
				Swal.fire({
					title: 'Success!',
					text: 'Pelamar berhasil ',
					icon: 'success',
					confirmButtonText: 'OK'
				});
			}
			const index = data.findIndex((item) => item.recruitment.ID_recruitment === id);
			if (index !== -1) {
				data[index].success = true; // Menandai bahwa rekruitmen berhasil
			}
		} catch (error) {
			console.error('Recruitment failed:', error);
		}
	}

	let token = localStorage.getItem('token');

	const fetchRecruitment = () => {
		axios
			.get('https://sinaker.pocari.id/api/recruitments', {
				headers: {
					Authorization: `Bearer ${token}`
				}
			})
			.then((response) => {
				data = response.data.filter((item) => item.recruitment.info === 'diterima');
				console.log('Filtered Data:', data);
				status = true;
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};
	onMount(() => {
		fetchRecruitment();
	});

	const handleSilang = async (ID_user, action) => {
        const result = await Swal.fire({
            title: 'Apakah kamu yakin?',
            text: "Kamu tidak bisa mengembalikan proses ini!",
            icon: 'warning',
            showCancelButton: true,
            confirmButtonText: 'Iya, Tolak Rekrutkmen!',
            cancelButtonText: 'Tidak, batalkan!',
            reverseButtons: true
        });

        if (result.isConfirmed) {
            await recruitUser(ID_user, action);
        } else if (result.dismiss === Swal.DismissReason.cancel) {
            Swal.fire(
                'Dibatalkan',
                'Proses rekrutmen dibatalkan',
                'error'
            );
        }
    };
     const handleCentang = async (ID_user, action) => {
        const result = await Swal.fire({
            title: 'Apakah kamu yakin?',
            text: "Kamu tidak bisa mengembalikan proses ini!",
            icon: 'warning',
            showCancelButton: true,
            confirmButtonText: 'Iya, rekrut!',
            cancelButtonText: 'Tidak, batalkan!',
            reverseButtons: true
        });

        if (result.isConfirmed) {
            await recruitUser(ID_user, action);
        } else if (result.dismiss === Swal.DismissReason.cancel) {
            Swal.fire(
                'Dibatalkan',
                'Proses rekrutmen dibatalkan',
                'error'
            );
        }
    };
</script>

<div id="after-login-layout">
	<NavbarAdmin />
	<div class="flex">
		<Sidebar statusPointer="Nup" pagePointer="mitra" />
		<div class="w-80 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="flex flex-between-horizontal w-100">
					<div class="title-content">Daftar Pelamar Yang ditawarkan</div>
					<div class="flex flex-gap-regular">
						<button class="btn-outline flex flex-center-vertical flex-gap-small">
							<span>Download Data Pelamar</span>
							<img src="/images/icons/File_Download.svg" />
						</button>
					</div>
				</div>
				<div class="flex flex-direction-col flex-gap-regular">
					<div class="card w-100 height-fit">
						<div class="flex flex-gap-regular">
							<div class="flex flex-gap-small flex-center-vertical w-10">
								<div class="text-drop-card">NPK</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
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
								<div class="text-drop-card">Pendidikan</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-10">
								<div class="text-drop-card">Info</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-10">
								<div class="text-drop-card">Aksi</div>
							</div>
						</div>
					</div>

					{#if status}
						{#each data as d}
							<!-- Bagian centang atau silang -->
							{#if d.recruitment.info === 'diterima' && d.recruitment.info_penerimaan === null}
								<div class="card w-100 height-fit">
									<div class="flex flex-direction-col flex-gap-regular">
										<div class="flex flex-gap-regular">
											<div class="flex flex-gap-small flex-center-vertical w-10">
												<div class="text-drop-card">3000{d.user.ID_user}</div>
											</div>
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
												<div class="text-drop-card">{d.user.info.pendidikan}</div>
											</div>
											<div class="flex flex-gap-regular flex-center-vertical w-10">
												<a
													href={`/Admin_mitra/detail-pelamar?id=${d.user.ID_user}`}
													class="text-blue">Detail</a
												>
											</div>
											<div class="flex flex-gap-regular flex-center-vertical w-10">
												<div
													class="check-circle"
													on:click={() => handleCentang(d.recruitment.ID_recruitment, 'check')}
												>
													<CheckCircle style="width: 18px; height: 18px;" />
												</div>
												<div
													class="x-circle"
													on:click={() => handleSilang(d.recruitment.ID_recruitment, 'cross')}
												>
													<XCircle style="width: 18px; height: 18px;" />
												</div>
											</div>
										</div>
									</div>
								</div>
							{/if}
						{/each}
						<!-- Bagian button status lainnya -->
						{#each data as d}
							{#if d.recruitment.info !== 'diterima' || d.recruitment.info_penerimaan !== null}
								<div class="card w-100 height-fit">
									<div class="flex flex-direction-col flex-gap-regular">
										<div class="flex flex-gap-regular">
											<div class="flex flex-gap-small flex-center-vertical w-10">
												<div class="text-drop-card">3000{d.user.ID_user}</div>
											</div>
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
												<div class="text-drop-card">{d.user.info.pendidikan}</div>
											</div>
											<div class="flex flex-gap-regular flex-center-vertical w-10">
												<a
													href={`/Admin_mitra/detail-pelamar?id=${d.user.ID_user}`}
													class="text-blue">Detail</a
												>
											</div>

											<div class="flex flex-gap-small flex-center-vertical w-10">
												{#if d.recruitment.info_penerimaan === 'menunggu'}
													<Button classList="btn-pending">Menunggu</Button>
												{:else if d.recruitment.info_penerimaan === 'diterima'}
													<Button classList="btn-success">Diterima</Button>
												{:else}
													<Button classList="btn-danger">Ditolak</Button>
												{/if}
											</div>
										</div>
									</div>
								</div>
							{/if}
						{/each}
					{:else}
						<p>Loading...</p>
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
	.text-successful {
		color: #198754;
		font-weight: bold;
	}
</style>
