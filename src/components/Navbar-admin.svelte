<script>
    import '@fortawesome/fontawesome-free/css/all.min.css';

    let dropdownActive = false;

    function signOut() {
        alert('Signing out...');
        window.location.href = '/User/Login';
    }

    function toggleDropdown() {
        dropdownActive = !dropdownActive;
    }
</script>

<style>
    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 10px;
        background-color: white;
    }

    .flex {
        display: flex;
    }

    .w-20 {
        width: 20%;
    }

    .w-80 {
        width: 80%;
    }

    .flex-start-horizontal {
        justify-content: flex-start;
    }

    .flex-between-horizontal {
        justify-content: space-between;
    }

    .flex-center-vertical {
        align-items: center;
    }

    .flex-gap-semi-small {
        gap: 10px;
    }

    .rounded-img {
        width: 30px;
        height: 30px;
        border-radius: 50%;
        cursor: pointer;
    }

    .fa-regular.fa-bell {
        font-size: 20px;
        cursor: pointer;
    }

    .fa-solid.fa-bars {
        font-size: 20px;
        cursor: pointer;
    }

    .dropdown-menu {
        display: none;
        position: absolute;
        top: 60px;
        right: 10px;
        background-color: white;
        box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        border-radius: 5px;
        z-index: 1000;
    }

    .dropdown-menu.active {
        display: block;
    }

    .dropdown-item {
        padding: 10px 20px;
        cursor: pointer;
    }

    .dropdown-item:hover {
        background-color: #f0f0f0;
    }
</style>

<div class="navbar flex">
    <div class="flex w-20 flex-start-horizontal flex-center-vertical">
        <i class="fa-solid fa-bars"></i>
    </div>
    <div class="flex w-80 flex-between-horizontal flex-center-vertical">
        <div>
            <svg width="174" height="48" viewBox="0 0 174 48" fill="none" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <g filter="url(#filter0_b_32_1602)">
                    <path d="M68.92 35.224C67.3627 35.224 65.9547 34.9573 64.696 34.424C63.4587 33.8907 62.4773 33.1227 61.752 32.12C61.0267 31.1173 60.6533 29.9333 60.632 28.568H65.432C65.496 29.4853 65.816 30.2107 66.392 30.744C66.9893 31.2773 67.8 31.544 68.824 31.544C69.8693 31.544 70.6907 31.2987 71.288 30.808C71.8853 30.296 72.184 29.6347 72.184 28.824C72.184 28.1627 71.9813 27.6187 71.576 27.192C71.1707 26.7653 70.6587 26.4347 70.04 26.2C69.4427 25.944 68.6107 25.6667 67.544 25.368C66.0933 24.9413 64.9093 24.5253 63.992 24.12C63.096 23.6933 62.3173 23.064 61.656 22.232C61.016 21.3787 60.696 20.248 60.696 18.84C60.696 17.5173 61.0267 16.3653 61.688 15.384C62.3493 14.4027 63.2773 13.656 64.472 13.144C65.6667 12.6107 67.032 12.344 68.568 12.344C70.872 12.344 72.7387 12.9093 74.168 14.04C75.6187 15.1493 76.4187 16.7067 76.568 18.712H71.64C71.5973 17.944 71.2667 17.3147 70.648 16.824C70.0507 16.312 69.2507 16.056 68.248 16.056C67.3733 16.056 66.6693 16.28 66.136 16.728C65.624 17.176 65.368 17.8267 65.368 18.68C65.368 19.2773 65.56 19.7787 65.944 20.184C66.3493 20.568 66.84 20.888 67.416 21.144C68.0133 21.3787 68.8453 21.656 69.912 21.976C71.3627 22.4027 72.5467 22.8293 73.464 23.256C74.3813 23.6827 75.1707 24.3227 75.832 25.176C76.4933 26.0293 76.824 27.1493 76.824 28.536C76.824 29.7307 76.5147 30.84 75.896 31.864C75.2773 32.888 74.3707 33.7093 73.176 34.328C71.9813 34.9253 70.5627 35.224 68.92 35.224ZM85.188 12.664V35H80.708V12.664H85.188ZM108.718 35H104.238L94.0943 19.672V35H89.6143V12.632H94.0943L104.238 27.992V12.632H108.718V35ZM128.346 12.664V16.28H122.394V35H117.914V16.28H111.962V12.664H128.346ZM145.31 30.744H136.414L134.942 35H130.238L138.27 12.632H143.486L151.518 35H146.782L145.31 30.744ZM144.094 27.16L140.862 17.816L137.63 27.16H144.094ZM167.129 35L159.001 25.048V35H154.521V12.664H159.001V22.68L167.129 12.664H172.537L163.321 23.736L172.793 35H167.129Z" fill="black"/>
                </g>
                <rect y="3" width="43" height="42" fill="url(#pattern0_32_1602)"/>
            </svg>
        </div>

        <div class="flex flex-gap-semi-small flex-center-vertical">
            
            <div class="profile-dropdown">
                <img src="/profile.jpg" alt="Profile" class="rounded-img" on:click={toggleDropdown} />
                <div id="dropdown-menu" class="dropdown-menu {dropdownActive ? 'active' : ''}">
                    <div class="dropdown-item" on:click={signOut}>Sign Out</div>
                </div>
            </div>
        </div>
    </div>
</div>
