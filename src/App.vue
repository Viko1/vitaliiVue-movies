<template>
    <header>
        <router-link to="/">
            <h1>
        <span>VitaliiVue</span>Movies</h1>
        </router-link>
    </header>
    <main>

    </main>
    <router-view/>
</template>

<style lang="scss">
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: 'Copperplate', sans-serif;

        &::selection {
            background: transparentize(#7482FF, 0.5);
        }
    }

    body {
        background-color: #284357;
    }

    a {
        text-decoration: none;
    }

    header {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px 16px;
        background-color: #25364a;
        box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);

        h1 {
            color: white;
            font-size: 28px;

            span {
                color: aqua;
            }
        }

    }

</style>
