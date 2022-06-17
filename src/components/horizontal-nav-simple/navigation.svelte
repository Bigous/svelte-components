<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let menu = [
		{
			icon: 'home',
			text: 'Home'
		},
		{
			icon: 'person',
			text: 'Perfil'
		},
		{
			icon: 'mail',
			text: 'Mensagem',
			active: true
		},
		{
			icon: 'camera',
			text: 'Fotos'
		},
		{
			icon: 'settings',
			text: 'Configurações'
		}
	];

	/**
	 * @type {HTMLDivElement}
	 */
	let indicator;

	/**
	 * @param {{ icon: string; text: string; href: string; active?: undefined; } | { icon: string; text: string; href: string; active: boolean; }} item
	 */
	function changeActiveTo(item) {
		for (let i = 0; i < menu.length; i++) {
			menu[i].active = false;
			if (item === menu[i]) {
				menu[i].active = true;
				indicator.style.transform = `translateX(${i * 70}px)`;
				dispatch('selected', item);
			}
		}
	}

	if (menu.findIndex((i) => i.active == true) == -1) {
		menu[0].active = true;
	}
</script>

<div class="navigation" style="width: {menu.length * 70 + 50}px">
	<ul style="width: {menu.length * 70}px">
		{#each menu as item}
			<li class="list {item.active ? 'active' : ''}">
				<span class="menuitem" on:click={changeActiveTo(item)}>
					<span class="icon"><ion-icon name={item.icon} /></span>
					<span class="text">{item.text}</span>
        </span>
			</li>
		{/each}
		<div
			class="indicator"
			bind:this={indicator}
			style="transform: translateX({70 * menu.findIndex((i) => i.active == true)}px)"
		/>
	</ul>
</div>

<style>
	.navigation {
		position: relative;
		height: 70px;
		background: #fff;
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 10px;
		transform: translateY(35px);
	}
	.navigation ul {
		display: flex;
	}
	.navigation ul li {
		position: relative;
		list-style: none;
		width: 70px;
		height: 70px;
		z-index: 1;
	}
	.navigation ul li .menuitem {
		position: relative;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 100%;
		height: 100%;
		text-align: center;
		font-weight: 500;
    cursor: pointer;
	}
	.navigation ul li .menuitem .icon {
		position: relative;
		display: block;
		line-height: 75px;
		font-size: 1.5em;
		text-align: center;
		transition: 0.5s;
		color: var(--back-color);
	}
	.navigation ul li.active .menuitem .icon {
		transform: translateY(-30px);
	}
	.navigation ul li .menuitem .text {
		position: absolute;
		color: var(--back-color);
		font-family: Poppins;
		font-weight: 400;
		font-size: 0.75em;
		letter-spacing: 0.05em;
		transition: 0.5s;
		opacity: 0;
		transform: translateY(20px);
	}
	.navigation ul li.active .menuitem .text {
		opacity: 1;
		transform: translateY(10px);
	}
	.indicator {
		position: absolute;
		top: -50%;
		width: 70px;
		height: 70px;
		background: var(--sel-color);
		border-radius: 50%;
		border: 6px solid var(--back-color);
		transition: 0.5s;
	}
	.indicator::before {
		content: '';
		position: absolute;
		top: 50%;
		left: -22px;
		width: 20px;
		height: 20px;
		background: transparent;
		border-top-right-radius: 20px;
		box-shadow: 0 -10px 0 0 var(--back-color);
	}
	.indicator::after {
		content: '';
		position: absolute;
		top: 50%;
		right: -22px;
		width: 20px;
		height: 20px;
		background: transparent;
		border-top-left-radius: 20px;
		box-shadow: 0 -10px 0 0 var(--back-color);
	}
</style>
