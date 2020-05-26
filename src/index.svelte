<script>
  let lowercase = true;
  let numbers = false;
  let specialCharacters = false;
  let uppercase = false;

  let passwordLength = 8;
  let password = "";

  function makePassword() {
    password = "";
    if (
      lowercase === false &&
      numbers === false &&
      specialCharacters === false &&
      uppercase === false
    ) {
      password = "Please tick at least one checkbox";
    } else {
      while (password.length < passwordLength) {
        let randomSelection = Math.floor(Math.random() * 4 + 1);
        if (randomSelection === 1 && lowercase) {
          let randomNum = Math.floor(Math.random() * 26 + 97);
          password += String.fromCharCode(randomNum);
        }
        if (randomSelection === 2 && numbers) {
          let randomNum = Math.floor(Math.random() * 10 + 48);
          password += String.fromCharCode(randomNum);
        }
        if (randomSelection === 3 && specialCharacters) {
          let randomNum = Math.floor(Math.random() * 11 + 33);
          password += String.fromCharCode(randomNum);
        }
        if (randomSelection === 4 && uppercase) {
          let randomNum = Math.floor(Math.random() * 26 + 65);
          password += String.fromCharCode(randomNum);
        }
      }
    }
  }
</script>

<style>

</style>

<section class="section content">
  <h1>Password Generator!</h1>
  Password Length: {passwordLength}
  <input
    class="slider"
    type="range"
    min="4"
    max="20"
    bind:value={passwordLength} />

  <p>I would like:</p>
  <input type="checkbox" bind:checked={lowercase} />
  Lowercase Letters
  <input type="checkbox" bind:checked={numbers} />
  Numbers
  <input type="checkbox" bind:checked={specialCharacters} />
  Special Characters
  <input type="checkbox" bind:checked={uppercase} />
  Uppercase Letters
  <button on:click={makePassword}>Generate Password!</button>
  {password}

{#if passwordLength < 6}
<p>Password should be at least 6 letters</p>
{/if}

</section>
