<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import Navbar from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import { fly, scale } from 'svelte/transition';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import axios from 'axios';
	import Button from '../../../components/Button.svelte';
	

	let data;
	let status = false;

	axios
		.get('https://sinaker.pocari.id/api/admin/mitra')
		.then((response) => {
			status = true;
			data = response.data;
			console.log(data);
		})
		.catch((error) => {
			console.error('Ada kesalahan:', error);
		});

	function handleClick() {
		window.location.href = '/Admin_citratama/tambah-akun'; // Arahkan ke URL tujuan
	}
</script>

<div id="after-login-layout">
	<NavbarAdmin />
	<div class="flex">
		<Sidebar active="Data Perusahaan" pagePointer="ams" />
		<div class="w-100 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="flex flex-between-horizontal w-100">
					<div class="title-content">Akun Perusahaan</div>
				</div>
				<div>
					<Button classList="btn-tambah" onClick={handleClick}>tambah Akun</Button>
				</div>
				<div class="flex flex-direction-col flex-gap-regular">
					<div class="card w-80 height-fit">
						<div class="flex flex-gap-regular">
							<div class="flex flex-gap-small flex-center-vertical w-25">
								<div class="text-drop-card">Email</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<!-- <div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Password</div>
								<img src="/images/icons/Arrow.svg" />
							</div> -->
							<div class="flex flex-gap-small flex-center-vertical w-25">
								<div class="text-drop-card">Nama Perusahaan</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Alamat</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">No Handphone</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Bidang Usaha</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-15">
								<div class="text-drop-card">Role</div>
							</div>
						</div>
					</div>
					{#if status}
						{#each data as d}
							<div class="card w-80 height-fit">
								<div class="flex flex-direction-col flex-gap-regular">
									<div class="flex flex-gap-regular">
										<div class="flex flex-gap-small flex-center-vertical w-25">
											<div class="text-drop-card">{d.email}</div>
										</div>
										<!-- <div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">{d.password}</div>
										</div> -->
										<div class="flex flex-gap-small flex-center-vertical w-25">
											<div class="text-drop-card">{d.info.name}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">{d.info.alamat}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">{d.info.no_HP}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">{d.info.bidang_usaha}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-15">
											<div class="text-drop-card">{d.role}</div>
										</div>
									</div>
								</div>
							</div>
						{/each}
					{/if}
				</div>
			</div>
		</div>
	</div>
</div>
