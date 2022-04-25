<script>
    let email = "";
    let password = "";
    import { router } from "tinro";

    let isLoading = false;
    let users = [];

    async function loadUsers() {
        isLoading = true;
        await fetch("https://demo-blood-bank-app.herokuapp.com/getAllUsers")
            .then((response) => response.json())
            .then((data) => {
                users = data;
                console.log(data);
            })
            .catch((error) => {
                console.log(error);
            });
        isLoading = false;
    }

    async function login() {
        await loadUsers();

        let user = {};
        users = users.filter(v=> v.email == email)
        user = users[0]
        console.log(user)

        if (user.email == email && user.password == password) {
            localStorage.setItem("user", email);
            router.goto("/listusers");
        } else {
            alert("credentials are not valid");
        }
    }
</script>

<section class="section">
    <div class="container">
        <h1 class="title">
            Login {#if isLoading}
                (Loading...)
            {/if}
        </h1>
        <p class="subtitle">Login to Blood Bank Management Portal</p>

        <div class="columns">
            <div class="column">
                <div class="field">
                    <label class="label">Email</label>
                    <div class="control ">
                        <input
                            class="input"
                            type="email"
                            placeholder="Email input"
                            bind:value={email}
                        />
                        <span class="icon is-small is-left">
                            <i class="fas fa-envelope" />
                        </span>
                    </div>
                </div>

                <div class="field">
                    <label class="label">Password</label>
                    <div class="control ">
                        <input
                            class="input"
                            type="password"
                            placeholder="Password input"
                            bind:value={password}
                        />
                        <span class="icon is-small is-left">
                            <i class="fas fa-key" />
                        </span>
                    </div>
                </div>

                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-link" on:click={login}
                            >Login</button
                        >
                    </div>
                    <!-- <div class="control">
                        <a class="button is-link is-light" href="/signup"
                            >Signup</a
                        >
                    </div> -->
                </div>
            </div>
            <!--column one-->
            <div class="column" />
        </div>
    </div>
</section>
