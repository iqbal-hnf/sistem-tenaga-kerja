<script>
    import axios from 'axios';
    import { navigate } from 'svelte-routing';
	import Button from '../../../components/Button.svelte';

    let email = '';
    let password = '';
    let status = false;
    let data = {};
    let errorMessage = ''; // Variabel untuk menyimpan pesan kesalahan

    const handleSubmit = async (event) => {
        event.preventDefault();

        try {
            let userIsAdmin = false;
            let role = '';


            const response = await axios.post('https://sinaker.pocari.id/api/login', {
                email: email,
                password: password
            });

            data = response.data;
            status = true;

            if(data.user == null) userIsAdmin = true;

            console.log(userIsAdmin);
            console.log(data);

            // Menyimpan token ke local storage atau session storage
            localStorage.setItem('token', data.access_token);

            // Arahkan pengguna ke halaman lain jika login berhasil
            if(userIsAdmin) {            
               window.location.href='/Admin_mitra/dashboard';
            } else {            
                window.location.href='/User/Dashboard';
            }
     
        } catch (error) {
            console.error('Error logging in:', error);
            status = false;
            data = {};
            errorMessage = 'Maaf, email dan password yang Anda inputkan salah'; // Tetapkan pesan kesalahan
        }
    };
</script>

<div class="container">
    <div class="login-card">
        <div class="left-panel"></div>
        <div class="right-panel">
            <h1>SIGN IN</h1>

            <p>Enter your email and password to login</p>
            {#if errorMessage} <!-- Tampilkan pesan kesalahan jika ada -->
                <p class="error">{errorMessage}</p>
            {/if}
            <form id="loginform" on:submit={handleSubmit}>
                <input type="email" id="email" bind:value={email} placeholder="Enter Email" />
                <input type="password" id="password" bind:value={password} placeholder="Enter Password" />

                <div class="remember-me">
                    <input type="checkbox" id="rememberMe" />
                    <label for="rememberMe">Remember Me</label>
                </div>
                <Button type="submit" classList="btn-submit">Login</Button>
            </form>
            <div class="divider">
                <span>OR</span>
            </div>
            <div class="google-signin">
                <img src="/google-logo.png" alt="Google Logo" style="width: 15px; height:15px; margin-right:8px;" />
                <span>Sign In With Google</span>
            </div>

            <div class="signup-link">
                <p>Don't have account? <a href="/User/register">SIGN UP</a></p>
            </div>
        </div>
    </div>
</div>

<style>
    .container {
        display: flex;
        height: 100vh;
        align-items: center;
        justify-content: center;
        background-image: url('/bg-gradient.png');
        background-repeat: no-repeat;
        background-size: 100%;
    }

    .login-card {
        display: flex;
        flex-direction: row;
        background-color: rgba(255, 255, 255, 0);
        border-radius: 10px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        overflow: hidden;
        width: 1360px;
        height: 656px;
    }

    .left-panel {
        padding: 30px;
        color: white;
        display: flex;
        align-items: center;
        justify-content: center;
        flex: 1;
        flex-direction: column;
        background-image: url('/SideLogin.png');
        background-size: cover;
        background-size: 90%;
        background-repeat: no-repeat;
    }


    .right-panel {
        padding: 30px;
        flex: 1;
        display: flex;
        flex-direction: column;
        justify-content: center;
        background-color: rgba(255, 255, 255, 0);
    }

    h1 {
        font-weight: 500;
        font-size: 48px;
        font-family: 'poppins';
        color: #00195e;
    }

    p {
        font-weight: 500;
        font-size: 16px;
        font-family: 'poppins';
        color: #9398b0;
    }

    .error {
        color: red;
        font-weight: bold;
        font-size: 14px;
        margin-bottom: 10px;
    }

    input[type='email'],
    input[type='password'] {
        width: 100%;
        padding: 10px;
        margin: 10px 0;
        border: 1px solid #ccc;
        border-radius: 5px;
    }

    button:hover {
        color: #00195e;
    }

    .google-signin {
        margin-top: 20px;
        display: flex;
        align-items: center;
        justify-content: center;
        background: white;
        color: #9398b0;
        border: 1px solid #9398b0;
        padding: 10px;
        border-radius: 5px;
        cursor: pointer;
        width: fit-content;
        margin-left: 228px;
    }

    .google-signin:hover {
        color: #485ee9;
    }

    span {
        font-size: 12px;
    }

    .signup-link {
        margin-top: 20px;
        text-align: center;
        font-size: 1px;
    }

    .signup-link p :hover {
        color: #00195e;
    }

    .signup-link p {
        font-size: 14px;
    }

    .remember-me {
        display: flex;
        flex-direction: row;
        align-items: center;
        gap: 2px;
        margin-top: 10px;
    }

    .remember-me label {
        font-size: 12px;
        color: #9398b0;
    }

    .divider {
        display: flex;
        align-items: center;
        text-align: center;
        margin: 20px 0; /* Atur margin sesuai kebutuhan */
    }

    .divider::before,
    .divider::after {
        content: '';
        flex: 1;
        border-bottom: 1px solid #cccccc; /* Ganti warna garis sesuai kebutuhan */
    }

    .divider::before {
        margin-right: 0px; /* Atur jarak antara garis dan teks */
    }

    .divider::after {
        margin-left: 0px; /* Atur jarak antara garis dan teks */
    }

    .divider span {
        white-space: nowrap;
        color: #cccccc; /* Ganti warna teks sesuai kebutuhan */
        border: 1px solid #cccccc; /* Tambahkan border untuk rectangle */
        border-radius: 4px; /* Opsional: untuk sudut melengkung */
        padding: 0px 5px; /* Atur padding dalam rectangle */
        background-color: white; /* Tambahkan background putih */
        font-size: 12px;
        font-family: 'poppins';
    }
    
</style>
