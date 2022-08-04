<script setup lang="ts">

enum State {
  STARTING,
  WAITING,
  FINISHED,
  LENGTH,  // number of states
}

enum Color {
  BLUE = "rgb(52, 137, 205)",
  RED = "rgb(206, 38, 56)",
  GREEN = "rgb(65, 218, 115)",
}

enum Message {
  STARTING = "Click to start",
  WAITING = "Wait for green",
  TOOFAST = "You clicked too fast",
  FINISHED = "Reaction time: ",
}

let start: number = Date.now();
let waitTime: number = randomNumber(1000, 3000);
let state: number = State.FINISHED;
let test: HTMLElement = document.createElement('test');
let message: HTMLElement = document.createElement('message');
const app: HTMLElement | null = document.getElementById("app");
let reactionTime: number = 0;
let delay_cnt: number= 0;



function randomNumber(min: number, max: number) {
    return Math.floor(Math.random() * (max - min + 1) + min)
}

async function delay(ms: number, this_cnt: number) {
    await new Promise( resolve => setTimeout(resolve, ms) );
    if (state == State.WAITING && this_cnt == delay_cnt) {
        test.style.backgroundColor = Color.GREEN;
    }
}

function update() {
    state = (state + 1) % State.LENGTH;
    if (state == State.STARTING) {
        test.style.backgroundColor = Color.BLUE;
        message.innerText = Message.STARTING;
    } else if (state == State.WAITING) {
        test.style.backgroundColor = Color.RED;
        message.innerText = Message.WAITING;
        waitTime = randomNumber(1000, 3000);
        start = Date.now();
        delay(waitTime, delay_cnt);
    } else if (state == State.FINISHED) {
        reactionTime = Date.now() - start - waitTime;
        test.style.backgroundColor = Color.BLUE;
        if (reactionTime < 0) {
            message.innerText = Message.TOOFAST;
            delay_cnt++;
        } else {
            message.innerText = Message.FINISHED + reactionTime + "ms";
        }
    } else {
        console.log("Invalid State");
    }
}

test.addEventListener('mousedown', update);
if (app) {
    app.appendChild(test);
}
test.appendChild(message);
update();

</script>

<template />

<style />