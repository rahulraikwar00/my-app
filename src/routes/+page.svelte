<script>
  import { signIn, signOut } from "@auth/sveltekit/client";
  export let data;
</script>

<style>
  nav {
    background-color: #333;
    color: #fff;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
  }

  nav p {
    margin: 0;
  }

  .actions {
    display: flex;
    align-items: center;
  }

  button {
    background-color: #4caf50;
    color: #fff;
    border: none;
    padding: 0.5rem 1rem;
    margin-left: 1rem;
    cursor: pointer;
    border-radius: 4px;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #45a049;
  }

  .post-preview {
    margin: 2rem;
  }

  .user-profile {
    display: flex;
    align-items: center;
  }

  .user-profile img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    object-fit: cover;
    margin-right: 1rem;
  }

  .user-profile h1 {
    margin: 0;
  }
</style>

<nav>
  <p>
    These actions are all using the methods exported from
    <code>@auth/sveltekit/client</code>
  </p>
  <div class="actions">
    {#if !data.session?.user}
      <button on:click={() => signIn("github")}>Sign In with GitHub</button>
    {:else}
      <button on:click={() => signOut()}>Sign Out</button>
    {/if}
  </div>
</nav>

<section class="post-preview">
  <pre>{JSON.stringify(data.session)}</pre>
  <div class="user-profile">
    {#if data.session && data.session.user}
      <img src={data.session.user.image} alt="User Profile Picture" />
      <h1>User Profile</h1>
    {:else}
      <p>No user session found.</p>
    {/if}
  </div>
</section>
