<script>
    import Navbar from "../../../components/Navbar.svelte";
    import axios from "axios";
    import { onMount } from 'svelte';
	let selectedUser={};
    let data=[];

	let title,content,photos;
	function getURLParameter(name) {
		const urlParams = new URLSearchParams(window.location.search);
		return urlParams.get(name);
      
	}

	const id = getURLParameter('id');

	// Contoh penggunaan: tampilkan id di console
	// console.log('ID dari URL adalah:', id);


    onMount(() => {
		let token = localStorage.getItem('token');
		axios
			.get('https://sinaker.pocari.id/api/admin/berita', {
				headers: {
					Authorization: `Bearer ${token}`
				}
			})
			.then((response) => {
				data = response.data;
				title = data.judul;
				selectedUser = data.find(user => user.ID_berita === parseInt(id));
				title = selectedUser.judul;
				content = selectedUser.konten;
				photos = selectedUser.gambar;
				
				
				console.log(data);
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	});
</script>


<Navbar/>
<section class="main-content container">
	
		<div class="card mb-5">
			<h1 class="card-title">{title}</h1>
			<img src={`https://sinaker.pocari.id/storage/${photos}`} class="card-img-top"  />
           
			<div class="card-body">
				
				<p class="card-text">{content}</p>
			</div>
		</div>
	
</section>



<style>
	.main-content {
		padding: 20px;
	
	}

	.card {
		border: none;
		width: 940px;
		height: 484px;
		margin: auto;
	}

	.card-img-top {
		width: 100%;
		height: 484px;
		border-radius: 8px;
	}

	.card-title {
		font-size: 32px;
		font-weight: 600;
		margin-bottom: 20px;
	}

	.card-text {
		margin-top: 20px;
		font-size: 18px;
		line-height: 1.6;
	}
</style>
