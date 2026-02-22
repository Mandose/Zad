<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>زاد</title>
  <link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@300;400&display=swap" rel="stylesheet">
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Vazirmatn', sans-serif;
      background: #050505;
      color: #f0f0f0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      min-height: 100vh;
      padding: 80px 24px 44px;
      text-align: center;
    }

    .top-group {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 20px;
    }

    .top {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0px;
    }
    .subtitle {
      font-size: 15px;
      font-weight: 300;
      color: #ffffff;
      letter-spacing: 0.06em;
    }
    h1 {
      font-size: 42px;
      font-weight: 400;
      color: #ffffff;
      letter-spacing: 0.01em;
      line-height: 1.2;
    }

    .circle-btn {
      width: 68px;
      height: 68px;
      border-radius: 50%;
      background: #ffffff;
      cursor: pointer;
      border: none;
      outline: none;
      transition: background 0.4s, box-shadow 0.4s;
      -webkit-tap-highlight-color: transparent;
    }
    .circle-btn.active {
      background: #b52a1e;
      box-shadow: 0 0 50px rgba(181, 42, 30, 0.4);
    }

    .middle {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 12px;
    }
    .notif-status {
      font-size: 11px;
      font-weight: 300;
      color: #333;
      letter-spacing: 0.08em;
      min-height: 16px;
      transition: color 0.3s;
    }
    .notif-status.active { color: #4ade80; }

    .monitor-row {
      display: flex;
      align-items: center;
      gap: 8px;
      direction: rtl;
      opacity: 0;
      transition: opacity 0.6s;
    }
    .monitor-row.visible { opacity: 1; }
    .dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: #4ade80;
      flex-shrink: 0;
      animation: blink 2s ease-in-out infinite;
    }
    @keyframes blink {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.1; }
    }
    .monitor-text {
      font-size: 11px;
      font-weight: 300;
      color: #3a3a3a;
      letter-spacing: 0.06em;
    }

    .bottom {
      font-family: -apple-system, 'SF Pro Text', 'Helvetica Neue', Helvetica, Arial, sans-serif;
      font-size: 12px;
      font-weight: 300;
      color: rgba(255,255,255,0.45);
      max-width: 320px;
      line-height: 1.9;
      letter-spacing: 0.02em;
    }
  </style>
</head>
<body>

  <div class="top-group">
    <div class="top">
      <span class="subtitle">هر وقت زدن</span>
      <h1>بهم خبر بده!</h1>
    </div>
    <button class="circle-btn" id="circleBtn" onclick="toggleNotif()"></button>
  </div>

  <div class="middle">
    <div class="notif-status" id="notifStatus"></div>
    <div class="monitor-row" id="monitorRow">
      <span class="dot"></span>
      <span class="monitor-text">در حال پایش منابع خبری رسمی</span>
    </div>
  </div>

  <p class="bottom">
    شما با فشردن دایره سفید، با خبر رسمی آغاز جنگ ایران–امریکا،<br/>
    تنها یک بار نوتیفیکیشن دریافت می‌کنید.<br/>
    «زدن»
  </p>

  <script src="https://cdn.onesignal.com/sdks/web/v16/OneSignalSDK.page.js" defer></script>
  <script>
    let isActive = false;

    window.OneSignalDeferred = window.OneSignalDeferred || [];
    OneSignalDeferred.push(async function(OneSignal) {
      await OneSignal.init({
        appId: "c5866cf0-d4fd-461b-ac78-1559a36bfa9b",
        allowLocalhostAsSecureOrigin: true,
      });
      if (OneSignal.Notifications.permission) setActive(true);
    });

    function setActive(val) {
      isActive = val;
      const btn = document.getElementById('circleBtn');
      const status = document.getElementById('notifStatus');
      const monitor = document.getElementById('monitorRow');
      if (val) {
        btn.classList.add('active');
        status.textContent = '✓ اطلاعیه فعاله';
        status.classList.add('active');
        monitor.classList.add('visible');
      } else {
        btn.classList.remove('active');
        status.textContent = '';
        status.classList.remove('active');
        monitor.classList.remove('visible');
      }
    }

    async function toggleNotif() {
      if (!isActive) {
        OneSignalDeferred.push(async function(OneSignal) {
          const result = await OneSignal.Notifications.requestPermission();
          if (result) {
            setActive(true);
          } else {
            document.getElementById('notifStatus').textContent = 'اجازه داده نشد';
          }
        });
      } else {
        setActive(false);
      }
    }
  </script>
</body>
</html>
