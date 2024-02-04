<h1>Hello, please enter your name and either create or join a planning room!</h1>
<script>
    //import Button from "../components/Button.svelte"
	let name = 'Enter Name';
    let joinRoom = 'Code to Join Room';
    let createRoom = 'Create Room Code';
</script>
<input bind:value={name} />
<input bind:value={joinRoom} />
<input bind:value={createRoom} />
<button on:click={()=>console.log("Clicked")}>
    <a href="/calendar">Continue</a>
</button>
<p>If you are creating a room, please create a passcode and share it with your planees.</p>
