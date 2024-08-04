<script type="text/javascript">
    import { fly, scale } from 'svelte/transition';

    let pelamar_drop = 0;
    let perusahaan_drop = 0;
    let settings_drop = 0;

    export let pagePointer;
</script>

<style>
    .sidebar {
        background-color: #2c3e50;
        color: #ecf0f1;
    }
    .sidebar-content {
        padding: 10px 20px;
        transition: background-color 0.3s ease;
    }
    .sidebar-content:hover {
        background-color: #34495e;
    }
    .active {
        background-color: #2980b9;
    }
    .text-sidebar-active {
        color: #ecf0f1;
        font-weight: bold;
    }
    .text-sidebar {
        color: #bdc3c7;
    }
    .no-decor {
        text-decoration: none;
        color: inherit;
    }
    .footer-sidebar {
        padding: 20px;
        text-align: center;
    }
</style>

{#if pagePointer == 'ams'}
    <div class="sidebar w-20">
        <div class="h-100 flex flex-direction-col flex-between-horizontal">
            <div class="flex flex-direction-col flex-gap-regular">
                <div class="flex flex-gap-semi-small sidebar-content">
                    <div class="flex flex-gap-small w-80">
                        <img src="/images/avatar.png" class="polished-img" />
                        <div class="flex flex-direction-col flex-center-horizontal">
                            <div class="welcome-sidebar">Selamat Datang</div>
                            <div class="name-sidebar">Jane Doe</div>
                        </div>
                    </div>
                    <div class="flex flex-end-horizontal w-10">
                        <i class="fa-solid fa-angle-up position-angle" />
                    </div>
                </div>
                <div class="flex flex-direction-col">
                    <a href="/Admin_citratama/dashboard" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Dashboard</span>
                            </div>
                        </div>
                    </a>
                    <a href="/Admin_citratama/pelamar" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Pelamar Kerja</span>
                            </div>
                        </div>
                    </a>
                    <a href="/Admin_citratama/persetujuan" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Persetujuan</span>
                            </div>
                        </div>
                    </a>
                    <a href="/Admin_citratama/berita" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Berita</span>
                            </div>
                        </div>
                    </a>
                    <a href="/Admin_citratama/perusahaan" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Perusahaan</span>
                            </div>
                        </div>
                    </a>
                    <a href="/Admin_citratama/jadwal" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Jadwal</span>
                            </div>
                        </div>
                    </a>
                </div>
            </div>
        </div>
        <div class="footer-sidebar">
            <div class="footer-text">Admin Citratama</div>
        </div>
    </div>
{:else if pagePointer == 'mitra'}
    <div class="sidebar w-20">
        <div class="h-100 flex flex-direction-col flex-between-horizontal">
            <div class="flex flex-direction-col flex-gap-regular">
                <div class="flex flex-gap-semi-small sidebar-content">
                    <div class="flex flex-gap-small w-80">
                        <img src="/images/avatar.png" class="polished-img" />
                        <div class="flex flex-direction-col flex-center-horizontal">
                            <div class="welcome-sidebar">Selamat Datang</div>
                            <div class="name-sidebar">Jane Doe</div>
                        </div>
                    </div>
                </div>
                <div class="flex flex-direction-col">
                    <a href="/Admin_mitra/dashboard" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Dashboard</span>
                            </div>
                        </div>
                    </a>
                    <a href="/Admin_mitra/persetujuan" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Approvement</span>
                            </div>
                        </div>
                    </a>
                    <a href="/Admin_mitra/jadwal" class="no-decor">
                        <div class="flex flex-gap-semi-small sidebar-content" in:fly={{ y: -20, duration: 600 }}>
                            <div class="flex flex-gap-semi-small flex-center-vertical w-90">
                                <div class="icon-sidebar" />
                                <span class="text-sidebar">Jadwal</span>
                            </div>
                        </div>
                    </a>
                </div>
            </div>
        </div>
        <div class="footer-sidebar">
            <div class="footer-text">Mitra</div>
        </div>
    </div>
{/if}
