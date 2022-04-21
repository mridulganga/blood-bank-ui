<script>
    import Nav from "../Nav.svelte";
</script>

<main>
    <Nav />
    <section class="section">
        <div class="container">
            <h1 class="title">List Orders</h1>
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
                            <th>blood id(s)</th>
                            <th>recipient</th>
                            <th>quantity</th>
                            <th>status</th>
                            <th>price</th>
                            <th>actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>order-1</td>
                            <td>21/04/2022</td>
                            <td>22/04/2022</td>
                            <td>B+</td>
                            <td>blood-1, blood-2</td>
                            <td>User three</td>
                            <td>1</td>
                            <td>scheduled</td>
                            <td>Rs 150</td>
                            <td>
                                <button class="button is-primary">mark completed</button>
                                <button class="button is-danger">delete</button>
                            </td>
                        </tr>
                        <tr>
                            <td>order-2</td>
                            <td>21/04/2022</td>
                            <td>22/04/2022</td>
                            <td>O+</td>
                            <td>blood-3, blood-4</td>
                            <td>User four</td>
                            <td>2</td>
                            <td>completed</td>
                            <td>Rs 250</td>
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
                        <p class="card-header-title">Create Order</p>
                    </div>
                    <div class="card-content">
                        <div class="field">
                            <label class="label">Recipient</label>
                           <div class="select" placeholder="Recipient">
                               <select>
                                 <option>Mridul Ganga</option>
                                 <option>User two</option>
                               </select>
                             </div>
                        </div>
                        <div class="field">
                            <label class="label">Transfusion Date</label>
                            <input class="input" type="date" placeholder="Transfusion Date"></div>
                        <div class="field">
                            <label class="label">Blood Group</label>
                           <div class="select" placeholder="Blood Group">
                               <select>
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
                            <label class="label">Total Quantity</label>
                            <input class="input" type="number" placeholder="Total Quantity" disabled></div>

                        <div class="field">
                            <label class="label">Select Blood</label>
                           <div class="select is-multiple" placeholder="Blood Group">
                               <select multiple >
                                 <option>Blood-1 (1L)</option>
                                 <option>Blood-2 (2L)</option>
                               </select>
                             </div>
                        </div>
                       
                        <button class="button is-primary">Order</button>
                        <button class="button is-danger">Clear</button>
                    </div>
                </div>
            </div>
        </div>
        
    </section>
</main>
