<script>
    import Sidebar from '../../../components/Sidebar.svelte';
    import NavbarAdmin from '../../../components/Navbar-admin.svelte';
    import { onMount } from 'svelte';
    import { fly } from 'svelte/transition';
    import Button from '../../../components/Button.svelte';
    import axios from 'axios';
    import { ThreeDotsVertical } from 'svelte-bootstrap-icons';
    
    let data = [];
    let status = false;
  
    function handleClick() {
      window.location.href = '/Admin_citratama/tambah-berita'; // Arahkan ke URL tujuan
    }
  
    async function fetchData() {
      try {
        const response = await axios.get('https://sinaker.pocari.id/api/admin/berita');
        status = true;
        data = response.data.map((item) => ({ ...item, showMenu: false }));
        console.log(data);
      } catch (error) {
        console.error('Ada kesalahan:', error);
      }
    }

    async function deleteBerita(id) {
      try {
        await axios.delete(`https://sinaker.pocari.id/api/admin/berita/${id}`);
        data = data.filter(item => item.ID_berita !== id);
        console.log(`Berita dengan ID ${id} berhasil dihapus`);
      } catch (error) {
        console.error('Ada kesalahan saat menghapus berita:', error);
      }
    }
  
    function toggleMenu(index) {
      data = data.map((item, i) => ({
        ...item,
        showMenu: i === index ? !item.showMenu : false,
      }));
    }
  
    function handleOutsideClick(event) {
      if (!event.target.closest('.dropdown-menu') && !event.target.closest('.menu-icon')) {
        data = data.map((item) => ({ ...item, showMenu: false }));
      }
    }
  
    onMount(() => {
      document.addEventListener('click', handleOutsideClick);
      fetchData();
      return () => {
        document.removeEventListener('click', handleOutsideClick);
      };
    });
  </script>
  
  <div id="after-login-layout">
    <NavbarAdmin />
    <div class="flex">
      <Sidebar active="Berita" pagePointer="ams" />
      <div class="w-100 content">
        <div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
          <div class="flex flex-between-horizontal w-100">
            <div class="title-content">Daftar Semua Berita</div>
  
            <div class="flex flex-gap-regular">
              <button class="btn-outline flex flex-center-vertical flex-gap-small">
                <span>Download Data Pelamar</span>
                <img src="/images/icons/File_Download.svg" />
              </button>
            </div>
          </div>
          <div>
            <Button classList="btn-tambah" onClick={handleClick}>tambah berita</Button>
          </div>
  
          <div class="flex flex-direction-col flex-gap-regular">
            <div class="card w-100 height-fit">
              <div class="flex flex-gap-regular">
                <div class="flex flex-gap-small flex-center-vertical w-5">
                  <div class="text-drop-card">ID</div>
                  <img src="/images/icons/Arrow.svg" />
                </div>
                <div class="flex flex-gap-small flex-center-vertical w-25">
                  <div class="text-drop-card">Judul</div>
                  <img src="/images/icons/Arrow.svg" />
                </div>
                <div class="flex flex-gap-small flex-center-vertical w-33">
                  <div class="text-drop-card">Konten</div>
                  <img src="/images/icons/Arrow.svg" />
                </div>
                <div class="flex flex-gap-small flex-center-vertical w-25">
                  <div class="text-drop-card">Gambar</div>
                  <img src="/images/icons/Arrow.svg" />
                </div>
                <div class="flex flex-gap-small flex-center-vertical w-20">
                  <div class="text-drop-card">Aksi</div>
                </div>
              </div>
            </div>
            {#if status}
              {#each data as d, index}
                <div class="card w-100 height-fit">
                  <div class="flex flex-direction-col flex-gap-regular">
                    <div class="flex flex-gap-regular">
                      <div class="flex flex-gap-small flex-center-vertical w-5">
                        <div class="text-drop-card">{d.ID_berita}</div>
                      </div>
                      <div class="flex flex-gap-small flex-center-vertical w-25">
                        <div class="text-drop-card">{d.judul}</div>
                      </div>
                      <div class="flex flex-gap-small flex-center-vertical w-33">
                        <div class="text-drop-card">{d.konten}</div>
                      </div>
                      <div class="flex flex-gap-small flex-center-vertical w-20">
                        {#if d.gambar}
                          <img src="{d.gambar}" alt="Gambar Berita" class="news-image" />
                        {:else}
                          <div class="text-drop-card">Tidak ada gambar</div>
                        {/if}
                      </div>
                      <div class="flex flex-center-vertical w-20">
                        <div class="menu-icon" on:click={() => toggleMenu(index)}>
                          <ThreeDotsVertical />
                        </div>
                        {#if d.showMenu}
                          <div class="dropdown-menu">
                            <a href="javascript:void(0)" class="menu-item" on:click={() => deleteBerita(d.ID_berita)}>Delete</a>
                            <a href="/Admin_citratama/update-berita" class="menu-item">Update</a>
                          </div>
                        {/if}
                      </div>
                    </div>
                  </div>
                </div>
              {/each}
            {/if}
  
            <div class="card w-100 height-fit">
              <div class="flex flex-between-horizontal">
                <div class="flex flex-gap-regular flex-center-vertical">
                  <div class="text-display-sort">Menampilkan</div>
                  <select class="select-sort">
                    <option>10</option>
                  </select>
                  <div class="text-display-sort">dari <span class="bold-number">28</span> berita</div>
                </div>
                <div class="flex flex-gap-regular flex-center-vertical">
                  <div class="flex flex-center-vertical flex-center-horizontal border-pagination">
                    <img src="/images/icons/Arrow_Left.svg" />
                  </div>
                  <div class="flex flex-center-vertical flex-center-horizontal border-pagination">
                    <div class="text-display-sort bold-number">1</div>
                  </div>
                  <div class="flex flex-center-vertical flex-center-horizontal border-pagination">
                    <img src="/images/icons/Arrow_Right.svg" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  
  <style>
    .news-image {
      max-width: 100px;
      max-height: 100px;
      object-fit: cover;
      border-radius: 4px;
    }
    .menu-icon {
      cursor: pointer;
    }
  
    .dropdown-menu {
      position: absolute;
      background-color: white;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      margin-top: 10px;
      padding: 10px;
      z-index: 100;
    }
  
    .menu-item {
      display: block;
      padding: 10px;
      text-decoration: none;
      color: black;
      border-bottom: 1px solid #eee;
    }
  
    .menu-item:last-child {
      border-bottom: none;
    }
  </style>
