<script>
	let lastscroll = 0;

    // let data2;
	let data = [1, 2, 3, 4, 5, 5, 6, 5];
	let pagenum = 1;
	let isfetching = false;
	let hasMore = true;
    
	/**
	 * @type {any[]}
	 */
	let items = [];

	/**
	 * @param {any} e
	 */
	function loadMore(e) {
		const scrollTopPosition = window.pageYOffset;
		if (scrollTopPosition > lastscroll) {
			lastscroll = scrollTopPosition;
			fetch(`https://jsonplaceholder.typicode.com/posts?_page=${1}`)
            
				.then((res) => res.json())
				.then((json) => {
                });
			console.log('down');
		}
	}

	async function fetchData(){
const response = await fetch(`https://jsonplaceholder.typicode.com/posts?_page=${1}`);

const  data2 = await response.json();

console.log(data2[0].body)


    }

    fetchData()
</script>

{#each data2 as item}
	<div class="item">{item.id}</div>
{/each}

<svelte:window on:scroll={loadMore} />

<style>
	.item {
		font-size: 20em;
	}
</style>
