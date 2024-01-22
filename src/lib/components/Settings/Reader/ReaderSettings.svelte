<script lang="ts">
  import { AccordionItem, Button, Label, Range } from 'flowbite-svelte';
  import ReaderSelects from './ReaderSelects.svelte';
  import ReaderToggles from './ReaderToggles.svelte';
  import { settings, updateSetting } from '$lib/settings';

  let value = $settings.swipeThreshold;
  function onChange() {
    updateSetting('swipeThreshold', value);
  }
</script>

<AccordionItem>
  <span slot="header">Reader</span>
  <div class="flex flex-col gap-5">
    <ReaderSelects />
    <hr class="border-gray-100 opacity-10" />
    <ReaderToggles />
    <div>
      <Label>Swipe threshold</Label>
      <Range on:change={onChange} min={20} max={90} disabled={!$settings.mobile} bind:value 
      style={`background: linear-gradient(to right, #EF562F ${(value - 20) / (90 - 20) * 100}%, #374151 ${(value - 20) / (90 - 20) * 100}%);`} />
    </div>
  </div>
</AccordionItem>
