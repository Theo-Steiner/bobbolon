<script>
  import { createEventDispatcher } from "svelte";
  export let password;
  const inputs = {};
  let userInput = "";

  const dispatch = createEventDispatcher();

  const fail = () => {
    userInput = "";
    inputs[0].focus();
  };

  const advance = () => {
    userInput = "";
    dispatch("advance");
  };

  const handleKeydown = (e) => {
    if (e.code === "Backspace") {
      userInput = userInput.slice(0, -1);
      if (userInput.length === 0) return;
      inputs[userInput.length - 1].focus();
      return;
    }
    if (e.key.length !== 1 || userInput.length + 1 > password.length) return;
    userInput += e.key;
    if (userInput.length === password.length) {
      const result = userInput === password ? advance : fail;
      setTimeout(result, 500);
      return;
    }
    inputs[userInput.length].focus();
  };

  $: shouldShake =
    userInput.length === password.length && userInput !== password;
</script>

<h1>Cooler login</h1>
<form class:shake={shouldShake}>
  {#each password as _, index}
    <label bind:this={inputs[index]}>
      <input
        value={userInput.charAt(index) || ""}
        on:keydown|preventDefault={handleKeydown}
      />
    </label>
  {/each}
</form>

<style>
  form {
    display: flex;
    justify-content: center;
  }
  input {
    width: 3ch;
    height: 3ch;
  }

  .shake {
    animation: shake-animation 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
    transform: translate3d(0, 0, 0);
    backface-visibility: hidden;
    perspective: 1000px;
  }

  @keyframes shake-animation {
    10%,
    90% {
      transform: translate3d(-1px, 0, 0);
    }

    20%,
    80% {
      transform: translate3d(2px, 0, 0);
    }

    30%,
    50%,
    70% {
      transform: translate3d(-4px, 0, 0);
    }

    40%,
    60% {
      transform: translate3d(4px, 0, 0);
    }
  }
</style>

