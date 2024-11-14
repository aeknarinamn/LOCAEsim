<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';

  let packages = [];
  let supportedCountries = [];
  let regionalName = "";
  const apiUrl = import.meta.env.VITE_API_URL;

  onMount(async () => {
    const res = await fetch(`${import.meta.env.VITE_API_URL}/airalo/regional-pack-data`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ id: $page.params.id })
    });
    const data = await res.json();
    packages = data.datas;
    regionalName = packages[0].regional_name
  });

  // ข้อมูลของกล่องแรก
  let detailsGroup1 = [
    { icon: 'fas fa-globe', label: 'Coverage', value: 'Thailand' },
    { icon: 'fas fa-exchange-alt', label: 'Data', value: '1 GB' },
    { icon: 'fas fa-calendar-alt', label: 'Validity', value: '30 Days' },
    { icon: 'fas fa-tag', label: 'Price', value: '$27.00 USD' }
  ];

  // ข้อมูลของกล่องที่สอง
  let detailsGroup2 = [
    { icon: 'fas fa-globe', label: 'Coverage', value: 'Thailand' },
    { icon: 'fas fa-exchange-alt', label: 'Data', value: '3 GB' },
    { icon: 'fas fa-calendar-alt', label: 'Validity', value: '30 Days' },
    { icon: 'fas fa-tag', label: 'Price', value: '$59.00 USD' }
  ];

  let showPopup = false;
  let searchQuery = ''; // เก็บค่าที่ค้นหา

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

  onMount(() => {
    fetchCountries();
  });

  // ฟิลเตอร์ประเทศตามการค้นหา
  $: filteredCountries = supportedCountries.filter((country) =>
    country.name.toLowerCase().includes(searchQuery.toLowerCase())
  );

  // ข้อมูลประเทศที่รองรับพร้อม URL รูปธง
  // let supportedCountries = [
  //   { name: 'Algeria', flag: 'https://flagcdn.com/w320/dz.png' },
  //   { name: 'Angola', flag: 'https://flagcdn.com/w320/ao.png' },
  //   { name: 'Benin', flag: 'https://flagcdn.com/w320/bj.png' },
  //   { name: 'Botswana', flag: 'https://flagcdn.com/w320/bw.png' },
  //   { name: 'Burkina Faso', flag: 'https://flagcdn.com/w320/bf.png' },
  //   { name: 'Burundi', flag: 'https://flagcdn.com/w320/bi.png' },
  //   { name: 'Cabo Verde', flag: 'https://flagcdn.com/w320/cv.png' },
  //   { name: 'Cameroon', flag: 'https://flagcdn.com/w320/cm.png' },
  //   { name: 'Central African Republic', flag: 'https://flagcdn.com/w320/cf.png' },
  //   { name: 'Chad', flag: 'https://flagcdn.com/w320/td.png' },
  //   { name: 'Comoros', flag: 'https://flagcdn.com/w320/km.png' },
  //   { name: 'Congo', flag: 'https://flagcdn.com/w320/cg.png' },
  //   { name: 'Democratic Republic of The Congo', flag: 'https://flagcdn.com/w320/cd.png' },
  //   { name: 'Djibouti', flag: 'https://flagcdn.com/w320/dj.png' },
  //   { name: 'Egypt', flag: 'https://flagcdn.com/w320/eg.png' },
  //   { name: 'Equatorial Guinea', flag: 'https://flagcdn.com/w320/gq.png' },
  //   { name: 'Eritrea', flag: 'https://flagcdn.com/w320/er.png' },
  //   { name: 'Eswatini', flag: 'https://flagcdn.com/w320/sz.png' },
  //   { name: 'Ethiopia', flag: 'https://flagcdn.com/w320/et.png' },
  //   { name: 'Gabon', flag: 'https://flagcdn.com/w320/ga.png' },
  //   { name: 'Gambia', flag: 'https://flagcdn.com/w320/gm.png' },
  //   { name: 'Ghana', flag: 'https://flagcdn.com/w320/gh.png' },
  //   { name: 'Guinea', flag: 'https://flagcdn.com/w320/gn.png' },
  //   { name: 'Guinea-Bissau', flag: 'https://flagcdn.com/w320/gw.png' },
  //   { name: 'Ivory Coast (Côte d\'Ivoire)', flag: 'https://flagcdn.com/w320/ci.png' },
  //   { name: 'Kenya', flag: 'https://flagcdn.com/w320/ke.png' },
  //   { name: 'Lesotho', flag: 'https://flagcdn.com/w320/ls.png' },
  //   { name: 'Liberia', flag: 'https://flagcdn.com/w320/lr.png' },
  //   { name: 'Libya', flag: 'https://flagcdn.com/w320/ly.png' },
  //   { name: 'Madagascar', flag: 'https://flagcdn.com/w320/mg.png' },
  //   { name: 'Malawi', flag: 'https://flagcdn.com/w320/mw.png' },
  //   { name: 'Mali', flag: 'https://flagcdn.com/w320/ml.png' },
  //   { name: 'Mauritania', flag: 'https://flagcdn.com/w320/mr.png' },
  //   { name: 'Mauritius', flag: 'https://flagcdn.com/w320/mu.png' },
  //   { name: 'Morocco', flag: 'https://flagcdn.com/w320/ma.png' },
  //   { name: 'Mozambique', flag: 'https://flagcdn.com/w320/mz.png' },
  //   { name: 'Namibia', flag: 'https://flagcdn.com/w320/na.png' },
  //   { name: 'Niger', flag: 'https://flagcdn.com/w320/ne.png' },
  //   { name: 'Nigeria', flag: 'https://flagcdn.com/w320/ng.png' },
  //   { name: 'Rwanda', flag: 'https://flagcdn.com/w320/rw.png' },
  //   { name: 'São Tomé and Príncipe', flag: 'https://flagcdn.com/w320/st.png' },
  //   { name: 'Senegal', flag: 'https://flagcdn.com/w320/sn.png' },
  //   { name: 'Seychelles', flag: 'https://flagcdn.com/w320/sc.png' },
  //   { name: 'Sierra Leone', flag: 'https://flagcdn.com/w320/sl.png' },
  //   { name: 'Somalia', flag: 'https://flagcdn.com/w320/so.png' },
  //   { name: 'South Africa', flag: 'https://flagcdn.com/w320/za.png' },
  //   { name: 'South Sudan', flag: 'https://flagcdn.com/w320/ss.png' },
  //   { name: 'Sudan', flag: 'https://flagcdn.com/w320/sd.png' },
  //   { name: 'Tanzania', flag: 'https://flagcdn.com/w320/tz.png' },
  //   { name: 'Togo', flag: 'https://flagcdn.com/w320/tg.png' },
  //   { name: 'Tunisia', flag: 'https://flagcdn.com/w320/tn.png' },
  //   { name: 'Uganda', flag: 'https://flagcdn.com/w320/ug.png' },
  //   { name: 'Zambia', flag: 'https://flagcdn.com/w320/zm.png' },
  //   { name: 'Zimbabwe', flag: 'https://flagcdn.com/w320/zw.png' }
  // ];

  function togglePopup() {
    showPopup = !showPopup;
  }

  function closePopup() {
    showPopup = false;
  }

  import { goto } from '$app/navigation';

  function goToBuyPage(id,packageId) {
    goto('/regional-esim-package/'+id+'/buy-page/'+packageId);
  }
</script>

<!-- Font Awesome สำหรับการใช้งานไอคอน -->
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"
/>

<style>
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f0f0f0;
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

  .container {
    max-width: 400px;
    margin: 50px auto;
    background-color: white;
    border-radius: 10px;
    /* box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); */
    overflow: hidden;
  }

  .header {
    padding: 15px;
    display: flex;
    align-items: center;
    background-color: white;
    border-bottom: 1px solid #ddd;
  }

  .header a {
    text-decoration: none;
    color: inherit; /* ให้สีตรงกับ parent */
    margin-right: 10px;
    display: flex;
    align-items: center;
  }

  .header i {
    font-size: 20px;
    cursor: pointer;
  }

  .header h1 {
    margin: 0;
    font-size: 22px;
    color: #333;
  }

  .card {
    position: relative;
    color: white;
    padding: 20px;
    border-radius: 15px;
    margin-bottom: 20px; /* เพิ่มช่องว่างระหว่างกล่อง */
  }

  .card img {
    position: absolute;
    top: 10px;
    right: 10px;
    width: 100px; /* ขนาดของรูป */
    border-radius: 8px;
  }

  .details-group {
    margin-top: 20px;
  }

  .details {
    display: flex;
    justify-content: space-between;
    padding: 10px 0;
    border-top: 1px solid rgba(255, 255, 255, 0.2);
  }

  .details div:first-child {
    border-top: none;
  }

  .details .label-value {
    display: flex;
    align-items: center; /* จัดให้ label ชิดกับไอคอน */
  }

  .details .icon {
    margin-right: 5px; /* ตั้งระยะห่างจากไอคอนถึง label เป็น 5px */
    color: white;
    font-size: 20px;
  }

  .details span {
    font-size: 16px;
  }

  .buy-now {
    padding: 10px;
    text-align: center;
    background-color: transparent;
    margin-top: 20px;
  }

  .buy-now button {
    width: 100%;
    max-width: 95%;
    padding: 10px 20px;
    font-size: 16px;
    background-color: transparent;
    color: white;
    border: 2px solid white;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .buy-now button:hover {
    background-color: white;
    color: #933cad;
    border: 2px solid #933cad;
  }

  .converage-button {
    text-align: right;
    background-color: transparent;
  }

  .converage-button button {
    display: inline-block; /* ขนาดปุ่มจะพอดีกับข้อความ */
    padding: 5px 15px; /* ลดขนาด padding เพื่อให้ปุ่มเล็กลง */
    font-size: 10px; /* ลดขนาด font */
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

  /* เพิ่มช่องว่างระหว่าง header และ body */
  .card {
    margin-top: 20px; /* เพิ่มช่องว่างด้านบนของ body */
  }

  /* สไตล์ของการ์ดที่สอง (พื้นหลังสีน้ำเงิน) */
  .card-blue {
    background: linear-gradient(45deg, #F4A460, #D2691E);
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

<div class="top-menu">
  <a href="javascript:history.back()">
    <div class="back-arrow">
      <i class="fas fa-arrow-left"></i>
    </div>
  </a>
  <h1>{regionalName}</h1>
</div>

<div class="container">
  <!-- Header พร้อมลูกศรสำหรับกลับ -->
  <!-- <div class="header">
    <a href="javascript:history.back()">
      <i class="fas fa-arrow-left"></i>
    </a>
    <h1>Thailand</h1>
  </div> -->

  <!-- การ์ดที่ 1 -->
  {#each packages as packageData}
    <div class="card" style="background: linear-gradient(45deg, {packageData.gradient_start}, {packageData.gradient_end});">
      <h2>{packageData.brand_title}</h2>
      <img src="{packageData.package_img_url}" alt="Tourist SIM card with Tuk-Tuk and Thailand flag" onerror="this.onerror=null; this.src='/images/default-esim.png'"/>
      <div class="details-group">
        <div class="details">
          <div class="label-value">
            <i class="fas fa-globe icon"></i>
            <span>Coverage</span>
          </div>
          <div class="converage-button">
            <button on:click={togglePopup}>{supportedCountries.length} COUNTRIES</button>
          </div>
        </div>
        <div class="details">
          <div class="label-value">
            <i class="fas fa-exchange-alt icon"></i>
            <span>Data</span>
          </div>
          <span>{packageData.package_data}</span>
        </div>
        <div class="details">
          <div class="label-value">
            <i class="fas fa-calendar-alt icon"></i>
            <span>Validity</span>
          </div>
          <span>{packageData.package_day} DAYS</span>
        </div>
        <div class="details">
          <div class="label-value">
            <i class="fas fa-tag icon"></i>
            <span>Price</span>
          </div>
          <span>${packageData.package_price} USD</span>
        </div>
        <!-- {#each detailsGroup1 as detail}
          <div class="details">
            <div class="label-value">
              <i class={detail.icon + " icon"}></i>
              <span>{detail.label}</span>
            </div>
            {#if detail.label == 'Coverage'}
              <div class="converage-button">
                <button on:click={togglePopup}>36 COUNTRIES</button>
              </div>
            {:else}
              <span>{detail.value}</span>
            {/if}
          </div>
        {/each} -->
      </div>
      <div class="buy-now">
        <button on:click={goToBuyPage(packageData.package_id,packageData.id)}>BUY NOW</button>
      </div>
    </div>
  {/each}

  <!-- การ์ดที่ 2 -->
  <!-- <div class="card card-blue">
    <h2>Hello Africa</h2>
    <img src="https://placehold.co/100x60" alt="Tourist SIM card with Tuk-Tuk and Thailand flag" />
    <div class="details-group">
      {#each detailsGroup2 as detail}
        <div class="details">
          <div class="label-value">
            <i class={detail.icon + " icon"}></i>
            <span>{detail.label}</span>
          </div>
          {#if detail.label == 'Coverage'}
            <div class="converage-button">
              <button>36 COUNTRIES</button>
            </div>
          {:else}
            <span>{detail.value}</span>
          {/if}
        </div>
      {/each}
    </div>
    <div class="buy-now">
      <button on:click={goToBuyPage}>BUY NOW</button>
    </div>
  </div> -->

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
</div>