<script>
	import Button from '../../../components/Button.svelte';
	// Data statis untuk profil
	import axios from 'axios';
	let data, nama,email,phone,date,location,summary,education,career,certifications,skill,language,address, classification,subClass;
let selectedUser={};
	// Ambil parameter id dari URL
	function getURLParameter(name) {
		const urlParams = new URLSearchParams(window.location.search);
		return urlParams.get(name);
      
	}

	// Simpan id ke dalam variabel
	const id = getURLParameter('id');

	// Contoh penggunaan: tampilkan id di console
	console.log('ID dari URL adalah:', id);

	axios
		.get('https://sinaker.pocari.id/api/admin/pelamar')
		.then((response) => {
			data = response.data;
			status = true;
			

            selectedUser = data.find(user => user.ID_user === parseInt(id));
            console.log(selectedUser);
            nama = selectedUser.info.name;
            email = selectedUser.email;
            phone = selectedUser.info.no_HP;
            date = selectedUser.info.tanggal_lahir;
            location = selectedUser.info.lokasi;
            summary = selectedUser.info.ringkasan_pribadi;
            education = selectedUser.info.pendidikan;
            career = selectedUser.info.riwayat_karir;
            certifications = selectedUser.info.sertifikat;
            skill = selectedUser.info.keahlian;
            language = selectedUser.info.bahasa;
            address = selectedUser.info.alamat;
            classification = selectedUser.info.klasifikasi_pilihan;
            subClass = selectedUser.info.sub_klasifikasi_pilihan;


            console.log(nama);
		})
		.catch((error) => {
			console.error('Ada kesalahan:', error);
		});

	let profile = {
		name: 'John Doe',
		email: 'john.doe@example.com',
		phone: '123-456-7890',
		dateOfBirth: '1985-10-25',
		location: 'New York, USA',
		summary: 'Experienced software developer with a strong background in full-stack development.',
		education: [
			{ degree: 'B.Sc in Computer Science', institution: 'ABC University', year: '2007' }
		],
		career: [{ title: 'Senior Developer', company: 'XYZ Corp', year: '2015-2020' }],
		certifications: [{ name: 'Certified Scrum Master', institution: 'Scrum Alliance' }],
		skills: ['JavaScript', 'React', 'Node.js'],
		languages: ['English', 'Spanish'],
		address: '123 Main St, New York, NY 10001',
		classification: 'Software Development'
	};

	function goBack() {
		window.history.back();
	}
</script>



<div class="profile-container">
	<h1>{nama}</h1>
	<p><strong>Email:</strong> {email}</p>
	<p><strong>Phone:</strong> {phone}</p>
	<p><strong>Date of Birth:</strong> {date}</p>
	<p><strong>Location:</strong> {location}</p>

	<div class="section">
		<h2>Personal Summary</h2>
		<p>{summary}</p>
	</div>

	<div class="section">
		<h2>Education</h2>
		{#each profile.education as edu}
			<p>{education} </p>
		{/each}

        
        <!-- classification = selectedUser.info.klasifikasi_pilihan; -->
	</div>

	<div class="section">
		<h2>Career History</h2>
		{#each profile.career as job}
			<p>{career}</p>
            <!-- {job.title} at {job.company} ({job.year}) -->
		{/each}
	</div>

	<div class="section">
		<h2>Licenses and Certifications</h2>
		{#each profile.certifications as cert}
			<p>{certifications}</p>
            <!-- {cert.name} - {cert.institution} -->
		{/each}
	</div>

	<div class="section">
		<h2>Skills</h2>
		<ul>
            {skill}
			<!-- {#each profile.skills as skill}
				<li>{skill}</li>
			{/each} -->
		</ul>
	</div>

	<div class="section">
		<h2>Languages</h2>
		<ul>
            {language}
			<!-- {#each profile.languages as language}
				<li>{language}</li>
			{/each} -->
		</ul>
	</div>

	<div class="section">
		<h2>Address</h2>
		<p>{address}</p>
	</div>

	<div class="section">
		<h2>Preferred Classification</h2>
		<p>{classification}</p>
        <p>{subClass}</p>
	</div>
	<div>
		<Button onClick={goBack} classList="btn-back">Kembali</Button>
	</div>
</div>

<style>
	.profile-container {
		max-width: 800px;
		margin: 0 auto;
		padding: 20px;
		border-radius: 8px;
		background-color: #f9f9f9;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	h1,
	h2 {
		color: #333;
	}

	.section {
		margin-bottom: 20px;
	}

	.section h2 {
		border-bottom: 2px solid #00195e;
		padding-bottom: 5px;
	}

	.section p {
		margin: 5px 0;
	}

	ul {
		list-style-type: none;
		padding: 0;
	}

	ul li {
		margin-bottom: 5px;
	}
</style>
