<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import { fly, scale } from 'svelte/transition';
	import axios from 'axios';
	import Button from '../../../components/Button.svelte';
	let data;
	let status = false;
	let selectedJadwal = null;

	function getDayName(dateString) {
		const days = ['Minggu', 'Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu'];
		const date = new Date(dateString);
		return days[date.getDay()];
	}

	axios
		.get('https://sinaker.pocari.id/api/jadwal', {})
		.then((response) => {
			data = response.data;
			console.log(data);
			status = true;
		})
		.catch((error) => {
			console.error('Ada kesalahan:', error);
		});

	let showModal = false;

	function openModal(jadwal) {
		selectedJadwal = jadwal;
		showModal = true;
	}

	function closeModal() {
		showModal = false;
	}

	function handleClickOutside(event) {
		if (event.target === event.currentTarget) {
			closeModal();
		}
	}
	function tambahJadwal(){
		window.location.href="/Admin_mitra/tambah-jadwal"
	}
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
						<button class="btn-outline flex flex-center-vertical flex-gap-small"
							><span>Download Data Pelamar</span>
							<img src="/images/icons/File_Download.svg" /></button
						>
					</div>
				</div>
				<div class="flex flex-between-horizontal w-100 mt-4">
					<div class="flex flex-gap-regular">
						<button class="btn-outline flex flex-center-vertical flex-gap-small" on:click={tambahJadwal}
							><span>Tambah Jadwal</span></button
						>
					</div>
				</div>
				<div class="flex flex-direction-col flex-gap-regular">
					<div class="card height-fit" style="width: max-content;">
						<div class="flex flex-gap-regular">
							<div class="flex flex-gap-small flex-center-vertical" style="width: 100px;">
								<div class="text-drop-card">Tanggal</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical" style="width: 100px;">
								<div class="text-drop-card">Hari</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical" style="width: 100px;">
								<div class="text-drop-card">Jam</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20" style="width: 120px;">
								<div class="text-drop-card">Tempat</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-15" style="width: 150px;">
								<div class="text-drop-card">Penerima Jadwal</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							
							<div class="flex flex-gap-small flex-center-vertical w-10" style="width: 100px;">
								<div class="text-drop-card">Action</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical" style="width: 120px;">
								<div class="text-drop-card">Status</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
						</div>
					</div>
					{#if status}
						{#each data as d}
							<div class="card w-100 height-fit" style="width: fit-content;">
								<div class="flex flex-direction-col flex-gap-regular">
									<div class="flex flex-gap-regular">
										<div class="flex flex-gap-small flex-center-vertical" style="width: 100px;">
											<div class="text-drop-card">{d.tanggal}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical" style="width: 100px;">
											<div class="text-drop-card">{getDayName(d.tanggal)}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical" style="width: 100px;">
											<div class="text-drop-card">Tanggal</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical" style="width: 120px;">
											<div class="text-drop-card">{d.tempat}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical" style="width: 150px;">
											<div class="text-drop-card">
												<button class="btn-penerima" on:click={() => openModal(d)}>Open Modal</button>
											</div>
										</div>
										<div class="flex flex-gap-regular flex-center-vertical" style="width: 100px;">
											<a href="" class="text-blue">Detail</a>
										</div>
										<div class="flex flex-gap-small flex-center-vertical" style="width: 120px;">
											<div class="text-drop-card">
												<Button classList="btn-success">Terkirim</Button>
											</div>
										</div>
									</div>
								</div>
							</div>
						{/each}
					{/if}
				</div>
			</div>
		</div>
	</div>
</div>

{#if showModal}
	<div class="modal" on:click={handleClickOutside}>
		<!-- Modal content -->
		<div class="modal-content" in:fly={{ y: 200, duration: 400 }} out:fly={{ y: 200, duration: 400 }}>
			<span class="close" on:click={closeModal}>&times;</span>
			<h3>Penerima Jadwal</h3>
			<hr />
			<p>
				{#if selectedJadwal}
					{#each selectedJadwal.penerima_jadwal as penerima}
						<div class="" style="width: 150px;">
							<div class="text-drop-card"><li>{penerima.user.info.name}</li></div>
						</div>
					{/each}
				{/if}
			</p>
		</div>
	</div>
{/if}

<style>
	.btn-penerima {
		color: black;
		background-color: #fff;
		font-size: 12px;
		align-items: center;
		border: 1px solid black;
		box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.125);
		width: 110px;
		height: 34px;
		padding: 0%;
		border-radius: 8px;
	}
	.btn-penerima:hover {
		color: blue;
		border-color: blue;
	}
	.modal {
		position: fixed;
		z-index: 1;
		padding-top: 100px;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		overflow: auto;
		background-color: rgba(0, 0, 0, 0.4);
		
	}
	hr {
		margin-bottom: 14px;
	}
	.modal-content li {
		padding-top: 8px;
	}
	.modal-content {
		background-color: #fefefe;
		margin: auto;
		padding: 20px;
		border: 1px solid #888;
		width: 332px;
		height: fit-content;
		position: relative; /* Menetapkan posisi relatif untuk konten modal */
		border-radius: 8px;
		transition: transform 0.3s ease;
	}

	.close {
		color: #aaaaaa;
		position: absolute; /* Mengatur posisi absolut untuk tombol close */
		top: 10px; /* Jarak dari atas */
		right: 20px; /* Jarak dari kanan */
		font-size: 28px;
		font-weight: bold;
		cursor: pointer;
	}

	.close:hover,
	.close:focus {
		color: #000;
		text-decoration: none;
	}
</style>
