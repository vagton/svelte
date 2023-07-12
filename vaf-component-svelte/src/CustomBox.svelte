<!-- CustomBox.svelte -->
<script>
    import { fade, fly } from "svelte/transition";

    export let transition;
    export let color;
    export let text;

    let newColor = color;
    let newText = text;

    function updateColor(event) {
        newColor = event.target.value;
    }

    function updateText(event) {
        newText = event.target.value;
    }
</script>

{#if transition === "fade"}
    <div transition:fade style="background-color: {newColor}">
        <p>{newText}</p>
    </div>
{:else if transition === "fly"}
    <div transition:fly={{ x: -100 }} style="background-color: {newColor}">
        <p>{newText}</p>
    </div>
{:else}
    <div style="background-color: {newColor}">
        <p>{newText}</p>
    </div>
{/if}

<div class="color-picker">
    <label>
        Color:
        <input type="color" bind:value={newColor} on:input={updateColor} />
    </label>
</div>

<div class="text-editor">
    <label>
        Text:
        <textarea bind:value={newText} on:input={updateText} />
    </label>
</div>

<style>
    div {
        padding: 20px;
        color: white;
        font-size: 16px;
        text-align: center;
    }

    .color-picker,
    .text-editor {
        margin-top: 20px;
    }

    textarea {
        width: 100%;
        height: 100px;
        resize: none;
    }
</style>
