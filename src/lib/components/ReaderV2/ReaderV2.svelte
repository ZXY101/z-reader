<script lang="ts">
  import { volume } from '$lib/catalog';
  import MangaPage from '../Reader/MangaPage.svelte';

  $: files = $volume ? Object.values($volume?.files).slice(0, 10) : [];
  $: pages = $volume?.mokuroData?.pages || [];

  $: {
    const { innerWidth, innerHeight } = window;
    console.log(innerWidth, innerHeight);
  }
</script>

<section>
  {#each files as file, i}
    <MangaPage src={file} page={pages[i]} />
  {/each}
</section>

<style>
  section {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
