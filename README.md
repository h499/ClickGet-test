<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>ClickGet - السوق المفتوح</title>
  
  <!-- Firebase SDKs -->
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-storage-compat.js"></script>

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
    nav { background: #eee; padding: 10px; text-align: center; overflow-x: auto; white-space: nowrap; }
    nav a { margin: 0 10px; text-decoration: none; color: #333; font-weight: bold; }
    .products { display: grid; grid-template-columns: repeat(auto-fill,minmax(200px,1fr)); gap: 20px; padding: 20px; }
    .product { background: #fff; padding: 10px; border-radius: 10px; box-shadow: 0 1px 3px rgba(0,0,0,0.1); }
    .product img { width: 100%; border-radius: 10px; }
    .product h3 { margin-top: 10px; font-size: 18px; }
    .add-btn { background: #28a745; color: #fff; padding: 10px 20px; border: none; border-radius: 6px; cursor: pointer; margin: 20px; font-size: 16px; }
    footer { background: #222; color: #aaa; text-align: center; padding: 10px; font-size: 14px; margin-top: 30px; }

    #auth-container {
      max-width: 400px;
      margin: 20px auto;
      padding: 20px;
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      text-align: center;
    }
    #auth-container input {
      width: 90%;
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
      border: 1px solid #ddd;
      font-size: 16px;
    }
    #auth-container button {
      padding: 10px 20px;
      margin: 10px 5px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }
    #login-btn { background: #007bff; color: white; }
    #register-btn { background: #28a745; color: white; }
    #logout-btn {
      background: #dc3545;
      color: white;
      padding: 10px 20px;
      margin: 20px auto;
      display: block;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }

    #add-product-form {
      max-width: 400px;
      margin: 20px auto;
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    #add-product-form input, #add-product-form textarea {
      width: 90%;
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
      border: 1px solid #ddd;
      font-size: 16px;
      display: block;
    }
    #add-product-form button {
      background: #28a745;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <header>ClickGet</header>

  <nav>
    <a href="#" data-category="سيارات">سيارات</a>
    <a href="#" data-category="جوالات">جوالات</a>
    <a href="#" data-category="عقارات">عقارات</a>
    <a href="#" data-category="أثاث">أثاث</a>
    <a href="#" data-category="ألعاب">ألعاب</a>
    <a href="#" data-category="أجهزة كهربائية">أجهزة كهربائية</a>
    <a href="#" data-category="كمبيوتر">كمبيوتر</a>
    <a href="#" data-category="ساعات">ساعات</a>
    <a href="#" data-category="ملابس">ملابس</a>
    <a href="#" data-category="أحذية">أحذية</a>
    <a href="#" data-category="كتب">كتب</a>
    <a href="#" data-category="دراجات">دراجات</a>
    <a href="#" data-category="حيوانات">حيوانات</a>
    <a href="#" data-category="معدات مطاعم">معدات مطاعم</a>
    <a href="#" data-category="كهربائيات">كهربائيات</a>
    <a href="#" data-category="ألعاب أطفال">ألعاب أطفال</a>
    <a href="#" data-category="إلكترونيات">إلكترونيات</a>
    <a href="#" data-category="خدمات">خدمات</a>
    <a href="#" data-category="موبايلات">موبايلات</a>
    <a href="#" data-category="وظائف">وظائف</a>
  </nav>

  <div id="auth-container">
    <h2>تسجيل دخول / تسجيل جديد</h2>
    <input type="email" id="email" placeholder="البريد الإلكتروني" />
    <input type="password" id="password" placeholder="كلمة السر" />
    <button id="login-btn">دخول</button>
    <button id="register-btn">إنشاء حساب</button>
  </div>

  <button id="logout-btn" style="display:none;">تسجيل خروج</button>

  <div id="products-container" class="products"></div>

  <button id="show-add-product" class="add-btn" style="display:none;">+ أضف منتج</button>

  <form id="add-product-form" style="display:none;">
    <h3>إضافة منتج جديد</h3>
    <input type="text" id="product-name" placeholder="اسم المنتج" required />
    <input type="number" id="product-price" placeholder="السعر (درهم)" required />
    <input type="url" id="product-image" placeholder="رابط صورة المنتج" required />
    <select id="product-category" required>
      <option value="" disabled selected>اختر التصنيف</option>
      <option>سيارات</option>
      <option>جوالات</option>
      <option>عقارات</option>
      <option>أثاث</option>
      <option>ألعاب</option>
      <option>أجهزة كهربائية</option>
      <option>كمبيوتر</option>
      <option>ساعات</option>
      <option>ملابس</option>
      <option>أحذية</option>
      <option>كتب</option>
      <option>دراجات</option>
      <option>حيوانات</option>
      <option>معدات مطاعم</option>
      <option>كهربائيات</option>
      <option>ألعاب أطفال</option>
      <option>إلكترونيات</option>
      <option>خدمات</option>
      <option>موبايلات</option>
      <option>وظائف</option>
    </select>
    <button type="submit">أضف المنتج</button>
  </form>

  <div class="hidden-contact" style="display:none;">
    <h3>تواصل معنا</h3>
    <form action="https://formsubmit.co/nawafhazzaa2008@gmail.com" method="POST">
      <input type="hidden" name="_captcha" value="false" />
      <input type="text" name="الاسم" placeholder="اسمك" required /><br />
      <input type="email" name="البريد" placeholder="بريدك" required /><br />
      <textarea name="الرسالة" placeholder="رسالتك" required></textarea><br />
      <button type="submit">إرسال</button>
    </form>
  </div>

  <footer>جميع الحقوق محفوظة © ClickGet 2025</footer>

  <script>
    // Firebase config - حط بياناتك هنا
    const firebaseConfig = {
      apiKey: "AIza...YourAPIKey...",
      authDomain: "your-project.firebaseapp.com",
      projectId: "your-project",
      storageBucket: "your-project.appspot.com",
      messagingSenderId: "1234567890",
      appId: "1:1234567890:web:abcdefghijklm"
    };

    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);

    const auth = firebase.auth();
    const db = firebase.firestore();

    // DOM Elements
    const authContainer = document.getElementById("auth-container");
    const loginBtn = document.getElementById("login-btn");
    const registerBtn = document.getElementById("register-btn");
    const logoutBtn = document.getElementById("logout-btn");
    const productsContainer = document.getElementById("products-container");
    const addProductBtn = document.getElementById("show-add-product");
    const addProductForm = document.getElementById("add-product-form");

    let currentUser = null;
    let currentCategory = null;

    // تابع عرض المنتجات حسب التصنيف
    function loadProducts(category = null) {
      productsContainer.innerHTML = "جاري التحميل...";

      let query = db.collection("products");
      if (category) {
        query = query.where("category", "==", category);
      }

      query.get()
        .then(snapshot => {
          productsContainer.innerHTML = "";
          if (snapshot.empty) {
            productsContainer.innerHTML = "<p>لا توجد منتجات</p>";
            return;
          }
          snapshot.forEach(doc => {
            const data = doc.data();
            const priceWithTax = Number(data.price) + 2; // 2 درهم ضريبة
            const productHTML = `
              <div class="product">
                <img src="${data.image}" alt="${data.name}" />
                <h3>${data.name}</h3>
                <p>السعر: ${priceWithTax} درهم (شامل 2 درهم ضريبة)</p>
              </div>
            `;
            productsContainer.insertAdjacentHTML("beforeend", productHTML);
          });
        })
        .catch(err => {
          productsContainer.innerHTML = `<p>خطأ بتحميل المنتجات: ${err.message}</p>`;
        });
    }

    // تسجيل دخول
    loginBtn.onclick = () => {
      const email = document.getElementById("email").value.trim();
      const password = document.getElementById("password").value.trim();
      if (!email || !password) {
        alert("عبي كل الحقول!");
        return;
      }
      auth.signInWithEmailAndPassword(email, password)
        .then(() => alert("تم تسجيل الدخول!"))
        .catch(e => alert("خطأ: " + e.message));
    };

    // تسجيل جديد
    registerBtn.onclick = () => {
      const email = document.getElementById("email").value.trim();
      const password = document.getElementById("password").value.trim();
      if (!email || !password) {
        alert("عبي كل الحقول!");
        return;
      }
      auth.createUserWithEmailAndPassword(email, password)
        .then(() => alert("تم إنشاء الحساب!"))
        .catch(e => alert("خطأ: " + e.message));
    };

    // تسجيل خروج
    logoutBtn.onclick = () => {
      auth.signOut();
    };

    // مراقبة حالة تسجيل الدخول
    auth.onAuthStateChanged(user => {
      currentUser = user;
      if (user) {
        authContainer.style.display = "none";
        logoutBtn.style.display = "block";
        addProductBtn.style.display = user.email === "nawafhazzaa2008@gmail.com" ? "block" : "none";
        loadProducts(currentCategory);
      } else {
        authContainer.style.display = "block";
        logoutBtn.style.display = "none";
        addProductBtn.style.display = "none";
        productsContainer.innerHTML = "<p>رجاءً سجّل دخول أو أنشئ حساب لعرض المنتجات.</p>";
      }
    });

    // عرض منتجات حسب اختيار التصنيف
    document.querySelectorAll("nav a").forEach(link => {
      link.onclick = (e) => {
        e.preventDefault();
        currentCategory = e.target.getAttribute("data-category");
        loadProducts(currentCategory);
      };
    });

    // فتح/إغلاق نموذج إضافة منتج
    addProductBtn.onclick = () => {
      addProductForm.style.display = addProductForm.style.display === "none" ? "block" : "none";
    };

    // إضافة منتج جديد
    addProductForm.onsubmit = (e) => {
      e.preventDefault();
      if (!currentUser || currentUser.email !== "nawafhazzaa2008@gmail.com") {
        alert("ما عندك صلاحية لإضافة منتجات");
        return;
      }

      const name = document.getElementById("product-name").value.trim();
      const price = Number(document.getElementById("product-price").value.trim());
      const image = document.getElementById("product-image").value.trim();
      const category = document.getElementById("product-category").value;

      if (!name || !price || !image || !category) {
        alert("عبي كل الحقول!");
        return;
      }

      db.collection("products").add({
        name,
        price,
        image,
        category,
        createdAt: new Date()
      })
      .then(() => {
        alert("تم إضافة المنتج!");
        addProductForm.reset();
        addProductForm.style.display = "none";
        loadProducts(currentCategory);
      })
      .catch(e => alert("خطأ أثناء إضافة المنتج: " + e.message));
    };
  </script>
</body>
</html>
