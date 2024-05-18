<script lang="ts">
  import type { Page } from '$lib/types';
  import { afterUpdate, onMount, onDestroy } from 'svelte';
  import TextBoxes from './TextBoxes.svelte';
  import { zoomDefault } from '$lib/panzoom';

  export let page: Page;
  export let src: File;

  $: url = src ? `url(${URL.createObjectURL(src)})` : '';

  let legacy: HTMLElement | null;

  onMount(() => {
    legacy = document.getElementById('popupAbout');
    zoomDefault();

    return () => {
      setTimeout(() => {
        zoomDefault();
      }, 10);
    };
  });

  $: {
    if (legacy) {
      legacy.style.backgroundImage = url;
    }
  }

  afterUpdate(() => {
    zoomDefault();
  });
</script>

<div
  draggable="false"
  style:width={`${window.innerWidth}px`}
  style:height={`${(window.innerWidth * page.img_height) / page.img_width}px`}
  style:background-image={url}
  class="relative"
>
  <TextBoxes {page} {src} />
</div>

<style>
  div {
    background-size: contain;
    background-repeat: no-repeat;
  }
</style>
