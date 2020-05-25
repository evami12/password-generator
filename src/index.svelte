<script>
  let lowercase = false;
  let numbers = false;
  let specialCharacters = false;
  let uppercase = false;

  let passwordLength = 4;
  let password = "";

  function makePassword() {
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
</script>

<style>

</style>

<section class="section content">
  <h1>Password Generator!</h1>
  Password Length: {passwordLength}
  <input
    class="slider"
    type="range"
    min="1"
    max="15"
    bind:value={passwordLength} />

  <p>I would like:</p>
  <input type="checkbox" bind:value={lowercase} />
  Lowercase Letters
  <input type="checkbox" bind:value={numbers} />
  Numbers
  <input type="checkbox" bind:value={specialCharacters} />
  Special Characters
  <input type="checkbox" bind:value={uppercase} />
  Uppercase Letters
  <button on:click={makePassword}>Generate Password!</button>
  {password}
</section>
