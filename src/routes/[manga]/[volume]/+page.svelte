<script lang="ts">
  import { page } from '$app/stores';
  import Reader from '$lib/components/Reader/Reader.svelte';
  import Timer from '$lib/components/Reader/Timer.svelte';
  import { initializeVolume, settings, startCount, volumeSettings, volumes } from '$lib/settings';
  import { onMount } from 'svelte';
  import ReaderV2 from '$lib/components/ReaderV2/ReaderV2.svelte';

  const volumeId = $page.params.volume;
  let count: undefined | number = undefined;

  onMount(() => {
    if (!$volumes?.[volumeId]) {
      initializeVolume(volumeId);
    }

    count = startCount(volumeId);

    return () => {
      clearInterval(count);
      count = undefined;
    };
  });
</script>

{#if $volumeSettings[volumeId]}
  {#if $settings.showTimer}
    <Timer bind:count {volumeId} />
  {/if}
  {#if $settings.reader === 'classic'}
    <Reader volumeSettings={$volumeSettings[volumeId]} />
  {:else}
    <ReaderV2 />
  {/if}
{/if}
