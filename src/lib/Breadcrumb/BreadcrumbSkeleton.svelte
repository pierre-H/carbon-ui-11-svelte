<script lang="ts">
	export let noTrailingSlash: boolean = false;
</script>

<div
	{...$$restProps}
	class="cds--breadcrumb cds--skeleton {$$restProps.class}"
	class:cds--breadcrumb--no-trailing-slash={noTrailingSlash}
>
	<div class="cds--breadcrumb-item"><span class="cds--link">&nbsp;</span></div>
	<div class="cds--breadcrumb-item"><span class="cds--link">&nbsp;</span></div>
	<div class="cds--breadcrumb-item"><span class="cds--link">&nbsp;</span></div>
</div>
