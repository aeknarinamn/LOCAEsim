<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  let packages = [];
  let id = ""
  let packageId = ""
  onMount(async () => {
    const res = await fetch(`${import.meta.env.VITE_API_URL}/airalo/local-pack-data-detail`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ id: $page.params.packageId })
    });
    const data = await res.json();
    packages = data.datas;
    id = packages.package_id
    packageId = packages.id
  });
  // console.log(packages)
  let showPopup = false;

  // ฟังก์ชันเพื่อเปิดหรือปิด popup
  const togglePopup = () => {
    showPopup = !showPopup;
  };

  import { goto } from '$app/navigation';

  function goToCheckOutPage() {
    goto('/local-esim-package/'+id+'/checkout-page/'+packageId);
  }
</script>

<!-- Font Awesome CDN for Icons -->
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"
/>

<style>
  /* Ensure no white margins or padding around the page */
  html,
  body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    background-color: #f4f4f4;
  }

  /* Top Menu/Header */
  .top-menu {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px;
    background-color: white;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    z-index: 10;
  }

  .top-menu a {
    text-decoration: none;
    color: inherit; /* ให้สีตรงกับ parent */
    margin-right: 10px;
    display: flex;
    align-items: center;
  }

  .top-menu h1 {
    font-size: 20px;
    margin: 0;
  }

  /* Container */
  .container {
    max-width: 400px;
    margin: 80px auto 0; /* เพิ่ม margin-top เป็น 80px เพื่อเว้นระยะห่างจาก top-menu */
    padding: 16px;
    background-color: #703199;
    color: white;
    border-radius: 16px;
  }

  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 16px;
  }

  .header a {
    text-decoration: none;
    color: inherit; /* ให้สีตรงกับ parent */
    margin-right: 10px;
    display: flex;
    align-items: center;
  }

  .header h1 {
    font-size: 24px;
    margin: 0;
  }

  .back-arrow {
    font-size: 20px;
    cursor: pointer;
  }

  img {
    width: 100%;
    border-radius: 16px;
    margin-bottom: 16px;
  }

  .details {
    background-color: #703199;
    padding: 16px;
    border-radius: 8px;
    margin-top: 16px;
  }

  .details div {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 0;
    border-bottom: 1px solid rgba(255, 255, 255, 0.3);
  }

  .details div:last-child {
    border-bottom: none;
  }

  .details div span {
    display: flex;
    align-items: center;
    font-size: 16px;
  }

  .details i {
    margin-right: 8px;
    color: white;
    font-size: 20px;
  }

  .details span:first-child {
    flex: 1;
  }

  .details span:last-child {
    text-align: right;
    flex-shrink: 0;
  }

  /* Additional Info Section */
  .additional-info,
  .footer {
    max-width: 400px;
    margin: 16px auto;
    background-color: white;
    border-radius: 16px;
    padding: 16px;
    color: #333;
    border: 2px solid white;
  }

  .additional-info h2 {
    font-size: 18px;
    margin-bottom: 16px;
  }

  .info-item {
    padding: 16px 0;
    border-top: 1px solid #e0e0e0;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
  }

  .info-item:first-child {
    border-top: none;
  }

  .info-item span {
    display: flex;
    align-items: center;
    font-size: 16px;
  }

  .info-item i {
    margin-right: 8px;
    color: black;
    font-size: 18px;
  }

  .info-item span:last-child {
    max-width: 200px;
    text-align: right;
    word-wrap: break-word;
  }

  .show-more {
    text-align: center;
    margin-top: 16px;
  }

  .show-more button {
    border: 1px solid #333;
    background-color: transparent;
    padding: 8px 16px;
    border-radius: 8px;
    cursor: pointer;
  }

  /* Alert Box */
  .alert {
    max-width: 400px;
    /* margin: 24px auto; */
    margin-bottom: 100px;
    background-color: #ff693a;
    color: white;
    padding: 16px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    font-size: 14px;
  }

  .alert-icon {
    font-size: 18px;
    margin-right: 8px;
  }

  /* Bottom Menu */
  .bottom-menu {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px;
    background-color: white;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
    border-top: 1px solid #e0e0e0;
  }

  /* ส่วนแสดงราคา */
  .price-section {
    font-size: 18px;
    font-weight: bold;
    color: #333;
    margin-right: 16px;
  }

  /* ปุ่ม BUY */
  .buy-button {
    background-color: #333;
    color: white;
    padding: 14px 20px; /* เพิ่ม padding เพื่อเพิ่มความสูง */
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    width: 220px; /* ปรับความกว้างเป็น 180px เพื่อเพิ่มความยาวมาครึ่งเท่า */
    transition: background-color 0.3s;
  }

  .buy-button:hover {
    background-color: #555;
  }

  .spacer {
    margin-bottom: 80px;
  }

  /* Popup CSS */
  .popup-background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 10;
  }

  .popup {
    background-color: white;
    border-radius: 10px;
    width: 90%;
    height: 90vh;
    padding: 20px;
    box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.1);
    position: relative;
    display: flex;
    flex-direction: column;
    color: black; /* เปลี่ยนฟอนต์ทั้งหมดใน popup เป็นสีดำ */
  }

  .popup-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #eee;
    /* padding-bottom: 10px; */
  }

  .popup-header h2 {
    font-size: 18px;
    font-weight: bold;
    margin: 0;
  }

  .close-button {
    background: none;
    border: none;
    font-size: 40px; /* ปรับขนาด font เป็น 24px */
    cursor: pointer;
    color: gray;
    line-height: 1; /* ควบคุมความสูงของปุ่ม */
    transition: transform 0.2s; /* เพิ่ม effect เมื่อ hover เพื่อความสวยงาม */
  }

  .close-button:hover {
    transform: scale(1.1); /* ขยายปุ่มเล็กน้อยเมื่อ hover */
  }

  .popup-content {
    flex-grow: 1;
    overflow-y: auto;
    margin-top: 20px;
    background-color: #f4f4f4; /* เปลี่ยนสีพื้นหลังของ popup-content เป็นสีเทา */
    padding: 20px;
    border-radius: 8px;
  }

  .popup-container ul {
    list-style-type: none; /* ลบ marker ของ bullet point */
    padding: 0; /* ลบ padding ด้านซ้ายของรายการ */
    margin: 0; /* ลบ margin ของรายการ */
  }

  .tips {
    font-size: 16px;
    margin-bottom: 20px;
  }

  .tips p {
    color: black;
    margin: 10px 0;
  }

  .tips ul {
    color: black;
    margin-left: 20px;
    list-style-type: none;
  }

  .tips ul li {
    margin: 5px 0;
  }

  .continue-button {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #333;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
    margin-top: 10px; /* เพิ่ม margin-top ให้ปุ่ม continue-button */
  }

  .privacy-policy {
    font-size: 12px;
    color: black; /* ทำให้สีของลิงก์เป็นสีดำ */
    text-align: center;
  }

  .privacy-policy a {
    color: black; /* ลิงก์มีสีดำตามคำขอ */
    text-decoration: none;
  }

  .privacy-policy a:hover {
    text-decoration: underline;
  }

  .popup-footer {
    margin-top: 10px;
    margin-bottom: 10px; /* เพิ่มระยะห่างด้านล่างของ popup-footer */
  }
</style>

<!-- Top Menu/Header -->
<div class="top-menu">
  <a href="javascript:history.back()">
    <div class="back-arrow">
      <i class="fas fa-arrow-left"></i>
    </div>
  </a>
  <h1>{packages.brand_title}</h1>
</div>

<!-- Container including top menu -->
<div class="container" style="background: linear-gradient(45deg, {packages.gradient_start}, {packages.gradient_end});">
  <!-- <div class="header">
    <a href="javascript:history.back()">
      <div class="back-arrow">
        <i class="fas fa-arrow-left"></i>
      </div>
    </a>
    <h1>dtac</h1>
  </div> -->

  <img
    src="{packages.package_img_url}"
    alt="Image of a colorful tuk-tuk with a background promoting tourist SIM card"
    onerror="this.onerror=null; this.src='/images/default-esim.png'"
  />

  <div class="details" style="background: linear-gradient(45deg, {packages.gradient_start}, {packages.gradient_end});">
    <div>
      <span><i class="fas fa-globe"></i> COVERAGE</span>
      <span>{packages.country_name}</span>
    </div>
    <div>
      <span><i class="fas fa-exchange-alt"></i> DATA</span>
      <span>{packages.package_data}</span>
    </div>
    <div>
      <span><i class="fas fa-phone-alt"></i> CALLS</span>
      <span>{packages.package_voice} MINS</span>
    </div>
    <div>
      <span><i class="fas fa-calendar-alt"></i> VALIDITY</span>
      <span>{packages.package_day} DAYS</span>
    </div>
    <div>
      <span><i class="fas fa-tag"></i> PRICE</span>
      <span>${packages.package_price} USD</span>
    </div>
  </div>
</div>

<!-- Footer -->
<div class="footer">
  <p><strong>Available Top-up Packages</strong></p>
  <p>There are no available top-up packages for this eSIM</p>
</div>

<!-- Additional Info Section -->
<div class="additional-info">
  <h2>Additional Information</h2>

  <div class="info-item">
    <span><i class="fas fa-signal"></i> NETWORK</span>
    <span>{packages.network}</span>
  </div>
  <div class="info-item">
    <span><i class="fas fa-file-alt"></i> PLAN TYPE</span>
    <span>{packages.plan_type}</span>
  </div>
  <div class="info-item">
    <span><i class="fas fa-tasks"></i> ACTIVATION POLICY</span>
    <span>{packages.activation_policy}</span>
  </div>
  <div class="info-item">
    <span><i class="fas fa-info-circle"></i> OTHER INFO</span>
    <span>{packages.other_info}</span>
  </div>

  <!-- Show More Button -->
  <!-- <div class="show-more">
    <button>SHOW MORE</button>
  </div> -->
</div>

<!-- Alert Box -->
<!-- <div class="alert">
  <span class="alert-icon"><i class="fas fa-exclamation-triangle"></i></span>
  <span
    >You must verify your identity to purchase this eSIM. Please start your
    identity verification process by submitting your documents.</span
  >
</div> -->

<!-- Spacer to avoid overlap -->
<div class="spacer"></div>

<!-- Bottom Menu with Button -->
<div class="bottom-menu">
  <div class="price-section">
    <span class="price">${packages.package_price} USD</span>
  </div>
  <button class="buy-button" on:click={goToCheckOutPage}>BUY</button>
</div>

<!-- Popup สำหรับ Identity Verification -->
{#if showPopup}
<div class="popup-background" on:click={togglePopup}>
  <div class="popup" on:click|stopPropagation>
    <!-- ส่วนหัวของ popup -->
    <div class="popup-header">
      <h2>Identity Verification</h2>
      <button class="close-button" on:click={togglePopup}>&times;</button>
    </div>

    <!-- ส่วนเนื้อหาของ popup -->
    <div class="popup-content">
      <!-- ส่วน Tips -->
      <div class="popup-container">
        <h3>Tips</h3>
        <p
          >Before going through the identity verification process, please make sure
          that you:</p
        >
        <ul>
          <li>- Are in a room with good lighting</li><br/>
          <li>
            - Either hold the ID document by hand (but not covering any part of the
            documents) OR:
          </li><br/>
          <li>
            - Place the ID document on a darker surface background (so that the
            contrast between the ID document and background is obvious)
          </li><br/>
          <li>- Avoid glare on the ID document</li>
        </ul>
      </div>
    </div>

    <!-- Privacy Policy -->
    <div class="popup-footer">
      <div class="privacy-policy">
        By continuing the identity verification process, you agree to
        <a href="#">Jumio’s Privacy Policy</a> and
        <a href="#">Airalo's Privacy Policy</a>
      </div>
    </div>

    <!-- ปุ่ม Continue -->
    <button class="continue-button">CONTINUE</button>
  </div>
</div>
{/if}