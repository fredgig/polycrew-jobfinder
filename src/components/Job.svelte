<script>
    import Icon from "./Icon.svelte";

    export let jobTitle;
    export let jobLocation = null;
    export let jobCountry = "Switzerland";
    export let jobCompany = null;
    export let jobPostedDate = "21.10.2021";
    export let jobupId = null;
    export let selected = false;
    export let onclick = null;
</script>

<div class="rounded p-2 space-y-1 border-2 w-full {selected ? "bg-purple-200 border-purple-500" : "bg-gray-100 border-gray-200 hover:bg-gray-200 hover:border-gray-300"} transition cursor-pointer" on:click={onclick}>
    <div class="flex items-center space-x-1">
        <h3 class="text-lg text-slate-600">{jobTitle}</h3>
    </div>
    <div class="flex items-center space-x-3">
        {#if jobCompany}
            <div class="text-slate-500 text-sm">{jobCompany}</div>
        {/if}
    </div>
    <div class="flex justify-between items-center">
        <div class="flex space-x-1">
            <Icon name="pin" class="fill-slate-400" />
            <img src="{jobCountry.toLowerCase()}.png" />
            <p class="text-slate-500 text-xs">{jobLocation}</p>
        </div>
        {#if jobupId}
            <a href="https://www.jobup.ch/fr/emplois/detail/{jobupId}" target="_blank" class="group">
                <Icon name="external-link" class="fill-purple-400 group-hover:fill-purple-500 transition" />
            </a>
        {/if}
    </div>
</div>