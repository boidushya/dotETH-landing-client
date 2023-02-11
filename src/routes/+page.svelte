<script>
	import { onDestroy, onMount } from 'svelte';
	import { browser } from '$app/environment';
	import Card from '../components/Card.svelte';

	const mouseMoveListener = (cards, e) => {
		cards.forEach((card) => {
			const rect = card.getBoundingClientRect();
			const x = e.clientX - rect.left;
			const y = e.clientY - rect.top;
			card.style.setProperty('--mouse-x', `${x}px`);
			card.style.setProperty('--mouse-y', `${y}px`);
		});
	};

	const removeCardHidden = (e) => {
		console.log('mouse in');
		e.target.classList.remove('card-hidden');
	};

	const addCardHidden = (e) => {
		console.log('mouse out');
		e.target.classList.add('card-hidden');
	};

	onMount(() => {
		const cards = document.querySelectorAll('.card');

		cards.forEach((card) => {
			card.addEventListener('mouseenter', removeCardHidden);
			card.addEventListener('mouseleave', addCardHidden);
		});

		document.addEventListener('mousemove', (e) => mouseMoveListener(cards, e));

		document.querySelector('.card').style.setProperty('--mouse-x', '0');
		document.querySelector('.card').style.setProperty('--mouse-y', '0');
	});

	onDestroy(() => {
		if (browser) {
			const cards = document.querySelectorAll('.card');
			document.removeEventListener('mousemove', (e) => mouseMoveListener(cards, e));
			cards.forEach((card) => {
				card.removeEventListener('mousemove', removeCardHidden);
				card.removeEventListener('mouseout', addCardHidden);
			});
		}
	});
</script>

<section class="grid place-items-center lg:w-3/4 w-[90%] mx-auto py-16">
	<div class="grid grid-cols-1 lg:grid-cols-5 gap-4 w-full">
		<Card color="var(--color-orange)" size="lg:col-span-3">
			<div
				class="grid place-items-center absolute inset-0 text-center max-w-[15rem] mx-auto"
				slot="text"
			>
				<p class="text-2xl font-medium">
					<span class="text-zinc-50">Some content</span> goes here
				</p>
			</div>
		</Card>
		<Card color="var(--color-red)">
			<p class="text-2xl font-medium " slot="text">
				<span class="text-zinc-50">Lorem ipsum</span> dolor sit amet consectetur adipiscing elit. Sed
				euismod, nisl nec ultricies ultricies.
			</p>
			<div class="bg-pink-400 rounded-[3rem] px-8 pb-0 mt-4" slot="img">
				<img class="-mt-5 z-10 relative" src="./illustration-1.png" alt="Illustration" />
			</div>
		</Card>
		<Card color="var(--color-green)">
			<p class="text-2xl font-medium " slot="text">
				<span class="text-zinc-50">Lorem ipsum</span> dolor sit amet consectetur adipiscing elit.
			</p>
			<div class="bg-green-400 rounded-[2rem] z-10" slot="img">
				<img class="-mt-8" src="./illustration-2.png" alt="Illustration" />
			</div>
		</Card>
		<Card color="var(--color-violet)" size="lg:col-span-3">
			<div
				class="grid place-items-center absolute inset-0 text-center max-w-[15rem] mx-auto"
				slot="text"
			>
				<p class="text-2xl font-medium">
					<span class="text-zinc-50">Other content</span> goes here though
				</p>
			</div>
		</Card>
		<Card color="var(--color-red)" size="lg:col-span-3">
			<div
				class="grid place-items-center absolute inset-0 text-center max-w-[15rem] mx-auto"
				slot="text"
			>
				<p class="text-2xl font-medium">
					<span class="text-zinc-50">Maybe a bit of text</span> can go here as well?
				</p>
			</div>
		</Card>
		<Card color="var(--color-purple)">
			<p class="text-2xl font-medium " slot="text">
				<span class="text-zinc-50">Lorem ipsum</span> dolor sit amet consectetur adipiscing elit.
			</p>
			<div class="bg-purple-400 rounded-[2rem] z-10" slot="img">
				<img class="-mt-8" src="./illustration-3.png" alt="Illustration" />
			</div>
		</Card>
	</div>
</section>
