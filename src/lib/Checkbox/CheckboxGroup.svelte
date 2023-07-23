<script lang="ts">
	import FormRequirement from '../Form/FormRequirement.svelte';
	import { uniqueId } from '../uniqueId.js';
	import InformationFilled from 'carbon-icons-svelte/lib/InformationFilled.svelte';
	import WarningAltFilled from 'carbon-icons-svelte/lib/WarningAltFilled.svelte';

	export let label: string | undefined = undefined;

	export let invalid: boolean = false;
	export let invalidText: string | undefined = undefined;

	export let warn: boolean = false;
	export let warnText: string | undefined = undefined;

	export let helperText: string | undefined = undefined;
	$: hasHelper = helperText || $$slots.helper;
	const helperId = uniqueId('checkbox-helper-');

	export let readOnly: boolean = false;
</script>

<fieldset
	{...$$restProps}
	class="cds--checkbox-group {$$restProps.class}"
	class:cds--checkbox-group--invalid={invalid}
	class:cds--checkbox-group--warning={warn && !invalid}
	class:cds--checkbox-group--readonly={readOnly}
	aria-readonly={readOnly}
	data-invalid={invalid}
	aria-describedby={hasHelper ? helperId : undefined}
>
	{#if label || $$slots.label}
		<legend class="cds--label"><slot name="label">{label}</slot></legend>
	{/if}
	<slot />
	<div class="cds--checkbox-group__validation-msg">
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
	{#if hasHelper}
		<div id={helperId} class="cds--form__helper-text">
			<slot name="helper">{helperText}</slot>
		</div>
	{/if}
</fieldset>
