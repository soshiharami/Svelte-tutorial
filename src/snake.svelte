<div>
    <canvas id="gc" width="4000" height="4000"></canvas>
</div>

<script>
    let canv;
    let ctx;
    let games;

    window.onload = function(){
        canv = document.getElementById("gc");
        ctx = canv.getContext("2d");
        document.addEventListener("keydown", keyPush);
        games = setInterval(game, 1000 / 15);
    }

    let px = 10, py = 10;
    let gs = 20, tc = 20;
    let ax = 15, ay = 15;
    let xv = 0, yv = 0;
    let trail = [];
    let tail = 5;

    function game() {
        px += xv;
        py += yv;
        /*if (px < 0) {
            px = 10;
            py = 10;
            tail = 5;
        }
        if (px > tc - 1) {
            px = 10;
            py = 10;
            tail = 5;
        }
        if (py < 0) {
            px = 10;
            py = 10;
            tail = 5;
        }
        if (py > tc - 1) {
            px = 10;
            py = 10;
            tail = 5;
        }*/
        ctx.fillStyle = "black";
        ctx.fillRect(0, 0, canv.width, canv.height);

        ctx.fillStyle = "lime";
        for (let i = 0; i < trail.length; i++) {
            ctx.fillRect(trail[i].x * gs, trail[i].y * gs, gs - 2, gs - 2);
            if (trail[i].x === px && trail[i].y === py) {
                tail = 5;
                px = 10;
                py = 10;
            }
        }
        trail.push({x: px, y: py});
        while (trail.length > tail) {
            trail.shift();
        }

        if (ax === px && ay === py) {
            tail++;
            ax = Math.floor(Math.random() * tc);
            ay = Math.floor(Math.random() * tc);
        }
        ctx.fillStyle = "red";
        ctx.fillRect(ax * gs, ay * gs, gs - 2, gs - 2);
    }

    function keyPush(evt) {
        switch (evt.keyCode) {
            case 37:
                xv = -1;
                yv = 0;
                break;
            case 38:
                xv = 0;
                yv = -1;
                break;
            case 39:
                xv = 1;
                yv = 0;
                break;
            case 40:
                xv = 0;
                yv = 1;
                break;
        }
    }
</script>

<style>

</style>
