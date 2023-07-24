<template>
    <main class="container">
        <p class="title">TODOLIST application</p>
        <h1 class="about">
            Leave the physical archive behind, use this simple Todolist app online
        </h1>
        <p class="description">
            Manage daily tasks, such as office work, school assignments to activity reminders in one
            comprehensive, secure local storage-based Todolist application.
        </p>
        <div class="cta">
            <a href="mailto:ramadhannkurniawan@gmail.com">Contact Developer</a>
            <span>|</span>
            <a href="https://github.com/muhammadramadhann/simple-todolist" target="_blank"
                >GitHub</a
            >
        </div>
    </main>
</template>

<style lang="scss" scoped>
main {
    display: flex;
    flex-direction: column;
    padding: 16px;
    min-height: 100vh;
    h1,
    p {
        margin-bottom: 8px;
    }
    .title {
        font-weight: bold;
    }
    .about {
        font-weight: bold;
        font-size: 40px;
    }
    .description {
        line-height: 1.8;
        color: #707070;
    }
    .cta {
        margin-top: 16px;
        display: flex;
        flex-wrap: wrap;
        gap: 16px;
        span {
            color: #dedede;
        }
        a {
            color: #42b883;
        }
    }
    @media (max-width: 767px) {
        .about {
            font-size: 32px;
        }
    }
}
</style>
