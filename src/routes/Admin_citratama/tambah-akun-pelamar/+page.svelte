<script>
	import Navbar from '../../../components/Navbar-admin.svelte';
	import Sidebar from '../../../components/Sidebar.svelte';
	import axios from 'axios';
	import { ArrowLeft } from 'svelte-bootstrap-icons';

	let email = '';
	let password = '';
	let role = '';
	let name = '';
	let address = '';
	let birthDate = '';
	let birthPlace = '';
	let phoneNumber = '';
	let classification = '';
	let subClassification = '';
	let photoFile = null;
	let photoUrl = '';

	function handleFileUpload(event) {
		const file = event.target.files[0];
		if (file) {
			photoFile = file;
			const reader = new FileReader();
			reader.onload = (e) => {
				photoUrl = e.target.result;
			};
			reader.readAsDataURL(file);
		}
	}

	async function handleSubmit() {
		const formData = new FormData();
		formData.append('email', email);
		formData.append('password', password);
		formData.append('role', role);
		formData.append('name', name);
		formData.append('alamat', address);
		formData.append('tempat_tanggal_lahir', `${birthPlace},${birthDate}`); // Gabungkan tempat dan tanggal lahir
		formData.append('no_hp', phoneNumber);
		formData.append('klasifikasi_pilihan', classification);
		formData.append('sub_klasifikasi_pilihan', subClassification);
		if (photoFile) {
			formData.append('photo', photoFile);
		}

		try {
			const response = await axios.post('https://sinaker.pocari.id/api/admin/tambah-pelamar', formData, {
				headers: {
					'Content-Type': 'multipart/form-data',
					Authorization: `Bearer ${localStorage.getItem('token')}`
				},
			});
			alert('Data berhasil ditambahkan!');
			console.log(response.data);

			// Reset form fields
			email = '';
			password = '';
			role = '';
			name = '';
			address = '';
			birthDate = '';
			birthPlace = '';
			phoneNumber = '';
			classification = '';
			subClassification = '';
			photoFile = null;
			photoUrl = '';
		} catch (error) {
			if (error.response && error.response.data) {
				// Display server-side validation errors
				alert(`Error: ${JSON.stringify(error.response.data)}`);
			} else {
				console.error('Error adding user:', error);
				alert('Terjadi kesalahan saat menambahkan data!');
			}
		}
	}

	function goBack() {
		window.location.href = '/Admin_citratama/pelamar';
	}
</script>

<Navbar />
<div class="main-content">
	<Sidebar statusPointer="pelamar" pagePointer="ams" />
	<div class="main-container">
		<div class="form-container">
			<div class="back-button" on:click={goBack}>
				<ArrowLeft/>
			</div>
			<h1>Tambah Pelamar</h1>
			<form on:submit|preventDefault={handleSubmit}>
				<div class="form-group">
					<label for="email">Email</label>
					<input type="email" id="email" bind:value={email} placeholder="Masukkan email" required />
				</div>
				<div class="form-group">
					<label for="password">Password</label>
					<input type="password" id="password" bind:value={password} placeholder="Masukkan password" required />
				</div>
				<div class="form-group">
					<label for="role">Role</label>
					<input type="text" id="role" bind:value={role} placeholder="Masukkan role" required />
				</div>
				<div class="form-group">
					<label for="name">Nama</label>
					<input type="text" id="name" bind:value={name} placeholder="Masukkan nama pelamar" required />
				</div>
				<div class="form-group">
					<label for="address">Alamat</label>
					<input type="text" id="address" bind:value={address} placeholder="Masukkan alamat pelamar" />
				</div>
				<div class="form-group">
					<label for="birthDate">Tanggal Lahir</label>
					<input type="date" id="birthDate" bind:value={birthDate} />
				</div>
				<div class="form-group">
					<label for="birthPlace">Tempat Lahir</label>
					<input type="text" id="birthPlace" bind:value={birthPlace} placeholder="Masukkan tempat lahir" />
				</div>
				<div class="form-group">
					<label for="phoneNumber">No Handphone</label>
					<input type="text" id="phoneNumber" bind:value={phoneNumber} placeholder="Masukkan no handphone" />
				</div>
				<div class="form-group">
					<label for="classification">Klasifikasi</label>
					<select id="classification" bind:value={classification}>
						<option value="">Pilih Klasifikasi</option>
						<option value="teknik informatika">Teknik Informatika</option>
						<!-- Add your options here -->
					</select>
				</div>
				<div class="form-group">
					<label for="subClassification">Sub Klasifikasi</label>
					<select id="subClassification" bind:value={subClassification}>
						<option value="">Pilih Sub Klasifikasi</option>
						<option value="komputer">Komputer</option>
						<!-- Add your options here -->
					</select>
				</div>
				<div class="form-group">
					<label for="photo">Unggah Foto</label>
					<input type="file" id="photo" accept="image/*" on:change={handleFileUpload} />
				</div>
				{#if photoUrl}
					<div class="form-group">
						<img src={photoUrl} alt="Preview" class="image-preview" />
					</div>
				{/if}
				<button type="submit" class="btn btn-primary">Tambahkan Pelamar</button>
			</form>
		</div>
	</div>
</div>






<style>
	.main-container {
	  display: flex;
	  margin: 0;
	  padding: 0;
	  width: 100vh;
	}

	.form-container {
	  flex: 1;
	  max-width: 600px;
	  margin: 50px auto;
	  padding: 20px;
	  border-radius: 8px;
	  background-color: #f9f9f9;
	  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	  position: relative;
	}

	.back-button {
	  position: absolute;
	  top: 20px;
	  left: 20px;
	  cursor: pointer;
	}

	.back-button img {
	  width: 24px;
	  height: 24px;
	}

	h1 {
	  color: #333;
	  margin-bottom: 20px;
	  text-align: center;
	}

	.form-group {
	  margin-bottom: 20px;
	}

	label {
	  display: block;
	  margin-bottom: 5px;
	  color: #333;
	}

	input,
	textarea,
	select {
	  width: 100%;
	  padding: 10px;
	  border-radius: 4px;
	  border: 1px solid #ccc;
	  box-sizing: border-box;
	}

	input:focus,
	textarea:focus,
	select:focus {
	  border-color: #485ee9;
	  outline: none;
	}

	.btn {
	  display: inline-block;
	  padding: 10px 20px;
	  font-size: 16px;
	  color: white;
	  background-color: #485ee9;
	  border: none;
	  border-radius: 4px;
	  cursor: pointer;
	  text-align: center;
	}

	.btn-primary {
	  background-color: #485ee9;
	}

	.btn-primary:hover {
	  background-color: #3b4fc6;
	}

	.main-content {
	  display: flex;
	  flex-direction: row;
	  gap: 200px;
	}
</style>
