يحبيب# ClickGet-test
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ClickGet - سوق الإمارات</title>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Cairo', sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f4;
    }
    header {
      background-color: #111827;
      color: white;
      padding: 1rem 2rem;
      text-align: center;
    }
    nav {
      display: flex;
      justify-content: center;
      gap: 1rem;
      background: #1f2937;
      padding: 0.5rem;
    }
    nav a {
      color: white;
      text-decoration: none;
    }
    .hero {
      background-color: #e5e7eb;
      padding: 2rem;
      text-align: center;
    }
    .hero h1 {
      color: #111827;
    }
    .sections {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 1rem;
      padding: 2rem;
    }
    .section {
      background-color: white;
      padding: 1rem;
      border-radius: 10px;
      text-align: center;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      transition: 0.3s;
    }
    .section:hover {
      transform: translateY(-5px);
    }
    footer {
      text-align: center;
      padding: 1rem;
      background-color: #111827;
      color: white;
      margin-top: 2rem;
    }
  </style>
</head>
<body>
  <header>
    <h1>ClickGet - المنصة الأفضل للإعلانات في الإمارات</h1>
    <p>بيع واشتري أي شيء بسهولة وبأمان!</p>
  </header>

  <nav>
    <a href="#">الرئيسية</a>
    <a href="#">جميع المنتجات</a>
    <a href="#">أضف إعلان</a>
    <a href="#">تواصل معنا</a>
  </nav>

  <div class="hero">
    <h1>ابحث عن المنتجات اللي تحتاجها</h1>
    <p>كل الأقسام - كل الإمارات - أسعار مميزة</p>
  </div>

  <section class="sections">
    <div class="section">📱 إلكترونيات</div>
    <div class="section">🎮 ألعاب</div>
    <div class="section">👕 ملابس</div>
    <div class="section">👜 شنط واكسسوارات</div>
    <div class="section">🚗 سيارات</div>
    <div class="section">🏡 عقارات</div>
    <div class="section">💻 كمبيوترات</div>
    <div class="section">🛒 عروض</div>
  </section>

  <footer>
    <p>جميع الحقوق محفوظة &copy; ClickGet 2025</p>
  </footer>
</body>
</html>
