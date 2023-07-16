<script lang="ts">
	export let title: boolean = false;
</script>

<p
	{...$$restProps}
	class="cds--skeleton__text {$$restProps.class ?? ''}"
	class:cds--accordion__title={title}
/>
