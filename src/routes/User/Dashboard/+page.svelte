<script>
	import Navbar from '../../../components/Navbar.svelte';
	import Footer from '../../../components/Footer.svelte';
	import Button from '../../../components/Button.svelte';
	import { Splide, SplideSlide } from '@splidejs/svelte-splide';
	import '@splidejs/svelte-splide/css';
	import axios from 'axios';
	import { onMount } from 'svelte';
	import Chatbotwidget from '../../../components/Chatbotwidget.svelte';
	import { PersonFill, BoxArrowLeft, ChevronDown, BellFill } from 'svelte-bootstrap-icons';
	let data = [];
	let activeSlideIndex = 0;

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
				console.log(data);
			})
			.catch((error) => {
				console.error('Ada kesalahan:', error);
			});
	});

	onMount(async () => {
		if (typeof window !== 'undefined') {
			const bootstrap = await import('bootstrap/dist/js/bootstrap.bundle.min.js');
			const carouselElement = document.querySelector('#carouselExampleFade');
			if (carouselElement) {
				const carousel = new bootstrap.Carousel(carouselElement);

				// Tambahkan event listener untuk perubahan slide
				carouselElement.addEventListener('slid.bs.carousel', () => {
					activeSlideIndex = carouselElement.querySelector('.carousel-inner .carousel-item.active')
						.dataset.bsSlideTo;
				});
			}
		}
	});
</script>
<Chatbotwidget/>
<Navbar />
<div class="contain">
	<div class="teks-contain">
		<h3>Langkah Awal Menuju Karir Impianmu</h3>
		<div class="teks-button">
			<Button classList="btn-card-profile">Lengkapi Profile</Button>
			<p>Ayo, lengkapi profil Anda sekarang dan tunjukkan siapa Anda sebenarnya!
			</p>
				
		</div>
	</div>
</div>

<section class="main-content">
	<div class="status-pekerjaan">
		<h3>Status Pekerjaan</h3>
		<div class="status-paraghraf">
			<p>Perusahaan</p>
			<p>: belum Tersedia</p>
		</div>
		<div class="status-paraghraf">
			<p>Jadwal</p>
			<p>: belum Tersedia</p>
		</div>
		<div class="status-paraghraf">
			<p>Tempat</p>
			<p>: belum Tersedia</p>
		</div>
	</div>

	<div class="contain-card">
		<div class="card-isi" style="background-color: #E60278;">
			<div class="card-sec">
				"Hello" Lihat Berita Dan Tips Menarik
				<Button classList="btn-card-img">Cek Berita</Button>
			</div>
			<div class="card-sec bg-female"></div>
		</div>
		<div class="card-isi" style="background-color: #E6EAF2;">
			<div class="card-sec" style="color: #2E3849;">
				"Hello" Bingung dan ingin bertanya?
				<Button classList="btn-card-bg">Tanyakan kepada Chatbot</Button>
			</div>
			<div class="card-sec bg-male"></div>
		</div>
	</div>
	<div class="tips-trick">
		<h3>Tips & Trick</h3>
		<Splide
			options={{
				perPage: 3,
				gap: '25px',
				fixedWidth: 'auto',
				height: 'auto'
			}}
		>
			{#each data as item}
				<SplideSlide>
					<div class="card" style="width: 18rem;">
						<img
							src={`http://127.0.0.1:8000/storage/${item.gambar}`}
							class="card-img-top"
							alt={item.judul}
						/>
						<div class="card-body">
							<p class="card-text">{item.judul}</p>
						</div>
					</div>
				</SplideSlide>
			{/each}
		</Splide>
	</div>
</section>
<Footer />

<style>
	@import url('https://fonts.googleapis.com/css2?family=Yrsa:ital,wght@0,300..700;1,300..700&display=swap');
	.main-content {
		padding: 20px;
		overflow-x: hidden;
		padding-left: 8rem;
		padding-right: 8rem;
		display: flex;
		flex-direction: column;
	}
	.contain {
		background-image: url('/Home-female.png');
		background-position: right;
		background-repeat: no-repeat;
		background-size: contain;
		border-radius: 16px;
		background-color: #ffff;
		padding: 20px;
		height: 550px;
		width: max;
		border-radius: 10px;
		margin-bottom: 20px;
		
		text-align: left;
		position: relative;
	}
	.teks-contain {
		width: 700px;
		margin-left: 110px;
	}
	.teks-contain h3 {
		font-family: 'Yrsa', serif;
		font-size: 68px;
		font-weight: 700;
		font-style: normal;
		word-spacing: 10px;
	}
	.teks-button {
		display: flex;
		flex-direction: row;
		gap: 12px;
		height: 100px;
		width: 600px;
		justify-content: space-between;
		align-items: center;

	}
	.teks-button p {
		
		font-size: 11px;
		width: 378px;
		line-height: 1.5;
		color: #333;
		margin: auto;
	}
	.bg-female {
		background-image: url('/bg-female.png');
		background-size: cover;
		border-radius: 16px;
	}
	.bg-male {
		background-image: url('/bg-male.png');
		background-size: cover;
		border-radius: 16px;
	}
	.tips-trick {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	li {
		display: flex;
		flex-direction: row;
	}
	.card-text {
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: normal;
	}

	a {
		color: inherit;
		text-decoration: none;
	}
	h3 {
		padding-top: 66px;
	}
	.status-paraghraf {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		width: 258px;
	}
	.contain-card {
		margin-top: 96px;
		display: flex;
		flex-direction: row;
	
		width: 100%;
		justify-content: space-between;
		gap: 20px;
		height: 393px;
	}
	.card-isi {
		width: 628px;
		height: 393px;
		border-radius: 20px;
		display: flex;
		flex-direction: row;
	}

	.card-sec {
		display: flex;
		flex-direction: column;
		justify-content: center;
		font-size: 24px;
		color: #e6eaf2;
		padding: 48px;
		width: 314px;
		height: 393px;
		font-weight: 500;
		font-family: Arial, Helvetica, sans-serif;
		border-radius: 20px;
		gap: 20px;
	}
</style>
