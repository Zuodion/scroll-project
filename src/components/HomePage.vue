<template>
<div>
    <div class="white-block">
        <div class="progress-bar">
            <div class="progress-bar length" :style="{width: calculateWidth + '%'}" />
        </div>
    </div>
    <p style="position: absolute; margin-top: 5px;">{{ text }}</p>
    <div v-if="calculateWidth > 25">
        <button @click="upButton()" class="topbutton">^</button>
    </div>
</div>
</template>

<script>
import {
    someText
} from "../text.js";
export default {
    name: "HomePage",
    data() {
        return {
            text: someText.someString,
            calculateWidth: 0
        };
    },
    methods: {
        handleScroll() {
            this.calculateWidth = ((document.documentElement.scrollTop * 100) / (document.documentElement.scrollHeight - (window.innerHeight)))
        },
        upButton() {
            document.documentElement.scrollTop = 0;
        }
    },
    created() {
        window.addEventListener("scroll", this.handleScroll);
    },
    destroyed() {
        window.removeEventListener("scroll", this.handleScroll);
    }
};
</script>

<style>
p {
    font-family: 'Andele Mono', Monospace, serif;
    font-weight: 500;
    color: black;
    font-size: 20px;
    margin: 30%;
    text-align: justify;
}

.white-block {
    position: fixed;
    top: -0.2%;
    z-index: 1;
    width: 100%;
    min-height: 15px;
    background-color: white;
}

.progress-bar {
    border: 1px solid #333;
    z-index: 2;
    position: inherit;
    top: -0.2%;
    width: 100%;
    height: 5px;
    background-color: #eee;
    transition: width 500ms;
}

.length {
    top: -0.2%;
    z-index: 0;
    background-color: grey;
    background: -webkit-linear-gradient(left, red 0%, green 50%, blue 100%);
}

.topbutton {
    width: 50px;
    border: 2px solid #ccc;
    background: #f7f7f7;
    text-align: center;
    padding: 10px;
    position: fixed;
    bottom: 50px;
    right: 50px;
    cursor: pointer;
    color: #333;
    font-family: verdana;
    font-size: 12px;
    border-radius: 5px;
    -moz-border-radius: 5px;
    -webkit-border-radius: 5px;
    -khtml-border-radius: 5px;
}
</style>
