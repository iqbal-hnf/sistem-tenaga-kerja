<script type="text/javascript">
	import Sidebar from '../../../components/sidebar.svelte'
	import Navbar from '../../../components/navbar.svelte'
	import { onMount } from 'svelte';
	import {fly, scale} from 'svelte/transition'
	

	let reportList = null

	let getWeeklyReport = () => {
		ApiController({
			method: "POST",
			endpoint: `weekly-report`
		}).then(response => {
			reportList =  response.data.data
		})
	}
	
	onMount(() => {
		getWeeklyReport()
	})

</script>

<div id="after-login-layout">
	<Navbar/>
	<div class="flex">
		<Sidebar statusPointer="Laporan" pagePointer="admin"/>
		<div class="w-80 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="flex flex-between-horizontal flex-center-vertical w-100">
					<div class="title-content">Laporan Mingguan</div>
					<div class="flex flex-gap-regular">
						<button class="btn-outline flex flex-center-vertical flex-gap-small"><span>Download Laporan Mingguan</span> <img src="/images/icons/File_Download.svg"></button>
					</div>
				</div>
				<div class="flex flex-direction-col flex-gap-regular">
					<div class="flex">
						<select class="select-col-2 w-25">
							<option disabled selected>Semua Perum</option>
							<option>Epicentrum Sepatan</option>
							<option>Serpong</option>
						</select>
					</div>
					<div class="flex flex-gap-semi-large w-100">
						<select class="select-col-3 w-15">
							<option>2023</option>
							<option>Serpong</option>
						</select>
						<select class="select-col-3 w-15">
							<option>Mingguan</option>
							<option>Serpong</option>
						</select>
					</div>
					<div class="scroll-x overflow-hidden flex-direction-col flex-gap-regular">
						<div class="card-head height-fit">
							<div class="flex">
								<div class="flex flex-gap-small flex-center-vertical w-10 border-separate">
									<div class="text-drop-card">NPK</div>
									<img src="/image/icon/Arrow.svg">
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 border-separate">
									<div class="text-drop-card">Nama</div>
									<img src="/image/icon/Arrow.svg">
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 border-separate">
									<div class="text-drop-card">Kualifikasi Pilihan</div>
									<img src="/image/icon/Arrow.svg">
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 border-separate">
									<div class="text-drop-card">Sub Kualifikasi Pilihan</div>
									<img src="/image/icon/Arrow.svg">
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-10 border-separate">
									<div class="text-drop-card">Umur</div>
									<img src="/image/icon/Arrow.svg">
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-8 border-separate">
									<div class="text-drop-card">Pendidikan</div>
									<img src="/image/icon/Arrow.svg">
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-8 border-separate">
									<div class="text-drop-card">Info</div>
									<img src="/image/icon/Arrow.svg">
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-8 border-separate">
									<div class="text-drop-card">Status</div>
									<img src="/image/icon/Arrow.svg">
								</div>
							</div>
						</div>
						{#if reportList != null}
						{#each reportList as report, i}
						<div class="card-head w-content-2 height-fit">
							<div class="flex">
								<div class="flex flex-gap-small flex-center-vertical w-10 no-border-table">
								<div class="text-drop-card">Ke-{i+1}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.rentang_waktu}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.NUP}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.pemberkasan}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-25 no-border-table">
									<div class="text-drop-card">{report.proses_bank}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.sp3k}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.declined}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.akad}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.sppkr}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.keaktifan_marketing_lead}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.keaktifan_marketing_lepas}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.ready_stok_legal}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.ready_stok_teknis}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.ready_stok_marketing}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-20 no-border-table">
									<div class="text-drop-card">{report.sisa_spk3}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-30 no-border-table">
									<div class="text-drop-card">{report.update_ready_stok_legal}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-30 no-border-table">
									<div class="text-drop-card">{report.update_ready_stok_teknis}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-30 no-border-table">
									<div class="text-drop-card">{report.update_ready_stok_marketing}</div>
								</div>
								<div class="flex flex-gap-small flex-center-vertical w-30 no-border-table">
									<div class="text-drop-card">0</div>
								</div>
							</div>
						</div>
						{/each}
						{/if}
					</div>
					<div class="card w-100 height-fit">
						<div class="flex flex-between-horizontal">
							<div class="flex flex-gap-regular flex-center-vertical">
								<div class="text-display-sort">Menampilkan</div>
								<select class="select-sort">
									<option>10</option>
								</select>
								<div class="text-display-sort">dari <span class="bold-number">28</span> data NUP</div>
							</div>
							<div class="flex flex-gap-regular flex-center-vertical">
								<div class="flex flex-center-vertical flex-center-horizontal border-pagination"><img src="/images/icons/Arrow_Left.svg"></div>
								<div class="flex flex-center-vertical flex-center-horizontal border-pagination"><div class="text-display-sort bold-number">1</div></div>
								<div class="flex flex-center-vertical flex-center-horizontal border-pagination"><img src="/images/icons/Arrow_Right.svg"></div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>