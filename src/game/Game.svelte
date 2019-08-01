<script>
import Player from './Player.svelte';
import Missile from './Missile.svelte';

let missiles = [];
function handleFire(event) {
    missiles = [...missiles, event.detail];
}
</script>

{#each missiles as {position, direction}}
    <Missile {position} {direction}/>
{/each}

<Player on:fire={handleFire}/>