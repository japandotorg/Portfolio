<template>
    <Terminal />
</template>

<script lang="ts">
    import { Options, Vue } from "vue-class-component";
    import Terminal from "../components/Terminal.vue";

    @Options(
        {
            components: {
                Terminal,
            },
        }
    )

    export default class Home extends Vue {}; 
</script>
