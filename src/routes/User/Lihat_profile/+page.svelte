<script>
	import Button from '../../../components/Button.svelte';
	import Navbar from '../../../components/Navbar.svelte';
	import { Envelope, Geo, JournalText, Pencil, PlusLg } from 'svelte-bootstrap-icons';
	import axios from 'axios';
	import { onMount } from 'svelte';
	import { Divider } from 'svelte-materialify';
	import { A } from 'flowbite-svelte';

	let id;
	let status = false;
	let data;
	let nama, email, loca, icon, alamat, tglLahir, classification, subClass, noHp, ID;

	let ketersediaan = 'Tidak Ditentukan'; // initial value

	onMount(() => {
		let token = localStorage.getItem('token');
		axios
			.get('https://sinaker.pocari.id/api/show-profile', {
				headers: {
					Authorization: `Bearer ${token}`
				}
			})
			.then((response) => {
				status = true;
				data = response.data;
				nama = data.user.info.name;
				email = data.user.email;
				loca = data.user.info.lokasi;
				alamat = data.user.info.alamat;
				tLahir = data.user.info.tempat_lahir;
				tglLahir = data.user.info.tanggal_lahir;
				classification = data.user.info.klasifikasi_pilihan;
				subClass = data.user.info.sub_klasifikasi_pilihan;
				noHp = data.user.info.no_HP;
				ID = data.user.ID_user;
				console.log(ID);
				console.log(subClass);
				console.log(tglLahir);

				console.log(data);
				id = response.data.user.ID_user;
				personalSummary = response.data.user.info.ringkasan_pribadi;
				education = response.data.user.info.pendidikan;
				jobHistory = response.data.user.info.riwayat_karir;
				licenses = response.data.user.info.sertifikat;
				skills = response.data.user.info.keahlian;
				languages = response.data.user.info.bahasa;
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	});

	let showModal = false;
	let modalContent = '';
let showModal1 = false;
	let personalSummary = '';
	let education = '';
	let jobHistory = '';
	let licenses = '';
	let skills = '';
	let languages = '';

	const openModal = (content) => {
		modalContent = content;
		showModal = true;
	};
	const openModal1 = () =>{
		showModal1 = true
	}

	const closeModal = () => {
		showModal = false;
		showModal1 = false;
	};
	

	const saveChanges = () =>{
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					no_HP : noHp,
					email : email,
					pendidikan : education,
					klasifikasi_pilihan : classification,
					alamat : loca

				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + personalSummary);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const savePersonalSummary = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					ringkasan_pribadi: personalSummary
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + personalSummary);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const saveEducation = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					pendidikan: education
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + education);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const saveJobHistory = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					riwayat_karir: jobHistory
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + jobHistory);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const saveLicenses = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					sertifikat: licenses
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + licenses);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const saveSkills = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					keahlian: skills
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + skills);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const saveLanguages = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					bahasa: languages
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + languages);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const saveLokasi = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					lokasi: loca
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + loca);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const saveAlamat = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					alamat: alamat
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + alamat);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};
	let tLahir;

	const savetLahir = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					tempat_lahir: tLahir
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + tLahir);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const savenoHP = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					no_HP: noHp
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + noHp);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const savetglLahir = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					tanggal_lahir: tglLahir
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + tglLahir);
				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	const saveKlasifikasi = () => {
		let token = localStorage.getItem('token');
		axios
			.post(
				'https://sinaker.pocari.id/api/update-profile/' + id,
				{
					klasifikasi_pilihan: classification,
					sub_klasifikasi_pilihan: subClass
				},
				{
					headers: {
						Authorization: `Bearer ${token}`
					}
				}
			)
			.then((response) => {
				alert('Personal Summary Saved: ' + classification + subClass);

				closeModal();
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	};

	let imageUrl = '';
	let imageFile = null;

	function handleFileUpload(event) {
		const file = event.target.files[0];
		if (file) {
			imageFile = file;
			const reader = new FileReader();
			reader.onload = (e) => {
				imageUrl = e.target.result;
			};
			reader.readAsDataURL(file);
		}
	}
	function triggerFileInput() {
		document.getElementById('image').click();
	}
</script>

<Navbar />

<div class="container">
	<div class="main-contain">
		<div class="header-contain">
			<div class="h-tulisan">
				<h2>{nama}</h2>
				<p class="p-env"><Geo /> {loca}</p>

				<div class="h-button">
					<Button classList="btn-card-header">
						<a
							style="text-decoration: none; color:white"
							href={`/Admin_mitra/detail-pelamar?id=${ID}`}>Lihat Profile</a
						></Button
					>
				</div>
			</div>
		</div>
	</div>

	<div class="flex-row">
		<div class="col-6">
			<div class="profile-edit">
				<div class="image-wrapper" on:click={triggerFileInput}>
					<img src={imageUrl || '/people.jpg'} alt="Rounded Image" class="rounded-image" />
					<div class="edit-icon">
						<div class="icon-pencil"><Pencil style="width:35px; height:35px;" /></div>
					</div>
				</div>

				<input
					type="file"
					id="image"
					accept="image/*"
					on:change={handleFileUpload}
					style="display: none;"
				/>
				<div class="colomn-edit">
					<div style="flex-direction: row; display:flex; gap:150px">
						<h2>Edit Profile</h2>
						<div class="icon-right" on:click={openModal1}><Pencil style="width: 20px; height:20px;" /></div>
					</div>

					<div class="row-edit">
						<div>
							<div class="p-footer-teks">
								<p>PHONE</p>
								{#if !noHp}
									<p class="isi-content-footer">-</p>
								{:else}
									<p class="isi-content-footer">{noHp}</p>
								{/if}
							</div>
							<div class="p-footer-teks">
								<p>LOKASI</p>
								{#if !loca}
									<p class="isi-content-footer">-</p>
								{:else}
									<p class="isi-content-footer">{loca}</p>
								{/if}
							</div>
							<div class="p-footer-teks">
								<p>PENDIDIKAN TERAKHIR</p>
								{#if !education}
									<p class="isi-content-footer">-</p>
								{:else}
									<p class="isi-content-footer">{education}</p>
								{/if}
							</div>
						</div>
						<div>
							<div class="logo-footer">
								<div class="footer-content-teks">
									<div class="p-footer-teks">
										<p>Email</p>
										<p class="isi-content-footer">{email}</p>
									</div>
									<div class="p-footer-teks">
										<p>Usia</p>
										{#if !tglLahir}
											<p class="isi-content-footer">-</p>
										{:else}
											<p class="isi-content-footer">{loca}</p>
										{/if}
									</div>
									<div class="p-footer-teks">
										<p>KLASIFIKASI PILIHAN</p>
										{#if !classification}
											<p class="isi-content-footer">-</p>
										{:else}
											<p class="isi-content-footer">{classification}</p>
										{/if}
									</div>
								</div>

								<!-- <div class="icon-right">
									<a
										style="text-decoration: none; color:black"
										href={`/Admin_mitra/detail-pelamar?id=${ID}`}
										><JournalText style="width: 20px; height:20px;" /></a
									>
								</div>
								<div class="icon-right"><Pencil style="width: 20px; height:20px;" /></div> -->
							</div>
						</div>
					</div>
				</div>
			</div>
			<div class="profile-card-data-diri">
				{#if !loca}
					<h3 class="h3-teks-card">
						Lokasi
						<div class="edit-prof" on:click={() => openModal('loca')} style="cursor: pointer; ">
							<PlusLg />
						</div>
					</h3>
					<p class="p-teks-card">Lengkapi Lokasi Anda</p>
				{:else}
					<h3 class="h3-teks-card">
						Lokasi
						<div class="edit-prof" on:click={() => openModal('loca')} style="cursor: pointer; ">
							<Pencil />
						</div>
					</h3>
					<p class="p-teks-card">{loca}</p>
				{/if}

				{#if !alamat}
					<h3 class="h3-teks-card">
						Alamat
						<div class="edit-prof" on:click={() => openModal('alamat')} style="cursor: pointer; ">
							<PlusLg />
						</div>
					</h3>
					<p class="p-teks-card">Lengkapi alamat anda</p>
				{:else}
					<h3 class="h3-teks-card">
						Alamat
						<div class="edit-prof" on:click={() => openModal('alamat')} style="cursor: pointer; ">
							<Pencil />
						</div>
					</h3>
					<p class="p-teks-card">{alamat}</p>
				{/if}
				{#if !tLahir}
					<h3 class="h3-teks-card">
						Tempat Lahir
						<div class="edit-prof" on:click={() => openModal('tLahir')} style="cursor: pointer; ">
							<PlusLg />
						</div>
					</h3>
					<p class="p-teks-card">Lengkapi Tempat Lahir Anda</p>
				{:else}
					<h3 class="h3-teks-card">
						Tempat Lahir
						<div class="edit-prof" on:click={() => openModal('tLahir')} style="cursor: pointer; ">
							<Pencil />
						</div>
					</h3>
					<p class="p-teks-card">{tLahir}</p>
				{/if}

				{#if !tglLahir}
					<h3 class="h3-teks-card">
						Tanggal Lahir
						<div class="edit-prof" on:click={() => openModal('tglLahir')} style="cursor: pointer; ">
							<PlusLg />
						</div>
					</h3>
					<p class="p-teks-card">Lengkapi Tempat Lahir Anda</p>
				{:else}
					<h3 class="h3-teks-card">
						Tanggal Lahir
						<div class="edit-prof" on:click={() => openModal('tglLahir')} style="cursor: pointer; ">
							<Pencil />
						</div>
					</h3>
					<p class="p-teks-card">{tglLahir}</p>
				{/if}
				{#if !classification}
					<h3 class="h3-teks-card">
						klasifikasi
						<div
							class="edit-prof"
							on:click={() => openModal('classification')}
							style="cursor: pointer; "
						>
							<PlusLg />
						</div>
					</h3>
					<p class="p-teks-card">Lengkapi klasifikasi</p>
				{:else}
					<h3 class="h3-teks-card">
						klasifikasi
						<div
							class="edit-prof"
							on:click={() => openModal('classification')}
							style="cursor: pointer; "
						>
							<Pencil />
						</div>
					</h3>
					<p class="p-teks-card">{classification}, {subClass}</p>
				{/if}

				{#if !noHp}
					<h3 class="h3-teks-card">
						No Handphone
						<div class="edit-prof" on:click={() => openModal('noHp')} style="cursor: pointer; ">
							<PlusLg />
						</div>
					</h3>
					<p class="p-teks-card">Lengkapi No Handphone anda</p>
				{:else}
					<h3 class="h3-teks-card">
						Handphone
						<div class="edit-prof" on:click={() => openModal('noHp')} style="cursor: pointer; ">
							<Pencil />
						</div>
					</h3>
					<p class="p-teks-card">{noHp}</p>
				{/if}
			</div>
		</div>
		<div class="col-6">
			<div class="section">
				<h2>Ringkasan Pribadi</h2>
				<p class="btn-teks">
					Tambahkan ringkasan pribadi ke profile untuk memperkenalkan diri Anda
				</p>
				<Button classList="btn-section" onClick={() => openModal('personalSummary')}
					>Tambah Ringkasan</Button
				>
			</div>

			<div class="section">
				<h2 class="teks-cls">Pendidikan</h2>
				<p class="btn-teks">Beritahu pendidikan mengenai pendidikan anda</p>
				<Button classList="btn-section" onClick={() => openModal('education')}
					>Tambah Pendidikan</Button
				>
			</div>

			<div class="section">
				<h2 class="teks-cls">Riwayat Karir</h2>
				<p class="btn-teks">
					Semakin anda memberi tahu perusahaan mengenai pengalaman Anda, Semakin Anda bisa tampil
					menonjol.
				</p>
				<Button classList="btn-section" onClick={() => openModal('jobHistory')}
					>Tambah Jabatan</Button
				>
			</div>

			<div class="section">
				<h2 class="teks-cls">Lisensi dan Sertifikasi</h2>
				<p class="btn-teks">
					Tunjukkan kredensial profesional Anda, Tambahkan lisensi, sertifikat, keanggotaan, dan
					akreditasi Anda yang relevan di sini.
				</p>
				<Button classList="btn-section" onClick={() => openModal('licenses')}
					>Tambah Lisensi dan sertifikasi</Button
				>
			</div>

			<div class="section">
				<h2 class="teks-cls">Keahlian</h2>
				<p class="btn-teks">Beri tahu perusahaan betapa berharganya keahlian anda bagi mereka</p>
				<Button classList="btn-section" onClick={() => openModal('skills')}>Tambah Keahlian</Button>
			</div>

			<div class="section">
				<h2 class="teks-cls">Bahasa</h2>
				<p class="btn-teks">
					Tambahkan bahasa untuk menarik lebih banyak perusahaan dan pemberi kerja
				</p>
				<Button classList="btn-section" onClick={() => openModal('languages')}>Tambah Bahasa</Button
				>
			</div>
		</div>
	</div>
</div>

{#if showModal}
	<div class="modal-backdrop" on:click={closeModal}></div>
	<div class="modal">
		{#if modalContent === 'personalSummary'}
			<textarea
				class="styled-textarea"
				bind:value={personalSummary}
				placeholder="Tambahkan ringkasan..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={savePersonalSummary}>Simpan Ringkasan</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'education'}
			<textarea class="styled-textarea" bind:value={education} placeholder="Beritahu pendidikan..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={saveEducation}>Simpan Pendidikan</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'jobHistory'}
			<textarea
				class="styled-textarea"
				bind:value={jobHistory}
				placeholder="Tambahkan riwayat karir..."
			></textarea>
			<Button classList="btn-section" onClick={saveJobHistory}>Simpan Jabatan</Button>
		{/if}
		{#if modalContent === 'licenses'}
			<textarea class="styled-textarea" bind:value={licenses} placeholder="Tambahkan lisensi..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={saveLicenses}
					>Simpan Lisensi dan sertifikasi</Button
				>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'skills'}
			<textarea class="styled-textarea" bind:value={skills} placeholder="Beritahu keahlian..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={saveSkills}>Simpan Keahlian</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'languages'}
			<textarea class="styled-textarea" bind:value={languages} placeholder="Tambahkan bahasa..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={saveLanguages}>Simpan Bahasa</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'loca'}
			<textarea class="styled-textarea" bind:value={loca} placeholder="Tambahkan lokasi..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={saveLokasi}>Simpan Lokasi</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'alamat'}
			<textarea class="styled-textarea" bind:value={alamat} placeholder="Tambahkan lokasi..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={saveAlamat}>Simpan Alamat</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'tLahir'}
			<textarea class="styled-textarea" bind:value={tLahir} placeholder="Tambahkan Tempat lahir..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={savetLahir}>Simpan Tempat Lahir</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'classification'}
			<textarea
				class="styled-textarea"
				style="height: fit-content;"
				bind:value={classification}
				placeholder="Tambahkan Klasifikasi"
			></textarea>
			<textarea
				class="styled-textarea"
				style="height: fit-content;"
				bind:value={subClass}
				placeholder="Tambahkan Sub Klasifikasi"
			></textarea>
			<div>
				<Button classList="btn-section" onClick={saveKlasifikasi}>Simpan klasifikasi</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
		{#if modalContent === 'tglLahir'}
			<input
				type="date"
				bind:value={tglLahir}
				class="styled-textarea"
				style="height: fit-content;"
				placeholder="Tambahkan Tanggal Lahir..."
			/>
			<div>
				<Button classList="btn-section" on:click={savetglLahir}>Simpan Tanggal Lahir</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}

		{#if modalContent === 'noHp'}
			<textarea class="styled-textarea" bind:value={noHp} placeholder="Tambahkan lokasi..."
			></textarea>
			<div>
				<Button classList="btn-section" onClick={savenoHP}>Simpan No Hp</Button>
				<Button classList="btn-section" onClick={closeModal}>Close</Button>
			</div>
		{/if}
	</div>
{/if}


<button on:click={openModal}>Edit Profile</button>

{#if showModal1}
    <div class="modal-overlay">
        <div class="modal-content">
            <h2>Edit Profile</h2>
            <div>
                
                <input style="width: 100%;" placeholder="No Handphone" id="nohp" type="text" bind:value={noHp} />
            </div>
            <div>
                <input style="width: 100%;" placeholder="Email" id="email" type="email" bind:value={email} />
            </div>
            <!-- <div>
                <label for="usia">Usia:</label>
                <input style="width: 100%;" id="usia" type="number" bind:value={noHp} />
            </div> -->
            <div>
                
                <input style="width: 100%;" placeholder="Pendidikan Terakhir" id="pendidikanTerakhir" type="text" bind:value={education} />
            </div>
            <div>
                
                <input style="width: 100%;" placeholder="klasifikasi Pilihan" id="klasifikasiPilihan" type="text" bind:value={classification} />
            </div>
            <div>
                
                <input style="width: 100%;" placeholder="Lokasi" id="lokasi" type="text" bind:value={loca} />
            </div>

			<div style="display:flex; justify-content:space-between;">
				<Button classList="btn-section" onClick={saveChanges}>Save</Button>
				<Button classList="btn-section" onClick={closeModal}>Kembali</Button>
			</div>
           
        </div>
    </div>
{/if}

<style>
	p {
		margin-bottom: 0;
	}
	@import url('https://fonts.googleapis.com/css2?family=Noto+Sans:ital,wght@0,100..900;1,100..900&display=swap');
	.footer-content {
		background-color: #ffffff;
		border: 1px solid #fff;
		box-shadow: 0 1px 3px rgba(0, 0, 0, 0.15);
		width: max;
		height: 163px;
		padding-left: 230px;

		padding-top: 10px;
		display: grid;
		grid-template-columns: auto auto;
		gap: 55px;
	}
	.footer-content-teks {
		margin-right: 500px;
	}
	.icon-footer {
		color: black;
		display: flex;
		flex-direction: row;
		gap: 8px;
	}
	.icon-right:hover {
		color: #007bff;
		cursor: pointer;
	}
	.row-edit {
		display: flex;
		flex-direction: row;
		gap: 102px;
	}

	.logo-footer {
		justify-content: space-between;
		display: flex;
		flex-direction: row;
		margin-right: 10px;
	}
	.footer-content {
		font-size: 14px;
		color: #acacad;
		font-weight: bold;
	}
	.profile-edit {
		display: flex;
		flex-direction: row;
		width: 480px;
		gap: 28px;
		margin-bottom: 40px;
	}
	.isi-content-footer {
		color: black;
	}
	.profile-card-head {
		display: flex;
	}
	.container {
		max-width: 1250px;
		border-radius: 20px;
		margin: auto;
		gap: 50px;
		padding: 20px;
		font-family: 'poppins', sans-serif;
		display: flex;
		flex-direction: column;
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
	.h3-card {
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
	.h-tulisan {
		display: flex;
		flex-direction: column;
		height: 161px !important;
		margin-bottom: 0 !important;
		line-height: 24px;
		font-size: 16px;
		gap: 22px;
	}

	.header-contain {
		background-image: url('/image.png');
		background-color: #00195e;

		background-size: cover;
		background-position: center;
		height: 250px;
		color: white;
		padding: 50px;
		border-radius: 20px 20px 0 0;
		display: flex;
		flex-direction: row;
		gap: 16px;
	}
	.p-footer-teks {
		font-size: 14px;
		display: flex;
		flex-direction: column;
		gap: 0;
		margin-bottom: 0;
		padding-bottom: 10px;
	}

	.header-contain h1 {
		padding-left: 180px;
		position: absolute;
		top: 297px;
		font-size: 32px;
		font-family: 'Noto Sans', sans-serif;
		font-weight: 700;
	}
	.section {
		margin-bottom: 20px;
	}
	.profile-card-data-diri {
		border: 1px solid #718284;
		box-shadow: 0 1px 6px rgba(0, 0, 0, 0.25);
		padding-left: 25px;
		padding-top: 32px;
		border-radius: 20px;
		margin-right: 125px;
		width: 480px;
		height: fit-content;
	}
	.p-env,
	.p-mail {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 10px;
		margin-bottom: 0 !important;
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

	.h-button {
		display: flex;
		align-items: center;
	}
	.modal-backdrop {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		z-index: 1000;
	}
	.modal-overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .modal-content {
        background-color: white;
        padding: 20px;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
		width: 20rem;
    }
    .modal-content h2 {
        margin-bottom: 20px;
    }
    .modal-content div {
        margin-bottom: 10px;
    }
	.modal {
		position: fixed;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		background: white;
		padding: 20px;
		border-radius: 8px;
		box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
		z-index: 1001;
		display: flex;
		flex-direction: column;
		height: fit-content;
		width: 80%;
		max-width: 500px;
	}
	.btn-close {
		margin-top: 10px;
	}

	.styled-textarea {
		width: 100%;
		height: 150px;
		padding: 10px;
		border: 1px solid #ccc;
		border-radius: 8px;
		resize: vertical;
		font-family: 'poppins', sans-serif;
		font-size: 16px;
		box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
		outline: none;
		transition:
			border-color 0.3s,
			box-shadow 0.3s;
	}

	.styled-textarea:focus {
		border-color: #007bff;
		box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
	}

	.styled-textarea:hover {
		border-color: #007bff;
		box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
	}
	.edit-prof:hover {
		color: #007bff;
	}

	.rounded-image {
		width: 150px;
		height: 150px;
		border-radius: 50%;
		object-fit: cover;
		cursor: pointer;
		position: relative;
	}

	.edit-icon {
		position: absolute;
		top: 464px;
		left: 229px;

		transform: translate(-50%, -50%);
		background: rgba(0, 0, 0, 0.5);
		border-radius: 50%;
		padding: 47px;
		display: none;
		color: white;
		width: 150px;
		height: 150px;
		cursor: pointer;
	}
	.icon-pencil {
		position: absolute;
		top: 55px;
		left: 55px;
	}

	.image-wrapper:hover .edit-icon {
		display: block;
	}

	.image-wrapper {
		display: inline-block;
	}
</style>
