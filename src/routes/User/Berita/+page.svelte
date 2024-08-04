<script>
	import Footer from '../../../components/Footer.svelte';
	import Navbar from '../../../components/Navbar.svelte';
	import { HeartFill, Instagram } from 'svelte-bootstrap-icons';
	import { Splide, SplideSlide } from '@splidejs/svelte-splide';
	import '@splidejs/svelte-splide/css';
	import 'bootstrap/dist/css/bootstrap.min.css';
	import { onMount } from 'svelte';
	import axios from 'axios';

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

<Navbar />

<section class="main-content">
	<div class="card mb-5" style="margin-left: 62px; margin-right:62px;">
		<div class="row g-1">
			<div class="col-md-6">
				<div id="carouselExampleFade" class="carousel slide carousel-fade">
					<div class="carousel-inner">
						{#each data as item, index}
							<a href={`/User/details-berita/${item.id}`} class="carousel-item {index == 0 ? 'active' : ''}" data-bs-slide-to={index}>
								<img src={`https://sinaker.pocari.id/storage/${item.gambar}`} class="d-block w-100" alt="..." />
							</a>
						{/each}
					</div>
					<button
						class="carousel-control-prev"
						type="button"
						data-bs-target="#carouselExampleFade"
						data-bs-slide="prev"
					>
						<span class="carousel-control-prev-icon" aria-hidden="true"></span>
						<span class="visually-hidden">Previous</span>
					</button>
					<button
						class="carousel-control-next"
						type="button"
						data-bs-target="#carouselExampleFade"
						data-bs-slide="next"
					>
						<span class="carousel-control-next-icon" aria-hidden="true"></span>
						<span class="visually-hidden">Next</span>
					</button>
				</div>
			</div>
			<div class="col-md-6">
				<div class="card-body">
					<h5 class="card-title">
						{#if data[activeSlideIndex]}
							{data[activeSlideIndex].judul}
						{:else}
							Loading...
						{/if}
					</h5>
					<p class="card-text">
						{#if data[activeSlideIndex]}
							{data[activeSlideIndex].konten}
						{:else}
							Loading...
						{/if}
					</p>
				</div>
			</div>
		</div>
	</div>

	<div class="grid text-center">
		{#each data as item}
			<a href={`/User/details-berita?id=${item.ID_berita}`} class="g-col-4">
				<div class="card" style="width: 296px; height: 235px; padding:0;">
					<img src={`https://sinaker.pocari.id/storage/${item.gambar}`} class="card-img-top" />
					<div class="card-body">
						<p class="card-text">{item.judul}</p>
					</div>
				</div>
			</a>
		{/each}
	</div>
</section>
<Footer />

<style>
	.grid {
		display: grid;
		grid-template-columns: repeat(4, 1fr); /* Empat kolom dengan lebar yang sama */
		gap: 36px; /* Jarak antar kolom */
		margin-left: 62px;
		margin-right: 62px;
		margin-bottom: 50px;
	}
	.main-content {
		padding: 20px;
		overflow-x: hidden;
	}

	.carousel {
		position: relative;
		width: 100%;
		max-width: 800px;
		margin: auto;
		overflow: hidden;
		border: 2px solid #ddd;
	}

	.carousel-item {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.carousel-item img {
		width: 100%;
		height: auto;
	}

	.tips-trick {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.card-title {
		font-size: 32px;
		font-weight: 600;
		display: -webkit-box;
		-webkit-line-clamp: 2; /* Jumlah baris teks yang ingin ditampilkan */
		-webkit-box-orient: vertical;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: normal;
	}

	.card-text {
		display: -webkit-box;
		-webkit-line-clamp: 2; /* Jumlah baris teks yang ingin ditampilkan */
		-webkit-box-orient: vertical;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: normal;
	}

	a {
		color: inherit;
		text-decoration: none;
	}
</style>
