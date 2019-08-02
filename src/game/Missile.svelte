<script context="module">
export const MISSILE_SIZE = 10;
</script>

<script>
export let position;
export let direction;
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