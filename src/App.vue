<template>
    <div id="app">
        <router-view />
    </div>
</template>

<style>
    @font-face {
        font-family: "Comic Sans MS";
        src: url("./fonts/comic-sans.ttf");
    }

    #app {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 101.5%;
        padding: 2px;
    }
 
    * {
        font-family: "Comic Sans MS";
        margin: 0;
        padding: 0;
        border: 0;
    }

    html,
    body {
        height: 99%;
        width: 99%;
    }
</style>
