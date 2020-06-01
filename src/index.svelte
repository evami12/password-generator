<script>
  //Creating variables for different character types & numbers
  let lowercase = true;
  let numbers = false;
  let specialCharacters = false;
  let uppercase = false;

  //Setting default password length to 8
  let passwordLength = 8;
  let password = "";

  function makePassword() {
    console.log("Generate Password button is clicked");
    password = "";

    while (password.length < passwordLength) {
      console.log("Generating password loop started");

      //Randomly selecting which type of character to choose
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
  #checkboxes {
    display: block;
    padding: 10px;
    margin-left: 10px;
    margin-right: 20px;
    margin-bottom: 10px;
    background-color: antiquewhite;
    color: black;
  }

  #password {
    display: block;
    size: 5px;
    margin-top: 20px;
  }
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

  <div id="checkboxes">
    <label>
      <input type="checkbox" bind:checked={lowercase} />
      Lowercase Letters
    </label>

    <label>
      <input type="checkbox" bind:checked={numbers} />
      Numbers
    </label>

    <label>
      <input type="checkbox" bind:checked={specialCharacters} />
      Special Characters
    </label>

    <label>
      <input type="checkbox" bind:checked={uppercase} />
      Uppercase Letters
    </label>
  </div>

  <label>
    <!--If No checkboxes are selected, the button will disappear and it will prompt input from user-->
    {#if lowercase === false && numbers === false && specialCharacters === false && uppercase === false}
      <p>Please select a checkbox</p>
    {:else}
      <button class="button is-success" on:click={makePassword}>
        Generate Password!
      </button>
    {/if}
  </label>

  <p id="password">Password: {password}</p>

  <!--Suggests a password length of at least six if user selects number less than six-->
  {#if passwordLength < 6}
    <p>Password should be at least 6 letters</p>
  {/if}

</section>
