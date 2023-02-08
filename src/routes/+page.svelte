<svelte:head>
	<title>Gabey</title>
</svelte:head>

<script lang="ts">
	interface Links {
		name: string;
		url?: string;
		class: string;
		tooltip?: string;
		color: string;
	}

	const fa = 'fa-2xl';
	const linksClass = 'tooltip tooltip-bottom p-4 w-full flex items-center justify-center rounded-3xl m-1 shadow-2xl';
	const links: Links[] = [
		{
			name: 'Osu',
			tooltip: 'Gabey',
			url: 'https://osu.ppy.sh/users/12904237',
			class: 'fa-solid fa-circle',
      color: '#ff66aa'
		},
		{
			name: 'Discord',
			tooltip: 'Gabey#5450',
			class: 'fa-brands fa-discord',
			color: '#7289da'
		},
		{
			name: 'Twitter',
			tooltip: '@gabeyosu',
			url: 'https://twitter.com/gabeyosu',
			class: 'fa-brands fa-twitter',
			color: '#1da1f2'
		},
    {
      name: 'Twitch',
      tooltip: 'gaybey_',
      url: 'https://twitch.tv/gaybey_',
      class: 'fa-brands fa-twitch',
      color: '#9146ff'
    }
	];

	const handleClick = () => {
		const textarea: any = document.createElement('textarea');
		textarea.value = links[1].tooltip;
		document.body.appendChild(textarea);
		textarea.select();
		document.execCommand('copy');
		textarea.remove();

		const tooltip: any = document.querySelector('#discord');
		tooltip.setAttribute('data-tip', 'Copied to clipboard!');
		setTimeout(() => {
			tooltip.setAttribute('data-tip', links[1].tooltip);
		}, 1000);
	};
</script>

<div class="flex flex-col sm:flex-row justify-center items-center text-white w-2/5 min-w-[300px]">
  <img src="https://a.ppy.sh/12904237" class="rounded-full w-48 mr-4 shadow-2xl" alt="profile-pic" />
  <span class="flex flex-col w-full">
    <section class="ml-1 mb-1">
      <h1 class="text-5xl font-bold shadow-text">Gabey.</h1>
    </section>
    <section class="flex justify-center w-full max-w-[600px]">
      {#each links as link}
        {#if link.name === 'Discord'}
          <button
            id="discord"
            on:click={handleClick}
            class={linksClass}
            data-tip={link.tooltip}
            style="background-color: {link.color};"
          >
            <i class="{link.class} {fa}" />
          </button>
        {:else if link.name === 'Osu'}
          <a
            href={link.url}
            class='{linksClass} max-w-24'
            data-tip={link.tooltip}
            style="background-color: {link.color};"
          >
            <img src='/osulogo.png' class="max-w-[32px]" alt="osu-logo">
          </a>
        {:else}
          <a
            href={link.url}
            class={linksClass}
            data-tip={link.tooltip}
            style="background-color: {link.color};"
          >
            <i class="{link.class} {fa}" />
          </a>
        {/if}
      {/each}
    </section>
  </span>
</div>

<style>
  .shadow-text {
    text-shadow: 5px 0 10px rgba(0, 0, 0, 0.5);
  }
</style>
