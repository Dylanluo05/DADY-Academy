<h1 id="user"> </h1>

<label for="inputEmail">Email</label>
<input id="inputEmail" type="text" name="inputEmail" autocomplete="off" />

 
<label for="inputPassword">Password</label>
<input id="inputPassword" type="password" name="inputPassword" />

<button class="button1" onclick="login()">Login</button>

<button class="button1" onclick="logout()">Logout</button>


<script>

function login() {
  const email = document.getElementById("inputEmail").value;
  const password = document.getElementById("inputPassword").value;

  const url = "https://frq.dtsivkovski.tk/authenticate";
  
  const options = {
    method: 'POST', 
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'include', // include, *same-origin, omit
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        "email" : email,
        "password" : password
    })
  };

  console.log(options);

  // fetch(url, options)
  //   .then(response => console.log(response.text()))
  //   .then(result => console.log(result))
  //   .catch(error => console.log('error', error));


  // Fetch JWT
  fetch(url, options)
  .then(response => {
      // trap error response from Web API
      if (!response.ok) {
          const errorMsg = 'Login error: ' + response.status;
          console.log(errorMsg);
          return; 
      }
      // Success!!!
      
      sessionStorage.setItem("username", email);
      window.location.reload();
      // window.location.href = "{{site.baseurl}}/home";


  })





  
}

function logout() {
  document.cookie = "jwt=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
  sessionStorage.setItem("username", "Guest");
  sessionStorage.setItem("token", null);
  window.location.reload();

}




if (sessionStorage.getItem("username") == null) {
  sessionStorage.setItem("username", "Guest");
}


document.getElementById("user").innerHTML = "Hello " + sessionStorage.getItem("username") + "!";



</script>

