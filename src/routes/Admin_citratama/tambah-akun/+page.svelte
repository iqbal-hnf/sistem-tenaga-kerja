<script>
	import Sidebar from '../../../components/Sidebar.svelte';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import { fly, scale } from 'svelte/transition';
	import axios from 'axios';
	import Button from '../../../components/Button.svelte';

	let email = '';
	let password = '';
	let namaPerusahaan = '';
	let alamat = '';
	let noHandphone = '';
	let bidangUsaha = '';
	let role = 'Mitra';

	const tambahAkun = async () => {
		try {
			const response = await axios.post('https://sinaker.pocari.id/api/admin/tambah-mitra', {
				email: email,
				password: password,
				name: namaPerusahaan,
				alamat: alamat,
				no_hp: noHandphone,
				bidang_usaha: bidangUsaha,
				role: role
			});

			if (response.status === 201) {
				alert('Akun perusahaan berhasil ditambahkan');
				// Redirect atau lakukan sesuatu setelah berhasil menambah akun
				window.location.href = '/Admin_citratama/akun-perusahaan'; // Redirect ke halaman akun perusahaan
			} else {
				alert('Gagal menambahkan akun perusahaan');
			}
		} catch (error) {
			console.error('Ada kesalahan:', error);
			alert('Terjadi kesalahan, silakan coba lagi');
		}
	};
</script>

<div id="after-login-layout">
	<NavbarAdmin />
	<div class="flex">
		<Sidebar active="Tambah Akun Perusahaan" pagePointer="ams" />
		<div class="container">
			<div class="w-100 content">
				<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
					<div class="flex flex-between-horizontal w-100">
						<div class="title-content">Tambah Akun Perusahaan</div>
					</div>
					<div class="form-group">
						<input type="email" bind:value={email} placeholder="Email" />
						<input type="password" bind:value={password} placeholder="Password" />
					</div>

					<div class="form-group">
						<input type="text" bind:value={namaPerusahaan} placeholder="Nama Perusahaan" />
					</div>
					<div class="form-group">
						<input type="text" bind:value={alamat} placeholder="Alamat" />
					</div>
					<div class="form-group">
						<input type="text" bind:value={noHandphone} placeholder="No Handphone" />
					</div>
					<div class="form-group">
						<input type="text" bind:value={bidangUsaha} placeholder="Bidang Usaha" />
					</div>
					<div class="form-group">
						<select bind:value={role}>
							<option value="Mitra">Mitra</option>
							<option value="Admin">Admin</option>
						</select>
					</div>
					<div>
						<Button classList="btn-tambah" onClick={tambahAkun} style="">Tambah Akun</Button>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	.form-group {
		margin-bottom: 20px;
		display: flex;
		flex-direction: row;
		width: max;
		gap: 5px;
	}

	.form-group input,
	.form-group select {
		width: 100%;
		padding: 8px;
		border: 1px solid #ccc;
		border-radius: 8px;
	}
	.container {
		background-color: white;
		display: flex;
		flex-direction: column;
		width: 40%;
		margin-left: 100px;
		margin-top: 10px;
		border: 1px solid #ccc;
		border-radius: 8px;
	}
</style>
