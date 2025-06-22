<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>极简倒计时</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            primary: '#FFFFFF', // 白色背景
            secondary: '#121212', // 黑色文本
            accent: '#333333', // 次要文本
          },
          fontFamily: {
            inter: ['Inter', 'sans-serif']
          }
        }
      }
    }
  </script>
  <style type="text/tailwindcss">
    @layer utilities {
      .content-auto {
        content-visibility: auto;
      }
      .time-separator {
        font-weight: 300;
        opacity: 0.7;
      }
    }
  </style>
</head>
<body class="bg-primary text-secondary min-h-screen flex items-center justify-center p-4 font-inter">
  <div class="max-w-md w-full mx-auto">
    <div class="text-center">
      <!-- 标题 -->
      <h1 class="text-xl font-medium text-accent mb-6">地生中考倒计时</h1>
      
      <!-- 时间显示 -->
      <div class="flex justify-center items-center">
        <div id="hours" class="text-[clamp(3rem,15vw,6rem)] font-black tracking-tight">00</div>
        <div class="time-separator text-[clamp(2rem,8vw,4rem)]">:</div>
        <div id="minutes" class="text-[clamp(3rem,15vw,6rem)] font-black tracking-tight">00</div>
        <div class="time-separator text-[clamp(2rem,8vw,4rem)]">:</div>
        <div id="seconds" class="text-[clamp(3rem,15vw,6rem)] font-black tracking-tight">00</div>
      </div>
      
      <!-- 日期显示 -->
      <div class="mt-8">
        <p class="text-sm text-accent/80" id="target-date">2025年6月30日 14:00</p>
      </div>
    </div>
  </div>

  <script>
    // 设置目标时间
    const targetTime = new Date('2025-06-30T14:00:00');
    
    // 获取DOM元素
    const hoursElement = document.getElementById('hours');
    const minutesElement = document.getElementById('minutes');
    const secondsElement = document.getElementById('seconds');
    const targetDateElement = document.getElementById('target-date');
    
    // 更新目标日期显示
    targetDateElement.textContent = targetTime.toLocaleString();
    
    function updateCountdown() {
      const now = new Date();
      const diffMs = targetTime - now;
      
      // 检查是否已过考试时间
      if (diffMs <= 0) {
        hoursElement.textContent = '00';
        minutesElement.textContent = '00';
        secondsElement.textContent = '00';
        return;
      }
      
      // 计算剩余时间
      const totalSeconds = Math.floor(diffMs / 1000);
      const hours = Math.floor(totalSeconds / 3600);
      const minutes = Math.floor((totalSeconds % 3600) / 60);
      const seconds = totalSeconds % 60;
      
      // 更新显示（补零处理）
      hoursElement.textContent = hours.toString().padStart(2, '0');
      minutesElement.textContent = minutes.toString().padStart(2, '0');
      secondsElement.textContent = seconds.toString().padStart(2, '0');
    }
    
    // 初始化并每秒更新
    updateCountdown();
    setInterval(updateCountdown, 1000);
  </script>
</body>
</html>
