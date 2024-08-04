<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import { onMount } from 'svelte';
	import { fly, scale } from 'svelte/transition';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import axios from 'axios';
	import Button from '../../../components/Button.svelte';
	import Swal from 'sweetalert2';

	let status = false;
	let data;

	const fetchUserRecruitments = () => {
	
		let token = localStorage.getItem('token');
		axios
			.get('https://sinaker.pocari.id/api/recruitments', {
				headers: {
					Authorization: `Bearer ${token}`
				}
			})
			.then((response) => {
				data = response.data;
				console.log(data);
				status = true;
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});	
};
onMount(() => {
	fetchUserRecruitments();
});
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
						<button class="btn-outline flex flex-center-vertical flex-gap-small"
							><span>Download Data Pelamar</span>
							<img src="/images/icons/File_Download.svg" /></button
						>
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
						{#each data as d}
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
                                            <a href={`/Admin_mitra/detail-pelamar?id=${d.user.ID_user}`} class="text-blue">Detail</a>

                                        </div>

										{#if d.recruitment.info === 'menunggu'}
											<Button classList="btn-pending">{d.recruitment.info}</Button>
										{:else if d.recruitment.info === 'diterima'}
											<Button classList="btn-success">{d.recruitment.info}</Button>
										{:else}
											<Button classList="btn-danger">{d.recruitment.info}</Button>
										{/if}
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
