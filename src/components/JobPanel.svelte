<script>
    import Icon from "./Icon.svelte";

    export let selectedJob = null;
</script>

<div class="sticky top-8 bg-gray-100 rounded grow px-4 py-2 space-y-3 w-3/4 h-full">
    <div class="space-y-4">
        <h1 class="text-gray-600 text-lg">{selectedJob.title}</h1>
        {#if selectedJob.prob}
            <div class="space-y-0.5">
                <h3 class="text-gray-400 text-xs">PROBABILITE SVM</h3>
                <div class="w-96 h-2 rounded-full bg-gray-300">
                    <div id="bar" class="h-full rounded-full bg-green-500" style={`width: ${Math.ceil(selectedJob.prob * 100)}%;`} />
                </div>
            </div>
        {/if}
        {#if selectedJob.company}
            <div class="space-y-0.5">
                <h3 class="text-gray-400 text-xs">COMPANY</h3>
                <div class="text-slate-500 text-sm">{selectedJob.company}</div>
            </div>
        {/if}
        <div class="space-y-0.5">
            <h3 class="text-gray-400 text-xs">LOCATION</h3>
            <div class="flex justify-between items-center">
                <div class="flex space-x-1">
                    <Icon name="pin" class="fill-slate-400" />
                    <img src="{selectedJob.country.toLowerCase()}.png" />
                    <p class="text-slate-500 text-xs">{selectedJob.city}</p>
                </div>
            </div>
        </div>
    </div>

    {#if selectedJob.content}
        <div class="space-y-0.5">
            <h3 class="text-gray-400 text-xs">DESCRIPTION</h3>
            <div class="text-gray-500 px-4 py-2 border-2 border-gray-200 rounded">{selectedJob.content}</div>
        </div>
    {/if}

    {#if selectedJob.jobup_id}
        <a href="https://www.jobup.ch/fr/emplois/detail/{selectedJob.jobup_id}" target="_blank" class="group flex space-x-1 items-center">
            <span class="text-purple-400 group-hover:text-purple-500 transition">View on jobup.ch</span>
            <Icon name="external-link" class="fill-purple-400 group-hover:fill-purple-500 transition" />
        </a>
    {/if}
</div>