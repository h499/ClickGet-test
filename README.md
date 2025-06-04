<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ClickGet - السوق المفتوح</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; font-family: sans-serif; }
    body { background: #f3f3f3; color: #333; }
    header { background: #333; color: #fff; padding: 20px; text-align: center; font-size: 24px; font-weight: bold; position: relative; }
    header::after {
      content: "";
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: linear-gradient(45deg, #999, #ccc);
      z-index: -1;
      animation: moveBg 5s linear infinite;
    }
    @keyframes moveBg {
      0% { background-position: 0 0; }
      100% { background-position: 100% 100%; }
    }
    nav { background: #eee; padding: 10px; text-align: center; }
    nav a { margin: 0 10px; text-decoration: none; color: #333; font-weight: bold; }
    .category { padding: 20px; background: #fff; margin: 10px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
    .products { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 20px; padding: 20px; }
    .product { background: #fff; padding: 10px; border-radius: 10px; box-shadow: 0 1px 3px rgba(0,0,0,0.1); }
    .product img { width: 100%; border-radius: 10px; }
    .product h3 { margin-top: 10px; font-size: 18px; }
    .add-btn { background: #28a745; color: #fff; padding: 10px 20px; border: none; border-radius: 6px; cursor: pointer; margin: 20px; font-size: 16px; }
    footer { background: #222; color: #aaa; text-align: center; padding: 10px; font-size: 14px; margin-top: 30px; }
    .hidden-contact, .login-form { display: none; }
  </style>
</head>
<body>
  <header>ClickGet</header>
  <nav>
    <a href="#">سيارات</a>
    <a href="#">جوالات</a>
    <a href="#">عقارات</a>
    <a href="#">أثاث</a>
    <a href="#">ألعاب</a>
    <a href="#">أجهزة كهربائية</a>
    <a href="#">كمبيوتر</a>
    <a href="#">ساعات</a>
    <a href="#">ملابس</a>
    <a href="#">أحذية</a>
    <a href="#">كتب</a>
    <a href="#">دراجات</a>
    <a href="#">حيوانات</a>
    <a href="#">معدات مطاعم</a>
    <a href="#">كهربائيات</a>
    <a href="#">ألعاب أطفال</a>
    <a href="#">إلكترونيات</a>
    <a href="#">خدمات</a>
    <a href="#">موبايلات</a>
    <a href="#">وظائف</a>
  </nav>

  <div class="products">
    <div class="product">
      <img src="https://via.placeholder.com/200x150" alt="منتج">
      <h3>منتج مثال - 50 درهم</h3>
      <p>بعد الضريبة: 52 درهم</p>
    </div>
    <div class="product">
      <img src="https://via.placeholder.com/200x150" alt="منتج">
      <h3>منتج ثاني - 100 درهم</h3>
      <p>بعد الضريبة: 102 درهم</p>
    </div>
  </div>

  <div style="text-align:center">
    <button class="add-btn" onclick="alert('ميزة إضافة المنتج غير مفعلة بالنسخة الحالية')">+ أضف منتج</button>
  </div>

  <div class="hidden-contact">
    <h3>تواصل معنا</h3>
    <form action="https://formsubmit.co/nawafhazzaa2008@gmail.com" method="POST">
      <input type="hidden" name="_captcha" value="false">
      <input type="text" name="الاسم" placeholder="اسمك" required><br>
      <input type="email" name="البريد" placeholder="بريدك" required><br>
      <textarea name="الرسالة" placeholder="رسالتك" required></textarea><br>
      <button type="submit">إرسال</button>
    </form>
  </div>

  <footer>جميع الحقوق محفوظة © ClickGet 2025</footer>
</body>
</html>
