<script>
import Player from './Player.svelte';
import Missile, {MISSILE_SIZE} from './Missile.svelte';
import Enemy, {ENEMY_SIZE} from './Enemy.svelte';

$: missiles = [];
function handleFire(event) {
    missiles = [...missiles, event.detail];
}

$: enemies = [];
function spawnEnemy() {
    enemies = [...enemies, {
        position: {
            x: Math.random() * window.innerWidth,
            y: window.innerHeight,
        }
    }];
}

function collisions() { enemies.forEach((enemy) => { missiles.forEach((missile) => {
            const c2 = Math.pow(enemy.position.x + ENEMY_SIZE / 2 - (missile.position.x + MISSILE_SIZE / 2), 2) + Math.pow(enemy.position.y + ENEMY_SIZE / 2 - (missile.position.y + MISSILE_SIZE / 2), 2)
            const c3 = Math.pow(ENEMY_SIZE / 2 + MISSILE_SIZE / 2, 2);
            if (c2 <= c3) {
                enemies = enemies.filter((e) => e !== enemy)
                missiles = missiles.filter((m) => m !== missile);
            }
        })
    })
}

let rotation = 0;
let rotate = 0;

function loop() {
    if (Math.floor(Math.random() * 40) === 0) {
       spawnEnemy();
    }

    collisions();

    enemies.forEach(enemy => enemy.position.y -= .75);
    missiles.forEach(missile => {
        missile.position.x += missile.direction.x / 10;
        missile.position.y += missile.direction.y / 10;
    });

    enemies = [...enemies];
    missiles = [...missiles];

    rotation += rotate * 1.25;
    rotation = Math.max(-68, Math.min(68, rotation));

    requestAnimationFrame(loop);
}

function handleMove(event) {
    rotate = event.detail;
}

requestAnimationFrame(loop);
</script>

{#each enemies as {position}}
    <Enemy {position}/>
{/each}

{#each missiles as {position, direction}}
    <Missile {position} {direction}/>
{/each}

<Player {rotation} on:move={handleMove} on:fire={handleFire}/>
