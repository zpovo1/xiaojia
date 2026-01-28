<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>宝宝我们和好吧</title>
<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
        background-color: #ffe6e6;
        font-family: "Microsoft YaHei", sans-serif;
    }
    .container {
        text-align: center;
        padding: 30px;
        border-radius: 15px;
        background: white;
        box-shadow: 0 0 20px rgba(0,0,0,0.1);
    }
    .heart-icon {
        width: 80px;
        height: 80px;
        margin-bottom: 20px;
        transition: all 0.3s ease;
    }
    .button-group {
        display: flex;
        gap: 20px;
        justify-content: center;
    }
    .button {
        padding: 12px 30px;
        border: none;
        border-radius: 25px;
        cursor: pointer;
        font-size: 16px;
        transition: all 0.3s ease;
    }
    .accept-btn {
        background: #ff4d4d;
        color: white;
    }
    .reject-btn {
        background: #666;
        color: white;
        position: relative;
    }
    /* 文字颜色变化 */
    .text-red {
        color: #ff4d4d !important;
    }
</style>
</head>
<body>
<div class="container">
    <img src="src/1.png" alt="爱心" class="heart-icon">
    <!---->
    <h2>我们和好吧，好吗？</h2>
    <div class="button-group">
        <button class="button accept-btn" onclick="handleResponse(true)">❤️和好❤️</button>
        <button class="button reject-btn" onclick="handleResponse(false)">不要</button>
    </div>
</div>
 
<script>
    let rejectCount = 0;
    let acceptScale = 1;
    const messages = [
        "不要",
        "真的不要",
        "再考虑一下",
        "求求你啦",
        "最后一次机会",
        "你就那么不想和我和好吗"
    ];
    
    const imageSources = [
        'src/1.png',
        'src/2.png',
        'src/3.png',
        'src/4.png',
        'src/5.png',
        'src/6.png'
    ];
 
    function handleResponse(isAccept) {
        const heartIcon = document.querySelector('.heart-icon');
        const rejectBtn = document.querySelector('.reject-btn');
        const acceptBtn = document.querySelector('.accept-btn');
 
        if (!isAccept) {
            rejectCount = Math.min(rejectCount + 1, 5);
 
            // 更新按钮文字
            rejectBtn.textContent = messages[Math.min(rejectCount, 4)];
 
            // 更新图片（限制在前5张）
            const imgIndex = Math.min(rejectCount, imageSources.length - 2); // 最大索引为4
            heartIcon.src = imageSources[imgIndex];
 
            // 和好按钮持续放大
            acceptScale *= 1.2;
            acceptBtn.style.transform = `scale(${acceptScale})`;
 
            // 文字颜色变化
            rejectBtn.classList.add('text-red');
            setTimeout(() => {
                rejectBtn.classList.remove('text-red');
            }, 1000);
 
            // 第五次点击处理
            if (rejectCount === 5) {
                setTimeout(() => {
                    rejectBtn.textContent = messages[5];
                    alert('你就那么不想和我和好吗');
                    // 重置状态
                    rejectCount = 0;
                    acceptScale = 1;
                    acceptBtn.style.transform = 'scale(1)';
                    heartIcon.src = imageSources[0];
                }, 1000);
            }
        } else {
            // 接受后的效果
            heartIcon.src = imageSources[5];
            // 放大图片
            heartIcon.style.transform = 'scale(1.8)';
            document.body.style.backgroundColor = '#ffcccc';
            setTimeout(() => {
                alert('太好了！我们永远在一起吧！💖');
                // 重置状态
                acceptScale = 1;
                acceptBtn.style.transform = 'scale(1)';
                heartIcon.src = imageSources[0];
            }, 500);
        }
    }
</script>
</body>
</html>