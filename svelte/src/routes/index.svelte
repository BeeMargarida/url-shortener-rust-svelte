<script>
    let url = "";
    let shortenId = null;

    async function makeRequest() {
        let response = await fetch(`/api/shorten?url=${url}`, {
            method: "POST",
        });
        shortenId = await response.text();
    }

    function buildShortUrl() {
        return `${window.location.href}${shortenId}`;
    }

    function onClick() {
        makeRequest();
    }
</script>

<div class="container">
    <h1 class="title">URL Shortener</h1>

    {#if shortenId}
        <div class="input-container">
            <a href={buildShortUrl()} target="_blank">{buildShortUrl()}</a>
        </div>
    {:else}
        <div class="input-container">
            <input type="text" bind:value={url} />
            <button on:click={onClick}>Shorten</button>
        </div>
    {/if}
</div>
