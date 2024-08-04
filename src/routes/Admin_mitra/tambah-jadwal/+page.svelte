<script>
	import Sidebar from '../../../components/Sidebar.svelte';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import Button from '../../../components/Button.svelte';
	import axios from 'axios';
	import { onMount } from 'svelte';

	let tanggal = '';
	let tempat = '';
	let jam = '';
	let selectedUserIds = [];
	let users = [];

	function toggleUserSelection(userId, isChecked) {
		if (isChecked) {
			selectedUserIds = [...selectedUserIds, userId];
		} else {
			selectedUserIds = selectedUserIds.filter(id => id !== userId);
		}
	}

	// Fungsi untuk mendapatkan hari dari tanggal
	function getHariFromTanggal(tanggal) {
		const hariArray = ['Minggu', 'Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu'];
		const date = new Date(tanggal);
		return hariArray[date.getDay()];
	}

	async function fetchUsers() {
		try {
			let token = localStorage.getItem('token');
			const response = await axios.get('https://sinaker.pocari.id/api/recruitments', {
				headers: {
					Authorization: `Bearer ${token}`
				}
			});
			users = response.data;
			console.log(users);
		} catch (error) {
			console.error('Error fetching users:', error);
		}
	}

	async function tambahJadwal() {
		try {
			let token = localStorage.getItem('token');
			const response = await axios.post('http://127.0.0.1:8000/api/jadwal/add', {
				tanggal: tanggal,
				tempat: tempat,
				jam: jam,
				user_ids: selectedUserIds
			}, {
				headers: {
					Authorization: `Bearer ${token}`
				}
			});
			if (response.status === 201) {
				alert('Jadwal berhasil ditambahkan');
				// Clear form fields after successful submission
				tanggal = '';
				tempat = '';
				jam = '';
				selectedUserIds = [];
			}
		} catch (error) {
			console.error('Error:', error);
			if (error.response) {
				console.error('Response data:', error.response.data);
				console.error('Response status:', error.response.status);
				console.error('Response headers:', error.response.headers);
			}
			alert('Gagal menambahkan jadwal');
		}
	}

	// Fetch users when the component is mounted
	onMount(() => {
		fetchUsers();
	});
</script>

<NavbarAdmin />
<div class="flex">
	<Sidebar pagePointer="mitra" />
	<div class="w-100 content p-4">
		<div class="container">
			<h2 class="mb-4">Tambah Jadwal</h2>
			<form on:submit|preventDefault={tambahJadwal}>
				<div class="tabel-jadwal mb-3">
					<label for="tanggal" class="form-label">Tanggal</label>
					<input type="date" class="form-control" id="tanggal" bind:value={tanggal} required />
				</div>
				<div class="tabel-jadwal mb-3">
					<label for="tempat" class="form-label">Tempat</label>
					<input type="text" class="form-control" id="tempat" bind:value={tempat} required />
				</div>
				<div class="tabel-jadwal mb-3">
					<label for="jam" class="form-label">Jam</label>
					<input type="text" class="form-control" id="jam" bind:value={jam} placeholder="08:00 - 10:00" required />
				</div>
				<div class="tabel-jadwal mb-3">
					<label class="form-label">Pilih Pelamar</label>
					{#each users as user}
						<div>
							<input type="checkbox" id="{user.user.ID_user}" value="{user.user.ID_user}" on:change={e => toggleUserSelection(user.user.ID_user, e.target.checked)} />
							<label for="{user.user.ID_user}">{user.user.info.name}</label>
						</div>
					{/each}
				</div>
				<Button type="submit" classList="btn-tambah">Tambah Jadwal</Button>
			</form>
		</div>
	</div>
</div>

<style>
	.tabel-jadwal {
		display: flex;
		flex-direction: column;
	}
	.content {
		padding: 2rem;
		background-color: #f8f9fa;
		min-height: 100vh;
	}

	.container {
		max-width: 600px;
		padding: 2rem;
		background-color: #f8f9fa;
		border-radius: 8px;
	}

	h2 {
		color: #333;
		text-align: center;
	}

	.mb-3 {
		margin-bottom: 1.5rem !important;
	}

	.form-label {
		margin-bottom: 0.5rem;
		font-weight: 500;
		color: #495057;
	}

	.btn-primary {
		background-color: #007bff;
		border-color: #007bff;
		width: 100%;
		padding: 0.75rem;
		font-size: 1rem;
		border-radius: 8px;
	}
</style>
