<script>
	import Navigation from '../components/horizontal-nav-simple/navigation.svelte';

	const menu = [
		{
			icon: 'home',
			text: 'Home',
			active: true
		},
		{
			icon: 'person',
			text: 'Perfil'
		},
		{
			icon: 'mail',
			text: 'Mensagem'
		}
	];

	/**
	 * @param {{ detail: { text: string; }; }} event
	 */
	function handleMenuSelected(event) {
		console.log(`O menu selecionado foi: ${event.detail.text}`);
	}
</script>

<div class="menubar">
	<div class="position">
		<Navigation {menu} on:selected={handleMenuSelected} />
	</div>
</div>

<style>
	.menubar {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 105px;
		background-color: var(--back-color);
		z-index: 1;
		justify-content: right;
	}
	.position {
		position: absolute;
		right: 0;
	}
</style>
