<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>元旦快乐与烟花动画</title>
    <style>
        body {
            background-color: #f1f1f1;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: 'Arial', sans-serif;
            overflow: hidden;
            position: relative;
        }
        .happy-new-year {
            font-size: 50px;
            color: #ff4500;
            text-align: center;
            font-weight: bold;
            animation: glow 2s infinite alternate, slide 5s ease-in-out infinite;
            z-index: 10;
        }
        @keyframes glow {
            0% {
                text-shadow: 0 0 5px #ff4500, 0 0 10px #ff4500, 0 0 15px #ff4500, 0 0 20px #ff4500;
            }
            100% {
                text-shadow: 0 0 20px #ff4500, 0 0 30px #ff4500, 0 0 40px #ff4500, 0 0 50px #ff4500;
            }
        }
        @keyframes slide {
            0% {
                transform: translateX(-100%);
            }
            100% {
                transform: translateX(100%);
            }
        }
    </style>
</head>
<body>
    <div class="happy-new-year">元旦快乐！</div>
    <canvas id="fireworks"></canvas>
    <script>
        const canvas = document.getElementById('fireworks');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        class Firework {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                this.size = Math.random() * 3 + 2;
                this.speedX = Math.random() * 4 - 2; 
                this.speedY = Math.random() * -4 - 4; 
                this.life = 100; 
                this.color = 'hsl(' + Math.random() * 360 + ', 100%, 50%)'; 
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                this.life--;
            }
            draw() {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fillStyle = this.color;
                ctx.fill();
            }
            isDead() {
                return this.life <= 0;
            }
        }
        let fireworks = [];
        function createFirework(x, y) {
            for (let i = 0; i < 100; i++) {
                fireworks.push(new Firework(x, y));
            }
        }
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            for (let i = 0; i < fireworks.length; i++) {
                const firework = fireworks[i];
                firework.update();
                firework.draw();
                if (firework.isDead()) {
                    fireworks.splice(i, 1);
                    i--;
                }
            }
            requestAnimationFrame(animate);
        }
        canvas.addEventListener('click', (event) => {
            createFirework(event.clientX, event.clientY);
        });
        animate();
    </script>
</body>
</html>
