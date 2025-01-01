<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>元旦快乐烟花动画</title>
<style>
  body, html {
    margin: 0;
    padding: 0;
    height: 100%;
    overflow: hidden;
    background: #000;
  }
  .fireworks {
    position: absolute;
    bottom: -100px;
    width: 100%;
  }
  .firework {
    position: absolute;
    bottom: 100%;
    width: 3px;
    height: 3px;
    background: #fff;
    border-radius: 50%;
    opacity: 0.8;
    /* 随机位置和动画 */
    left: calc((var(--i) - 1) * (100% / 10));
    animation: firework var(--d) var(--t) linear infinite;
  }
  @keyframes firework {
    0% {
      transform: translateY(0);
      opacity: 0.8;
    }
    100% {
      transform: translateY(-500px);
      opacity: 0;
    }
  }
</style>
</head>
<body>

<div class="fireworks">
  <!-- 生成10个烟花 -->
  <div class="firework" style="--i:1; --d:200; --t:0.5s;"></div>
  <div class="firework" style="--i:2; --d:300; --t:0.8s;"></div>
  <div class="firework" style="--i:3; --d:150; --t:1.2s;"></div>
  <div class="firework" style="--i:4; --d:250; --t:0.7s;"></div>
  <div class="firework" style="--i:5; --d:350; --t:1.0s;"></div>
  <div class="firework" style="--i:6; --d:180; --t:1.5s;"></div>
  <div class="firework" style="--i:7; --d:220; --t:0.9s;"></div>
  <div class="firework" style="--i:8; --d:280; --t:1.1s;"></div>
  <div class="firework" style="--i:9; --d:130; --t:1.3s;"></div>
  <div class="firework" style="--i:10; --d:310; --t:0.6s;"></div>
</div>

<div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); color: #fff; font-size: 24px; font-family: 'Arial', sans-serif;">
  元旦快乐！
</div>

</body>
</html>

