<script lang="ts">
	import { onMount } from 'svelte';

	let pageNo = 1;
	let inLoading = false;

	interface Post {
		userId: number;
		id: number;
		title: string;
		body: string;
	}

	/**
	 * @type {any[]}
	 */
	let posts: Array<Post> = [];

	onMount(async () => {
		loadMore();
	});

	/**
	 *
	 */
	async function loadMore() {
		if (inLoading) return;
		inLoading = true;
		const response = await fetch(`https://jsonplaceholder.typicode.com/posts?_page=${pageNo}`);
		const data = await response.json();
		posts = [...posts, ...data];
		pageNo++;
		inLoading = false;
	}

	function onScroll(e: Event) {
		const el = document.documentElement;
		const bottom = el.scrollHeight - el.clientHeight - el.scrollTop;
		if (bottom <= 300) loadMore();
	}
</script>

<svelte:window on:scroll={onScroll} />

{#each posts as post}
	<div class="item">
		<div>No. {post.id}</div>
		<div>{post.title}</div>
		<div>{post.body}</div>
	</div>
	<hr />
{/each}

<style>
	.item {
		font-size: 2em;
	}
</style>
