<script context="module">
export const ENEMY_SIZE = 50;
</script>

<script>
export let position;
</script>

<style>
.enemy {
    position: absolute;
    width: 50px;
    height: 50px;

    background-color: blue; 
    border-radius: 100%;
}
</style>

<div class="enemy" style="bottom: {position.y - 5}px; left: {position.x - 5}px;"></div>
