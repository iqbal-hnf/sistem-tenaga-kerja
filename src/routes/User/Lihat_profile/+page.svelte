<script>
	import Button from '../../../components/Button.svelte';
    import Navbar from'../../../components/Navbar.svelte';
	import { Geo, Envelope,PlusLg,Pencil} from 'svelte-bootstrap-icons';
	let showPersonalSummary = false;
	let showEducation = false;
	let showJobHistory = false;
	let showLicenses = false;
	let showSkills = false;
	let showLanguages = false;

	let personalSummary = '';
	let education = '';
	let jobHistory = '';
	let licenses = '';
	let skills = '';
	let languages = '';

	const togglePersonalSummary = () => {
		showPersonalSummary = !showPersonalSummary;
	};

	const toggleEducation = () => {
		showEducation = !showEducation;
	};

	const toggleJobHistory = () => {
		showJobHistory = !showJobHistory;
	};

	const toggleLicenses = () => {
		showLicenses = !showLicenses;
	};

	const toggleSkills = () => {
		showSkills = !showSkills;
	};

	const toggleLanguages = () => {
		showLanguages = !showLanguages;
	};

	const savePersonalSummary = () => {
		alert('Personal Summary Saved: ' + personalSummary);
		showPersonalSummary = false;
	};

	const saveEducation = () => {
		alert('Education Saved: ' + education);
		showEducation = falsex;
	};

	const saveJobHistory = () => {
		alert('Job History Saved: ' + jobHistory);
		showJobHistory = false;
	};

	const saveLicenses = () => {
		alert('Licenses Saved: ' + licenses);
		showLicenses = false;
	};

	const saveSkills = () => {
		alert('Skills Saved: ' + skills);
		showSkills = false;
	};

	const saveLanguages = () => {
		alert('Languages Saved: ' + languages);
		showLanguages = false;
	};
</script>
<Navbar/>
<div class="container">
	<div class="header">
		<div class="h-tulisan">
			<h1>Muhammad Iqbal Hanafi</h1>
			<p class="p-env"><Envelope />Pekanbaru, Riau</p>
			<p class="p-mail"><Geo />hanafi20@mahasiswa.per.ac.id</p>
		</div>
		<div class="h-button">
			<Button classList="btn-card-header">Submit</Button>
		</div>
	</div>
	<div class="flex-row">
		<div class="col-6">
			<div class="section">
				<h2>Ringkasan Pribadi</h2>
				<p class="btn-teks">
					Tambahkan ringkasan pribadi ke profile untuk memperkenalkan diri Anda
				</p>
				{#if showPersonalSummary}
					<textarea bind:value={personalSummary} placeholder="Tambahkan ringkasan..."></textarea>
					<Button classList="btn-section" onClick={savePersonalSummary}>Simpan Ringkasan</Button>
				{:else}
					<Button classList="btn-section" onClick={togglePersonalSummary}>Tambah Ringkasan</Button>
				{/if}
			</div>

			<div class="section">
				<h2 class="teks-cls">Pendidikan</h2>
				<p class="btn-teks">Beritahu pendidikan mengenai pendidikan anda</p>
				{#if showEducation}
					<textarea bind:value={education} placeholder="Beritahu pendidikan..."></textarea>
					<Button classList="btn-section" onclick={saveEducation}>Simpan Pendidikan</Button>
				{:else}
					<Button classList="btn-section" onclick={toggleEducation}>Tambah Pendidikan</Button>
				{/if}
			</div>

			<div class="section">
				<h2 class="teks-cls">Riwayat Karir</h2>
				<p class="btn-teks">
					Semakin anda memberi tahu perusahaan mengenai pengalaman Anda, Semakin Anda bisa tampil
					menonjol.
				</p>
				{#if showJobHistory}
					<textarea bind:value={jobHistory} placeholder="Tambahkan riwayat karir..."></textarea>
					<Button classList="btn-section" onClick={saveJobHistory}>Simpan Jabatan</Button>
				{:else}
					<Button classList="btn-section" onClick={toggleJobHistory}>Tambah Jabatan</Button>
				{/if}
			</div>

			<div class="section">
				<h2 class="teks-cls">Lisensi dan Sertifikasi</h2>
				<p class="btn-teks">
					Tunjukkan kredensial profesional Anda, Tambahkan lisensi, sertifikat, keanggotaan, dan
					akreditasi Anda yang relevan di sini.
				</p>
				{#if showLicenses}
					<textarea bind:value={licenses} placeholder="Tambahkan lisensi..."></textarea>
					<Button classList="btn-section" onClick={saveLicenses}>
						Simpan Lisensi dan sertifikasi</Button
					>
				{:else}
					<Button classList="btn-section" onClick={toggleLicenses}>
						Tambah lisensi dan sertifikasi</Button
					>
				{/if}
			</div>

			<div class="section">
				<h2 class="teks-cls">Keahlian</h2>
				<p class="btn-teks">Beri tahu perusahaan betapa beharganya keahlian anda bagi mereka</p>
				{#if showSkills}
					<textarea bind:value={skills} placeholder="Beritahu keahlian..."></textarea>
					<Button classList="btn-section" onClick={saveSkills}>Simpan Keahlian</Button>
				{:else}
					<Button classList="btn-section" onClick={toggleSkills}>Tambah Keahlian</Button>
				{/if}
			</div>

			<div class="section">
				<h2 class="teks-cls">Bahasa</h2>
				<p class="btn-teks">
					Tambahkan bahasa untuk menarik lebih banyak perusahaan dan pemberi kerja
				</p>
				{#if showLanguages}
					<textarea bind:value={languages} placeholder="Tambahkan bahasa..."></textarea>
					<Button classList="btn-section" onClick={saveLanguages}>Simpan Bahasa</Button>
				{:else}
					<Button classList="btn-section" onClick={toggleLanguages}>Tambah Bahasa</Button>
				{/if}
			</div>
		</div>
		<div class="col-6">
			<!-- <div class="profile-card">
				<h3>Visibilitas profil</h3>
				<p>Dapat dicari oleh perusahaan</p>
				<h3>Kekuatan Profil</h3>
				<p>Anda 50% lebih mungkin dihubungi perusahaan jika menambahkan resume.</p>
				<button>Tambah Resume</button>
			</div> -->

			<div class="profile-card-data-diri">
				<h3 class="h3-teks-card">Ketersediaan <PlusLg/></h3>
				<p class="p-teks-card">Tidak Ditentukan</p>
				<h3 class="h3-teks-card">Lokasi <Pencil/></h3>
				<p class="p-teks-card">Pekanbaru, Riau</p>
				<h3 class="h3-teks-card">Alamat Lengkap<PlusLg/></h3>
				<p class="p-teks-card">Belum Tersedia</p>
				<h3 class="h3-teks-card">Tempat, Tanggal Lahir<Pencil/></h3>
				<p class="p-teks-card">Tenggaron, 29 Maret 2002</p>
				<h3 class="h3-teks-card">Klasifikasi yang diminati<Pencil/></h3>
				<p class="p-teks-card">Teknologi Informasi dan Komunikasi, Teknik Perangkat Lunak</p>
				<h3 class="h3-teks-card">No Handphone<Pencil/></h3>
				<p style="font-size: 14px; font-weight: 250; padding-bottom: 10px; margin-bottom: 20px;;">082389252034 </p>
			</div>
		</div>
	</div>
</div>

<style>
	/* Add your styles here */
	.container {
		max-width: 1250px;
		border-radius: 200px;
		margin: auto;
		display: flex;
		flex-direction: column;
		padding: 20px;
		font-family: 'poppins', sans-serif;
		gap: 60px;
	}
	h2 {
		font-size: 24px;
		font-weight: 600;
	}
	.h3-teks-card {
		padding-bottom: 10px;
		font-size: 16px;
		font-weight: 700;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        margin-right: 20px;
        
	}
    
	.p-teks-card {
		font-size: 14px;
		font-weight: 250;
		padding-bottom: 25px;
		margin-bottom: 25px;
		border-bottom: 1px solid rgba(147, 152, 178, 0.8);
		margin-right: 20px;
	}

	.header {
		background-image: url('/image.png');
		background-size: cover;
		background-position: center;
		height: 271px;
		color: white;
		padding: 50px;
		border-radius: 20px;
		display: flex;
		flex-direction: column;
		gap: 45px;
	}

	.section {
		margin-bottom: 20px;
	}
	.profile-card {
		border: 1px solid #718284;
		margin-left: 125px;
		margin-bottom: 50px;
	}

	.profile-card-data-diri {
		border: 1px solid #718284;
		box-shadow: 0 1px 6px rgba(0, 0, 0, 0.25);
		padding-left: 25px;
		padding-top: 32px;
		border-radius: 20px;
		margin-left: 125px;
		width: 480px;
		height: fit-content;
	}
	.p-env {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 10px;
	}
	.p-mail {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 10px;
	}
	.flex-row {
		display: flex;
		flex-wrap: wrap;
	}
	.col-6 {
		flex: 0 0 50%;
		max-width: 50%;
	}
	.btn-teks {
		margin-top: 9px;
		font-weight: 250;
		font-size: 15px;
		max-width: 538px;
	}
	.teks-cls {
		padding-top: 52px;
	}
</style>
