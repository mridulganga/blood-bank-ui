<script>
    import Nav from "../Nav.svelte";
</script>

<main>
    <Nav />
    <section class="section">
        <div class="container">
            <h1 class="title">List Donations</h1>
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
                        <tr>
                            <td>blood-1</td>
                            <td>21/04/2022</td>
                            <td>B+</td>
                            <td>Mridul Ganga</td>
                            <td>1</td>
                            <td>scheduled</td>
                            <td>
                                <button class="button is-primary">mark donated</button>
                                <button class="button is-danger">delete</button>
                            </td>
                        </tr>
                        <tr>
                            <td>blood-2</td>
                            <td>21/04/2022</td>
                            <td>O+</td>
                            <td>User two</td>
                            <td>1</td>
                            <td>donated</td>
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
                        <p class="card-header-title">Create Donation</p>
                    </div>
                    <div class="card-content">
                        <div class="field">
                            <label class="label">Donor</label>
                           <div class="select" placeholder="Donor">
                               <select>
                                 <option>Mridul Ganga</option>
                                 <option>User two</option>
                               </select>
                             </div>
                        </div>
                        <div class="field">
                            <label class="label">Donation Date</label>
                            <input class="input" type="date" placeholder="Donation Date"></div>
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
                            <label class="label">Quantity</label>
                            <input class="input" type="number" placeholder="Quantity"></div>
                       
                        <button class="button is-primary">Create Donation</button>
                        <button class="button is-danger">Clear</button>
                    </div>
                </div>
            </div>
        </div>

    </section>
</main>
