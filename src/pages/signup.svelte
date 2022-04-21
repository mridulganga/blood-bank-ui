<script>
    let email = "";
    let password = "";

    function signup(){
        
    }

</script>

<section class="section">
    <div class="container">
        <h1 class="title">Login</h1>
        <p class="subtitle">Login to Blood Bank Management Portal</p>

        <div class="columns">
            <div class="column">

                <div class="field">
                    <label class="label">Name</label>
                    <div class="control ">
                        <input
                            class="input"
                            type="text"
                            placeholder="Name input"
                        />
                        <span class="icon is-small is-left">
                            <i class="fas fa-envelope" />
                        </span>
                    </div>
                </div>

                <div class="field">
                    <label class="label">Email</label>
                    <div class="control ">
                        <input
                            class="input"
                            type="email"
                            placeholder="Email input"
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
                        />
                        <span class="icon is-small is-left">
                            <i class="fas fa-key" />
                        </span>
                    </div>
                </div>

                <div class="field">
                    <label class="label">Confirm Password</label>
                    <div class="control ">
                        <input
                            class="input"
                            type="password"
                            placeholder="Password input"
                        />
                        <span class="icon is-small is-left">
                            <i class="fas fa-key" />
                        </span>
                    </div>
                </div>

                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-link" on:click={signup}
                            >Signup</button
                        >
                    </div>
                    <div class="control">
                        <a class="button is-link is-light" href="/login"
                            >Login</a
                        >
                    </div>
                </div>
            </div>
            <!--column one-->
            <div class="column" />
        </div>
    </div>
</section>
