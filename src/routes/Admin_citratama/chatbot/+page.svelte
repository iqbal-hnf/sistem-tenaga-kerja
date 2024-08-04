<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import Button from '../../../components/Button.svelte';
	import { onMount } from 'svelte';
	import axios from 'axios';
	import { fly, scale } from 'svelte/transition';
    import {ThreeDotsVertical} from 'svelte-bootstrap-icons';

	let data;
	let status = false;
	let showModal = false; // Untuk mengontrol tampilan modal
	let newQuestion = '';
	let newAnswer = '';
	let newKeyword = '';

    async function deleteBerita(id) {
      try {
        await axios.delete(`https://sinaker.pocari.id/api/faq/delete/${id}`);
        data = data.filter(item => item.id !== id);
        console.log(`Berita dengan ID ${id} berhasil dihapus`);
      } catch (error) {
        console.error('Ada kesalahan saat menghapus berita:', error);
      }
    }
	// Ambil data FAQ dari API
	axios
		.get('https://sinaker.pocari.id/api/faq')
		.then((response) => {
			status = true;
			data = response.data;
			console.log(data);
		})
		.catch((error) => {
			console.error('Ada kesalahan:', error);
		});

	// Fungsi untuk menampilkan modal
	function toggleModal() {
		showModal = !showModal;
	}

	// Fungsi untuk mengirim data ke API
	function addQuestion() {
		axios
			.post('https://sinaker.pocari.id/api/faq/add', {
				question: newQuestion,
				answer: newAnswer,
				keyword: newKeyword
			})
			.then((response) => {
				console.log('Berhasil ditambahkan:', response.data);
				// Refresh data setelah berhasil menambah
				data.push(response.data);
				toggleModal(); // Sembunyikan modal
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	}
    function toggleMenu(index) {
      data = data.map((item, i) => ({
        ...item,
        showMenu: i === index ? !item.showMenu : false,
      }));
    }
  
    function handleOutsideClick(event) {
      if (!event.target.closest('.dropdown-menu') && !event.target.closest('.menu-icon')) {
        data = data.map((item) => ({ ...item, showMenu: false }));
      }
    }
  
    onMount(() => {
      document.addEventListener('click', handleOutsideClick);
     
      return () => {
        document.removeEventListener('click', handleOutsideClick);
      };
    });
</script>

<div id="after-login-layout">
	<NavbarAdmin />
	<div class="flex">
		<Sidebar active="Data Perusahaan" pagePointer="ams" />
		<div class="w-100 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="flex flex-between-horizontal w-100">
					<div class="title-content">Kelola Chatbot</div>
				</div>
				<div>
					<Button classList="btn-tambah" onClick={toggleModal}>Tambah Pertanyaan</Button>
				</div>
				<div class="flex flex-direction-col flex-gap-regular">
					<div class="card w-80 height-fit">
						<div class="flex flex-gap-regular">
							<div class="flex flex-gap-small flex-center-vertical w-25">
								<div class="text-drop-card">Pertanyaan</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-25">
								<div class="text-drop-card">Jawaban</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Keyword</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
						</div>
					</div>
					{#if status}
						{#each data as d,index}
							<div class="card w-80 height-fit">
								<div class="flex flex-direction-col flex-gap-regular">
									<div class="flex flex-gap-regular">
										<div class="flex flex-gap-small flex-center-vertical w-25">
											<div class="text-drop-card">{d.question}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-25">
											<div class="text-drop-card">{d.answer}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">{d.keyword}</div>
										</div>
                                        <div class="menu-icon" on:click={() => toggleMenu(index)}>
                                            <ThreeDotsVertical />
                                          </div>
                                          {#if d.showMenu}
                                            <div class="dropdown-menu">
                                              <a href="javascript:void(0)" class="menu-item" on:click={() => deleteBerita(d.id)}>Delete</a>
                                              <a href="/Admin_citratama/update-berita" class="menu-item">Update</a>
                                            </div>
                                          {/if}
									</div>
								</div>
							</div>
						{/each}
					{/if}
				</div>
			</div>
		</div>
	</div>

	{#if showModal}
		<div class="modal-overlay" on:click={toggleModal}>
			<div class="modal-content" on:click|stopPropagation>
				<h2>Tambah Pertanyaan</h2>
				<form on:submit|preventDefault={addQuestion}>
					<div>
						<label for="question">Pertanyaan:</label>
						<input type="text" id="question" bind:value={newQuestion} required />
					</div>
					<div>
						<label for="answer">Jawaban:</label>
						<input type="text" id="answer" bind:value={newAnswer} required />
					</div>
					<div>
						<label for="keyword">Keyword:</label>
						<input type="text" id="keyword" bind:value={newKeyword} required />
					</div>
					<button type="submit">Tambah</button>
					<button type="button" on:click={toggleModal}>Batal</button>
				</form>
			</div>
		</div>
	{/if}
</div>

<style>
	/* Gaya untuk modal */
	.modal-overlay {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.5);
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.modal-content {
		background: white;
		padding: 20px;
		border-radius: 8px;
		width: 400px;
	}
	form div {
		margin-bottom: 10px;
	}
	form label {
		display: block;
		margin-bottom: 5px;
	}
	form input {
		width: 100%;
		padding: 8px;
		box-sizing: border-box;
	}
	button {
		margin-right: 10px;
		padding: 10px 15px;
		border: none;
		background-color: #007bff;
		color: white;
		cursor: pointer;
	}
	button[type='button'] {
		background-color: #6c757d;
	}

    .news-image {
      max-width: 100px;
      max-height: 100px;
      object-fit: cover;
      border-radius: 4px;
    }
    .menu-icon {
      cursor: pointer;
    }
  
    .dropdown-menu {
      position: absolute;
      left: 1000px;
      background-color: white;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      margin-top: 10px;
      padding: 10px;
      z-index: 1000;
    
    }
  
    .menu-item {
      display: block;
      padding: 10px;
      text-decoration: none;
      color: black;
      border-bottom: 1px solid #eee;
    }
  
    .menu-item:last-child {
      border-bottom: none;
    }
</style>
