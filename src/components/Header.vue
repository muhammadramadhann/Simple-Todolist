<script setup></script>

<template>
    <header>
        <nav class="container">
            <div class="branding">Nice<span>Todos</span></div>
            <ul class="nav-routes">
                <li>
                    <router-link to="/">Home</router-link>
                </li>
                <li>
                    <router-link to="/about">About</router-link>
                </li>
            </ul>
        </nav>
    </header>
</template>

<style lang="scss" scoped>
nav {
    // background-color: #1a1a1a;
    // color: white;
    display: flex;
    align-items: center;
    padding: 24px 16px;
    .branding {
        font-size: 28px;
        font-weight: bold;
        color: #42b883;
        span {
            color: #35495e;
        }
    }
    .nav-routes {
        display: flex;
        flex: 1;
        justify-content: end;
        gap: 16px;
        list-style: none;
        a {
            text-decoration: none;
            transition: 300ms ease-in-out;
            color: inherit;
            &:hover,
            &.router-link-active {
                color: #42b883;
            }
        }
    }
}
</style>
