<script>
    import Nav from "../Nav.svelte";

    let users = [];
    let user = {};

    fetch("https://demo-blood-bank-app.herokuapp.com/getAllUsers")
        .then((response) => response.json())
        .then(data => {users = data; console.log(data)})
        .catch((error) => {
            console.log(error);
        });


    async function createUser(){
        console.log("creating new user")
        console.log(user)

        
		const res = await fetch('https://demo-blood-bank-app.herokuapp.com/registerUser', {
			method: 'POST',
			body: JSON.stringify(user),
            headers: {"content-type":"application/json"}
		})

		clear()
    }

    function clear(){
        console.log("clearing form user")
        user = {};
    }
</script>

<main>
    <Nav />
    <section class="section">
        <div class="container">
            <h1 class="title">List Users</h1>
            <p class="subtitle">List of users</p>
        </div>
    </section>
    <section class="section">
        <div class="columns">
            <div class="column">
                <table class="table is-bordered">
                    <thead>
                        <tr>
                            <th>user id</th>
                            <th>fullname</th>
                            <th>email</th>
                            <th>phone</th>
                            <th>address</th>
                            <th>type</th>
                            <th>actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        {#each users as u}
                        <tr>
                            <td>{u.userId}</td>
                            <td>{u.fullName}</td>
                            <td>{u.email}</td>
                            <td>{u.phone}</td>
                            <td>{u.houseNo}, {u.street}, {u.city}, {u.pin}</td>
                            <td>{u.userType}</td>
                            <td>
                                <button class="button is-danger">delete</button>
                            </td>
                        </tr>
                        {/each}
                    </tbody>
                </table>
            </div>
            <div class="column">
                <div class="card">
                    <div class="card-header">
                        <p class="card-header-title">Create User</p>
                    </div>
                    <div class="card-content">
                        <div class="field">
                            <label class="label">Full Name</label>
                            <input
                                class="input"
                                type="text"
                                placeholder="Full Name"
                                bind:value={user.fullName}
                            />
                        </div>
                        <div class="field">
                            <label class="label">Email</label>
                            <input
                                class="input"
                                type="email"
                                placeholder="Email"
                                bind:value={user.email}
                            />
                        </div>
                        <div class="field">
                            <label class="label">Phone</label>
                            <input
                                class="input"
                                type="tel"
                                placeholder="Phone"
                                bind:value={user.phone}
                            />
                        </div>
                        <div class="field">
                            <label class="label">House No</label>
                            <input
                                type="number"
                                class="input"
                                placeholder="House No"
                                bind:value={user.houseNo}
                            />
                        </div>
                        <div class="field">
                            <label class="label">Street</label>
                            <input
                                type="text"
                                class="input"
                                placeholder="Street"
                                bind:value={user.street}
                            />
                        </div>
                        <div class="field">
                            <label class="label">City</label>
                            <input
                                type="text"
                                class="input"
                                placeholder="City"
                                bind:value={user.city}
                            />
                        </div>
                        <div class="field">
                            <label class="label">Pin</label>
                            <input
                                type="number"
                                class="input"
                                placeholder="Pin"
                                bind:value={user.pin}
                            />
                        </div>
                        <div class="field">
                            <label class="label">User Type</label>
                            <div class="select" placeholder="User Type">
                                <select bind:value={user.userType}>
                                    <option>admin</option>
                                    <option>user</option>
                                </select>
                            </div>
                        </div>
                        <div class="field">
                            <label class="label">Password</label>
                            <input
                                class="input"
                                type="password"
                                placeholder="Password"
                                bind:value={user.password}
                            />
                        </div>
                        <button class="button is-primary" on:click={createUser}>Create User</button>
                        <button class="button is-danger" on:click={clear}>Clear</button>
                    </div>
                </div>
            </div>
        </div>
    </section>
</main>
