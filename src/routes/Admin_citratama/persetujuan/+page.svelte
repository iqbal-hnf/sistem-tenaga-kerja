<script>
	import Sidebar from '../../../components/Sidebar.svelte';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import axios from 'axios';
	import Button from '../../../components/Button.svelte';
	import { CheckCircle, XCircle } from 'svelte-bootstrap-icons';
	import Swal from 'sweetalert2';
	let user = {};
	let status = false;

	async function recruitUser(id, status) {
		try {
			const response = await axios.post(`https://sinaker.pocari.id/api/admin/approve/${id}`, {
				status
			});
            if (response.status === 200) {
				Swal.fire({
					title: 'Success!',
					text: 'Pelamar berhasil ',
					icon: 'success',
					confirmButtonText: 'OK'
				});
			}
			console.log('Recruitment successful:', response.data);
			fetchUserStatus();
		} catch (error) {
			console.error('Recruitment failed:', error);
		}
	}

	const fetchUserStatus = () => {
		axios
			.get('https://sinaker.pocari.id/api/userStatus', {})
			.then((response) => {
				console.log('Response dari API:', response);
				status = true;
				user = response.data.users;
				console.log('User:', user);

				user.forEach((d) => {
					if (d.recruitments && d.recruitments.length > 0) {
						d.recruitments.sort((a, b) => new Date(b.info.updated_at) - new Date(a.info.updated_at));
					}
				});
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	onMount(() => {
		fetchUserStatus();
	});

    
    const handleSilang = async (ID_user,status) => {
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
            await recruitUser(ID_user,status);
        } else if (result.dismiss === Swal.DismissReason.cancel) {
            Swal.fire(
                'Dibatalkan',
                'Proses rekrutmen dibatalkan',
                'error'
            );
        }
    };
     const handleCentang = async (ID_user,status) => {
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
            await recruitUser(ID_user,status);
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
		<Sidebar statusPointer="Nup" pagePointer="ams" />
		<div class="w-100 content">
			<div class="flex flex-direction-col flex-gap-large">
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
							<div class="flex flex-gap-small flex-center-vertical w-10">
								<div class="text-drop-card">Aksi</div>
							</div>
						</div>
					</div>

					{#if status}
						<!-- Render entri dengan status "menunggu" terlebih dahulu -->
						{#each user as d}
							{#if d.recruitments.length > 0}
								{#each d.recruitments.filter(rec => rec.info === 'menunggu') as rec}
									<div class="card w-100 height-fit">
										<div class="flex flex-direction-col flex-gap-regular">
											<div class="flex flex-gap-regular">
												<div class="flex flex-gap-small flex-center-vertical w-10">
													<div class="text-drop-card">{rec.user.info.name}</div>
												</div>
												<div class="flex flex-gap-small flex-center-vertical w-15">
													<div class="text-drop-card">{rec.user.info.klasifikasi_pilihan}</div>
												</div>
												<div class="flex flex-gap-small flex-center-vertical w-20">
													<div class="text-drop-card">{rec.user.info.sub_klasifikasi_pilihan}</div>
												</div>
												<div class="flex flex-gap-small flex-center-vertical w-20">
													<div class="text-drop-card">{rec.perusahaanmitra.info.name}</div>
												</div>
												<div class="flex flex-gap-regular flex-center-vertical w-10">
													<a href="" class="text-blue">Detail</a>
												</div>
												<div class="flex flex-gap-small flex-center-vertical w-15">
													<Button classList="btn-pending">{rec.info}</Button>
												</div>
												<div class="flex flex-gap-regular flex-center-vertical w-10">
													<div
														class="check-circle"
														on:click={() => handleCentang(rec.ID_recruitment, 'centang')}
													>
														<CheckCircle style="width: 18px; height: 18px;" />
													</div>
													<div
														class="x-circle"
														on:click={() => handleSilang(rec.ID_recruitment, 'silang')}
													>
														<XCircle style="width: 18px; height: 18px;" />
													</div>
												</div>
											</div>
										</div>
									</div>
								{/each}
							{/if}
						{/each}

						<!-- Render entri dengan status selain "menunggu" -->
						{#each user as d}
							{#if d.recruitments.length > 0}
								{#each d.recruitments.filter(rec => rec.info !== 'menunggu').sort((a, b) => new Date(b.info.updated_at) - new Date(a.info.updated_at)) as rec}
									<div class="card w-100 height-fit">
										<div class="flex flex-direction-col flex-gap-regular">
											<div class="flex flex-gap-regular">
												<div class="flex flex-gap-small flex-center-vertical w-10">
													<div class="text-drop-card">{rec.user.info.name}</div>
												</div>
												<div class="flex flex-gap-small flex-center-vertical w-15">
													<div class="text-drop-card">{rec.user.info.klasifikasi_pilihan}</div>
												</div>
												<div class="flex flex-gap-small flex-center-vertical w-20">
													<div class="text-drop-card">{rec.user.info.sub_klasifikasi_pilihan}</div>
												</div>
												<div class="flex flex-gap-small flex-center-vertical w-20">
													<div class="text-drop-card">{rec.perusahaanmitra.info.name}</div>
												</div>
												<div class="flex flex-gap-regular flex-center-vertical w-10">
													<a href="" class="text-blue">Detail</a>
												</div>
												<div class="flex flex-gap-small flex-center-vertical w-15">
													{#if rec.info === 'diterima'}
														<Button classList="btn-success">{rec.info}</Button>
													{:else if rec.info === 'ditolak'}
														<Button classList="btn-danger">{rec.info}</Button>
													{:else if !rec.status}
														<Button classList="btn-success">Tersedia</Button>
													{:else}
														<Button classList="btn-danger">{rec.status}</Button>
													{/if}
												</div>
												<div class="flex flex-gap-regular flex-center-vertical w-10">
													<div>Successful</div>
												</div>
											</div>
										</div>
									</div>
								{/each}
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
