<script>
	import {
		HouseDoorFill,
		BriefcaseFill,
		ChevronDown,
		ChevronUp,
		BuildingsFill,
		ClockFill,
		PeopleFill,
		PersonFillCheck,
		CalendarPlusFill,

		Chat



	} from 'svelte-bootstrap-icons';

	
	export let active = 'Dashboard';
	export let isOpen = false;
	export let pagePointer;
	const handleOpen = () => (isOpen = !isOpen);
	let isOpenCompany = false;

	const handleOpenCompany = () => {
		isOpenCompany = !isOpenCompany;
	};
</script>

<aside>
	<div class="sidebar">
		<div class="flex-column p-3" style="gap: 14px;">
			<img src="/images/avatar.png" class="polished-img" />
			<div>
				<div class="flex flex-direction-col flex-center-horizontal">
					<div class="welcome-sidebar">Selamat Datang</div>
					<div class="name-sidebar">Jane Doe</div>
				</div>
			</div>

			<ul class="sidebar-menu">
				{#if pagePointer == 'ams'}
					<li>
						<a
							href="/Admin_citratama/dashboard"
							class="menu {active == 'Dashboard' ? 'menu-active' : ''}"
						>
							<HouseDoorFill
								width="20"
								height="20"
								color={active == 'Dashboard' ? '#00195E' : '#00195E'}
							/>
							<p class="body-side {active == 'Dashboard' ? 'text-active' : ''}">Beranda</p>
						</a>
					</li>
					<li>
						<button
							class="menu {isOpen ? 'menu-active' : ''} justify-content-between"
							on:click={handleOpen}
						>
							<div class="icon-text-gap">
								<BriefcaseFill width="20" height="20" color={isOpen ? '#00195E' : '#00195E'} />
								<p class="body-small-semi-bold {isOpen ? 'text-active' : ''}">Pelamar</p>
							</div>
							{#if isOpen}
								<ChevronUp width="20" height="20" color="#00195E" />
							{:else}
								<ChevronDown width="20" height="20" color="#00195E" />
							{/if}
						</button>
						{#if isOpen}
							<div class="menu-dropdown">
								<a href="/Admin_citratama/pelamar" class="menu-dropdown-item">
									<div class="flex gap-4">
										<BriefcaseFill width="20" height="20" color="transparent" />
										<p
											class="body-small-semi-bold {active == 'Pelamar Kerja' ? 'text-active' : ''}"
										>
											Data Pelamar
										</p>
									</div>
								</a>
								<a href="/Admin_citratama/persetujuan" class="menu-dropdown-item">
									<div class="flex gap-4">
										<BriefcaseFill width="20" height="20" color="transparent" />
										<p class="body-small-semi-bold {active == 'Persetujuan' ? 'text-active' : ''}">
											Persetujuan
										</p>
									</div>
								</a>
								<a href="/Admin_citratama/penerimaan-pelamar" class="menu-dropdown-item">
									<div class="flex gap-4">
										<BriefcaseFill width="20" height="20" color="transparent" />
										<p class="body-small-semi-bold {active == 'Penerimaan' ? 'text-active' : ''}">
											Penerimaan-pelamar
										</p>
									</div>
								</a>
								<a href="/Admin_citratama/berita" class="menu-dropdown-item">
									<div class="flex gap-4">
										<BriefcaseFill width="20" height="20" color="transparent" />
										<p class="body-small-semi-bold {active == 'Berita' ? 'text-active' : ''}">
											Berita
										</p>
									</div>
								</a>
								<a href="/Admin_citratama/akun-pelamar" class="menu-dropdown-item">
									<div class="flex gap-4">
										<BriefcaseFill width="20" height="20" color="transparent" />
										<p class="body-small-semi-bold {active == 'Berita' ? 'text-active' : ''}">
											Akun Pelamar
										</p>
									</div>
								</a>
							</div>
						{/if}
					</li>
					<li>
						<button
							class="menu {isOpenCompany ? 'menu-active' : ''} justify-content-between"
							on:click={handleOpenCompany}
						>
							<div class="icon-text-gap">
								<BuildingsFill
									width="20"
									height="20"
									color={isOpenCompany ? '#00195E' : '#00195E'}
								/>
								<p class="body-small-semi-bold {isOpenCompany ? 'text-active' : ''}">Perusahaan</p>
							</div>
							{#if isOpenCompany}
								<ChevronUp width="20" height="20" color="#00195E" />
							{:else}
								<ChevronDown width="20" height="20" color="#00195E" />
							{/if}
						</button>
						{#if isOpenCompany}
							<div class="menu-dropdown">
								<a href="/Admin_citratama/perusahaan" class="menu-dropdown-item">
									<div class="icon-text-gap">
										<BuildingsFill width="20" height="20" color="transparent" />
										<p
											class="body-small-semi-bold {active == 'Data Perusahaan'
												? 'text-active'
												: ''}"
										>
											Data Perusahaan
										</p>
									</div>
								</a>
								<a href="/Admin_citratama/akun-perusahaan" class="menu-dropdown-item">
									<div class="icon-text-gap">
										<BuildingsFill width="20" height="20" color="transparent" />
										<p
											class="body-small-semi-bold {active == 'Akun Perusahaan'
												? 'text-active'
												: ''}"
										>
											Akun Perusahaan
										</p>
									</div>
								</a>
							</div>
						{/if}
						
					</li>

					<li>
						<a
							href="/Admin_citratama/jadwal"
							class="menu {active == 'Paket Kursus' ? 'menu-active' : ''}"
						>
							<ClockFill
								width="20"
								height="20"
								color={active == 'Paket Kursus' ? '#00195E' : '#00195E'}
							/>
							<p
								class="body-small-semi-bold {active == 'Jadwal'
									? '00195E'
									: '00195E'}"
							>
								jadwal
							</p>
						</a>
					</li>
					<li>
						<a
							href="/Admin_citratama/chatbot"
							class="menu {active == 'Paket Kursus' ? 'menu-active' : ''}"
						>
							<Chat
								width="20"
								height="20"
								color={active == 'Paket Kursus' ? '#00195E' : '#00195E'}
							/>
							<p
								class="body-small-semi-bold {active == 'Jadwal'
									? '00195E'
									: '00195E'}"
							>
								Chatbot
							</p>
						</a>
					</li>


					<!-- Additional Menu Items -->
				{:else if pagePointer == 'mitra'}
					<li>
						<a
							href="/Admin_mitra/dashboard"
							class="menu body-small-semi-bold {active == 'Dashboard' ? 'menu-active' : ''}"
						>
							<HouseDoorFill
								width="20"
								height="20"
								color={active == 'Dashboard' ? '#3951A8' : '#8191AC'}
							/>
							<p>Beranda</p>
						</a>
					</li>
					<li>
						<a
							href="/Admin_mitra/pelamar"
							class="menu {active == 'Paket Kursus' ? 'menu-active' : ''}"
						>
							<PeopleFill
								width="20"
								height="20"
								color={active == 'Paket Kursus' ? '#00195E' : '#00195E'}
							/>
							<p
								class="body-small-semi-bold {active == 'Jadwal'
									? '00195E'
									: '00195E'}"
							>
								Data Pelamar 
							</p>
						</a>
					</li>
					<li>
						<a
							href="/Admin_mitra/persetujuan"
							class="menu {active == 'Paket Kursus' ? 'menu-active' : ''}"
						>
							<PersonFillCheck
								width="20"
								height="20"
								color={active == 'Paket Kursus' ? '#00195E' : '#00195E'}
							/>
							<p
								class="body-small-semi-bold {active == 'Jadwal'
									? '00195E'
									: '00195E'}"
							>
								Persetujuan Pelamar
							</p>
						</a>
					</li>
					<li>
						<a
							href="/Admin_mitra/penerimaan-pelamar"
							class="menu {active == 'Paket Kursus' ? 'menu-active' : ''}"
						>
							<PersonFillCheck
								width="20"
								height="20"
								color={active == 'Paket Kursus' ? '#00195E' : '#00195E'}
							/>
							<p
								class="body-small-semi-bold {active == 'Jadwal'
									? '00195E'
									: '00195E'}"
							>
								Penerimaan Pelamar
							</p>
						</a>
					</li>
					<li>
						<a
							href="/Admin_mitra/jadwal"
							class="menu {active == 'Paket Kursus' ? 'menu-active' : ''}"
						>
							<CalendarPlusFill
								width="20"
								height="20"
								color={active == 'Paket Kursus' ? '#00195E' : '#00195E'}
							/>
							<p
								class="body-small-semi-bold {active == 'Jadwal'
									? '00195E'
									: '00195E'}"
							>
								jadwal
							</p>
						</a>
					</li>

				{/if}
			</ul>
		</div>
		<div class="flex-column gap-2 px-4 py-3">
			<div class="h5">Citratama citratama_indonesia?igsh</div>
			<div class="body-small-reguler">©2024 CITRATAMA. Semua hak dilindungi.</div>
		</div>
	</div>
</aside>

<style>
	aside {
		background-color: var(--neutral-white);
		display: flex;
		width: 18.5rem;
		max-width: 18.5rem;
		height: 100vh;
		max-height: 100%;
		position: sticky;
		top: 0;
	}

	aside > div {
		overflow-y: auto;
	}

	.sidebar {
		display: flex;
		flex-direction: column;
		flex-grow: 1;
		justify-content: space-between;
		
	}

	button {
		color: #00195e;
		font-family: 'Poppins', sans-serif;
		font-weight: 400;
	}
	.sidebar-menu {
		padding: 0;
		margin: 0;
		list-style: none;
		display: flex;
		flex-direction: column;
		gap: 14px;
	}
	p {
		font-size: 14px;
	}

	.menu {
		font-family: 'Poppins', sans-serif;
		display: flex;
		gap: 24px;
		padding: 20px 14px;
		align-items: center;
		border-radius: 0.25rem;
		cursor: pointer;
		border: none;
		width: 100%;
		background-color: transparent;
		transition: all 0.25s ease;
		size: 12px;
	}

	.menu:hover {
		background-color: #f5f6fd;
		padding: 1.375rem 0.875rem;
	}

	.menu-dropdown-item {
		padding: 20px 14px;
		transition: all 0.25s ease;
		border-radius: 0.25rem;
		display: flex;
		align-items: center;
	}

	.menu-dropdown-item:hover {
		background-color: #f5f6fd;
	}

	.menu-active {
		background-color: #f5f6fd;
	}

	.text-active {
		color: #667BC6;
	}

	a {
		text-decoration: none;
		color: #00195e;
	}

	.icon-text-gap {
		display: flex;
		align-items: center;
		gap: 24px;
	}
	.body-small-reguler{
		font-size: 14px;
	}
</style>
