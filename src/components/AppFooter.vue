<template>
    <footer>
        <div class="container">
            <div class="logotype_information">
                <img class="logotype_footer" src="../assets/logo/logo.svg" alt="alpha_logo">
                <p class="logotype_copyright">© alpha, 2023</p>
            </div>
        </div>
    </footer>
</template>

<style scoped>
    footer {
        width: 100%;
        height: 74px;
        padding: 64px 0px;
    }

    .logotype_information {
        width: 114px;
        height: fit-content;
        display: grid;
        row-gap: 16px;
    }

    .logotype_footer {
        width: 114px;
        height: 36px;
    }

    .logotype_copyright {
        font-size: 16px;
        font-style: normal;
        font-weight: 400;
        line-height: 140%; 
        margin: 0;
        color: #81899D;
    }
</style>