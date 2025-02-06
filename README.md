<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Valentine's Day Proposal</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #ffe6e6;
            margin: 0;
            text-align: center;
            overflow: hidden;
        }

        .container {
            border: 2px solid #ff4d4d;
            padding: 20px;
            border-radius: 10px;
            background-color: white;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
        }

        h1 {
            color: #ff4d4d;
            font-size: 2.5rem;
            margin-bottom: 20px;
        }

        img {
            width: 300px;
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .buttons {
            display: flex;
            justify-content: space-around;
        }

        button {
            background-color: #ff4d4d;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 15px 30px;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        button:hover {
            background-color: #ff1a1a;
        }

        #yes-button {
            transform: scale(1);
        }

        #no-button {
            transform: scale(1);
        }

        #yes-button.clicked {
            transform: scale(1.2);
        }

        #no-button.clicked {
            transform: scale(0.8);
        }

        .message {
            display: none;
            margin-top: 20px;
            font-size: 1.5rem;
            color: #ff4d4d;
        }

        /* Fireworks and flowers animations */
        .fireworks {
            position: absolute;
            top: 10%;
            left: 50%;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1000;
            display: none;
        }

        .firework {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #ff4d4d;
            border-radius: 50%;
            opacity: 0;
            animation: firework 1.5s ease-in-out infinite;
        }

        @keyframes firework {
            0% {
                transform: scale(1);
                opacity: 0;
            }
            50% {
                transform: scale(4);
                opacity: 1;
            }
            100% {
                transform: scale(0);
                opacity: 0;
            }
        }

        /* Flower effect */
        .flower {
            position: absolute;
            width: 30px;
            height: 30px;
            background-image: url('https://www.pngitem.com/pimgs/m/148-1489397_transparent-background-png-flower-png-download-flower-png.png');
            background-size: cover;
            animation: flowerAnimation 2s infinite ease-in-out;
            opacity: 0;
        }

        @keyframes flowerAnimation {
            0% {
                transform: scale(0) translate(0, 0);
                opacity: 1;
            }
            50% {
                transform: scale(1.5) translate(50px, 50px);
                opacity: 1;
            }
            100% {
                transform: scale(0) translate(100px, 100px);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Will you be my Valentine?</h1>
        <img src="https://i.pinimg.com/originals/f5/80/c8/f580c8489373a47f49f83984e053ca57.jpg" alt="Funny Cat Meme">
        <div class="buttons">
            <button id="yes-button">Yes</button>
            <button id="no-button">No</button>
        </div>
        <div id="message" class="message">
            Be ready Feb 14th love ❤️
        </div>
    </div>

    <!-- Audio soundtrack for "Love You" -->
    <audio id="audio" src="https://www.soundjay.com/button/beep-07.wav" preload="auto"></audio>

    <div id="fireworks" class="fireworks"></div>

    <script>
        const yesButton = document.getElementById("yes-button");
        const noButton = document.getElementById("no-button");
        const message = document.getElementById("message");
        const audio = document.getElementById("audio");
        const fireworksContainer = document.getElementById("fireworks");

        let noClickCount = 0; // To track how many times "No" has been clicked

        yesButton.addEventListener("click", function () {
            yesButton.classList.add("clicked");
            message.style.display = "block";
            setTimeout(function () {
                message.innerHTML = "Be ready Feb 14th love ❤️";
            }, 500);

            // Play audio sound "Love you"
            audio.play();

            // Display fireworks and flowers effect
            fireworksContainer.style.display = "block";
            createFireworks();
            createFlowers();
        });

        noButton.addEventListener("click", function () {
            noClickCount++;
            
            if (noClickCount === 1) {
                noButton.textContent = "No, Are you sure pookie?";
                noButton.classList.add("clicked");
            } else if (noClickCount === 2) {
                noButton.style.transform = "scale(0.6)"; // Get even smaller
            } else if (noClickCount === 3) {
                noButton.style.transform = "scale(0.4)"; // Get even smaller
            }
            
            // Increase "Yes" size every time "No" is clicked
            yesButton.classList.add("clicked");
        });

        // Mouse tracking to move the "No" button away
        document.addEventListener("mousemove", function(event) {
            const noButtonRect = noButton.getBoundingClientRect();
            const mouseX = event.clientX;
            const mouseY = event.clientY;

            const buffer = 100; // Distance threshold from the mouse to start moving

            if (mouseX > noButtonRect.left - buffer && mouseX < noButtonRect.right + buffer &&
                mouseY > noButtonRect.top - buffer && mouseY < noButtonRect.bottom + buffer) {
                // Move the "No" button away from the mouse
                const randomX = Math.random() * (window.innerWidth - noButton.offsetWidth);
                const randomY = Math.random() * (window.innerHeight - noButton.offsetHeight);
                noButton.style.left = randomX + "px";
                noButton.style.top = randomY + "px";
            }
        });

        // Fireworks animation
        function createFireworks() {
            for (let i = 0; i < 10; i++) {
                let firework = document.createElement("div");
                firework.classList.add("firework");
                firework.style.top = Math.random() * 100 + "%";
                firework.style.left = Math.random() * 100 + "%";
                fireworksContainer.appendChild(firework);
                setTimeout(() => firework.remove(), 1500);
            }
        }

        // Flower animation
        function createFlowers() {
            for (let i = 0; i < 10; i++) {
                let flower = document.createElement("div");
                flower.classList.add("flower");
                flower.style.top = Math.random() * 100 + "%";
                flower.style.left = Math.random() * 100 + "%";
                document.body.appendChild(flower);
                setTimeout(() => flower.remove(), 2000);
            }
        }
    </script>
</body>
</html>
