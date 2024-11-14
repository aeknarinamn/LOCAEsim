<script>
  import { goto } from '$app/navigation';

  function goToEsimDetailPage() {
    goto('/my-esim/detail');
  }

  // Variables to handle visibility of popups (if needed)
  let showOrderCompleted = true; // Assuming the order completed page is being shown
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

  .order-summary {
    text-align: center;
    margin-bottom: 40px;
  }

  .order-summary h2 {
    font-size: 24px;
    margin: 10px 0;
  }

  .order-summary p {
    font-size: 14px;
    color: #666;
    margin: 5px 0;
  }

  .order-summary .order-id {
    font-weight: bold;
    font-size: 12px;
    color: #333;
  }

  .status-icon {
    width: 50px;
    height: 50px;
    background-color: #4caf50;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 10px;
  }

  .status-icon i {
    color: white;
    font-size: 24px;
  }

  .package-card {
    background-color: #d9534f;
    border-radius: 16px;
    padding: 20px;
    color: white;
    margin-bottom: 20px;
    position: relative;
    min-height: 280px; /* ปรับความสูงขั้นต่ำของการ์ดให้มากขึ้น */
    display: flex;
    flex-direction: column;
    justify-content: space-between; /* จัดข้อมูลภายในให้มีระยะห่างที่เหมาะสม */
  }

  .package-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 22px; /* ปรับขนาดฟอนต์ให้ใหญ่ขึ้น */
    font-weight: bold;
  }

  .package-image {
    width: 120px; /* ขยายขนาดของภาพให้เหมาะสมกับความสูงใหม่ */
    border-radius: 8px;
    position: absolute;
    top: -15px;
    right: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  }

  .package-details {
    margin-top: 20px; /* เพิ่มระยะห่างจากหัวการ์ด */
  }

  .package-details div {
    display: flex;
    justify-content: space-between;
    padding: 12px 0; /* เพิ่ม padding เพื่อให้เนื้อหาในแต่ละบรรทัดดูโดดเด่นขึ้น */
    border-bottom: 1px solid rgba(255, 255, 255, 0.3);
  }

  .package-details div:last-child {
    border-bottom: none;
  }

  .package-details span {
    font-size: 16px; /* ปรับขนาดฟอนต์ให้ใหญ่ขึ้นเพื่อเหมาะกับความสูงใหม่ */
    display: flex;
    align-items: center;
  }

  .package-details i {
    margin-right: 12px; /* ปรับระยะห่างระหว่างไอคอนกับข้อความ */
  }

  .payment-details {
    background-color: #fff;
    border-radius: 12px;
    padding: 16px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 80px;
  }

  .payment-details h3 {
    font-size: 18px;
    margin: 0 0 8px;
    color: #333;
  }

  .payment-info,
  .price-info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 12px 0;
    font-size: 14px;
    color: #333;
  }

  .price-info span {
    font-weight: bold;
  }

  .price-info .negative {
    color: #d9534f;
  }

  .payment-info i {
    font-size: 24px;
  }

  .instructions {
    margin-top: 20px;
    margin-bottom: 20px;
  }

  .instructions h3 {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 8px;
    color: #333;
  }

  .instructions p {
    font-size: 14px;
    color: #666;
    margin-bottom: 12px;
  }

  .instructions-button {
    background-color: #fff;
    border: 1px solid #e0e0e0;
    padding: 12px;
    border-radius: 8px;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    font-size: 16px;
    color: #333;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }

  .bottom-menu {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 16px;
    background-color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
    border-top: 1px solid #e0e0e0;
  }

  .view-button {
    background-color: #333;
    color: white;
    padding: 12px 24px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    flex-grow: 1;
    max-width: 400px;
  }

  .view-button:hover {
    background-color: #555;
  }
</style>

<!-- Top Menu/Header -->
<div class="top-menu">
  <h1>Order Completed</h1>
</div>

<!-- Main Container -->
<div class="container">
  {#if showOrderCompleted}
    <!-- Order Summary -->
    <div class="order-summary">
      <div class="status-icon">
        <i class="fas fa-check"></i>
      </div>
      <h2>Thank you for your order.</h2>
      <p>We’ve sent you a confirmation receipt to aeknarin.amn@gmail.com.</p>
      <p class="order-id">ORDER ID: #20240928-35308943</p>
    </div>

    <!-- Package Card -->
    <div class="package-card">
      <div class="package-header">
        <span>Xin Chao</span>
        <img
          class="package-image"
          src="https://placehold.co/70x50"
          alt="SIM card image"
        />
      </div>
      <div class="package-details">
        <div>
          <span><i class="fas fa-globe"></i> COVERAGE</span>
          <span>Vietnam</span>
        </div>
        <div>
          <span><i class="fas fa-exchange-alt"></i> DATA</span>
          <span>1 GB</span>
        </div>
        <div>
          <span><i class="fas fa-calendar-alt"></i> VALIDITY</span>
          <span>7 Days</span>
        </div>
        <div>
          <span><i class="fas fa-tag"></i> PRICE</span>
          <span>$4.50 USD</span>
        </div>
      </div>
    </div>

    <!-- How to Install an eSIM -->
    <div class="instructions">
      <h3>How to Install an eSIM</h3>
      <p>You can install your eSIM by visiting your eSIM details now.</p>
      <button class="instructions-button" on:click={goToEsimDetailPage}>
        <i class="fas fa-sim-card"></i> Go to eSIM Details <i class="fas fa-chevron-right"></i>
      </button>
    </div>

    <!-- Payment Details -->
    <div class="payment-details">
      <h3>Payment Details</h3>
      <div class="payment-info">
        <span>PAYMENT METHOD</span>
        <span><i class="fab fa-cc-mastercard"></i> **** 8852</span>
      </div>
      <div class="price-info">
        <span>TOTAL PRICE</span>
        <span>$4.50 USD</span>
      </div>
      <div class="price-info">
        <span>REFERRAL REWARD</span>
        <span class="negative">-$3.00 USD</span>
      </div>
      <div class="price-info">
        <span>FINAL PRICE</span>
        <span>$1.50 USD</span>
      </div>
    </div>
  
  {/if}
</div>

<!-- Bottom Menu with View eSIM Details Button -->
<div class="bottom-menu">
  <button class="view-button" on:click={goToEsimDetailPage}>VIEW eSIM DETAILS</button>
</div>