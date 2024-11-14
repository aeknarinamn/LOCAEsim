<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';

  const apiUrl = import.meta.env.VITE_API_URL;

  let showPopup = false;
  let packages = [];
  let searchQuery = ''; // เก็บค่าที่ค้นหา
  let supportedCountries = []
  let supportedCountrieNetworks = []
  let showNetworkPopup = false; // ตัวแปรสำหรับ Popup ใหม่
  let id = ""
  let packageId = ""
  
  onMount(async () => {
    // console.log($page.params.id)
    const res = await fetch(`${import.meta.env.VITE_API_URL}/airalo/regional-pack-data-detail`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ id: $page.params.packageId })
    });
    const data = await res.json();
    packages = data.datas;
    id = packages.package_id
    packageId = packages.id
  });

  async function fetchCountries() {
      try {
          const response = await fetch(`${apiUrl}/airalo/list-regional-pack-data-country`, {
              method: 'POST',
              headers: {
                  'Content-Type': 'application/json',
              },
              body: JSON.stringify({
                id : $page.params.id
              }),
          });
          const datas = await response.json();
          supportedCountries = datas.datas.map(country => ({
              name: country.country_name,
              flag: country.country_image_url
          }));
      } catch (error) {
          console.error('Error fetching popular countries:', error);
      }
  }

  async function fetchNetworks() {
      try {
          const response = await fetch(`${apiUrl}/airalo/list-regional-pack-data-coverage`, {
              method: 'POST',
              headers: {
                  'Content-Type': 'application/json',
              },
              body: JSON.stringify({
                id : $page.params.id
              }),
          });
          const datas = await response.json();
          supportedCountrieNetworks = datas.datas
      } catch (error) {
          console.error('Error fetching popular countries:', error);
      }
  }

  onMount(() => {
    fetchCountries();
    fetchNetworks();
  });

  // ฟิลเตอร์ประเทศตามการค้นหา
  $: filteredCountries = supportedCountries.filter((country) =>
    country.name.toLowerCase().includes(searchQuery.toLowerCase())
  );

  $: filteredNetworks = supportedCountrieNetworks.filter((network) =>
    network.country_name.toLowerCase().includes(searchQuery.toLowerCase())
  );

  function togglePopup() {
    showPopup = !showPopup;
  }

  function closePopup() {
    showPopup = false;
  }

  function toggleNetworkPopup() {
    showNetworkPopup = !showNetworkPopup;
  }

  import { goto } from '$app/navigation';

  function goToCheckOutPage() {
    goto('/regional-esim-package/'+id+'/checkout-page/'+packageId);
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
    background: linear-gradient(45deg, #F4A460, #D2691E);
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
    background: linear-gradient(45deg, #F4A460, #D2691E);
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

  /* สไตล์สำหรับ Popup ใหม่ */
  .network-modal {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100%;
    background-color: white;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.2);
    z-index: 9999;
    overflow: hidden;
  }

  .network-modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px;
    background-color: white;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    position: sticky;
    top: 0;
    z-index: 1;
  }

  .network-modal-header h2 {
    font-size: 24px;
    margin: 0;
  }

  .network-modal-header i {
    font-size: 24px;
    cursor: pointer;
  }

  .network-search-box {
    position: relative;
    width: 95%;
    margin: 10px auto;
    display: flex;
    align-items: center;
  }

  .network-search-box input {
    width: 100%;
    padding: 10px 15px;
    padding-left: 40px;
    border-radius: 10px;
    border: 1px solid #ddd;
    font-size: 16px;
  }

  .network-search-box i {
    position: absolute;
    left: 15px;
    font-size: 18px;
    color: #888;
  }

  .network-country-list {
    padding: 20px;
    padding-top: 0;
    overflow-y: auto;
    max-height: calc(100% - 150px);
    padding-bottom: 5px;
  }

  /* สไตล์สำหรับการแสดงผลชื่อเครือข่ายและกล่อง 4G */
  .network-country-item {
    display: flex;
    align-items: center;
    padding: 10px 0;
    font-size: 18px;
  }

  .network-country-item img {
    width: 35px;
    height: 25px;
    margin-right: 20px;
  }

  /* ป้องกันไม่ให้ country_name ไปทับ network_details */
  .network-country-item span {
    flex-grow: 1; /* ให้ country_name ขยายเต็มพื้นที่ที่เหลือ */
  }

  .network-details {
    display: flex;
    flex-direction: column;
    align-items: flex-end; /* ชิดขวา */
  }

  /* จัดให้ network_name และกล่อง 4G ชิดกัน */
  .network-name {
    display: inline-flex; /* ใช้ inline-flex เพื่อให้จัดเรียงอยู่ชิดกัน */
    align-items: center;
    font-size: 16px;
    margin-bottom: 4px;
  }

  .network-name span {
    margin-left: 8px;
    padding: 2px 6px;
    border: 1px solid #333;
    border-radius: 4px;
    font-size: 12px;
    font-weight: bold;
    display: inline-block; /* ทำให้กล่อง 4G มีขนาดตามเนื้อหา */
  }

  .network-close-btn {
    font-size: 30px;
  }

  /* เพิ่มสไตล์สำหรับเว้นระยะไอคอน */
  .icon-spacing {
    margin-left: 8px; /* ปรับขนาดตามต้องการ */
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
      <div class="converage-button">
        <button on:click={togglePopup}>{supportedCountries.length} COUNTRIES</button>
      </div>
    </div>
    <div>
      <span><i class="fas fa-exchange-alt"></i> DATA</span>
      <span>{packages.package_data}</span>
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

  <div class="info-item" on:click={toggleNetworkPopup}>
    <span><i class="fas fa-signal"></i> NETWORK</span>
    <span>Check Available Networks<i class="fas fa-chevron-right icon-spacing"></i></span>
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
    <span class="price">${packages.package_price} USD</span>
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

<!-- Popup ใหม่สำหรับ Network -->
{#if showNetworkPopup}
<div class="network-modal">
  <div class="network-modal-header">
    <h2>Network</h2>
    <i class="fas fa-times network-close-btn" on:click={toggleNetworkPopup}></i>
  </div>

  <div class="network-search-box">
    <i class="fas fa-search"></i>
    <input
      type="text"
      placeholder="Country Name"
      bind:value="{searchQuery}"
    />
  </div>

  <div class="network-country-list">
    {#each filteredNetworks as coverage}
      <div class="network-country-item">
        <img src={coverage.country_image_url} alt={coverage.country_name} />
        <span>{coverage.country_name}</span>
        <div class="network-details">
          {#each coverage.network as network}
            <div class="network-name">
              {network.network_name}
              <span>{network.network_type}</span>
            </div>
          {/each}
        </div>
      </div>
    {/each}
  </div>
</div>
{/if}