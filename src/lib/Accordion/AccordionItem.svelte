<script lang="ts">
	import ChevronRight from 'carbon-icons-svelte/lib/ChevronRight.svelte';
	import { getContext } from 'svelte';
	import { uniqueId } from '../uniqueId.js';
	import type { Writable } from 'svelte/store';
	import AccordionSkeleton from './AccordionSkeleton.svelte';

	export let disabled: boolean = false;
	export let open: boolean = false;

	export let title: string = '';

	export let iconDescription = 'Expand/Collapse';

	const accordionContext =
		getContext<Writable<{ disabled: boolean; skeleton: boolean }>>('cds-accordion');

	const itemId = uniqueId('accordion');

	let animation: 'expanding' | 'collapsing' | undefined = undefined;

	function resetAnimation() {
		animation = undefined;
	}

	function toggleOpen() {
		open = !open;

		animation = open ? 'expanding' : 'collapsing';
	}

	function onKeyDown({ key }: KeyboardEvent) {
		if (open && key === 'Escape') {
			open = false;
		}
	}
</script>

<li
	{...$$restProps}
	class="cds--accordion__item {$$restProps.class ?? ''}"
	class:cds--accordion__item--active={open}
	class:cds--accordion__item--expanding={animation === 'expanding'}
	class:cds--accordion__item--collapsing={animation === 'collapsing'}
	on:animationend
	on:animationend={resetAnimation}
>
	{#if $accordionContext.skeleton}
		<span class="cds--accordion__heading">
			<ChevronRight class="cds--accordion__arrow" aria-label={iconDescription} />
			<AccordionSkeleton title style="width: 100%;" />
		</span>
		{#if open}
			<div class="cds--accordion__content">
				<AccordionSkeleton style="width: 90%;" />
				<AccordionSkeleton style="width: 90%;" />
				<AccordionSkeleton style="width: 90%;" />
			</div>
		{/if}
	{:else}
		<button
			type="button"
			aria-controls="accordion-item-{itemId}"
			aria-expanded="false"
			class="cds--accordion__heading"
			title={iconDescription}
			on:click
			on:click={toggleOpen}
			disabled={disabled || $accordionContext.disabled}
			on:focus
			on:mouseover
			on:mouseenter
			on:mouseleave
			on:keydown
			on:keydown={onKeyDown}
		>
			<ChevronRight class="cds--accordion__arrow" aria-label={iconDescription} />
			<div class="cds--accordion__title" dir="auto">
				<slot name="title">{title}</slot>
			</div>
		</button>
		<div id="accordion-item-{itemId}" class="cds--accordion__content">
			<slot />
		</div>
	{/if}
</li>
