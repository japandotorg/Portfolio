<template>
    <div class="terminal">
        <div class="icon-btn close"></div>
        <div class="icon-btn min"></div>
        <div class="icon-btn max"></div>
        <header>root@japandotorg: <span class="color-cold">~</span></header>

        <p class="margin-left">
            Type <span class="color-hot">help</span> for a list of supported commands.
        </p>

        <div class="terminal-text">
            <aside class="margin-left">
                <br />
                <span>
                    <font-awesome-icon class="color-cold" icon="arrow-right-long" />
                    <span class="color-hot"> ~ </span>
                </span>

                <span v-for="item in output" :key="item" class="test">
                    {{ item.input }}
                    <div class="output" v-html="item.response"></div>
                    <font-awesome-icon class="color-cold" icon="arrow-right-long" />
                    <span class="color-hot"> ~ </span>
                </span>

                <span class="user-input">
                    <input type="text" v-model="message" ref="commandInput" @keypress="changeSize"
                        @keydown.delete="changeSize" @blur="autoFocus" :style="`width: ${inputSize}px;`" autofocus />
                </span>
            </aside>
        </div>
    </div>
</template>
  
<script lang="ts">
    import { Vue } from "vue-class-component";
    
    export default class Terminal extends Vue {
        inputSize: number = 1;
        message: string = "";
        output: any = [];
    
        changeSize(event) {
            if (event.keyCode == 8) {
                if (this.message.length > 0) {
                    this.inputSize -= 8.5;
                }
            } else if (event.keyCode == 13) {
                this.handleCommand();
            } else {
                this.inputSize += 8.5;
            }
            return this.inputSize;
        }
    
        private reset(): void {
            this.message = "";
            this.inputSize = 1;
        }
    
        handleCommand() {
            switch (this.message.toLowerCase()) {
                case "help": {
                    this.output.push({
                        input: this.message,
                        response:
                            'Available Commands: ["<span class="color-hot">About</span>", "<span class="color-hot">Links</span>", <span class="color-hot">"Skills"</span>]',
                    });
                    break;
                }
                case "about": {
                    this.output.push({
                        input: this.message,
                        response:
                            "Hello, I'm Lemon and I'm a full stack developer!",
                    });
                    break;
                }
                case "github": {
                    this.output.push({
                        input: this.message,
                        response:
                            "<a class='color-hot' href='https://github.com/japandotorg'>Github</a>",
                    });
                    break;
                }
                case "skills": {
                    this.output.push({
                        input: this.message,
                        response: `<div><span class='color-hot'>Languages:</span> Python, Rust, Go, JavaScript, TypeScript, Ruby, SQL, Swift, Redis, Kotlin</div> <div><span class='color-hot'>Frameworks:</span> Django, Flask, FastAPI, Angular, React, VueJS, NextJS</div><div><span class='color-hot'>Technologies:</span> Git, GraphQL, Rest, OCR</div>`,
                    });
                    break;
                }
                default: {
                    this.output.push({
                        input: this.message,
                        response: "This command does not exist.",
                    });
                    break;
                }
            }
            this.reset();
        }
    
        autoFocus() {
            window.setTimeout(() => {
                (this.$refs.commandInput as any).focus();
            }, 0);
        }
    }
</script>
  
<style lang="scss">
    $letter-color: rgb(229, 231, 237);
    $main-color: rgb(33, 34, 36);
    
    div {
        height: 100%;
        width: 100%;
    
        .terminal {
            font-size: 0.95em;
            border-radius: 10px;
            box-shadow: 1px 1px 10px 1px rgba(33, 34, 36, 0.5);
            max-width: 1044px;
            min-width: 400px;
            max-height: 400px;
            background-color: $main-color;
            color: $letter-color;
        }
    
        .terminal-text {
            overflow: auto;
            max-height: 325px;
            margin-top: 5px;
        }
    
        >header {
            height: 10%;
            line-height: 2.4rem;
            text-align: center;
            font-size: 0.85em;
        }
    }
    
    aside {
        margin-top: -15px;
        font-size: 0.9em;
    
        .user-input {
            &:after {
                position: relative;
                display: inline-block;
                content: "";
                background-color: rgb(159, 162, 171);
                height: 20px;
                width: 2px;
                top: 4px;
                animation: blink 1s step-start 0s infinite;
            }
    
            @keyframes blink {
                50% {
                    opacity: 0;
                }
            }
        }
    
        .test {
            &:before {
                position: relative;
                display: inline-block;
                content: "";
                height: 20px;
                width: 0px;
            }
        }
    }
    
    .margin-left {
        margin-left: 1.05rem;
    }
    
    .footer {
        position: fixed;
        color: $main-color;
        bottom: 2em;
    }
    
    .output {
        margin-top: 0.2rem;
        margin-bottom: -0.2rem;
    }
    
    .icon-btn {
        position: absolute;
        border-radius: 50%;
        height: 10px;
        width: 10px;
        margin-top: 0.8em;
    }
    
    .close {
        background-color: #f96256;
        border: 1px solid #f65549;
        margin-left: 1.2em;
    }
    
    .min {
        background-color: #fdbc3d;
        border: 1px solid #ffb524;
        margin-left: 2.5em;
    }
    
    .max {
        background-color: #33c948;
        border: 1px solid #2dbb41;
        margin-left: 3.8em;
    }
    
    .color-hot {
        color: rgb(47, 255, 158);
    }
    
    .color-cold {
        color: rgb(150, 236, 255);
    }
    
    a {
        text-decoration: none;
    }
    
    input {
        background-color: inherit;
        outline: none;
        caret-color: transparent;
    
        color: $letter-color;
        font-size: 1em;
    }
</style>
