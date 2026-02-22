<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>هشدار - یک اطلاعیه</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: Tahoma, Arial, sans-serif;
      background: #0f0f0f;
      color: #f0f0f0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      padding: 24px;
      text-align: center;
    }
    .icon { font-size: 64px; margin-bottom: 24px; }
    h1 { font-size: 24px; margin-bottom: 16px; color: #ffffff; }
    p {
      font-size: 16px;
      line-height: 1.8;
      color: #aaaaaa;
      max-width: 400px;
      margin-bottom: 32px;
    }
    .badge {
      background: #1a1a1a;
      border: 1px solid #333;
      border-radius: 12px;
      padding: 16px 24px;
      font-size: 14px;
      color: #888;
      max-width: 400px;
    }
    .status {
      margin-top: 48px;
      font-size: 13px;
      color: #444;
    }
  </style>
</head>
<body>
  <div class="icon">🔔</div>
  <h1>یک اطلاعیه — فقط اگه لازم باشه</h1>
  <p>
    این اپ فقط یک بار نوتیفیکیشن می‌فرسته.<br/>
    نه خبر مداوم، نه اضطراب بیشتر.<br/>
    فقط یک لحظه مهم، اگه اتفاق بیفته.
  </p>
  <div class="badge">
    🟢 در حال پایش منابع رسمی خبری
  </div>
  <div class="status">ساخته شده با آرامش، برای آرامش</div>

  <!-- OneSignal SDK -->
  <script src="https://cdn.onesignal.com/sdks/web/v16/OneSignalSDK.page.js" defer></script>
  <script>
    window.OneSignalDeferred = window.OneSignalDeferred || [];
    OneSignalDeferred.push(async function(OneSignal) {
      await OneSignal.init({
        appId: "c5866cf0-d4fd-461b-ac78-1559a36bfa9b",
      });
    });
  </script>
</body>
</html>
