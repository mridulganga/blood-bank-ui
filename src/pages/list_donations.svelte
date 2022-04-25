<script>
    import Nav from "../Nav.svelte";

    let isLoading = true;
    let bloods = [];
    let blood = { user: {} };

    let users = [];

    async function loadUsers() {
        isLoading = true
        await fetch("https://demo-blood-bank-app.herokuapp.com/getAllUsers")
            .then((response) => response.json())
            .then((data) => {
                users = data;
                console.log(data);
            })
            .catch((error) => {
                console.log(error);
            });
        isLoading = false
    }

    async function loadBloods() {
        isLoading = true
        let res = await fetch(
            "https://demo-blood-bank-app.herokuapp.com/getAllBloodDetails"
        );
        bloods = await res.json();
        isLoading = false
    }

    loadBloods();
    loadUsers();

    async function createBlood() {
        isLoading = true
        blood.status = "scheduled";
        const res = await fetch(
            "https://demo-blood-bank-app.herokuapp.com/saveBloodDetails",
            {
                method: "POST",
                body: JSON.stringify(blood),
                headers: { "content-type": "application/json" },
            }
        );

        clear();
        loadBloods();
        isLoading = false
    }

    async function deleteBlood(id) {
        isLoading = true
        await fetch(
            "https://demo-blood-bank-app.herokuapp.com/deleteBloodDetails/" +
                id,
            {
                method: "DELETE",
            }
        );
        loadBloods();
        isLoading = false
    }

    async function markDonated(id) {
        isLoading = true
        await fetch(
            "https://demo-blood-bank-app.herokuapp.com/updateBloodDetails",
            {
                method: "PUT",
                headers: {
                    Accept: "application/json",
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    bloodDetailsId: id,
                    status: "donated",
                }),
            }
        );
        loadBloods()
        isLoading = false
    }

    function clear() {
        console.log("clearing form blood");
        blood = { user: {} };
    }
</script>

<main>
    <Nav />
    <section class="section">
        <div class="container">
            <h1 class="title">List Donations {#if isLoading}
                (Loading...)
            {/if}</h1>
            <p class="subtitle">List of donations</p>
        </div>
    </section>
    <section class="section">
        <div class="columns">
            <div class="column">
                <table class="table is-bordered">
                    <thead>
                        <tr>
                            <th>blood id</th>
                            <th>donation date</th>
                            <th>blood group</th>
                            <th>donor</th>
                            <th>quantity</th>
                            <th>status</th>
                            <th>actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        {#each bloods as b}
                            <tr>
                                <td>{b.bloodId}</td>
                                <td>{b.donationDate}</td>
                                <td>{b.bloodGroup}</td>
                                <td>{b.user.fullName}</td>
                                <td>{b.quantity}</td>
                                <td>{b.status}</td>
                                <td>
                                    <button 
                                        class="button is-primary"
                                        on:click={() => {
                                            markDonated(b.bloodId);
                                        }}
                                        >mark donated</button
                                    >
                                    <button
                                        class="button is-danger"
                                        on:click={() => {
                                            deleteBlood(b.bloodId);
                                        }}>delete</button
                                    >
                                </td>
                            </tr>
                        {/each}
                    </tbody>
                </table>
            </div>
            <div class="column">
                <div class="card">
                    <div class="card-header">
                        <p class="card-header-title">Create Donation</p>
                    </div>
                    <div class="card-content">
                        <div class="field">
                            <label class="label">Donor</label>
                            <div class="select" placeholder="Donor">
                                <select bind:value={blood.user.userId}>
                                    {#each users as u}
                                        <option value={u.userId}
                                            >{u.fullName}</option
                                        >
                                    {/each}
                                </select>
                            </div>
                        </div>
                        <div class="field">
                            <label class="label">Donation Date</label>
                            <input
                                class="input"
                                type="date"
                                placeholder="Donation Date"
                                bind:value={blood.donationDate}
                            />
                        </div>
                        <div class="field">
                            <label class="label">Blood Group</label>
                            <div class="select" placeholder="Blood Group">
                                <select bind:value={blood.bloodGroup}>
                                    <option>B+</option>
                                    <option>O+</option>
                                    <option>AB+</option>
                                    <option>B-</option>
                                    <option>O-</option>
                                    <option>AB-</option>
                                </select>
                            </div>
                        </div>
                        <div class="field">
                            <label class="label">Quantity</label>
                            <input
                                class="input"
                                bind:value={blood.quantity}
                                type="number"
                                placeholder="Quantity"
                            />
                        </div>

                        <button class="button is-primary" on:click={createBlood}
                            >Create Donation</button
                        >
                        <button class="button is-danger" on:click={clear}
                            >Clear</button
                        >
                    </div>
                </div>
            </div>
        </div>
    </section>
</main>
