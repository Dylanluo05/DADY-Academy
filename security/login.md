# Get Started

<form id="loginForm" action="https:frrq.dtsivkovski.tk/api/person/post" method="post">
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required><br>
    <label for="password">Password:</label>
    <input type="password" id="password" name="password" required><br>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required><br>
    <button class="button" value="Sign Up" onclick="submitForm()">Sign Up</button>
</form>

<script>
    function submitForm() {
        $.post("https:frq.dtsivkovski.tk/api/person/post", $("#loginForm").serialize(), function(data) {
            console.log(data);
        });
    }
</script>