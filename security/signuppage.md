<h1> Sign Up </h1>

<label for="inputName">Name</label>
<input id="inputName" type="text" name="inputName" autocomplete="off" />

<label for="inputEmail">Email</label>
<input id="inputEmail" type="text" name="inputEmail" autocomplete="off" />
 
<label for="inputPassword">Password</label>
<input id="inputPassword" type="password" name="inputPassword" />

<h3> Interest Form </h3>

<div whitespace="nowrap">
<label style="inline-block" for="inputStats">Statistics  </label>
<input style="inline-block" id="inputStats" type="checkbox" name="inputStats" />
</div>

<div whitespace="nowrap">
<label style="inline-block" for="inputBio">Biology  </label>
<input style="inline-block" id="inputBio" type="checkbox" name="inputBio" />
</div>

<div whitespace="nowrap">
<label style="inline-block" for="inputChem">Chemistry  </label>
<input style="inline-block" id="inputChem" type="checkbox" name="inputChem" />
</div>

<div whitespace="nowrap">
<label style="inline-block" for="inputPhys">Physics  </label>
<input style="inline-block" id="inputPhys" type="checkbox" name="inputPhys" />
</div>

<button class="button1" onclick="signup()">Sign Up</button>

<button class="button1" onclick="location.href='/DADY-Academy/security/testpagelogin'">I already have an account</button>


<script>

function signup() {
    const name = document.getElementById("inputName").value;
    const email = document.getElementById("inputEmail").value;
    const password = document.getElementById("inputPassword").value;
    const stats = document.getElementById("inputStats").checked;
    const bio = document.getElementById("inputBio").checked;
    const chem = document.getElementById("inputChem").checked;
    const phys = document.getElementById("inputPhys").checked;

    const url = "https://frq.dtsivkovski.tk/register";
  
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
        "password" : password,
        "name" : name,
        "stats": stats,
        "chem": chem,
        "phys": phys,
        "bio": bio
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
    //   if (!response.ok) {
    //       const errorMsg = 'Login error: ' + response.status;
    //       console.log(errorMsg);
    //       return; 
    //   }
      // Success!!!
      
      sessionStorage.setItem("username", email);
      login();
    //   window.location.reload();
      // window.location.href = "{{site.baseurl}}/home";


  })

}

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
  
  const logoutUrl = "https://frq.dtsivkovski.tk/logoutJWT";
  const optionsLogout = {
    method: 'GET', 
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'include', // include, *same-origin, omit
    headers: {
        'Content-Type': 'application/json'
    }
  };


  fetch(logoutUrl, optionsLogout).then(response => {
    console.log(response);

    if (!response.ok) {
          const errorMsg = 'Login error: ' + response.status;
          console.log(errorMsg);
          return; 
      }

    window.location.reload();

  });
  sessionStorage.setItem("username", "Guest");
  sessionStorage.setItem("token", null);

}




if (sessionStorage.getItem("username") == null) {
  sessionStorage.setItem("username", "Guest");
}


document.getElementById("user").innerHTML = "Hello " + sessionStorage.getItem("username") + "!";



</script>

