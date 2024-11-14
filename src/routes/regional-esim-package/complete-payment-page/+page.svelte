<script>
  import { goto } from '$app/navigation';

  function goToEsimDetailPage() {
    goto('/my-esim/detail');
  }

  // Variables to handle visibility of popups (if needed)
  let showOrderCompleted = true; // Assuming the order completed page is being shown

  let showPopup = false;
  let searchQuery = ''; // เก็บค่าที่ค้นหา

  // ฟิลเตอร์ประเทศตามการค้นหา
  $: filteredCountries = supportedCountries.filter((country) =>
    country.name.toLowerCase().includes(searchQuery.toLowerCase())
  );

  // ข้อมูลประเทศที่รองรับพร้อม URL รูปธง
  let supportedCountries = [
    { name: 'Algeria', flag: 'https://flagcdn.com/w320/dz.png' },
    { name: 'Angola', flag: 'https://flagcdn.com/w320/ao.png' },
    { name: 'Benin', flag: 'https://flagcdn.com/w320/bj.png' },
    { name: 'Botswana', flag: 'https://flagcdn.com/w320/bw.png' },
    { name: 'Burkina Faso', flag: 'https://flagcdn.com/w320/bf.png' },
    { name: 'Burundi', flag: 'https://flagcdn.com/w320/bi.png' },
    { name: 'Cabo Verde', flag: 'https://flagcdn.com/w320/cv.png' },
    { name: 'Cameroon', flag: 'https://flagcdn.com/w320/cm.png' },
    { name: 'Central African Republic', flag: 'https://flagcdn.com/w320/cf.png' },
    { name: 'Chad', flag: 'https://flagcdn.com/w320/td.png' },
    { name: 'Comoros', flag: 'https://flagcdn.com/w320/km.png' },
    { name: 'Congo', flag: 'https://flagcdn.com/w320/cg.png' },
    { name: 'Democratic Republic of The Congo', flag: 'https://flagcdn.com/w320/cd.png' },
    { name: 'Djibouti', flag: 'https://flagcdn.com/w320/dj.png' },
    { name: 'Egypt', flag: 'https://flagcdn.com/w320/eg.png' },
    { name: 'Equatorial Guinea', flag: 'https://flagcdn.com/w320/gq.png' },
    { name: 'Eritrea', flag: 'https://flagcdn.com/w320/er.png' },
    { name: 'Eswatini', flag: 'https://flagcdn.com/w320/sz.png' },
    { name: 'Ethiopia', flag: 'https://flagcdn.com/w320/et.png' },
    { name: 'Gabon', flag: 'https://flagcdn.com/w320/ga.png' },
    { name: 'Gambia', flag: 'https://flagcdn.com/w320/gm.png' },
    { name: 'Ghana', flag: 'https://flagcdn.com/w320/gh.png' },
    { name: 'Guinea', flag: 'https://flagcdn.com/w320/gn.png' },
    { name: 'Guinea-Bissau', flag: 'https://flagcdn.com/w320/gw.png' },
    { name: 'Ivory Coast (Côte d\'Ivoire)', flag: 'https://flagcdn.com/w320/ci.png' },
    { name: 'Kenya', flag: 'https://flagcdn.com/w320/ke.png' },
    { name: 'Lesotho', flag: 'https://flagcdn.com/w320/ls.png' },
    { name: 'Liberia', flag: 'https://flagcdn.com/w320/lr.png' },
    { name: 'Libya', flag: 'https://flagcdn.com/w320/ly.png' },
    { name: 'Madagascar', flag: 'https://flagcdn.com/w320/mg.png' },
    { name: 'Malawi', flag: 'https://flagcdn.com/w320/mw.png' },
    { name: 'Mali', flag: 'https://flagcdn.com/w320/ml.png' },
    { name: 'Mauritania', flag: 'https://flagcdn.com/w320/mr.png' },
    { name: 'Mauritius', flag: 'https://flagcdn.com/w320/mu.png' },
    { name: 'Morocco', flag: 'https://flagcdn.com/w320/ma.png' },
    { name: 'Mozambique', flag: 'https://flagcdn.com/w320/mz.png' },
    { name: 'Namibia', flag: 'https://flagcdn.com/w320/na.png' },
    { name: 'Niger', flag: 'https://flagcdn.com/w320/ne.png' },
    { name: 'Nigeria', flag: 'https://flagcdn.com/w320/ng.png' },
    { name: 'Rwanda', flag: 'https://flagcdn.com/w320/rw.png' },
    { name: 'São Tomé and Príncipe', flag: 'https://flagcdn.com/w320/st.png' },
    { name: 'Senegal', flag: 'https://flagcdn.com/w320/sn.png' },
    { name: 'Seychelles', flag: 'https://flagcdn.com/w320/sc.png' },
    { name: 'Sierra Leone', flag: 'https://flagcdn.com/w320/sl.png' },
    { name: 'Somalia', flag: 'https://flagcdn.com/w320/so.png' },
    { name: 'South Africa', flag: 'https://flagcdn.com/w320/za.png' },
    { name: 'South Sudan', flag: 'https://flagcdn.com/w320/ss.png' },
    { name: 'Sudan', flag: 'https://flagcdn.com/w320/sd.png' },
    { name: 'Tanzania', flag: 'https://flagcdn.com/w320/tz.png' },
    { name: 'Togo', flag: 'https://flagcdn.com/w320/tg.png' },
    { name: 'Tunisia', flag: 'https://flagcdn.com/w320/tn.png' },
    { name: 'Uganda', flag: 'https://flagcdn.com/w320/ug.png' },
    { name: 'Zambia', flag: 'https://flagcdn.com/w320/zm.png' },
    { name: 'Zimbabwe', flag: 'https://flagcdn.com/w320/zw.png' }
  ];

  function togglePopup() {
    showPopup = !showPopup;
  }

  function closePopup() {
    showPopup = false;
  }
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
    background: linear-gradient(45deg, #F4A460, #D2691E);
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

  .converage-button {
    text-align: right;
  }

  .converage-button button {
    display: inline-block;
    padding: 5px 15px;
    font-size: 10px;
    background-color: transparent;
    color: white;
    border: 2px solid white;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .converage-button button:hover {
    background-color: white;
    color: #933cad;
    border: 2px solid #933cad;
  }

  .modal {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100%; /* Make the modal cover almost the entire screen */
    background-color: white;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.2);
    /* border-radius: 10px 10px 0 0; */
    z-index: 9999;
    overflow: hidden;
  }

  .modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px;
    background-color: white;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Added shadow */
    position: sticky;
    top: 0;
    z-index: 1;
  }

  .modal-header h2 {
    font-size: 24px;
    margin: 0;
  }

  .modal-header i {
    font-size: 24px;
    cursor: pointer;
  }

  .search-box {
    position: relative;
    width: 95%; /* Reduced the width */
    margin: 10px auto; /* Center the search box */
    display: flex;
    align-items: center;
  }

  .search-box input {
    width: 100%;
    padding: 10px 15px;
    padding-left: 40px; /* Added padding to the left for the icon */
    border-radius: 10px;
    border: 1px solid #ddd;
    font-size: 16px; /* Increased font size */
  }

  .search-box i {
    position: absolute;
    left: 15px;
    font-size: 18px;
    color: #888;
  }

  .country-list {
    padding: 20px;
    padding-top: 0; /* ลด padding เพื่อลดช่องว่างระหว่าง header และ body */
    overflow-y: auto;
    max-height: calc(100% - 150px); /* ปรับความสูงเพื่อให้เหมาะสม */
    padding-bottom: 5px; /* เพิ่ม padding ด้านล่าง */
  }

  .country-item {
    display: flex;
    align-items: center;
    padding: 10px 0;
    font-size: 18px; /* Increased font size */
  }

  .country-item img {
    width: 35px; /* Increased size */
    height: 25px;
    margin-right: 20px; /* Increased spacing */
  }

  .close-btn {
    font-size: 30px; /* Increased size for the close button */
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
        <span>Africa</span>
        <img
          class="package-image"
          src="https://placehold.co/70x50"
          alt="SIM card image"
        />
      </div>
      <div class="package-details">
        <div>
          <span><i class="fas fa-globe"></i> COVERAGE</span>
          <div class="converage-button">
            <button on:click={togglePopup}>36 COUNTRIES</button>
          </div>
        </div>
        <div>
          <span><i class="fas fa-exchange-alt"></i> DATA</span>
          <span>1 GB</span>
        </div>
        <div>
          <span><i class="fas fa-calendar-alt"></i> VALIDITY</span>
          <span>30 Days</span>
        </div>
        <div>
          <span><i class="fas fa-tag"></i> PRICE</span>
          <span>$27.00 USD</span>
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
        <span>$27.00 USD</span>
      </div>
      <div class="price-info">
        <span>REFERRAL REWARD</span>
        <span class="negative">-$3.00 USD</span>
      </div>
      <div class="price-info">
        <span>FINAL PRICE</span>
        <span>$21.00 USD</span>
      </div>
    </div>
  {/if}
</div>

<!-- Bottom Menu with View eSIM Details Button -->
<div class="bottom-menu">
  <button class="view-button" on:click={goToEsimDetailPage}>VIEW eSIM DETAILS</button>
</div>

{#if showPopup}
  <div class="modal">
    <div class="modal-header">
      <h2>Supported Countries</h2>
      <i class="fas fa-times close-btn" on:click={closePopup}></i>
    </div>

    <div class="search-box">
      <i class="fas fa-search"></i>
      <input
        type="text"
        placeholder="Search Country"
        bind:value="{searchQuery}"
      />
    </div>

    <div class="country-list">
      {#each filteredCountries as country}
        <div class="country-item">
          <img src={country.flag} alt={country.name} />
          <span>{country.name}</span>
        </div>
      {/each}
    </div>
  </div>
{/if}