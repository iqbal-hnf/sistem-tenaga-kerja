<script>
	import Navbar from '../../../components/Navbar.svelte';
	import Footer from '../../../components/Footer.svelte';
	let Name = '';
	let address = '';
	let birthPlaceDate = '';
	let phoneNumber = '';
	let classification = '';
	let subClassification = '';

	const handleSubmit = (event) => {
		event.preventDefault();
		// Handle form submission
		console.log({
			Name,
			address,
			birthPlaceDate,
			phoneNumber,
			classification,
			subClassification
		});
	};
</script>

<Navbar />

<div class="container">
	<div class="profile-section">
		<div class="profile-picture">
			<img src="/profile.jpg" alt="Profile Picture" />
		</div>
		<div class="form-section">
			<h2>Lengkapi Data Diri</h2>
			<form on:submit={handleSubmit}>
				<div>
					<input type="text" bind:value={Name} placeholder="Nama Lengkap" />
				</div>

				<div>
					<input type="text" bind:value={address} placeholder="Alamat" />
				</div>
				<div>
					<input type="text" bind:value={birthPlaceDate} placeholder="Tempat Tanggal Lahir" />
				</div>
				<div>
					<input type="text" bind:value={phoneNumber} placeholder="No Handphone" />
				</div>
				<div>
					<select bind:value={classification}>
						<option value="" disabled selected>Pilih Klasifikasi</option>
						<!-- Add your options here -->
					</select>
				</div>
				<div>
					<select bind:value={subClassification}>
						<option value="" disabled selected>Pilih Sub Klasifikasi</option>
						<!-- Add your options here -->
					</select>
				</div>
				<div>
					<button type="submit">Submit</button>
				</div>
			</form>
		</div>
	</div>
</div>

<Footer />

<style>
	.container {
		max-width: 950px;
		margin: auto;
		padding: 1rem;
	}
	.profile-section {
		display: flex;
		justify-content: flex-start;
		align-items: flex-start;
		margin-bottom: 2rem;
	}
	.profile-picture img {
		width: 250px;
		height: 250px;
		object-fit: cover;
		border-radius: 5px;
		border: 1px solid #ccc;
        
        
	}
	.form-section {
		flex: 1;
		margin-left: 2rem;
	}
	.form-section h2 {
		margin-bottom: 1rem;
	}
	.form-section input,
	.form-section select {
		display: block;
		width: 100%;
		padding: 0.5rem;
		margin-bottom: 2rem;
		font-size: 1rem;
		border: 1px solid #ccc;
		border-radius: 4px;
	}
	.form-section button {
		padding: 0.75rem 300px;
		font-size: 1rem;
		color: #fff;
		background-color: #007bff;
		border: none;
		border-radius: 4px;
		cursor: pointer;
	}
	.form-section button:hover {
		background-color: #0056b3;
	}
</style>
