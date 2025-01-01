<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>元旦快乐与烟花动画</title>
    <style>
        /* 设置页面背景和字体 */
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

        /* 设置文字的样式 */
        .happy-new-year {
            font-size: 50px;
            color: #ff4500;
            text-align: center;
            font-weight: bold;
            animation: glow 2s infinite alternate, slide 5s ease-in-out infinite;
            z-index: 10;
        }

        /* 闪烁效果的动画 */
        @keyframes glow {
            0% {
                text-shadow: 0 0 5px #ff4500, 0 0 10px #ff4500, 0 0 15px #ff4500, 0 0 20px #ff4500;
            }
            100% {
                text-shadow: 0 0 20px #ff4500, 0 0 30px #ff4500, 0 0 40px #ff4500, 0 0 50px #ff4500;
            }
        }

        /* 滚动效果的动画 */
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
        // 获取Canvas元素和其上下文
        const canvas = document.getElementById('fireworks');
        const ctx = canvas.getContext('2d');

        // 设置Canvas的宽高
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        // 烟花粒子的类
        class Firework {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                this.size = Math.random() * 3 + 2;
                this.speedX = Math.random() * 4 - 2; // 水平速度
                this.speedY = Math.random() * -4 - 4; // 垂直速度
                this.life = 100; // 粒子的生命值
                this.color = 'hsl(' + Math.random() * 360 + ', 100%, 50%)'; // 随机颜色
            }

            // 更新粒子的位置
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                this.life--;
            }

            // 绘制粒子
            draw() {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fillStyle = this.color;
                ctx.fill();
            }

            // 检查粒子是否已经死亡
            isDead() {
                return this.life <= 0;
            }
        }

        // 烟花数组
        let fireworks = [];

        // 生成烟花爆炸效果
        function createFirework(x, y) {
            for (let i = 0; i < 100; i++) {
                fireworks.push(new Firework(x, y));
            }
        }

        // 绘制烟花效果
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height); // 清除之前的画面

            // 更新并绘制所有的烟花粒子
            for (let i = 0; i < fireworks.length; i++) {
                const firework = fireworks[i];
                firework.update();
                firework.draw();
                
                // 删除已经死掉的粒子
                if (firework.isDead()) {
                    fireworks.splice(i, 1);
                    i--;
                }
            }

            requestAnimationFrame(animate); // 继续调用动画
        }

        // 鼠标点击时触发烟花爆炸
        canvas.addEventListener('click', (event) => {
            createFirework(event.clientX, event.clientY);
        });

        // 启动动画
        animate();
    </script>
</body>
</html>
