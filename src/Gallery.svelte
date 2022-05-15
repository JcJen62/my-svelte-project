<script>
	import { fade, fly } from 'svelte/transition';
    import Gallery from 'svelte-image-gallery'
	let visible = false;

    const handleClick = () => {
        visible = true
    }
</script>

<label>
	<button on:click={handleClick}>
	    See Photos
    </button>
</label>

{#if visible}
    <Gallery gap="10" maxColumnWidth='200'>
        <img in:fly="{{ y: 200, duration: 2000 }}" out:fade src="./_M7A5145.jpg" alt="Test"/>

    </Gallery>
    <div class="container">
        
    </div>
{/if}

<style>
    img {
        width: 100%;
        height: auto;
    }

    button {
        padding: 12px 10px;
        border: none;
        background-color: rgb(157, 174, 189);
        color: white;
    }
</style>