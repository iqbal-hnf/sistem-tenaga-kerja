<script>
	import axios from 'axios';
	import { onMount } from 'svelte';

	let message = '';
	let messages = [];
	let userName = '';
	let isWaitingForResponse = false;
	let isChatOpen = false;

	const toggleChat = () => {
		isChatOpen = !isChatOpen;
	};

	const sendMessage = async () => {
		if (message.trim() === '' || isWaitingForResponse) return;

		// Tambahkan pesan pengguna ke daftar pesan
		messages = [...messages, { text: message, sender: 'user' }];

		// Kirim pesan ke backend
		try {
			isWaitingForResponse = true;
			const response = await axios.post('http://127.0.0.1:8000/api/botman', {
				driver: 'web',
				userId: 'svelte-user',
				message: message
			});

			// Tambahkan balasan bot ke daftar pesan
			response.data.messages.forEach((msg) => {
				messages = [...messages, { text: msg.text, sender: 'bot' }];
			});

			// Reset pesan input
			message = '';
		} catch (error) {
			console.error('Error sending message', error);
			if (error.response) {
				// Server responded with a status other than 200 range
				console.error('Response data:', error.response.data);
				console.error('Response status:', error.response.status);
				console.error('Response headers:', error.response.headers);
			} else if (error.request) {
				// Request was made but no response received
				console.error('Request data:', error.request);
			} else {
				// Something happened in setting up the request
				console.error('Error message:', error.message);
			}
		} finally {
			isWaitingForResponse = false;
		}
	};
</script>

<div>
	<div class="chat-icon" on:click={toggleChat}>💬</div>
	{#if isChatOpen}
		<div class="chat-container">
			<div class="text-chat">
				<p>Chat Bot</p>
				<hr />
			</div>
			<div class="messages">
				{#each messages as message}
					<div class="message {message.sender}">
						{message.text}
					</div>
				{/each}
			</div>

			<div class="input-container">
				<input
					type="text"
					bind:value={message}
					on:keypress={(e) => e.key === 'Enter' && sendMessage()}
					disabled={isWaitingForResponse}
				/>
				<button on:click={sendMessage} disabled={isWaitingForResponse}>Send</button>
			</div>
		</div>
	{/if}
</div>

<style>
	.chat-icon {
		position: fixed;
		bottom: 20px;
		right: 20px;
		background-color: #007bff;
		color: white;
		border-radius: 50%;
		width: 50px;
		height: 50px;
		display: flex;
		justify-content: center;
		align-items: center;
		cursor: pointer;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		font-size: 24px;
		z-index: 1000;
	}
	.text-chat {
		border-radius: 10px;
		max-width: 400px;
		z-index: 1000;
	}

	.text-chat p {
		font-size: 20px;
		font-weight: bold;
		margin: 0 0 10px;
		color: var(--black);
		z-index: 1000;
	}

	.text-chat hr {
		color: var(--black);
		margin: 0;
		margin-bottom: 10px;
	}

	.chat-container {
		z-index: 1000;
		display: flex;
		flex-direction: column;
		position: fixed;
		bottom: 80px;
		right: 20px;
		max-width: 400px;
		max-height: 350px;
		height: 350px;
		width: 100%;
		background-color: white;
		border: 1px solid #ccc;
		padding: 10px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		overflow: hidden;
		border-radius: 20px;
	}

	.messages {
		flex: 1;
		overflow-y: auto;
		margin-bottom: 10px;
	}

	.message {
		padding: 5px;
		margin-bottom: 5px;
		border-radius: 5px;
	}

	.message.user {
		align-self: flex-end;
		background-color: #e1ffc7;
		padding: 10px;
		padding-left: 20px;
		padding-right: 20px;
		border-radius: 10px;
		max-width: fit-content;
		float: right;
		display: inline-block;
		text-align: right;
		clear: both; /* Ensure it doesn't overlap with previous messages */
	}

	.message.bot {
		align-self: flex-start;
		background-color: #f1f1f1;
		padding: 10px;
		border-radius: 10px;
		max-width: 80%;
		float: left;
		display: inline-block;
		text-align: left;
		clear: both; /* Ensure it doesn't overlap with previous messages */
	}

	.input-container {
		display: flex;
	}

	.input-container input {
		flex: 1;
		padding: 10px;
		border: 1px solid #ccc;
		border-radius: 5px 0 0 5px;
	}

	.input-container button {
		padding: 10px;
		border: none;
		background-color: #007bff;
		color: white;
		cursor: pointer;
		border-radius: 0 5px 5px 0;
	}
</style>
