<h1>Hello, please enter your name and either create or join a planning room!</h1>
<script>
	let name = '';
    let joinRoom = '';
    let createRoom = '';
</script>
<input bind:value={name} placeholder='Enter Name'/>
<input bind:value={joinRoom} placeholder='Code to Join Room'/>
<input bind:value={createRoom} placeholder='Create Room Code'/>
<button on:click={()=>console.log("Clicked")}>
    <a href="/calendar">Continue</a>
</button>
<p>If you are creating a room, please create a room code and share it with your planees.</p>
