<script>
	import data from "$lib/data.json";
	import JobPanel from "../components/JobPanel.svelte";
	import Job from "../components/Job.svelte";
	import ShowMoreButton from "../components/ShowMoreButton.svelte";
	import { onMount } from "svelte";

	const displayedJobsIncrement = 100;

	let displayedJobs = displayedJobsIncrement;
	let jobsFilter = "";
	let selectedJob = null;
	$: filtersShown = false;

	let shownCountries = {
		france: true,
		switzerland: true
	}

	$: jobs = data.filter(job => {
		return job.title?.toLowerCase().includes(jobsFilter.toLowerCase()) && shownCountries[job.country.toLowerCase()];
	});

	onMount(() => {
		const element = document.querySelector('[aria-label="La Chaux-de-Fonds"]');

		console.log(element);
	});
</script>

<nav class="sticky top-0 flex space-x-2 items-center bg-white bg-opacity-70">
	<img src="logo.png" width="80" class="p-2" />
	<span class="text-black font-black text-xl">POLYCREW</span>
</nav>


<iframe title="V1917" width="100%" height="600" src="https://app.powerbi.com/view?r=eyJrIjoiNjJjZTUzYWMtYTIwYS00OTdkLWExODYtNjg1MmY2ODE1ZjQzIiwidCI6ImUyMWU5NzgzLWQwYTAtNDhmOC04NTBlLTBiMDgxYjQ2ZDc4OCIsImMiOjh9&pageName=ReportSection" frameborder="0" allowFullScreen="true"></iframe>

<div class="p-2 flex space-x-6 justify-between items-center">
	<iframe title="V2" width="49%" height="500" src="https://app.powerbi.com/view?r=eyJrIjoiNWU2OWM1YmUtYThmOC00YWIzLTkwYTktMDI0MmJhM2Q2ZDZlIiwidCI6ImUyMWU5NzgzLWQwYTAtNDhmOC04NTBlLTBiMDgxYjQ2ZDc4OCIsImMiOjh9&pageName=ReportSectionc16d267d2a858b6ec1f2" frameborder="0" allowFullScreen="true"></iframe>
	<div class="w-1 h-[500px] rounded bg-gray-100"></div>
	<iframe title="V2 heat map - Page 1" width="49%" height="500" src="https://app.powerbi.com/view?r=eyJrIjoiMDM1Nzc0ZTQtNzgxNC00OTk4LTkyMGUtMTc5YjdiY2UzYzVhIiwidCI6ImUyMWU5NzgzLWQwYTAtNDhmOC04NTBlLTBiMDgxYjQ2ZDc4OCIsImMiOjh9" frameborder="0" allowFullScreen="true"></iframe>
</div>

<div class="p-4 bg-gray-50 flex min-h-screen w-screen space-x-6 h-full items-start selection:bg-accent selection:text-white selection:bg-purple-400">
	<aside class="top-20 h-full w-1/4 space-y-2 self-start">
		<h1 class="text-lg text-gray-600">Search for jobs</h1>
		<div class="flex items-center w-full space-x-1">
			<input bind:value={jobsFilter} placeholder="Search" class="grow bg-gray-100 space-x-1 px-2 py-1 rounded border-2 border-gray-200 transition-all ring-2 ring-white focus:ring-purple-300 outline-none" />
			<button on:click={() => filtersShown = !filtersShown} class="border-2 px-2 py-1 w-20 h-full rounded {filtersShown ? "text-white bg-purple-400 hover:bg-purple-500 border-purple-400" : "border-purple-400 text-purple-400 hover:border-purple-500 hover:text-purple-500"} transition">Filtres</button>
		</div>
		{#if filtersShown}
			<div class="space-y-2 bg-gray-100 rounded w-full px-4 py-2">
				<span class="text-gray-700">Countries</span>
				<div class="flex space-x-2">
					{#each Object.entries(shownCountries) as [country, shown]}
						<div class="flex space-x-2 items-center">
							<button class="rounded-full border-2 {shown ? "border-purple-500 opacity-100" : "border-purple-100 opacity-90"} transition" on:click={() => shownCountries[country] = !shownCountries[country]}>
								<img src="{country}-lg.png" />
							</button>
						</div>
					{/each}
				</div>
			</div>
		{/if}
		<span class="text-gray-400 text-sm">{jobs.length} jobs found</span>
		{#each jobs as job, index}
			{#if index < displayedJobs}
				<Job jobTitle={job.title} jobCompany={job.company} jobLocation={job.city} jobupId={parseInt(job.jobup_id)} onclick={() => selectedJob = job} selected={selectedJob == job} />
			{/if}
		{/each}

		{#if displayedJobs < jobs.length}
			<ShowMoreButton onclick={() => displayedJobs += displayedJobsIncrement} />
		{/if}
	</aside>
	{#if selectedJob}
		<JobPanel {selectedJob} />
	{/if}
</div>

