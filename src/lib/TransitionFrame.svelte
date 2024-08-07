<script context="module" lang="ts">
  interface Dismissable {
    dismissable?: boolean;
    open?: boolean;
  }
</script>

<script
  lang="ts"
  generics="TElement extends keyof HTMLElementTagNameMap, TTransition extends Transition"
>
  import type { ComponentProps } from "svelte";
  import Frame, { type Transition } from "./Frame.svelte";

  interface $$Props
    extends ComponentProps<Frame<TElement, TTransition>>,
      Dismissable {}

  let className: $$Props["class"] = undefined;
  export { className as class };
  export let open: $$Props["open"] = true;
  export let transition: $$Props["transition"] = undefined;
  export let transitionParams: ComponentProps<
    Frame<TElement, TTransition>["transitionParams"]
  > = {
    duration: 150,
  };

  function close(ev: MouseEvent | undefined) {
    if (ev?.stopPropagation) ev.stopPropagation();
    open = false;
  }
</script>

<Frame
  bind:open
  class="{className}"
  {transition}
  {transitionParams}
  on:show
  {...$$restProps}
>
  <slot {close} />
</Frame>
