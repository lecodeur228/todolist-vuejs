
<template>
    <div class="layout" >
        <header>

        </header>
        <aside>

        </aside>
        <main> </main>
        <footer></footer>

    </div>
</template>

<style>
.layout {
    display: grid;
    grid-template-columns: 200px 1fr;
}
.layout > * {
    padding: 1rem;
    border: solid 1px red;
}
.layout header , .layout footer {
    grid-column: 1 / -1;

}

</style>