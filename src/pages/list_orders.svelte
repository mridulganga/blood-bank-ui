<script>
    import Nav from "../Nav.svelte";

    let isLoading = true;
    let orders = [];
    let order = { user: {} };

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

    function getDateNow() {
        var today = new Date();
        var dd = String(today.getDate()).padStart(2, "0");
        var mm = String(today.getMonth() + 1).padStart(2, "0"); //January is 0!
        var yyyy = today.getFullYear();

        var todayString = dd + "/" + mm + "/" + yyyy;
        return todayString;
    }

    async function loadOrders() {
        isLoading = true
        let res = await fetch(
            "https://demo-blood-bank-app.herokuapp.com/getAllOrderDetails"
        );
        orders = await res.json();
        isLoading = false
    }

    loadOrders();
    loadUsers();

    async function createOrder() {
        isLoading = true
        order.status = "ordered";
        order.orderDate = getDateNow();

        await fetch(
            "https://demo-blood-bank-app.herokuapp.com/saveOrderDetails",
            {
                method: "POST",
                body: JSON.stringify(order),
                headers: { "content-type": "application/json" },
            }
        );

        clear();
        loadOrders();
        isLoading = false
    }

    async function deleteOrder(id) {
        isLoading = true
        await fetch(
            "https://demo-blood-bank-app.herokuapp.com/deleteOrder/" + id,
            {
                method: "DELETE",
            }
        );
        loadOrders();
        isLoading = false
    }

    async function markCompleted(id) {
        isLoading = true
        await fetch(
            "https://demo-blood-bank-app.herokuapp.com/updateOrderDetails",
            {
                method: "PUT",
                headers: {
                    Accept: "application/json",
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    orderId: id,
                    status: "completed",
                }),
            }
        );
        loadOrders()
        isLoading = false
    }

    function clear() {
        console.log("clearing form order");
        order = { user: {} };
    }
</script>

<main>
    <Nav />
    <section class="section">
        <div class="container">
            <h1 class="title">List Orders {#if isLoading}
                (Loading...)
            {/if}</h1>
            <p class="subtitle">List of orders</p>
        </div>
    </section>
    <section class="section">
        <div class="columns">
            <div class="column">
                <table class="table is-bordered">
                    <thead>
                        <tr>
                            <th>order id</th>
                            <th>order date</th>
                            <th>transfusion date</th>
                            <th>blood group</th>
                            <!-- <th>blood id(s)</th> -->
                            <th>recipient</th>
                            <th>status</th>
                            <th>price</th>
                            <th>actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        {#each orders as o}
                            <tr>
                                <td>{o.orderId}</td>
                                <td>{o.orderDate}</td>
                                <td>{o.transfusionDate}</td>
                                <td>{o.bloodGroup}</td>
                                <td>{o.user.fullName}</td>
                                <td>{o.status}</td>
                                <td>{o.price}</td>
                                <td>
                                    <button 
                                        class="button is-primary"
                                        on:click={() => {
                                            markCompleted(o.orderId);
                                        }}
                                        >mark completed</button
                                    >
                                    <button
                                        class="button is-danger"
                                        on:click={() => {
                                            deleteOrder(o.orderId);
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
                        <p class="card-header-title">Create Order</p>
                    </div>
                    <div class="card-content">
                        <div class="field">
                            <label class="label">Recipient</label>
                            <div class="select" placeholder="Recipient">
                                <select bind:value={order.user.userId}>
                                    {#each users as u}
                                        <option value={u.userId}
                                            >{u.fullName}</option
                                        >
                                    {/each}
                                </select>
                            </div>
                        </div>
                        <div class="field">
                            <label class="label">Transfusion Date</label>
                            <input
                                class="input"
                                type="date"
                                placeholder="Transfusion Date"
                                bind:value={order.transfusionDate}
                            />
                        </div>
                        <div class="field">
                            <label class="label">Blood Group</label>
                            <div class="select" placeholder="Order Group">
                                <select bind:value={order.bloodGroup}>
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
                            <label class="label">Price</label>
                            <input
                                class="input"
                                type="number"
                                placeholder="Price (Rs)"
                                bind:value={order.price}
                            />
                        </div>

                        <button class="button is-primary" on:click={createOrder}
                            >Order</button
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
