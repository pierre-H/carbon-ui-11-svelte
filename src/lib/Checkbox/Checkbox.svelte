<script lang="ts" context="module">
	import '@carbon/styles/scss/components/checkbox/_index.scss';
</script>

<script lang="ts">
	import FormRequirement from '../Form/FormRequirement.svelte';
	import { uniqueId } from '../uniqueId.js';
	import InformationFilled from 'carbon-icons-svelte/lib/InformationFilled.svelte';
	import WarningAltFilled from 'carbon-icons-svelte/lib/WarningAltFilled.svelte';

	export let label: string | undefined = undefined;

	export let id: string = uniqueId('checkbox-');
	export let name: string | undefined = undefined;
	export let value: string | undefined = undefined;
	export let checked: boolean = false;

	export let invalid: boolean = false;
	export let invalidText: string | undefined = undefined;

	export let warn: boolean = false;
	export let warnText: string | undefined = undefined;

	export let readOnly: boolean = false;
	export let title: string = '';

	export let indeterminate: boolean = false;

	let inputElm: HTMLInputElement;

	$: if (inputElm) {
		inputElm.indeterminate = indeterminate;
	}

	export let disabled: boolean = false;
</script>

<div
	{...$$restProps}
	class="cds--form-item cds--checkbox-wrapper {$$restProps.class ?? ''}"
	class:cds--checkbox-wrapper--readonly={readOnly}
	class:cds--checkbox-wrapper--invalid={invalid}
	class:cds--checkbox-wrapper--warning={warn && !invalid}
>
	<input
		type="checkbox"
		class="cds--checkbox"
		bind:this={inputElm}
		{id}
		{name}
		{value}
		bind:checked
		{disabled}
		aria-readonly={readOnly}
		on:change
	/><label for={id} class="cds--checkbox-label" {title}
		><span class="cds--checkbox-label-text" dir="auto">
			<slot>{label}</slot>
		</span></label
	>
	<div class="cds--checkbox__validation-msg">
		{#if invalid || warn}
			{#if invalid}
				<InformationFilled class="cds--checkbox__invalid-icon" />
			{:else if warn}
				<WarningAltFilled
					class="cds--checkbox__invalid-icon cds--checkbox__invalid-icon--warning"
				/>
			{/if}
			<FormRequirement>
				{#if invalid}
					<slot name="invalid">{invalidText}</slot>
				{:else if warn}
					<slot name="warn">{warnText}</slot>
				{/if}
			</FormRequirement>
		{/if}
	</div>
</div>
