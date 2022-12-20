<script>
  import Login from "./lib/Login.svelte";
  import Content from "./lib/Content.svelte";
  let state = "";
</script>

{#if state === "login"}
  <Login password="plompl" on:advance={() => (state = "content")} />
{:else}
  <Content on:reset={() => (state = "login")} />
{/if}

