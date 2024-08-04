<script>
    import Navbar from '../../../components/Navbar-admin.svelte';
    import Sidebar from '../../../components/Sidebar.svelte';
    import axios from 'axios';
    import { onMount } from 'svelte';
    import { ArrowLeft } from 'svelte-bootstrap-icons';
  
    let title = '';
    let content = '';
    let imageUrl = '';
    let imageFile = null;
    let beritaId = '';
  
    function handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        imageFile = file;
        const reader = new FileReader();
        reader.onload = (e) => {
          imageUrl = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    }
  
    async function handleSubmit() {
      if (title && content) {
        const formData = new FormData();
        formData.append('judul', title);
        formData.append('konten', content);
        if (imageFile) {
          formData.append('gambar', imageFile);
        }
  
        try {
          const response = await axios.post(`https://sinaker.pocari.id/api/admin/update-berita/${beritaId}`, formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          });
          alert('Berita berhasil diperbarui!');
          console.log(response.data);
          
          // Reset form fields
          title = '';
          content = '';
          imageUrl = '';
          imageFile = null;
        } catch (error) {
          console.error('Error updating news:', error);
          alert('Terjadi kesalahan saat memperbarui berita!');
        }
      } else {
        alert('Mohon isi semua bidang yang diperlukan!');
      }
    }
  
    function goBack() {
      window.location.href = '/Admin_citratama/berita';
    }
  
    onMount(async () => {
      const urlParams = new URLSearchParams(window.location.search);
      beritaId = urlParams.get('id');
      
      if (beritaId) {
        try {
          const response = await axios.get(`https://sinaker.pocari.id/api/admin/berita/${beritaId}`);
          const berita = response.data;
          title = berita.judul;
          content = berita.konten;
          imageUrl = `https://sinaker.pocari.id/storage/${berita.gambar}`;
        } catch (error) {
          console.error('Error fetching berita:', error);
        }
      }
    });
  </script>
  
  <Navbar />
  <div class="main-content">
    <Sidebar statusPointer="berita" pagePointer="ams" />
    <div class="main-container">
      <div class="form-container">
        <div class="back-button" on:click={goBack}>
          <ArrowLeft/>
        </div>
        <h1>{beritaId ? 'Update Berita' : 'Tambah Berita'}</h1>
        <form on:submit|preventDefault={handleSubmit}>
          <div class="form-group">
            <label for="title">Judul</label>
            <input type="text" id="title" bind:value={title} placeholder="Masukkan judul berita" />
          </div>
          <div class="form-group">
            <label for="content">Konten</label>
            <textarea id="content" bind:value={content} placeholder="Masukkan konten berita"></textarea>
          </div>
          <div class="form-group">
            <label for="image">Unggah Gambar</label>
            <input type="file" id="image" accept="image/*" on:change={handleFileUpload} />
          </div>
          {#if imageUrl}
            <div class="form-group">
              <img src={imageUrl} alt="Preview" class="image-preview" />
            </div>
          {/if}
          <button type="submit" class="btn btn-primary">{beritaId ? 'Update Berita' : 'Tambahkan Berita'}</button>
        </form>
      </div>
    </div>
  </div>
  
  <style>
    .main-container {
      display: flex;
      margin: 0;
      padding: 0;
      width: 100vh;
    }
  
    .form-container {
      flex: 1;
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
      border-radius: 8px;
      background-color: #f9f9f9;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      position: relative;
    }
  
    .back-button {
      position: absolute;
      top: 20px;
      left: 20px;
      cursor: pointer;
    }
  
    .back-button img {
      width: 24px;
      height: 24px;
    }
  
    h1 {
      color: #333;
      margin-bottom: 20px;
      text-align: center;
    }
  
    .form-group {
      margin-bottom: 20px;
    }
  
    label {
      display: block;
      margin-bottom: 5px;
      color: #333;
    }
  
    input,
    textarea {
      width: 100%;
      padding: 10px;
      border-radius: 4px;
      border: 1px solid #ccc;
      box-sizing: border-box;
    }
  
    input[type='file'] {
      padding: 0;
    }
  
    input:focus,
    textarea:focus {
      border-color: #485ee9;
      outline: none;
    }
  
    .image-preview {
      max-width: 100%;
      height: auto;
      margin-top: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
  
    .btn {
      display: inline-block;
      padding: 10px 20px;
      font-size: 16px;
      color: white;
      background-color: #485ee9;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      text-align: center;
    }
  
    .btn-primary {
      background-color: #485ee9;
    }
  
    .btn-primary:hover {
      background-color: #3b4fc6;
    }
  
    .main-content {
      display: flex;
      flex-direction: row;
      gap: 200px;
    }
  </style>
  