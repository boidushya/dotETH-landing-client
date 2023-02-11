<script>
	import '../styles/app.css';
</script>

<slot />

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.zinc.900);
		color: theme(colors.zinc.500);
	}
	:global(html),
	:global(body) {
		@apply h-full;
	}
	:global(*),
	:global(*):after,
	:global(*):before {
		@apply box-border;
	}
	:global(:root) {
		--color-orange: theme(colors.orange.500);
		--color-red: theme(colors.pink.500);
		--color-blue: theme(colors.blue.500);
		--color-violet: theme(colors.violet.500);
		--color-green: theme(colors.green.500);
		--color-amber: theme(colors.amber.500);
		--color-purple: theme(colors.purple.500);
	}
</style>
