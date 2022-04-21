<script>
    import Nav from "../Nav.svelte";
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
                        <tr>
                            <td>user-1</td>
                            <td>Mridul Ganga</td>
                            <td>mridul@gmail.com</td>
                            <td>+91 9000000000</td>
                            <td>123, Flat 1, Area 2, Bangalore</td>
                            <td>user</td>
                            <td>
                                <button class="button is-danger">delete</button>
                            </td>
                        </tr>
                        <tr>
                            <td>user-2</td>
                            <td>Admin User</td>
                            <td>admin@gmail.com</td>
                            <td>+91 9000000001</td>
                            <td>129, Flat 1, Area 2, Bangalore</td>
                            <td>admin</td>
                            <td>
                                <button class="button is-danger">delete</button>
                            </td>
                        </tr>
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
                            <input class="input" type="text" placeholder="Full Name"></div>
                        <div class="field">
                            <label class="label">Email</label>
                            <input class="input" type="email" placeholder="Email"></div>
                        <div class="field">
                            <label class="label">Phone</label>
                            <input class="input" type="tel" placeholder="Phone"></div>
                        <div class="field">
                            <label class="label">Address</label>
                            <textarea class="input" cols="30" rows="10" placeholder="Address"></textarea></div>
                        <div class="field">
                             <label class="label">User Type</label>
                            <div class="select" placeholder="User Type">
                                <select>
                                  <option>admin</option>
                                  <option>user</option>
                                </select>
                              </div>
                        </div>
                        <div class="field">
                            <label class="label">Password</label>
                            <input class="input" type="password" placeholder="Password"></div>
                        <button class="button is-primary">Create User</button>
                        <button class="button is-danger">Clear</button>
                    </div>
                </div>

            </div>
        </div>
        
    </section>
</main>
