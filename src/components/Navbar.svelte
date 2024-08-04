<script>
    import { PersonFill, BoxArrowLeft, ChevronDown, BellFill } from 'svelte-bootstrap-icons';
    import axios from 'axios';
    import { onMount } from 'svelte';

    let isOpen = false;
    let isNotificationsOpen = false;
    let notifications = [];
    let status = false;

    const toggleProfile = () => {
        isOpen = !isOpen;
    };

    const toggleNotifications = () => {
        isNotificationsOpen = !isNotificationsOpen;
    };

    const handleLogout = async () => {
        const userConfirmed = confirm('Apakah Anda ingin logout?');
        if (userConfirmed) {
            try {
                const response = await axios.post(
                    'https://sinaker.pocari.id/api/logout',
                    {},
                    {
                        headers: {
                            Authorization: `Bearer ${localStorage.getItem('token')}`
                        }
                    }
                );
                if (response.status === 200) {
                    alert('Successfully logged out');
                    localStorage.removeItem('token');
                    window.location.href = '/User/Login';
                } else {
                    alert('Failed to logout. Please try again.');
                }
            } catch (error) {
                console.error('Error logging out:', error);
                alert('Error logging out. Please try again.');
            }
        }
    };
    

    onMount(async () => {
        const token = localStorage.getItem('token');
        console.log(token);
        try {
            const response = await axios.get('https://sinaker.pocari.id/api/notifUser', {
                headers: {
                    Authorization: `Bearer ${token}`
                }
            });
            console.log(token);
            status = true;
            notifications = response.data;
            console.log('Filtered notifications:', notifications);
        } catch (error) {
            console.error('Error fetching notifications:', error);
            if (error.response) {
                console.error('Response data:', error.response.data);
                console.error('Response status:', error.response.status);
                console.error('Response headers:', error.response.headers);     
            }
        }
    });
    

</script>


<nav class="navbar">
	<img src="/logo.png" alt="logo" class="navbar-logo" />
	<ul class="navbar-list">
		<li><a href="/User/Dashboard">Dashboard</a></li>
		<li><a href="/User/lihat_profile">Lihat Profile</a></li>
		<li><a href="/User/Berita">Berita</a></li>
		<li><a href="/User/Profile_perusahaan">Profile Perusahaan</a></li>
	</ul>

	<div class="profile-dropdown">
		<div class="notifications">
			<button class="notifications-btn" on:click={toggleNotifications}>
				<BellFill />
				<span class="badge">{notifications.length}</span>
			</button>
			{#if status}
				<ul class="notifications-list {isNotificationsOpen ? 'active' : ''}">
					{#each notifications as notif}
						<li class="notification-item">{notif.data.message}</li>
					{/each}
				</ul>
			{/if}
		</div>
		<div class="profile-dropdown-btn" on:click={toggleProfile}>
			<div class="profile-img">
				<i class="fa-solid fa-circle-question"></i>
			</div>
			<span>Hanafi</span>
			<i class="fa-solid fa-angle-down"><ChevronDown /></i>
		</div>
		<ul class="profile-dropdown-list {isOpen ? 'active' : ''}">
			<li class="profile-dropdown-list-item">
				<a href="#">
					<i class="fa-reguler fa-user"><PersonFill /> </i>
					Edit Profile
				</a>
			</li>
			<li class="profile-dropdown-list-item">
				<a href="#" on:click={handleLogout}>
					<i class="fa-reguler fa-user"><BoxArrowLeft /></i>
					Log Out
				</a>
			</li>
		</ul>
	</div>
</nav>


<style>
	/* Your existing CSS styles */
	:root {
		--primary: #eeeeee;
		--secondary: #00195e;
		--blue: #0f67b1;
		--secondary-light: rgba(48, 182, 255, 0.2);
		--secondary-light-2: rgba(48, 182, 255, 0.1);
		--white: #fff;
		--black: #393e46;
		--shadow: 0px 2px 8px 0px var(--secondary-light);
	}

	* {
		margin: 0;
		padding: 0;
		list-style-type: none;
		box-sizing: border-box;
	}

	.navbar {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		height: 70px;
		background-color: var(--white);
		padding: 0 8%;
	}

	.navbar-logo {
		cursor: pointer;
		width: 48px;
		height: 48px;
	}

	.navbar-list {
		display: flex;
		flex-direction: row;
		gap: 18px;
		align-items: center;
	}

	.navbar-list li {
		display: inline-block;
	}

	.navbar-list li a:hover {
		color: var(--blue);
	}

	.navbar-list li a:active {
		color: var(--blue);
	}

	.navbar-list li a {
		font-size: 16px;
		font-weight: 500;
		text-decoration: none;
		color: var(--black);
	}

	.notifications {
		position: relative;
	}

	.notifications-btn {
		position: relative;
		background: none;
		border: none;
		cursor: pointer;
		font-size: 1.5rem;
		color: var(--black);
	}

	.badge {
		position: absolute;
		top: -10px;
		right: -10px;
		background: red;
		color: white;
		border-radius: 50%;
		padding: 0.2rem 0.5rem;
		font-size: 0.8rem;
	}

	.notifications-list {
		position: absolute;
		top: 40px;
		right: 0;
		background-color: var(--primary);
		border-radius: 10px;
		box-shadow: var(--shadow);
		max-height: 0;
		overflow: hidden;
		transition: max-height 0.3s ease-in-out;
		width: 250px;
		z-index: 1000;
	}

	.notifications-list.active {
		max-height: 300px;
	}

	.notification-item {
		padding: 0.5rem 1rem;
		border-bottom: 1px solid var(--secondary-light-2);
		transition: background-color 0.2s;
        font-size: 12px;
        
	}
   

	.notification-item:hover {
		background-color: var(--secondary-light);
	}

	.profile-dropdown {
		position: relative;
		width: fit-content;
		display: flex;
		flex-direction: row;
		gap: 24px;
	}

	.profile-dropdown-list {
		position: absolute;
		top: 58px;
		width: 180px;
		right: 0;
		background-color: var(--primary);
		border-radius: 10px;
		box-shadow: var(--shadow);
		font-size: 12px;
		max-height: 0;
		overflow: hidden;
		z-index: 1000;
		transition: max-height 0.3s ease-in-out;
	}

	.profile-dropdown-list.active {
		max-height: 500px;
	}

	.profile-dropdown-list-item {
		padding: 0.5rem 0 0.5rem 1rem;
		transition:
			background-color 0.2s,
			padding-left 0.2s;
	}

	.profile-dropdown-list-item a i {
		margin-right: 0.8rem;
		font-size: 1.1rem;
		width: 2.3rem;
		height: 2.3rem;
		background-color: var(--secondary);
		color: var(--white);
		border-radius: 50%;
		line-height: 2.4rem;
		text-align: center;
	}

	.profile-dropdown-list-item:hover {
		padding-left: 1.5rem;
		background-color: var(--secondary-light-2);
	}

	.profile-dropdown-list-item a {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 6px;
		text-decoration: none;
		font-weight: 500;
		color: var(--black);
	}

	.profile-img {
		width: 40px;
		height: 40px;
		border-radius: 50%;
		background-image: url(/people.jpg);
		background-size: cover;
		position: relative;
	}

	.profile-img i {
		position: absolute;
		right: 0;
		bottom: 0.3rem;
		color: var(--blue);
	}

	.profile-dropdown-btn {
		display: flex;
		width: 150px;
		align-items: center;
		justify-content: space-between;
		padding-right: 1rem;
		font-size: 0.9rem;
		border: 1px solid var(--secondary);
		border-radius: 50px;
		cursor: pointer;
		height: 38px;
		transition:
			box-shadow 0.2s,
			background-color 0.2s;
	}

	.profile-dropdown-btn:hover {
		background-color: var(--secondary-light-2);
		box-shadow: var(--shadow);
	}

	.profile-dropdown-btn span {
		font-weight: 500;
		margin: 0 0.5rem;
		margin-right: 0;
	}

	.profile-dropdown-btn i {
		display: flex;
		align-items: center;
		font-weight: 500;
	}
</style>
