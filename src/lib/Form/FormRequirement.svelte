<script lang="ts" context="module">
	import '@carbon/styles/scss/components/form/_index.scss';
</script>

<div {...$$restProps} class="cds--form-requirement {$$restProps.class ?? ''}">
	<slot />
</div>
