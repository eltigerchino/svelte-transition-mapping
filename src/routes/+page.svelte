<script>
  import TransitionFrame from "$lib/TransitionFrame.svelte";
  import { fly } from "svelte/transition";
</script>

<TransitionFrame
  as="a"
  href="/dog"
  transition="{fly}"
  transitionParams="{{ blur: 5 }}"
></TransitionFrame>
