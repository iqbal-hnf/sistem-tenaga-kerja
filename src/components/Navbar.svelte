<nav>
	<div>
		<div>
			<img src="/logo.png" alt="logo" class="logo-img" width="43" height="42" />
			<a href="">SINTAK</a>
		</div>

		<ul>
			<li>Dashboard</li>
			<li>Lihat Profile</li>
			<li>Berita</li>
			<li>Profile Perusahaan</li>
			<li>Chat</li>
		</ul>
		<div>
			<img src="/profile.jpg" alt="" class="profile-img" />
		</div>
	</div>
</nav>

<style>
	nav > div {
		margin: 0 auto;
		padding: 10px;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		width: 100%;
		background-color: white;
	}
	nav > div > ul {
		list-style: none;
		display: flex;
		flex-direction: row;
	}

	nav > div > ul > li {
		padding: 15px;
	}
	
	.profile-img {
		width: 30px;
		height: 30px;
		border-radius: 50%;
		margin-left: 10px;
	}
	nav > div > div > a {
		font-size: 32px;
		font-family: 'Poppins', sans-serif;
		color: black;
		text-decoration: none;
        
        
	}
	.logo-img {
        margin-right: 10px;
        
	}
    nav > div > div{
        align-items: center;
        display: flex;
        flex-direction: row;
    }
</style>
