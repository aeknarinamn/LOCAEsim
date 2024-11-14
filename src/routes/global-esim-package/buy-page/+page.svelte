<script>
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

  import { goto } from '$app/navigation';

  function goToCheckOutPage() {
    goto('/global-esim-package/checkout-page');
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
    background: linear-gradient(45deg, #1E90FF, #00BFFF);
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

  .container img {
    width: 100%;
    border-radius: 16px;
    margin-bottom: 16px;
  }

  .details {
    background: linear-gradient(45deg, #1E90FF, #00BFFF);
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
  <a href="javascript:history.back()">
    <div class="back-arrow">
      <i class="fas fa-arrow-left"></i>
    </div>
  </a>
  <h1>Africa</h1>
</div>

<!-- Container including top menu -->
<div class="container">
  <!-- <div class="header">
    <a href="javascript:history.back()">
      <div class="back-arrow">
        <i class="fas fa-arrow-left"></i>
      </div>
    </a>
    <h1>dtac</h1>
  </div> -->

  <img
    src="https://placehold.co/400x200"
    alt="Image of a colorful tuk-tuk with a background promoting tourist SIM card"
  />

  <div class="details">
    <div>
      <span><i class="fas fa-globe"></i> COVERAGE</span>
      <div class="converage-button">
        <button on:click={togglePopup}>135 COUNTRIES</button>
      </div>
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
      <span>$9.00 USD</span>
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
    <span>Check Available Networks</span>
  </div>
  <div class="info-item">
    <span><i class="fas fa-file-alt"></i> PLAN TYPE</span>
    <span>Data Only</span>
  </div>
  <div class="info-item">
    <span><i class="fas fa-tasks"></i> ACTIVATION POLICY</span>
    <span>The validity period starts when the eSIM connects to any supported network/s.</span>
  </div>
  <div class="info-item">
    <span><i class="fas fa-info-circle"></i> OTHER INFO</span>
    <span>Restrictions apply to extended usage(over 91 days) in Turkey according to the local legislation.</span>
  </div>

  <!-- Show More Button -->
  <div class="show-more">
    <button>SHOW MORE</button>
  </div>
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
    <span class="price">$9.00 USD</span>
  </div>
  <button class="buy-button" on:click={goToCheckOutPage}>BUY</button>
</div>

<!-- Popup Modal -->
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