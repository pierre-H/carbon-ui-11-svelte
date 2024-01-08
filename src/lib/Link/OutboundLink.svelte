<script lang="ts">
	import Link, { type LinkProps } from './Link.svelte';
	import Launch from 'carbon-icons-svelte/lib/Launch.svelte';

	let { ...anchorProps } = $props<LinkProps>();
</script>

<Link rel="noopener noreferrer" target="_blank" {...anchorProps} icon={Launch} />
