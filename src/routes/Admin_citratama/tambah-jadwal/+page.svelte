<script>
	import Sidebar from '../../../components/Sidebar.svelte';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import Button from '../../../components/Button.svelte';
	let tanggal = '';
	let hari = '';
	let tempat = '';
	let jam = '';
</script>

<NavbarAdmin />
<div class="flex">
	<Sidebar pagePointer="ams" />
	<div class="w-100 content p-4">
		<div class="container">
			<h2 class="mb-4">Tambah Jadwal</h2>
			<form>
				<div class=" tabel-jadwal mb-3">
					<label for="tanggal" class="form-label">Tanggal</label>
					<input type="date" class="form-control" id="tanggal" bind:value={tanggal} required />
				</div>
				<div class="tabel-jadwal mb-3">
					<label for="hari" class="form-label">Hari</label>
					<input type="text" class="form-control" id="hari" bind:value={hari} required />
				</div>
				<div class="tabel-jadwal mb-3">
					<label for="tempat" class="form-label">Tempat</label>
					<input type="text" class="form-control" id="tempat" bind:value={tempat} required />
				</div>
				<div class="tabel-jadwal mb-3">
					<label for="jam" class="form-label">Jam</label>
					<input type="time" class="form-control" id="jam" bind:value={jam} required />
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
