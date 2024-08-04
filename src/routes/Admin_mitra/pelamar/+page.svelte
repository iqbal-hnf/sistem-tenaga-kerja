<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import Navbar from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import { fly, scale } from 'svelte/transition';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import axios from 'axios';
	import { CheckCircle } from 'svelte-bootstrap-icons';
	import Swal from 'sweetalert2';
	let data = [];
	let status = false;
	let nama;

	const recruitUser = async (ID_user) => {
		try {
			let token = localStorage.getItem('token');
			const response = await axios.post(
				'https://sinaker.pocari.id/api/recruit',
				{
					ID_user: ID_user
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			);
			if (response.status === 200) {
				Swal.fire({
					title: 'Success!',
					text: 'Pelamar berhasil ',
					icon: 'success',
					confirmButtonText: 'OK'
				});
			}
			console.log('Recruitment successful:', response.data);
			fetchUserTersedia();
			
		} catch (error) {
			console.error('Recruitment failed:', error);
			
		}
	};
    const handleRecruit = async (ID_user) => {
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
            await recruitUser(ID_user);
        } else if (result.dismiss === Swal.DismissReason.cancel) {
            Swal.fire(
                'Dibatalkan',
                'Proses rekrutmen dibatalkan',
                'error'
            );
        }
    };
	const fetchUserTersedia = () => {
		axios
			.get('https://sinaker.pocari.id/api/userTersedia')
			.then((response) => {
				data = response.data;
				status = true;
				nama = data.alamat;
				console.log(data);
				console.log(nama);
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	onMount(() => {
		fetchUserTersedia();
	});
</script>

<div id="after-login-layout">
	<NavbarAdmin />
	<div class="flex">
		<Sidebar statusPointer="Nup" pagePointer="mitra" />
		<div class="w-80 content">
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
				<div class="flex flex-gap-regular"></div>
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
								<img src="/images/icons/Arrow.svg" />
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
							<div class="card w-100 height-fit">
								<div class="flex flex-direction-col flex-gap-regular">
									<div class="flex flex-gap-regular">
										<div class="flex flex-gap-small flex-center-vertical w-10">
											<div class="text-drop-card">3000{d.ID_user}</div>
										</div>
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
											<div class="text-drop-card">{d.info.pendidikan}</div>
										</div>
										<div class="flex flex-gap-regular flex-center-vertical w-10">
											<a href={`/Admin_mitra/detail-pelamar?id=${d.ID_user}`} class="text-blue"
												>Detail</a
											>
										</div>
										<div class="flex flex-gap-regular flex-center-vertical w-10">
											<div class="ceklis" on:click={() => handleRecruit(d.ID_user)}>
												<CheckCircle />
											</div>
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

<style>
	.ceklis {
		cursor: pointer;
	}
	.ceklis:hover {
		color: blue;
	}
</style>
