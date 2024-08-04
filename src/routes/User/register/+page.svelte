<script>
    import axios from 'axios';
    import { navigate } from 'svelte-routing';
    import Swal from 'sweetalert2';
	import Button from '../../../components/Button.svelte';

    let name = '';
    let email = '';
    let password = '';
    let confirmPassword = '';
    let errorMessage = '';

    const handleSubmit = async (event) => {
        event.preventDefault();

        if (password !== confirmPassword) {
            errorMessage = 'Passwords do not match';
            return;
        }

        try {
            const response = await axios.post('https://sinaker.pocari.id/api/register', {
                name: name,
                email: email,
                password: password,
                password_confirmation: confirmPassword
            });

            if (response.status === 200) {
                Swal.fire({
                title: 'Success!',
                text: 'Account created successfully. You will be redirected to the login page.',
                icon: 'success',
                confirmButtonText: 'OK'
                }).then((result) =>{
                    if(result.isConfirmed){
                        window.location.href = '/User/Login'
                    }
                

                });
               
            }
            
        } catch (error) {
            console.error('Error registering:', error);
            errorMessage = 'Registration failed. Please try again.';
        }
    };
</script>

<div class="container">
    <div class="register-card">
        <div class="left-panel"></div>
        <div class="right-panel">
            <h1>SIGN UP</h1>

            <p>Enter your details to create an account</p>
            {#if errorMessage} <!-- Tampilkan pesan kesalahan jika ada -->
                <p class="error">{errorMessage}</p>
            {/if}
            <form id="registerform" on:submit={handleSubmit}>
                <input type="text" id="name" bind:value={name} placeholder="Enter Name" required />
                <input type="email" id="email" bind:value={email} placeholder="Enter Email" required />
                <input type="password" id="password" bind:value={password} placeholder="Enter Password" required />
                <input type="password" id="confirmPassword" bind:value={confirmPassword} placeholder="Confirm Password" required />

                <Button type="submit" classList="btn-submit">SIGN UP</Button>
            </form>
            <div class="divider">
                <span>OR</span>
            </div>
            <div class="google-signin">
                <img src="/google-logo.png" alt="Google Logo" style="width: 15px; height:15px; margin-right:8px;" />
                <span>Sign Up With Google</span>
            </div>

            <div class="login-link">
                <p>Already have an account? <a href="/User/Login">SIGN IN</a></p>
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

    .register-card {
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

    .left-panel img {
        max-width: 100%;
        height: auto;
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

    input[type='text'],
    input[type='email'],
    input[type='password'] {
        width: 100%;
        padding: 10px;
        margin: 10px 0;
        border: 1px solid #ccc;
        border-radius: 5px;
    }

    button {
        background: linear-gradient(90deg, #e2186d 34.77%, #485ee9 63.43%);
        border: 1px solid #9398b0;
        color: white;
        padding: 10px;
        border-radius: 8px;
        cursor: pointer;
        margin-top: 10px;
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

    .login-link {
        margin-top: 20px;
        text-align: center;
        font-size: 1px;
    }

    .login-link p :hover {
        color: #00195e;
    }

    .login-link p {
        font-size: 14px;
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
