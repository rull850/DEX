<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dex</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f1f3f5;
      color: #333;
      font-size: 14px;
    }

    .header {
      background: linear-gradient(135deg, #00c6ff, #0072ff, #00f2fe );
      color: white;
      padding: 30px 15px;
      text-align: center;
      font-size: 16px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    
    .clock {
      margin: 3px;
      color: black;
    }

    .header h1 {
      font-size: 20px;
      margin-bottom: 5px;
    }

    .navbar {
      background-color: #ffffff;
      color: #0072ff;
      padding: 10px;
      display: flex;
      align-items: center;
      border: 1px solid #0072ff;
      border-radius: 6px;
      width: calc(100% - 20px);
      max-width: 100%;
      cursor: pointer;
      transition: color 0.3s, border-color 0.3s;
      margin: 10px;
      font-size: 14px;
    }

    .navbar.active {
      color: white;
      background-color: #0072ff;
      border-color: #0072ff;
    }

    .navbar i {
      margin-right: 8px;
      font-size: 14px;
    }

    .menu-items {
      display: none;
      flex-direction: column;
      background-color: #e3f2fd;
      color: #333;
      padding: 10px 15px;
      animation: slideDown 0.3s ease-out;
      margin: 0 10px 10px;
      border-radius: 6px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
      font-size: 13px;
    }

    .menu-item {
      display: flex;
      align-items: center;
      padding: 8px 0;
      cursor: pointer;
      color: #0072ff;
      transition: color 0.3s, background 0.3s;
      border-radius: 4px;
      padding-left: 6px;
    }

    .menu-item.clicked {
      background-color: #cfe8ff;
      color: #000;
    }

    .menu-item:hover {
      background-color: rgba(0, 114, 255, 0.1);
    }

    .menu-item i {
      margin-right: 8px;
      font-size: 13px;
    }

    .search-bar {
      display: block;
      align-items: center;
      padding: 10px;
      background-color: #d0e6ff;
      border-radius: 8px;
      margin-top: 8px;
    }

    .search-bar input {
      background: none;
      border: none;
      color: #333;
      outline: none;
      margin-left: 8px;
      flex: 1;
      font-size: 13px;
    }

    .search-bar i {
      color: #000;
      font-size: 14px;
    }

    section {
      max-width: 800px;
      margin: 40px auto;
      padding: 20px;
      background: cyan;
      border-radius: 10px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.06);
      opacity: 0;
      transform: translateY(40px);
      transition: all 0.8s ease;
    }

    section.visible {
      opacity: 1;
      transform: translateY(0);
    }

    h2 {
      color: #0072ff;
      margin-bottom: 10px;
    }

    @media (max-width: 600px) {
      .header h1 {
        font-size: 18px;
      }
      section {
        margin: 20px 10px;
      }
    }

    @keyframes slideDown {
      from { opacity: 0; transform: translateY(-10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    .AC {
      display: flex;
      align-items: center;
      gap: 20px;
    }
    
  </style>
</head>
<body>

  <div class="header">
    <h1>Dex Web Server</h1>
    <p>Be Yours</p>
    <div class="clock" id="clock">00:00:00</div>

  </div>

  <div onclick="toggleMenu()" class="navbar" id="navbar">
    <i class="fas fa-bars"></i> NAVIGASI MENU
  </div>

  <div class="menu-items" id="menuItems">
    <div class="menu-item" onclick="markClicked(this)"><i class="fas fa-home"></i> HOME</div>
    <div class="menu-item" onclick="markClicked(this)"><i class="fas fa-file-alt"></i> PROJECT</div>
    <div class="menu-item" onclick="markClicked(this)"><i class="fas fa-user"></i> STAFF</div>
    <div class="menu-item" onclick="markClicked(this)"><i class="fas fa-envelope"></i> CONTACT</div>
    <div class="menu-item" onclick="markClicked(this)"><i class="fas fa-folder"></i> ARCHIVE</div>
  </div>
  <!--
      <div class="search-bar">
      <i class="fas fa-search"></i>
      <input type="text" id="search" placeholder="CARI MENU..." oninput="filterList()" />
    </div>
  -->
  <!-- Konten Deskripsi -->
  <section data-title="Action & stuff">
    <div class="AC">
      <img src="pack_icon.png" alt="action and stuff" width=" 50px" height="auto" />
    <h2>Action & Stuff</h2>
    </div>
    <p>Action and Stuff adalah resource pack atau texture pack Minecraft Bedrock yang paling populer hingga saat ini. Texture pack ini memiliki banyak animasi player mob dan juga items.</p>
  </section>

  <script>
    
    function updateClock() {
const now = new Date();
const timeString = now.toLocaleTimeString();
document.getElementById("clock").textContent = timeString;
}
setInterval(updateClock, 1000);
updateClock();
    
    function toggleMenu() {
      const menu = document.getElementById("menuItems");
      const navbar = document.getElementById("navbar");
      if (menu.style.display === "flex") {
        menu.style.display = "none";
        navbar.classList.remove("active");
      } else {
        menu.style.display = "flex";
        navbar.classList.add("active");
      }
    }

    function markClicked(item) {
      document.querySelectorAll('.menu-item').forEach(el => el.classList.remove('clicked'));
      item.classList.add('clicked');
    }

    // Animasi scroll masuk & keluar
    const sections = document.querySelectorAll("section");

    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add("visible");
        } else {
          entry.target.classList.remove("visible"); // agar animasi bisa muncul lagi saat diskroll ulang
        }
      });
    }, {
      threshold: 0.15,
    });

    sections.forEach(section => observer.observe(section));
    
    function filterList() {
  const input = document.getElementById("search").value.toLowerCase();
  const sections = document.querySelectorAll("section");

  sections.forEach(section => {
    const title = section.getAttribute("data-title").toLowerCase();
    const content = section.textContent.toLowerCase();
    
    if (title.includes(input) || content.includes(input)) {
      section.style.display = "block";
    } else {
      section.style.display = "none";
    }
  });
}
    
  </script>

  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
</body>
</html>
