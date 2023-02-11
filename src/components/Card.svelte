<script>
	export let color = 'var(--color-orange)';
	export let size = 'lg:col-span-2';
</script>

<div class="space-y-4 card h-[26rem] card-hidden {size}" style="--color: {color};">
	<div class="card-content">
		<div class="p-8">
			<slot name="text" />
		</div>
		<slot name="img" />
	</div>
</div>

<style lang="scss">
	.card {
		@apply rounded-[3rem] relative overflow-hidden grid place-items-center bg-zinc-600;

		&-hidden {
			&:after {
				opacity: 0 !important;
			}
		}

		&-content {
			@apply z-[2] rounded-[inherit] overflow-hidden flex flex-col items-start justify-between absolute h-[calc(100%_-_2px)] w-[calc(100%_-_2px)] bg-gradient-to-br from-[hsl(240,6%,12%)] to-[hsl(240,6%,10%)];
		}
		&:before {
			@apply absolute opacity-100 inset-0 z-[1] will-change-[opacity] transition-opacity duration-500 pointer-events-none;
			background: radial-gradient(
				400px circle at var(--mouse-x) var(--mouse-y),
				var(--color),
				transparent 40%
			) !important;
			content: '';
		}
		&:after {
			@apply absolute opacity-100 inset-0 z-[2] will-change-[opacity] transition-opacity duration-500 pointer-events-none;
			background: radial-gradient(
				800px circle at var(--mouse-x) var(--mouse-y),
				hsla(0, 0%, 20%, 0.25),
				transparent 40%
			);
			content: '';
		}
	}
</style>
