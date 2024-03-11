<script>
    import { signIn, signOut } from "@auth/sveltekit/client"
    export let data;
</script>

<nav style="background-color: grey; display: flex;">
  <p>
    These actions are all using the methods exported from
    <code>@auth/sveltekit/client</code>
  </p>
  <div class="actions" style="display: flex">
    {#if !data.session?.user }
    <div class="wrapper-form">
      <button on:click={() => signIn("github")}>Sign In with GitHub</button>
    </div>

    {:else}
    <div>
      <button on:click={() => signOut()}>
        Sign Out
      </button>
    </div>
      
    {/if}
   
  </div> <!-- Close div for "actions" -->
</nav>

<section class = "post preview" >
  <pre>

    {JSON.stringify(data.session)}
  </pre>
    <h1>User Profile</h1>
    {#if data.session && data.session.user}
        <!-- svelte-ignore a11y-img-redundant-alt -->
        <img src={data.session.user.image} alt="User Profile Picture" />
    {:else}
        <p>No user session found.</p>
    {/if}
</section>
