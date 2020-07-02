<script>
  //Creating variables for different character types & numbers. lowercase is automatically true so the user is less likely to select no options. 
  let lowercase = true;
  let numbers = false;
  let specialCharacters = false;
  let uppercase = false;

  //Setting default password length to 10 and clearing result
  let passwordLength = 10;
  let userPassword = ""

//function takes user inputs and sends them to the makePassword function then gets the result and gives it to the user 
  function getPassword(){
    console.log("Generate Password button is clicked");

    //sending the user selections to the makepassword funtion
    userPassword = makePassword(passwordLength, lowercase, uppercase, numbers, specialCharacters)
  }


//function generates a random password based on the options received from the getPAssword function and returns the value to the getPassword function. it creates constants for ranges for rng. The function randomly chooses an option of character type from the user selected options and generates a random number within the range which is then translated from charcode into a character. it then returns password. 
  function makePassword(length, optionOne, optionTwo, optionThree, optionFour) {
    console.log("Generating password")
    //resets password
    let password = "";

    //creating constants for min and range of random character generator for the charcode
    //setting charcode min of lowercase to 97 and range to 26
    const lowercaseMin = 97
    const lowercaseRange = 26

    //setting charcode min of uppercase to 65 and range to 26
    const uppercaseMin = 65
    const uppercaseRange = 26

    //setting charcode min of numbers to 48 and range to 10
    const numbersMin = 48
    const numbersRange = 10

    //setting charcode min of special characters to 33 and range to 11
    const specialCharactersMin = 33
    const specialCharactersRange = 11

    while (password.length < length) {
      console.log("Generating password loop started");

      //Randomly selecting which type of character to choose
      let randomSelection = Math.floor(Math.random() * 4 + 1);

      //takes the random selection and generated a random character/number from within the selection (tyoe of character)
      if (randomSelection === 1 && optionOne) {
        let randomNum = Math.floor(Math.random() * lowercaseRange + lowercaseMin);
        password += String.fromCharCode(randomNum);
      }
      if (randomSelection === 4 && optionTwo) {
        let randomNum = Math.floor(Math.random() * uppercaseRange + uppercaseMin);
        password += String.fromCharCode(randomNum);
      }      
      if (randomSelection === 2 && optionThree) {
        let randomNum = Math.floor(Math.random() * numbersRange + numbersMin);
        password += String.fromCharCode(randomNum);
      }
      if (randomSelection === 3 && optionFour) {
        let randomNum = Math.floor(Math.random() * specialCharactersRange + specialCharactersMin);
        password += String.fromCharCode(randomNum);
      }
    }
    return password
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
    min="6"
    max="20"
    bind:value={passwordLength} />

  <p>I would like:</p>

  <div id="checkboxes">
    <label>
      <input type="checkbox" bind:checked={lowercase} />
      Lowercase Letters
    </label>

    <label>
      <input type="checkbox" bind:checked={uppercase} />
      Uppercase Letters
    </label>

    <label>
      <input type="checkbox" bind:checked={numbers} />
      Numbers
    </label>

    <label>
      <input type="checkbox" bind:checked={specialCharacters} />
      Special Characters
    </label>
  </div>

  <label>
    <!--If No checkboxes are selected, the button will disappear and it will prompt input from user-->
    {#if lowercase === false && numbers === false && specialCharacters === false && uppercase === false}
      <p>Please select a checkbox</p>
    {:else}
      <button class="button is-success" on:click={getPassword}>
        Generate Password!
      </button>
    {/if}
  </label>

  <p id="password">Password: </p>
  
  <p>{userPassword}</p>

  <!--Suggests a password length of at least eight if user selects number less than eight-->
  {#if passwordLength < 10}
    <p>A good password should be at least 10 characters</p>
  {/if}

</section>
