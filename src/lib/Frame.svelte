<script context="module" lang="ts">
  import type { AriaRole } from "svelte/elements";
  import type { Action } from "svelte/action";
  import type { default as svelteTransition } from "svelte/transition";

  export type TransitionMap = Omit<
    typeof svelteTransition,
    "crossfade" | "draw"
  >;

  export type Transition = TransitionMap[keyof TransitionMap];
</script>

<script
  lang="ts"
  generics="TElement extends keyof HTMLElementTagNameMap, TTransition extends Transition"
>
  interface Props {
    as?: TElement;
    action?: Action<HTMLElementTagNameMap[TElement], any, any> | undefined;
    actionOptions?: Record<string, unknown> | undefined;
    class?: HTMLElementTagNameMap[TElement]["className"];
    node?: HTMLElementTagNameMap[TElement];
    href?:
      | (HTMLElementTagNameMap[TElement] extends
          | HTMLAnchorElement
          | HTMLLinkElement
          | HTMLAreaElement
          | HTMLBaseElement
          ? string
          : never)
      | null
      | undefined;
    open?: boolean;
    role?: AriaRole;
    testId?: string;
    transition?: TTransition;
    transitionParams?: Parameters<TTransition>[1];
    [key: `data-${string}`]: string | undefined;
    [key: `aria-${string}`]: string | undefined;
  }

  type $$Props = Props & typeof $$restProps;

  export let as: TElement | undefined = undefined;
  export let action: Action<
    HTMLElementTagNameMap[TElement],
    any,
    any
  > = () => {};
  export let actionOptions: Parameters<typeof action>[1] = undefined;
  export let transition: TTransition = (() => ({})) as any;
  export let transitionParams: Parameters<TTransition>[1] = undefined;
  export let node: HTMLElementTagNameMap[TElement] | undefined = undefined;
  export let testId: string | undefined = undefined;
  export let href:
    | (HTMLElementTagNameMap[TElement] extends
        | HTMLAnchorElement
        | HTMLLinkElement
        | HTMLAreaElement
        | HTMLBaseElement
        ? string
        : never)
    | null
    | undefined = undefined;
  export let role: AriaRole | undefined = undefined;
</script>

<svelte:element
  this="{as}"
  use:action="{actionOptions}"
  transition:transition="{transitionParams}"
  bind:this="{node}"
  data-testid="{testId}"
  {href}
  {role}
  on:click
  on:mouseenter
  on:mouseleave
  on:focusin
  on:focusout
  on:keydown
  on:keyup
  on:touchstart
  on:touchend
  on:touchcancel
  {...$$restProps}
>
  <slot />
</svelte:element>
