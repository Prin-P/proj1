<script>
    let isVisible = false;
    export function toggleToolbar(){
        isVisible = !isVisible;
    }
</script>

{#if isVisible}
        <div class="toolbar-header">
            <button on:click={bufferAction}>Add Buffers</button>
            <button on:click={deleteAction}>Delete</button>
        </div>
{/if}


<style>
    .toolbar-header {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        background-color: #f0f0f0;
        display: flex;
        justify-content: space-around;
        padding: 10px;
        box-shadow: 0 2px 5px rgba(0,0,0,0.2);
    }
</style>
<script>


    function bufferAction() {
        console.log('Buffer action triggered');
        // add logic here
    }

    function deleteAction() {
        console.log('Delete action triggered');
        // add logic here
    }
</script>

//add to main page.svelte 
<!--
<script>
    import EventToolbar, { toggleToolbar } from './EventToolbar.svelte';

    function onEventClick() {
        toggleToolbar();
    }
</script>
-->
