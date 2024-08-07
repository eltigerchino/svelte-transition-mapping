<script>
  import TransitionFrame from "$lib/TransitionFrame.svelte";
  import { fly } from "svelte/transition";
</script>

<TransitionFrame transition="{fly}" transitionParams="{{ blur: 5 }}"
></TransitionFrame>
