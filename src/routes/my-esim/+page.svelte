<script>
  import { goto } from '$app/navigation';

  function goToEsimDetailPage() {
    goto('/my-esim/detail');
  }

  let showCurrentESIMs = true; // ตัวแปรจัดการการแสดงผล eSIM ปัจจุบัน
  let esims = [
    {
      name: 'Xin Chao',
      iccid: '8965012405032477005',
      coverage: 'Vietnam',
      remainingData: '1 GB',
      imageUrl: 'https://placehold.co/70x50',
    }
  ];

  let banners = [
    { id: 1, text: "How to get your free eSIM", color: "#ffe9a7", img: "📱" },
    { id: 2, text: "New Global eSIM Offers", color: "#ffd1a7", img: "🌍" },
    { id: 3, text: "Enjoy seamless internet anywhere!", color: "#ffa7b5", img: "🌐" }
  ];

  let currentBanner = 0;

  function nextBanner() {
    currentBanner = (currentBanner + 1) % banners.length;
  }

  setInterval(nextBanner, 3000);
</script>

<!-- Font Awesome CDN for Icons -->
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"
/>

<style>
  html,
  body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    background-color: #f4f4f4;
    font-family: 'Arial', sans-serif;
  }

  .top-menu {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 16px;
    background-color: white;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    z-index: 10;
  }

  .top-menu h1 {
    font-size: 20px;
    margin: 0;
  }

  .container {
    max-width: 400px;
    margin: 0 auto;
    padding: 16px;
    margin-top: 80px; /* Space for top-menu */
  }

  .tabs {
    display: flex;
    justify-content: space-around;
    margin-bottom: 20px;
  }

  .tab {
    flex: 1;
    text-align: center;
    padding: 10px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    border-bottom: 2px solid transparent;
  }

  .tab.active {
    color: #333;
    border-bottom: 2px solid #333;
  }

  .banner-slide {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 15px;
    border-radius: 10px;
    margin-top: 20px;
    margin-bottom: 40px;
    transition: background-color 0.5s ease;
  }

  .banner-img {
    font-size: 2rem;
  }

  .banner-slide p {
    font-size: 1.1rem;
    font-weight: bold;
  }

  .esim-card {
    background-color: #d9534f;
    border-radius: 16px;
    padding: 20px;
    color: white;
    margin-bottom: 20px;
    position: relative;
    min-height: 250px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .esim-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 22px;
    font-weight: bold;
  }

  .esim-image {
    width: 120px;
    border-radius: 8px;
    position: absolute;
    top: -20px;
    right: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  }

  .esim-details {
    margin-top: 20px;
  }

  .esim-details div {
    display: flex;
    justify-content: space-between;
    padding: 12px 0;
    border-bottom: 1px solid rgba(255, 255, 255, 0.3);
  }

  .esim-details div:last-child {
    border-bottom: none;
  }

  .esim-details span {
    font-size: 16px;
    display: flex;
    align-items: center;
  }

  .esim-details i {
    margin-right: 12px;
  }

  .esim-actions {
    display: flex;
    justify-content: space-between;
    gap: 10px; /* เพิ่ม gap เพื่อเพิ่มระยะห่างระหว่างปุ่ม */
    margin-top: 10px;
  }

  .action-button {
    flex: 1;
    padding: 12px;
    border: 1px solid white;
    background: transparent;
    border-radius: 8px;
    color: white;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .action-button:hover {
    background: rgba(255, 255, 255, 0.1);
  }

  .archived-message {
    text-align: center;
    /* padding: 40px 20px; */
    /* background-color: #fff;
    border-radius: 12px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1); */
    /* margin-top: 5px; */
  }

  .archived-message img {
    width: 100%; /* ทำให้รูปภาพครอบคลุมพื้นที่ container โดยไม่ล้น */
    max-width: 380px; /* กำหนดขนาดสูงสุดของรูป */
    margin-bottom: 30px;
  }

  .archived-message h2 {
    font-size: 20px;
    margin-bottom: 10px;
  }

  .archived-message p {
    font-size: 14px;
    color: #666;
  }

  .archived-message button {
    background-color: #333;
    color: white;
    padding: 12px 24px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    margin-top: 20px;
  }

  .bottom-menu {
    display: flex;
    justify-content: space-around;
    padding: 20px 0;
    border-top: 1px solid #ddd;
    position: fixed;
    bottom: 0;
    width: 100%;
    background-color: white;
    max-width: 100%;
    left: 0;
  }

  .bottom-menu a {
    color: inherit; /* ให้ใช้สีเดียวกับ parent */
    text-decoration: none; /* เอาขีดเส้นใต้ของลิงก์ออก */
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-size: 0.9rem;
    transition: color 0.3s ease;
  }

  .bottom-menu a:hover {
    color: #333; /* สีเมื่อ hover */
  }

  .menu-item {
    text-align: center;
    cursor: pointer;
  }

  .menu-item i {
    font-size: 20px;
    color: #555;
  }

  .menu-item p {
    margin: 5px 0 0 0;
    font-size: 0.9rem;
    color: #555;
  }
</style>

<!-- Top Menu/Header -->
<div class="top-menu">
  <h1>My eSIMs</h1>
</div>

<!-- Main Container -->
<div class="container">
  <!-- Tabs for Current and Archived eSIMs -->
  <div class="tabs">
    <div
      class="tab {showCurrentESIMs ? 'active' : ''}"
      on:click={() => (showCurrentESIMs = true)}
    >
      Current eSIMs
    </div>
    <div
      class="tab {!showCurrentESIMs ? 'active' : ''}"
      on:click={() => (showCurrentESIMs = false)}
    >
      Archived eSIMs
    </div>
  </div>

  <!-- Banner Section -->
  <div class="banner-slide" style="background-color: {banners[currentBanner].color}">
    <span class="banner-img">{banners[currentBanner].img}</span>
    <p>{banners[currentBanner].text}</p>
  </div>

  <!-- eSIM Cards -->
  {#if showCurrentESIMs}
    {#each esims as esim}
      <div class="esim-card">
        <div class="esim-header">
          <span>{esim.name}</span>
          <img class="esim-image" src={esim.imageUrl} alt="{esim.name} SIM card image" />
        </div>
        <div class="esim-details">
          <div>
            <span><i class="fas fa-sim-card"></i> ICCID</span>
            <span>{esim.iccid}</span>
          </div>
          <div>
            <span><i class="fas fa-globe"></i> COVERAGE</span>
            <span>{esim.coverage}</span>
          </div>
          <div>
            <span><i class="fas fa-exchange-alt"></i> REMAINING DATA</span>
            <span>{esim.remainingData}</span>
          </div>
        </div>
        <div class="esim-actions">
          <button class="action-button">TOP UP</button>
          <button class="action-button" on:click={goToEsimDetailPage}>DETAILS</button>
        </div>
      </div>
    {/each}
  {:else}
    <!-- Archived eSIMs -->
    <div class="archived-message">
      <img src="/images/default-myesim.jpg" alt="Archived eSIMs Image" />
    </div>
  {/if}
</div>

<!-- Bottom Menu -->
<div class="bottom-menu">
  <a href="/" class="menu-item">
    <span>🏪</span>
    <p>Store</p>
  </a>
  <a href="/my-esim" class="menu-item">
    <span>💳</span>
    <p>My eSIMs</p>
  </a>
  <a href="/" class="menu-item">
    <span>📋</span>
    <p>How to</p>
  </a>
</div>