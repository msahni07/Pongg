<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Game!</title>
    <style>
        canvas {
            border: 1px solid black;
            display: block;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <h1 id="gameTitle">The Game!</h1>
    <p id="gameInstructions">Click <button onclick="startGame()">here</button> to play the game!</p>
    
    <script>
        function startGame() {
            // Change the title and instructions
            document.getElementById("gameTitle").innerText = "Pong";
            document.getElementById("gameInstructions").innerText = "You're playing Pong! Good luck!";

            // Create canvas element
            var canvas = document.createElement("canvas");
            canvas.width = 800;
            canvas.height = 400;
            document.body.appendChild(canvas);

            // Get canvas context
            var ctx = canvas.getContext("2d");

            // Set starting position and speed
            var x = canvas.width / 2;
            var y = canvas.height - 30;
            var dx = 2;
            var dy = -2;

            // Draw ball function
            function drawBall() {
                ctx.beginPath();
                ctx.arc(x, y, 10, 0, Math.PI * 2);
                ctx.fillStyle = "#0095DD";
                ctx.fill();
                ctx.closePath();
            }

            // Main draw function
            function draw() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                drawBall();

                // Ball movement
                x += dx;
                y += dy;

                // Bounce off walls
                if (x + dx > canvas.width || x + dx < 0) {
                    dx = -dx;
                }
                if (y + dy > canvas.height || y + dy < 0) {
                    dy = -dy;
                }

                // "Glitch" effect
                if (Math.random() < 0.05) {
                    ctx.fillStyle = "#FF0000";
                    ctx.fillRect(0, 0, canvas.width, canvas.height);
                }
            }

            // Game loop
            setInterval(draw, 10);

            // Display "YOU LOSE THE GAME!" after 10 seconds
            setTimeout(function() {
                document.getElementById("gameTitle").innerText = "YOU LOSE THE GAME!";
                document.getElementById("gameInstructions").innerText = "";
            }, 10000);
        }
    </script>
</body>
</html>
