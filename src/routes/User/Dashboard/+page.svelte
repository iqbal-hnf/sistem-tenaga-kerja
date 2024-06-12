<script>
	import Navbar from '../../../components/Navbar.svelte';
	import Footer from '../../../components/Footer.svelte';
	import { HeartFill, Instagram } from 'svelte-bootstrap-icons';
  import { Splide, SplideSlide } from '@splidejs/svelte-splide';
  import "@splidejs/svelte-splide/css"
  import 'bootstrap/dist/css/bootstrap.min.css';
</script>

<Navbar />

<section class="main-content">
	<div class="carousel">
		<div class="carousel-item">
			<img src="/beranda1.jpg" alt="Image1" />
			<div class="carousel-caption">
				<h2>3 Cara Jitu Jawab Pertanyaan Deskripsi Diri Saat Wawancara</h2>
			</div>
		</div>
	</div>

	<div class="status-pekerjaan">
		<h3>Status Pekerjaan</h3>
		<p>Perusahaan : Belum Tersedia</p>
		<p>Jadwal : Belum Tersedia</p>
		<p>Tempat : Belum Tersedia</p>
	</div>

  <div class="tips-trick">
    <h3>Tips & Trick</h3>
    <Splide options={{
      perPage: 3,
      gap: '25px',
      fixedWidth: 'auto',
      height:'auto'
    }}>
      <SplideSlide>
        <div class="card" style="width: 18rem;">
          <img src="/beranda5.jpg" class="card-img-top" alt="tip2">
          <div class="card-body">
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </SplideSlide>
      <SplideSlide>
        <div class="card" style="width: 18rem;">
          <img src="/beranda5.jpg" class="card-img-top" alt="tip2">
          <div class="card-body">
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </SplideSlide>
      <SplideSlide>
        <div class="card" style="width: 18rem;">
          <img src="/beranda5.jpg" class="card-img-top" alt="tip2">
          <div class="card-body">
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </SplideSlide>
      <SplideSlide>
        <div class="card" style="width: 18rem;">
          <img src="/beranda5.jpg" class="card-img-top" alt="tip2">
          <div class="card-body">
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </SplideSlide>
      <SplideSlide>
        <div class="card" style="width: 18rem;">
          <img src="/beranda5.jpg" class="card-img-top" alt="tip2">
          <div class="card-body">
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </SplideSlide>
      <SplideSlide>
        <div class="card" style="width: 18rem;">
          <img src="/beranda5.jpg" class="card-img-top" alt="tip2">
          <div class="card-body">
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>
      </SplideSlide>
      <SplideSlide>
        <div class="card" style="width: 18rem;">
          <img src="/beranda5.jpg" class="card-img-top" alt="tip2">
          <div class="card-body">
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          </div>
        </div>  
      </SplideSlide>
    </Splide>
  </div>

	<!-- <div class="tips-trick">
		<h3>Tips & Trick</h3>
		<div class="tips-item-container">
			<div class="tips-item">
				<img src="/beranda2.jpg" alt="Tip 1" />
				<p>3 Cara Jawab Jitu pertanyaan</p>
			</div>
			<div class="tips-item">
				<img src="/beranda3.jpg" alt="Tip 2" />
				<p>Tips kembali kerja di perusahaan setelah...</p>
			</div>
			<div class="tips-item">
				<img src="/beranda4.jpg" alt="Tip 3" />
				<p>Bahas tuntas tentang quiet quitting</p>
			</div>
			<div class="tips-item">
				<img src="/beranda5.jpg" alt="Tip 4" />
				<p>Panduan bekerja freelance</p>
			</div>
      <div class="tips-item">
				<img src="/beranda5.jpg" alt="Tip 4" />
				<p>Panduan bekerja freelance</p>
			</div>
      <div class="tips-item">
				<img src="/beranda5.jpg" alt="Tip 4" />
				<p>Panduan bekerja freelance</p>
			</div>
		</div>
	</div> -->
</section>
<Footer />

<style>
 
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

	.carousel-caption {
		position: absolute;
		bottom: 20px;
		left: 20px;
		background-color: rgba(0, 0, 0, 0.5);
		color: white;
		padding: 10px;
	}

	.status-pekerjaan {
		margin: 20px 0;
	}

	.status-pekerjaan h3,
	.tips-trick h3 {
		margin-bottom: 10px;
	}

	.tips-trick {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		/* flex-wrap: wrap; */
	}

	.tips-item {
    display: inline-block;
		width: 23% !important;
		margin-bottom: 20px;
	}

  .tips-item-container{
    overflow-x: scroll;
  }

	.tips-item img {
		width: 100%;
		height: auto;
	}
</style>
