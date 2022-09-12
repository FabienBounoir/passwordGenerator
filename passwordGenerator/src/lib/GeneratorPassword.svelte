<script>
  import { onMount } from "svelte";
  import { writable } from "svelte/store";
  import { fade, scale, slide } from "svelte/transition";

  let message = "";
  let password = "";
  let passwordLength = 8;
  let Numbers = true;
  let Symbols = true;
  let Uppercase = true;
  let Lowercase = true;

  const copieToClipBoard = () => {
    if (password == "Choose Elements") return;
    navigator.clipboard.writeText(password);
    message = "Password copied to clipboard";

    setTimeout(() => {
      message = "";
    }, 3000);
  };

  const Generator = () => {
    let generatePassword = "";
    const numbers = "0123456789";
    const symbols = "!@#$%^&*_-+=";
    const uppercase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    const lowercase = "abcdefghijklmnopqrstuvwxyz";

    let characters = "";

    if (Numbers) {
      characters += numbers;
    }
    if (Symbols) {
      characters += symbols;
    }
    if (Uppercase) {
      characters += uppercase;
    }
    if (Lowercase) {
      characters += lowercase;
    }

    for (let i = 0; i < passwordLength; i++) {
      generatePassword += characters.charAt(
        Math.floor(Math.random() * characters.length)
      );
    }

    //check if password are all present
    if (Numbers) {
      if (!generatePassword.match(/[0-9]/g)) {
        return Generator();
      }
    }

    if (Symbols) {
      if (!generatePassword.match(/[!@#$%^&*_\-+=]/g)) {
        return Generator();
      }
    }

    if (Uppercase) {
      if (!generatePassword.match(/[A-Z]/g)) {
        return Generator();
      }
    }

    if (Lowercase) {
      if (!generatePassword.match(/[a-z]/g)) {
        return Generator();
      }
    }

    console.log(generatePassword);

    password = generatePassword || "Choose Elements";
  };

  Generator();

  function onChange(...args) {
    console.log("coucou");
    Generator();
  }

  $: onChange(Numbers, Symbols, Uppercase, Lowercase);
</script>

<main>
  <div class="passwordElements">
    <button
      class={Numbers ? "selected" : ""}
      on:click={() => (Numbers = !Numbers)}>Numbers</button
    >

    <button
      class={Symbols ? "selected" : ""}
      on:click={() => (Symbols = !Symbols)}>Symbols</button
    >

    <button
      class={Uppercase ? "selected" : ""}
      on:click={() => (Uppercase = !Uppercase)}>Uppercase</button
    >

    <button
      class={Lowercase ? "selected" : ""}
      on:click={() => (Lowercase = !Lowercase)}>Lowercase</button
    >
  </div>

  <p class="password" on:click={() => copieToClipBoard()}>{password}</p>
  {#if message != ""}
    <p class="message" transition:scale>{message}</p>
  {/if}
</main>

<!-- <button on:click={increment}>
  count is {count}
</button> -->
<style>
  .passwordElements {
    display: flex;
    gap: 1em;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    color: #fff;
    font-weight: bold;
    text-transform: uppercase;
  }

  .selected {
    background-color: #646cff;
  }

  button:focus {
    outline: 0px;
  }

  .element {
    border: 1px solid transparent;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    font-weight: bold;
    text-transform: uppercase;
  }
</style>
