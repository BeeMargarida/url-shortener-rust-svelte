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

    function onGoBackClick() {
        url = "";
        shortenId = null;
    }
</script>

<div class="page">
    <div class="container">
        <div class="container-title">
            <h1 class="title">URL Shortener</h1>
        </div>

        {#if shortenId}
            <div class="link-container">
                <a class="link" href={buildShortUrl()} target="_blank">{buildShortUrl()}</a>
                <button class="button" on:click={onGoBackClick}>Go back</button>
            </div>
        {:else}
            <div class="input-container">
                <input
                    class="input"
                    type="text"
                    placeholder="Place were the URL you wish to shorten"
                    bind:value={url}
                />
                <button class="button" on:click={onClick}>Shorten</button>
            </div>
        {/if}
    </div>
</div>

<style>
    .page {
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin-top: 40%;
    }

    .container {
        align-items: center;
        align-self: center;
        border-radius: 10px 10px 10px 10px;
        box-shadow: 0px 0px 10px rgb(143, 143, 143);
        background-color: #ffffff;
        width: 60%;
        max-width: 600px;
    }

    .container-title {
        background-color: #000000;
        width: 100%;
        height: 100%;
        border-radius: 10px 10px 0px 0px;
        padding-top: 10px;
        padding-bottom: 10px;
    }

    .title {
        color: #ffffff;
        text-align: center;
        font-family: "Roboto", sans-serif;
    }

    .input-container {
        display: flex;
        margin: 30px 20px 30px 20px;
    }

    .input {
        height: 34px;
        line-height: 34px;
        color: #1d1d1d;
        font-size: 13px;
        padding-right: 14px;
        padding-left: 14px;
        border-radius: 5px 5px 5px 5px;
        outline: none;
        border: 1px solid #e4e8f0;
        transition: width 0.2s ease, border-color 0.2s ease,
            background-color 0.2s ease, box-shadow 0.2s ease;
        width: 100%;
        display: inline-block;
        align-self: center;
        font-family: "Roboto", sans-serif;
        font-weight: 400;
    }

    .input:focus {
        border-color: #5ba4f6;
    }

    .link-container {
        display: flex;
        margin: 30px 20px 30px 20px;
        justify-content: space-between;
        align-items: center;
    }

    .link {
        color: #4b8dd7;
        font-family: "Roboto", sans-serif;
        cursor: pointer;
        text-decoration: none;
        border-bottom: 1px solid transparent;
        transition: border-color 0.1s ease-in, color 0.1s ease-in;
    }

    .link:hover {
        border-bottom: 1px solid #4b8dd7;
    }

    .button {
        margin-left: 10px;
        padding: 0px 20px 0px 20px;
        font-weight: 600;
        height: 38px;
        outline: none;
        transition: background-color 0.15s ease-in-out,
            border-color 0.15s ease-in-out, color 0.15s ease-in-out,
            opacity 0.15s ease-in-out;
        user-select: none;
        border-radius: 5px 5px 5px 5px;
        border: 1px solid #000000;
        background-color: #000000;
        color: #ffffff;
        line-height: 36px;
        vertical-align: middle;
        display: inline-block;
        font-family: "Roboto", sans-serif;
    }

    .button:hover {
        border: 1px solid #5d5d5d;
        background-color: #5d5d5d;
    }
</style>
