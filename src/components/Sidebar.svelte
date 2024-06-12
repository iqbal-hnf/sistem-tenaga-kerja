<script>
	import { BarChartLineFill, PeopleFill, HouseFill, RecordFill } from 'svelte-bootstrap-icons';
	import { onMount } from 'svelte';
	
	let isSidebarOpen = true;

	function toggleSidebar() {
		isSidebarOpen = !isSidebarOpen;
	}
</script>

<div class="sidebar" class:sidebar-open={isSidebarOpen}>
	<div class="profile">
		<img src="/profile.jpg" alt="Profile Picture" />
		<div class="welcome-text">
			<p style="font-size: 14px; font-weight:600;">Selamat Datang</p>
			<p style="font-size: 14px; margin-top:1px;">Adeline Patsy</p>
		</div>
	</div>
	<ul class="menu">
		<li>
			<a class="a-menu" href="#"><p class="p-menu"><BarChartLineFill />Dashboard</p></a>
		</li>
		<li>
			<a class="a-menu" href=""><p class="p-menu"><PeopleFill />Pelamar kerja</p></a>
			<ul class="submenu">
				<li>
					<a class="a-menu" href=""><p class="p-dot"><RecordFill width="6px" />Persetujuan</p></a>
				</li>
				<li>
					<a class="a-menu" href=""><p class="p-dot"><RecordFill width="6px" />Edit Status</p></a>
				</li>
				<li>
					<a class="a-menu" href=""><p class="p-dot"><RecordFill width="6px" />Data Pelamar</p></a>
				</li>
			</ul>
		</li>
		<li>
			<a class="a-menu" href=""><p class="p-menu"><HouseFill />Perusahaan</p></a>
			<ul class="submenu">
				<li><a class="a-menu" href=""><p class="p-dot"><RecordFill width="6px" />Jadwal</p></a></li>
				<li>
					<a class="a-menu" href=""><p class="p-dot"><RecordFill width="6px" />Data Perusahaan</p></a>
				</li>
			</ul>
		</li>
	</ul>
	<div class="footer">
		<p>Admin Perusahaan Citratama Indonesia</p>
	</div>
</div>

<button class="toggle-button" class:toggle-left={!isSidebarOpen} on:click={toggleSidebar}>
	{#if isSidebarOpen}
		<span>&#x25B2;</span> <!-- Tanda panah ke atas -->
	{:else}
		<span>&#x2630;</span> <!-- Tanda panah sandwich menu -->
	{/if}
</button>


<style>
	.sidebar {
		width: 250px;
		height: 100vh;
		background-color: #ffff;
		border-right: 1px solid #dee2e6;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		transition: transform 0.3s ease;
	}

	.sidebar.sidebar-open {
		transform: translateX(0);
	}

	.sidebar:not(.sidebar-open) {
		transform: translateX(-100%);
	}

	.profile {
		padding: 20px;
		display: flex;
		align-items: center;
		border-bottom: 1px solid #dee2e6;
		font-size: 14px;
	}

	.profile img {
		width: 50px;
		height: 50px;
		border-radius: 20%;
		margin-right: 10px;
		object-fit: cover; /* Menambahkan properti ini agar gambar tidak terdistorsi */
	}

	.p-dot {
		align-items: center;
		display: flex;
		flex-direction: row;
		gap: 5px;
		padding-left: 24px;
		font-size: 12px;
	}

	.welcome-text p {
		margin: 0;
	}

	p {
		font-size: 14px;
	}

	a {
		font-size: 12px;
	}

	.menu {
		list-style: none;
		padding: 0;
		margin: 0;
	}

	.p-menu {
		display: flex;
		flex-direction: row;
		gap: 10px;
		align-items: center;
	}

	.a-menu {
		box-sizing: border-box;
		display: flex;
		flex-direction: row;
		align-items: center;
		padding: 16px 40px;
		gap: 8px;
		width: max;
		height: 56px;
		background: #ffff;

		flex: none;
		order: 1;
		align-self: stretch;
		flex-grow: 0;
	}

	.a-menu:active {
		background-color: f5f6fd;
		border-left: 2px solid #0469ff;
	}

	.a-menu:hover {
		color: #0469ff;
		border-left: 2px solid #0469ff;
	}

	.menu a {
		display: block;
		padding: 15px 20px;
		text-decoration: dotted;
		color: #718284;
	}

	.menu a:hover {
		background-color: #e9ecef;
	}

	.submenu {
		list-style: none;
		padding: 0;
		margin: 0;
		display: none;
	}

	.submenu:active {
		display: block;
	}

	.menu li:hover .submenu {
		display: block;
	}

	.submenu li {
		border: none;
	}

	.footer {
		padding: 20px;
		border-top: 1px solid #dee2e6;
		text-align: center;
	}
    

	.toggle-button {
		position: absolute;
		top: 14px;
		left: 200px; /* Ubah posisi toggle ke kiri */
		background-color: transparent; /* Tombol tanpa latar belakang */
		color: #333; /* Warna ikon */
		border: none;
		padding: 10px;
		cursor: pointer;
		border-radius: 5px;
		transition: background-color 0.3s ease;
	}

	.toggle-button:hover {
		background-color: #f0f0f0; /* Warna latar belakang ketika dihover */
	}

	.toggle-button span {
		font-size: 15px; /* Ukuran ikon */
	}

	.toggle-left {
		left: 20px; /* Ubah kembali ke posisi semula */
	}
</style>
