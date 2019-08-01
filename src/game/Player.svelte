<script>
import { createEventDispatcher } from 'svelte';

const dispatch = createEventDispatcher();
const width = window.innerWidth / 2;

let rotate = 0;
let rotation = 0;

function handleKeyDown(event) {
    switch (event.key) {
        case 'ArrowLeft':
            rotate = -1;
            break;
        case 'ArrowRight':
            rotate = 1;
            break;
    }
}

function handleKeyUp(event) {
    switch (event.key) {
        case 'ArrowLeft':
            if (rotate === -1) {
                rotate = 0;
            }
            break;
        case 'ArrowRight':
            if (rotate === 1) {
                rotate = 0;
            }
            break;
        case ' ':
            fire();
            break;
    }
}

function fire() {
    const position = {
        x: (width + 60 * Math.cos((-1 * rotation + 90) * (Math.PI / 180))),
        y: (-20 + 60 * Math.sin((-1 * rotation + 90) * (Math.PI / 180))),
    };
    dispatch('fire', {
        position, direction: {
            x: position.x - width,
            y: position.y,
        }
    });
}

function loop() {
    rotation += rotate * 1.15;
    rotation = Math.max(-75, Math.min(75, rotation));
    requestAnimationFrame(loop);
}
 
requestAnimationFrame(loop);
</script>

<style>
#cannon {
    position: absolute;
    bottom: -20px;
    left: calc(50% - 10px);
    width: 20px;
    height: 60px;

    background-color: green;
    transform-origin: bottom center;
    border-bottom-left-radius: 50%;
    border-bottom-right-radius: 50%;
}
</style>

<svelte:window on:keyup={handleKeyUp} on:keydown={handleKeyDown}/>

<div id="cannon" style="transform: rotate({rotation}deg);"></div>