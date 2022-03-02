<html>

<head>
    <title>JavaScript</title>
    <style>
        .hide {
            display: none;
        }

        .car {
            position: absolute;
            bottom: 100px;
            margin: auto;
            width: 50px;
            height: 100px;
            background-color: blue;
        }

        .line {
            position: absolute;
            height: 100px;
            width: 10px;
            margin-left: 48%;
            background-color: white;
        }

        .gameArea {
            background-color: black;
            width: 200px;
            height: 100%;
            overflow: hidden;
            position: relative;
            margin: auto;
                /* background-color: black; */
                /* top: 0;
                left: 0; */
                /* width: 50vh;
                height: 100vh;  */
                /* overflow: hidden; */
                /* position: relative;
                margin: auto; */
        }
    </style>
</head>

<body>
    <div class="score"></div>
    <div class="game">
        <div class="startScreen">Welcome message</div>
        <div class="gameArea hide"></div>
    </div>
    <script>
        const score = document.querySelector(".score");
        const startScreen = document.querySelector(".startScreen");
        const gameArea = document.querySelector(".gameArea");
        let player = {
            speed: 5
        };
        let keys = {
            ArrowUp: false
            , ArrowDown: false
            , ArrowRight: false
            , ArrowLeft: false
        };
        startScreen.addEventListener("click", start);
        document.addEventListener("keydown", pressOn);
        document.addEventListener("keyup", pressOff);

        function playGame() {
            let car = document.querySelector(".car");
            let road = gameArea.getBoundingClientRect();
            if (player.start) {
                if (keys.ArrowUp && player.y > road.top) {
                    player.y -= player.speed;
                }
                if (keys.ArrowDown && player.y < road.bottom) {
                    player.y += player.speed;
                }
                if (keys.ArrowLeft && player.x > 0) {
                    player.x -= player.speed;
                }
                if (keys.ArrowRight && player.x < (road.width - 50)) {
                    player.x += player.speed;
                }
                car.style.left = player.x + 'px';
                car.style.top = player.y + 'px';
                window.requestAnimationFrame(playGame);
            }
        }

        function pressOn(e) {
            e.preventDefault();
            keys[e.key] = true;
            console.log(keys);
        }

        function pressOff(e) {
            e.preventDefault();
            keys[e.key] = false;
            console.log(keys);
        }

        function start() {
            startScreen.classList.add("hide");
            gameArea.classList.remove("hide");
            player.start = true;
            for (let x = 0; x < 5; x++) {
                let div = document.createElement("div");
                div.classList.add("line");
                div.style.top = (x * 150) + "px";
                gameArea.appendChild(div);
            }
            window.requestAnimationFrame(playGame);
            let car = document.createElement("div");
            car.innerText = "Car";
            car.setAttribute("class", "car");
            gameArea.appendChild(car);
            player.x = car.offsetLeft;
            player.y = car.offsetTop;
            console.log(player);
        }
    </script>
</body>

</html> 
