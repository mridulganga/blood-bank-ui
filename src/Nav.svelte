<script>
    import { router } from "tinro";

    let toggleMobileMenu = false;

    function logout() {
        localStorage.clear();
        router.goto("/login");
    }

    function toggleMenu() {
            toggleMobileMenu = !toggleMobileMenu;
    }
</script>

<nav class="navbar" aria-label="main navigation">
    <div class="navbar-brand">
        <a class="navbar-item" href="/listusers">
            <b>BLOOD BANK</b>
        </a>

        <a
            role="button"
            class="navbar-burger"
            class:is-active={toggleMobileMenu}
            aria-label="menu"
            aria-expanded="false"
            data-target="mainNav"
            on:click={toggleMenu}
        >
            <span aria-hidden="true" />
            <span aria-hidden="true" />
            <span aria-hidden="true" />
        </a>
    </div>

    <div id="mainNav" class="navbar-menu" class:is-active={toggleMobileMenu}>
        <div class="navbar-start">
            <a class="navbar-item" href="/listusers"> Users </a>

            <a class="navbar-item" href="/listorders"> Orders </a>

            <a class="navbar-item" href="/listdonations"> Donations </a>
        </div>

        <div class="navbar-end">
            <a class="navbar-item">
                {localStorage.getItem("user")}
            </a>
            <div class="navbar-item">

                <div class="buttons">
                    <button class="button is-danger" on:click={logout}>
                        Logout
                    </button>
                </div>
            </div>
        </div>
    </div>
</nav>
