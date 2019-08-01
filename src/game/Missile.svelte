<script>
export let position;
export let direction;

function loop() {
    position.x += direction.x / 10;
    position.y += direction.y / 10;
    requestAnimationFrame(loop);
}

requestAnimationFrame(loop);
</script>

<style>
.missile {
    position: absolute;
    width: 10px;
    height: 10px;

    background-color: red;
    border-radius: 50%;
}
</style>

<div class="missile" style="bottom: {position.y - 5}px; left: {position.x - 5}px;"></div>