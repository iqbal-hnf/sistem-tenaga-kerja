<script>
	import { Instagram } from 'svelte-bootstrap-icons';
</script>

<footer>
	<div class="footer-content">
		<div class="footer-desc">
			<h4>Citratama</h4>
			<p>
				Bersama Citratama, setiap pencarian kerja menjadi lebih mudah dan terarah. Kami
				menghubungkan Anda dengan peluang karir terbaik, memberikan bimbingan dan dukungan sepanjang
				perjalanan profesional Anda. Citratama, karena masa depan karir Anda adalah prioritas kami.
			</p>
		</div>
		<div class="footer-item">
			<h5>Navigasi</h5>
			<p>Dashboard</p>
			<p>Lihat Profile</p>
			<p>Profile Perusahaan</p>
			<p>Chatbot</p>
		</div>
		<div class="social-media">
			<a href="https://www.instagram.com/citratama_indonesia?igsh=bjYzaWFnMm4xOGs0 "
				><div class="ig-font"><Instagram style="color:#3951AB; width:24px; height:24px;" /></div></a
			>
		</div>
	</div>
	<div class="footer-bottom">
		<p>&2024 CITRATAMA. Semua hak dilindungi.</p>
	</div>
</footer>

<style>
	h5 {
		font-weight: 700;
	}
	h4 {
		font-weight: 700;
	}
	.ig-font {
		width: 22px;
		height: 22px;
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	.footer-desc {
		width: 30%;
	}
	p {
		color: rgb(113, 130, 132);
		font-size: 14px;
		font-weight: 500;
		line-height: 20px;
	}

	footer {
		background-color: #f8f8f8;
		padding-left: 128px;
		padding-top: 10px;
		padding-right: 128px;
	}

	.footer-content {
		display: flex;
		justify-content: space-between;
	}

	.footer-item {
		width: 30%;
	}
	.footer-item p {
    cursor: pointer;
  }

	.footer-bottom {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-top: 20px;
		border-top: 1px solid #ddd;
		padding-top: 10px;
	}

	.social-media {
		display: flex;
		flex-direction: row;
		align-items: center;
	}
</style>
