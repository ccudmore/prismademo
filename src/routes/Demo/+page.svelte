<script lang="ts">
  let { data } = $props();
</script>

<h1>SvelteKit + Prisma</h1>

{#each data.users as user} // [!code ++]
<h2>{user.name}</h2>
// [!code ++] {#each user.posts as post}
<ul>
  <li><a href="{post.content}">{post.title}</a></li>
</ul>
// [!code ++] {/each} // [!code ++] {/each}
