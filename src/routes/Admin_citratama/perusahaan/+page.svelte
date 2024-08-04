<script type="text/javascript">
	import Sidebar from '../../../components/Sidebar.svelte';
	import Navbar from '../../../components/Navbar-admin.svelte';
	import { onMount } from 'svelte';
	import { fly, scale } from 'svelte/transition';
	import NavbarAdmin from '../../../components/Navbar-admin.svelte';
	import axios from 'axios';

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
</script>

<div id="after-login-layout">
	<NavbarAdmin />
	<div class="flex">
		<Sidebar active="Data Perusahaan" pagePointer="ams" />
		<div class="w-100 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="flex flex-between-horizontal w-100">
					<div class="title-content">Data Perusahaan</div>
				</div>
				<div class="flex flex-direction-col flex-gap-regular">
					<div class="card w-80 height-fit">
						<div class="flex flex-gap-regular">
							<div class="flex flex-gap-small flex-center-vertical w-25">
								<div class="text-drop-card">Nama</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Alamat Lengkap</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-15">
								<div class="text-drop-card">No Handphone</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Bidang Usaha</div>
								<img src="/images/icons/Arrow.svg" />
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-5">
								<div class="text-drop-card">Aksi</div>
							</div>
						</div>
					</div>
					{#if status}
						{#each data as d}
							<div class="card w-80 height-fit">
								<div class="flex flex-direction-col flex-gap-regular">
									<div class="flex flex-gap-regular">
										<div class="flex flex-gap-small flex-center-vertical w-25">
											<div class="text-drop-card">{d.info.name}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">
												{d.info.alamat}
											</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-15">
											<div class="text-drop-card">{d.info.no_HP}</div>
										</div>
										<div class="flex flex-gap-small flex-center-vertical w-20">
											<div class="text-drop-card">{d.info.bidang_usaha}</div>
										</div>
										<div class="flex flex-gap-regular flex-center-vertical">
											<svg
												width="16"
												height="16"
												viewBox="0 0 16 16"
												fill="none"
												xmlns="http://www.w3.org/2000/svg"
											>
												<path
													d="M15.8538 0.146461C15.9952 0.287892 16.0388 0.500002 15.9645 0.68571L10.1456 15.2328C9.91865 15.8003 9.14465 15.8725 8.81653 15.3569L5.63806 10.3622L0.643323 7.18372C0.127708 6.8556 0.199981 6.0816 0.767436 5.85462L15.3145 0.0357762C15.5003 -0.0385071 15.7124 0.00502989 15.8538 0.146461ZM6.6374 10.07L9.39831 14.4085L14.1313 2.57605L6.6374 10.07ZM13.4242 1.86895L1.59172 6.60194L5.9303 9.36285L13.4242 1.86895Z"
													fill="#4361EE"
												/>
											</svg>
										</div>
										<div class="flex flex-gap-regular flex-center-vertical">
											<svg
												width="16"
												height="16"
												viewBox="0 0 16 16"
												fill="none"
												xmlns="http://www.w3.org/2000/svg"
											>
												<path
													d="M12.1465 0.146447C12.3417 -0.0488155 12.6583 -0.0488155 12.8536 0.146447L15.8536 3.14645C16.0488 3.34171 16.0488 3.65829 15.8536 3.85355L5.85357 13.8536C5.80569 13.9014 5.74858 13.9391 5.68571 13.9642L0.68571 15.9642C0.500001 16.0385 0.287892 15.995 0.146461 15.8536C0.00502989 15.7121 -0.0385071 15.5 0.0357762 15.3143L2.03578 10.3143C2.06092 10.2514 2.09858 10.1943 2.14646 10.1464L12.1465 0.146447ZM11.2071 2.5L13.5 4.79289L14.7929 3.5L12.5 1.20711L11.2071 2.5ZM12.7929 5.5L10.5 3.20711L4.00001 9.70711V10H4.50001C4.77616 10 5.00001 10.2239 5.00001 10.5V11H5.50001C5.77616 11 6.00001 11.2239 6.00001 11.5V12H6.29291L12.7929 5.5ZM3.03167 10.6755L2.92614 10.781L1.39754 14.6025L5.21903 13.0739L5.32456 12.9683C5.13496 12.8973 5.00001 12.7144 5.00001 12.5V12H4.50001C4.22387 12 4.00001 11.7761 4.00001 11.5V11H3.50001C3.28561 11 3.10272 10.865 3.03167 10.6755Z"
													fill="#00AB55"
												/>
											</svg>
										</div>
										<div class="flex flex-gap-regular flex-center-vertical">
											<svg
												width="16"
												height="16"
												viewBox="0 0 16 16"
												fill="none"
												xmlns="http://www.w3.org/2000/svg"
											>
												<path
													d="M4.92308 5.86667C5.26294 5.86667 5.53846 6.10545 5.53846 6.4V12.8C5.53846 13.0946 5.26294 13.3333 4.92308 13.3333C4.58321 13.3333 4.30769 13.0946 4.30769 12.8V6.4C4.30769 6.10545 4.58321 5.86667 4.92308 5.86667Z"
													fill="#E7515A"
												/>
												<path
													d="M8 5.86667C8.33987 5.86667 8.61538 6.10545 8.61538 6.4V12.8C8.61538 13.0946 8.33987 13.3333 8 13.3333C7.66013 13.3333 7.38462 13.0946 7.38462 12.8V6.4C7.38462 6.10545 7.66013 5.86667 8 5.86667Z"
													fill="#E7515A"
												/>
												<path
													d="M11.6923 6.4C11.6923 6.10545 11.4168 5.86667 11.0769 5.86667C10.7371 5.86667 10.4615 6.10545 10.4615 6.4V12.8C10.4615 13.0946 10.7371 13.3333 11.0769 13.3333C11.4168 13.3333 11.6923 13.0946 11.6923 12.8V6.4Z"
													fill="#E7515A"
												/>
												<path
													d="M16 3.2C16 3.7891 15.449 4.26667 14.7692 4.26667H14.1538V13.8667C14.1538 15.0449 13.0518 16 11.6923 16H4.30769C2.94822 16 1.84615 15.0449 1.84615 13.8667V4.26667H1.23077C0.551034 4.26667 0 3.7891 0 3.2V2.13333C0 1.54423 0.551034 1.06667 1.23077 1.06667H5.53846C5.53846 0.477563 6.0895 0 6.76923 0H9.23077C9.91051 0 10.4615 0.477563 10.4615 1.06667H14.7692C15.449 1.06667 16 1.54423 16 2.13333V3.2ZM3.2222 4.26667L3.07692 4.32962V13.8667C3.07692 14.4558 3.62796 14.9333 4.30769 14.9333H11.6923C12.372 14.9333 12.9231 14.4558 12.9231 13.8667V4.32962L12.7778 4.26667H3.2222ZM1.23077 3.2H14.7692V2.13333H1.23077V3.2Z"
													fill="#E7515A"
												/>
											</svg>
										</div>
									</div>
								</div>
							</div>
						{/each}
					{/if}
				</div>

				<!-- <div class="card w-80 height-fit">
					<div class="flex flex-direction-col flex-gap-regular">
						<div class="flex flex-gap-regular">
							<div class="flex flex-gap-small flex-center-vertical w-25">
								<div class="text-drop-card">PT. ALSINDO PEKANBARU</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">
									Jl. Duyung, Tengkerang Bar., Kec. Marpoyan Damai, Kota Pekanbaru, Riau 28125
								</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-15">
								<div class="text-drop-card">(0761) 586528</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Manajemen korporat.</div>
							</div>
							<div class="flex flex-gap-regular flex-center-vertical">
								<svg
									width="16"
									height="16"
									viewBox="0 0 16 16"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<path
										d="M15.8538 0.146461C15.9952 0.287892 16.0388 0.500002 15.9645 0.68571L10.1456 15.2328C9.91865 15.8003 9.14465 15.8725 8.81653 15.3569L5.63806 10.3622L0.643323 7.18372C0.127708 6.8556 0.199981 6.0816 0.767436 5.85462L15.3145 0.0357762C15.5003 -0.0385071 15.7124 0.00502989 15.8538 0.146461ZM6.6374 10.07L9.39831 14.4085L14.1313 2.57605L6.6374 10.07ZM13.4242 1.86895L1.59172 6.60194L5.9303 9.36285L13.4242 1.86895Z"
										fill="#4361EE"
									/>
								</svg>
							</div>
							<div class="flex flex-gap-regular flex-center-vertical">
								<svg
									width="16"
									height="16"
									viewBox="0 0 16 16"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<path
										d="M12.1465 0.146447C12.3417 -0.0488155 12.6583 -0.0488155 12.8536 0.146447L15.8536 3.14645C16.0488 3.34171 16.0488 3.65829 15.8536 3.85355L5.85357 13.8536C5.80569 13.9014 5.74858 13.9391 5.68571 13.9642L0.68571 15.9642C0.500001 16.0385 0.287892 15.995 0.146461 15.8536C0.00502989 15.7121 -0.0385071 15.5 0.0357762 15.3143L2.03578 10.3143C2.06092 10.2514 2.09858 10.1943 2.14646 10.1464L12.1465 0.146447ZM11.2071 2.5L13.5 4.79289L14.7929 3.5L12.5 1.20711L11.2071 2.5ZM12.7929 5.5L10.5 3.20711L4.00001 9.70711V10H4.50001C4.77616 10 5.00001 10.2239 5.00001 10.5V11H5.50001C5.77616 11 6.00001 11.2239 6.00001 11.5V12H6.29291L12.7929 5.5ZM3.03167 10.6755L2.92614 10.781L1.39754 14.6025L5.21903 13.0739L5.32456 12.9683C5.13496 12.8973 5.00001 12.7144 5.00001 12.5V12H4.50001C4.22387 12 4.00001 11.7761 4.00001 11.5V11H3.50001C3.28561 11 3.10272 10.865 3.03167 10.6755Z"
										fill="#00AB55"
									/>
								</svg>
							</div>
							<div class="flex flex-gap-regular flex-center-vertical">
								<svg
									width="16"
									height="16"
									viewBox="0 0 16 16"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<path
										d="M4.92308 5.86667C5.26294 5.86667 5.53846 6.10545 5.53846 6.4V12.8C5.53846 13.0946 5.26294 13.3333 4.92308 13.3333C4.58321 13.3333 4.30769 13.0946 4.30769 12.8V6.4C4.30769 6.10545 4.58321 5.86667 4.92308 5.86667Z"
										fill="#E7515A"
									/>
									<path
										d="M8 5.86667C8.33987 5.86667 8.61538 6.10545 8.61538 6.4V12.8C8.61538 13.0946 8.33987 13.3333 8 13.3333C7.66013 13.3333 7.38462 13.0946 7.38462 12.8V6.4C7.38462 6.10545 7.66013 5.86667 8 5.86667Z"
										fill="#E7515A"
									/>
									<path
										d="M11.6923 6.4C11.6923 6.10545 11.4168 5.86667 11.0769 5.86667C10.7371 5.86667 10.4615 6.10545 10.4615 6.4V12.8C10.4615 13.0946 10.7371 13.3333 11.0769 13.3333C11.4168 13.3333 11.6923 13.0946 11.6923 12.8V6.4Z"
										fill="#E7515A"
									/>
									<path
										d="M16 3.2C16 3.7891 15.449 4.26667 14.7692 4.26667H14.1538V13.8667C14.1538 15.0449 13.0518 16 11.6923 16H4.30769C2.94822 16 1.84615 15.0449 1.84615 13.8667V4.26667H1.23077C0.551034 4.26667 0 3.7891 0 3.2V2.13333C0 1.54423 0.551034 1.06667 1.23077 1.06667H5.53846C5.53846 0.477563 6.0895 0 6.76923 0H9.23077C9.91051 0 10.4615 0.477563 10.4615 1.06667H14.7692C15.449 1.06667 16 1.54423 16 2.13333V3.2ZM3.2222 4.26667L3.07692 4.32962V13.8667C3.07692 14.4558 3.62796 14.9333 4.30769 14.9333H11.6923C12.372 14.9333 12.9231 14.4558 12.9231 13.8667V4.32962L12.7778 4.26667H3.2222ZM1.23077 3.2H14.7692V2.13333H1.23077V3.2Z"
										fill="#E7515A"
									/>
								</svg>
							</div>
						</div>
					</div>
				</div>

				<div class="card w-80 height-fit">
					<div class="flex flex-direction-col flex-gap-regular">
						<div class="flex flex-gap-regular">
							<div class="flex flex-gap-small flex-center-vertical w-25">
								<div class="text-drop-card">PT. ALSINDO PEKANBARU</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">
									Jl. Duyung, Tengkerang Bar., Kec. Marpoyan Damai, Kota Pekanbaru, Riau 28125
								</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-15">
								<div class="text-drop-card">(0761) 586528</div>
							</div>
							<div class="flex flex-gap-small flex-center-vertical w-20">
								<div class="text-drop-card">Manajemen korporat.</div>
							</div>
							<div class="flex flex-gap-regular flex-center-vertical">
								<svg
									width="16"
									height="16"
									viewBox="0 0 16 16"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<path
										d="M15.8538 0.146461C15.9952 0.287892 16.0388 0.500002 15.9645 0.68571L10.1456 15.2328C9.91865 15.8003 9.14465 15.8725 8.81653 15.3569L5.63806 10.3622L0.643323 7.18372C0.127708 6.8556 0.199981 6.0816 0.767436 5.85462L15.3145 0.0357762C15.5003 -0.0385071 15.7124 0.00502989 15.8538 0.146461ZM6.6374 10.07L9.39831 14.4085L14.1313 2.57605L6.6374 10.07ZM13.4242 1.86895L1.59172 6.60194L5.9303 9.36285L13.4242 1.86895Z"
										fill="#4361EE"
									/>
								</svg>
							</div>
							<div class="flex flex-gap-regular flex-center-vertical">
								<svg
									width="16"
									height="16"
									viewBox="0 0 16 16"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<path
										d="M12.1465 0.146447C12.3417 -0.0488155 12.6583 -0.0488155 12.8536 0.146447L15.8536 3.14645C16.0488 3.34171 16.0488 3.65829 15.8536 3.85355L5.85357 13.8536C5.80569 13.9014 5.74858 13.9391 5.68571 13.9642L0.68571 15.9642C0.500001 16.0385 0.287892 15.995 0.146461 15.8536C0.00502989 15.7121 -0.0385071 15.5 0.0357762 15.3143L2.03578 10.3143C2.06092 10.2514 2.09858 10.1943 2.14646 10.1464L12.1465 0.146447ZM11.2071 2.5L13.5 4.79289L14.7929 3.5L12.5 1.20711L11.2071 2.5ZM12.7929 5.5L10.5 3.20711L4.00001 9.70711V10H4.50001C4.77616 10 5.00001 10.2239 5.00001 10.5V11H5.50001C5.77616 11 6.00001 11.2239 6.00001 11.5V12H6.29291L12.7929 5.5ZM3.03167 10.6755L2.92614 10.781L1.39754 14.6025L5.21903 13.0739L5.32456 12.9683C5.13496 12.8973 5.00001 12.7144 5.00001 12.5V12H4.50001C4.22387 12 4.00001 11.7761 4.00001 11.5V11H3.50001C3.28561 11 3.10272 10.865 3.03167 10.6755Z"
										fill="#00AB55"
									/>
								</svg>
							</div>
							<div class="flex flex-gap-regular flex-center-vertical">
								<svg
									width="16"
									height="16"
									viewBox="0 0 16 16"
									fill="none"
									xmlns="http://www.w3.org/2000/svg"
								>
									<path
										d="M4.92308 5.86667C5.26294 5.86667 5.53846 6.10545 5.53846 6.4V12.8C5.53846 13.0946 5.26294 13.3333 4.92308 13.3333C4.58321 13.3333 4.30769 13.0946 4.30769 12.8V6.4C4.30769 6.10545 4.58321 5.86667 4.92308 5.86667Z"
										fill="#E7515A"
									/>
									<path
										d="M8 5.86667C8.33987 5.86667 8.61538 6.10545 8.61538 6.4V12.8C8.61538 13.0946 8.33987 13.3333 8 13.3333C7.66013 13.3333 7.38462 13.0946 7.38462 12.8V6.4C7.38462 6.10545 7.66013 5.86667 8 5.86667Z"
										fill="#E7515A"
									/>
									<path
										d="M11.6923 6.4C11.6923 6.10545 11.4168 5.86667 11.0769 5.86667C10.7371 5.86667 10.4615 6.10545 10.4615 6.4V12.8C10.4615 13.0946 10.7371 13.3333 11.0769 13.3333C11.4168 13.3333 11.6923 13.0946 11.6923 12.8V6.4Z"
										fill="#E7515A"
									/>
									<path
										d="M16 3.2C16 3.7891 15.449 4.26667 14.7692 4.26667H14.1538V13.8667C14.1538 15.0449 13.0518 16 11.6923 16H4.30769C2.94822 16 1.84615 15.0449 1.84615 13.8667V4.26667H1.23077C0.551034 4.26667 0 3.7891 0 3.2V2.13333C0 1.54423 0.551034 1.06667 1.23077 1.06667H5.53846C5.53846 0.477563 6.0895 0 6.76923 0H9.23077C9.91051 0 10.4615 0.477563 10.4615 1.06667H14.7692C15.449 1.06667 16 1.54423 16 2.13333V3.2ZM3.2222 4.26667L3.07692 4.32962V13.8667C3.07692 14.4558 3.62796 14.9333 4.30769 14.9333H11.6923C12.372 14.9333 12.9231 14.4558 12.9231 13.8667V4.32962L12.7778 4.26667H3.2222ZM1.23077 3.2H14.7692V2.13333H1.23077V3.2Z"
										fill="#E7515A"
									/>
								</svg>
							</div>
						</div>
					</div>
				</div> -->
			</div>
		</div>
	</div>
</div>
