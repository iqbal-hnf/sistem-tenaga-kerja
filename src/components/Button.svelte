<script>
	export let id = '';
	export let classList = '';

	export let type = 'button';
	export let custom = '';
	export let disabled = '';
	export let onClick = () => {};
	const handleClick = (evt) => {
		onClick(evt);
	};
</script>

<button {type} {id} class={classList} on:click={handleClick} {disabled} style={custom}>
	<slot />
</button>

<style>
	button {
		border: 1px solid transparent;
		border-radius: 8px;
		cursor: pointer;
		font-size: 16px;
		padding: 8px 24px;
		background-color: transparent;
	}

	.btn-primary {
		background-color: #2d3e50;
		color: #fff;
	}
	.btn-secondary {
		background-color: 1px solid white;
		color: #2d3e50;
	}
	.btn-tambah {
		background: transparent;
		color: #0469ff;
		padding: 8px 16 px;
		border: 1px solid #0469ff;
		border-radius: 8px;
		cursor: pointer;
	}
	.btn-success {
		color: #fff;
		background-color: #198754;
		font-size: 12px;
		align-items: center;
		box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
		width: 110px;
		height: 34px;
		display: flex; /* Menjadikan button sebagai flex container */
		justify-content: center; /* Mengatur teks di tengah secara horizontal */
		align-items: center; /* Mengatur teks di tengah secara vertikal */
		padding: 8px; /* Tambahkan padding sesuai kebutuhan */
		border: none; /* Menghilangkan border jika perlu */
		cursor: pointer; /* Mengubah kursor menjadi pointer */
	}
	.btn-pending {
		color: #fff;
		background-color: #ffc107;
		font-size: 12px;
		align-items: center;
		box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
		width: 110px;
		height: 34px;
		display: flex; /* Menjadikan button sebagai flex container */
		justify-content: center; /* Mengatur teks di tengah secara horizontal */
		align-items: center; /* Mengatur teks di tengah secara vertikal */
		padding: 8px; /* Tambahkan padding sesuai kebutuhan */
		border: none; /* Menghilangkan border jika perlu */
		cursor: pointer; /* Mengubah kursor menjadi pointer */
	}
	.btn-danger {
		color: #fff;
		background-color: #dc3545;
		font-size: 12px;
		align-items: center;
		box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
		width: 110px;
		height: 34px;
		padding: 0%;
	}
	.btn-penerima{
		color: black;
		background-color: #fff;
		font-size: 12px;
		align-items: center;
		border: 1px solid black;
		box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.125);
		width: 110px;
		height: 34px;
		padding: 0%;
	}
	.btn-penerima:hover{
		border: 1px solid blue;
		color: blue;
	}


	.btn-card-profile {
		background-color: #E60278;
		font-size: 18px;
		color: #fff;
		width: 200px;
		height: 60px;
		box-shadow: inset 0 3px 5px rgba(255, 255, 255, 0.125);
		border-radius: 4px;
	}

	.btn-card-img {
		background-color: #e6eaf2;
		font-weight: 500;
		font-size: 14px;
	}
	.btn-card-bg {
		background-color: #e60278;
		color: #e6eaf2;
		font-weight: 500;
		height: 42px;
		font-size: 14px;
	}
	
	.btn-card-header {
		background-color: transparent;
		border: 1px solid #fff;
		color: #fff;
		border-radius: 5px;
		font: bold;
	}
	.btn-back {
		background-color: #00195e;
		border: #2d3e50;
		color: white;
		height: auto;
		width: fit-content;
	}
	.btn-section {
		background-color: transparent;
		border-radius: 10px;
		color: black;
		border: 2px solid #00195e;
		height: 42px;
		width: fit-content;
		margin-top: 35px;
		font-weight: 300;
		font-size: 16px;
	}

	.btn-secondary:hover {
		background-color: #2d3e50;
		color: #fff;
	}
	.btn-submit {
		background: linear-gradient(90deg, #e2186d 34.77%, #485ee9 63.43%);
		border: 1px solid #9398b0;
		color: white;

		border-radius: 8px;
		cursor: pointer;
		margin-top: 10px;
		width: 100%;
		height: 36px;
	}

	.btn-submit p {
		color: #00195e;
	}
</style>
