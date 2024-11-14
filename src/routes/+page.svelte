<script>
    const apiUrl = import.meta.env.VITE_API_URL;
    let searchQuery = '';

    import { goto } from '$app/navigation';
    import { onMount } from 'svelte';

    function goToBuyPage(id,packageId) {
        goto('/regional-esim-package/'+id+'/buy-page/'+packageId);
    }

    // กำหนดแท็บที่เลือกได้ในปัจจุบัน (เริ่มต้นที่ Local eSIMs)
    let selectedTab = 'Local eSIMs';
    let showPopup = false;
    let popularCountries = [];
    let regionals = [];
    let globalPackages = [];
    let supportedGlobalCountries = [];

    // ข้อมูลของกล่องแรก
    let detailsGroup1 = [
        { icon: 'fas fa-globe', label: 'Coverage', value: 'Thailand' },
        { icon: 'fas fa-exchange-alt', label: 'Data', value: '1 GB' },
        { icon: 'fas fa-calendar-alt', label: 'Validity', value: '7 Days' },
        { icon: 'fas fa-tag', label: 'Price', value: '$9.00 USD' }
    ];

    // ข้อมูลของกล่องที่สอง
    let detailsGroup2 = [
        { icon: 'fas fa-globe', label: 'Coverage', value: 'Thailand' },
        { icon: 'fas fa-exchange-alt', label: 'Data', value: '2 GB' },
        { icon: 'fas fa-calendar-alt', label: 'Validity', value: '15 Days' },
        { icon: 'fas fa-tag', label: 'Price', value: '$17.00 USD' }
    ];

    async function fetchPopularCountries() {
        try {
            const response = await fetch(`${apiUrl}/airalo/list-local-country`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                }),
            });
            const data = await response.json();
            // console.log(data)
            popularCountries = data.datas.map(country => ({
                name: country.country_name,
                flag: country.country_flag_image_url,  // Assuming the API provides a URL for the flag image
                id: country.id
            }));
        } catch (error) {
            console.error('Error fetching popular countries:', error);
        }
    }

    async function fetchRegional() {
        try {
            const response = await fetch(`${apiUrl}/airalo/list-regional`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                }),
            });
            const data = await response.json();
            regionals = data.datas.map(regional => ({
                name: regional.regional_name,
                icon: regional.regional_image_url,  // Assuming the API provides a URL for the flag image
                id: regional.id
            }));
        } catch (error) {
            console.error('Error fetching regional:', error);
        }
    }

    async function fetchGlobalPackages() {
        try {
            const response = await fetch(`${apiUrl}/airalo/global-pack-data`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                }),
            });
            const data = await response.json();
            globalPackages = data.datas;
        } catch (error) {
            console.error('Error fetching global package:', error);
        }
    }

    async function fetchCountries() {
      try {
          const response = await fetch(`${apiUrl}/airalo/list-global-pack-data-country`, {
              method: 'POST',
              headers: {
                  'Content-Type': 'application/json',
              },
              body: JSON.stringify({

              }),
          });
          const datas = await response.json();
          supportedGlobalCountries = datas.datas.map(country => ({
              name: country.country_name,
              flag: country.country_image_url
          }));
      } catch (error) {
          console.error('Error fetching popular countries:', error);
      }
  }

    onMount(() => {
        fetchPopularCountries();
        fetchRegional();
        fetchGlobalPackages();
        fetchCountries();
    });

    // let popularCountries = [
    //   { name: 'Thailand', flag: '🇹🇭', url: '/local-esim-package' },
    //   { name: 'Vietnam', flag: '🇻🇳', url: '/local-esim-package' },
    //   { name: 'Japan', flag: '🇯🇵', url: '/local-esim-package' },
    //   { name: 'Singapore', flag: '🇸🇬', url: '/local-esim-package' },
    //   { name: 'Indonesia', flag: '🇮🇩', url: '/local-esim-package' },
    //   { name: 'China', flag: '🇨🇳', url: '/local-esim-package' },
    //   { name: 'Cambodia', flag: '🇰🇭', url: '/local-esim-package' }
    // ];

    // let regionalCountries = [
    //     { name: 'Africa', icon: 'fa-solid fa-globe-africa', url: '/regional-esim-package' },
    //     { name: 'Asia', icon: 'fa-solid fa-globe-asia', url: '/regional-esim-package' },
    //     { name: 'Caribbean Islands', icon: 'fa-solid fa-umbrella-beach', url: '/regional-esim-package' },
    //     { name: 'Europe', icon: 'fa-solid fa-globe-europe', url: '/regional-esim-package' },
    //     { name: 'Latin America', icon: 'fa-solid fa-globe-americas', url: '/regional-esim-package' },
    //     { name: 'Middle East and North Africa', icon: 'fa-solid fa-mosque', url: '/regional-esim-package' },
    //     { name: 'North America', icon: 'fa-solid fa-globe-americas', url: '/regional-esim-package' },
    //     { name: 'Oceania', icon: 'fa-solid fa-globe', url: '/regional-esim-package' }
    // ];

    

    // ฟิลเตอร์ประเทศตามการค้นหา
    $: filteredCountries = supportedGlobalCountries.filter((country) =>
        country.name.toLowerCase().includes(searchQuery.toLowerCase())
    );

    // ข้อมูลประเทศที่รองรับพร้อม URL รูปธง
    // let supportedCountries = [
    //     { name: 'Algeria', flag: 'https://flagcdn.com/w320/dz.png' },
    //     { name: 'Angola', flag: 'https://flagcdn.com/w320/ao.png' },
    //     { name: 'Benin', flag: 'https://flagcdn.com/w320/bj.png' },
    //     { name: 'Botswana', flag: 'https://flagcdn.com/w320/bw.png' },
    //     { name: 'Burkina Faso', flag: 'https://flagcdn.com/w320/bf.png' },
    //     { name: 'Burundi', flag: 'https://flagcdn.com/w320/bi.png' },
    //     { name: 'Cabo Verde', flag: 'https://flagcdn.com/w320/cv.png' },
    //     { name: 'Cameroon', flag: 'https://flagcdn.com/w320/cm.png' },
    //     { name: 'Central African Republic', flag: 'https://flagcdn.com/w320/cf.png' },
    //     { name: 'Chad', flag: 'https://flagcdn.com/w320/td.png' },
    //     { name: 'Comoros', flag: 'https://flagcdn.com/w320/km.png' },
    //     { name: 'Congo', flag: 'https://flagcdn.com/w320/cg.png' },
    //     { name: 'Democratic Republic of The Congo', flag: 'https://flagcdn.com/w320/cd.png' },
    //     { name: 'Djibouti', flag: 'https://flagcdn.com/w320/dj.png' },
    //     { name: 'Egypt', flag: 'https://flagcdn.com/w320/eg.png' },
    //     { name: 'Equatorial Guinea', flag: 'https://flagcdn.com/w320/gq.png' },
    //     { name: 'Eritrea', flag: 'https://flagcdn.com/w320/er.png' },
    //     { name: 'Eswatini', flag: 'https://flagcdn.com/w320/sz.png' },
    //     { name: 'Ethiopia', flag: 'https://flagcdn.com/w320/et.png' },
    //     { name: 'Gabon', flag: 'https://flagcdn.com/w320/ga.png' },
    //     { name: 'Gambia', flag: 'https://flagcdn.com/w320/gm.png' },
    //     { name: 'Ghana', flag: 'https://flagcdn.com/w320/gh.png' },
    //     { name: 'Guinea', flag: 'https://flagcdn.com/w320/gn.png' },
    //     { name: 'Guinea-Bissau', flag: 'https://flagcdn.com/w320/gw.png' },
    //     { name: 'Ivory Coast (Côte d\'Ivoire)', flag: 'https://flagcdn.com/w320/ci.png' },
    //     { name: 'Kenya', flag: 'https://flagcdn.com/w320/ke.png' },
    //     { name: 'Lesotho', flag: 'https://flagcdn.com/w320/ls.png' },
    //     { name: 'Liberia', flag: 'https://flagcdn.com/w320/lr.png' },
    //     { name: 'Libya', flag: 'https://flagcdn.com/w320/ly.png' },
    //     { name: 'Madagascar', flag: 'https://flagcdn.com/w320/mg.png' },
    //     { name: 'Malawi', flag: 'https://flagcdn.com/w320/mw.png' },
    //     { name: 'Mali', flag: 'https://flagcdn.com/w320/ml.png' },
    //     { name: 'Mauritania', flag: 'https://flagcdn.com/w320/mr.png' },
    //     { name: 'Mauritius', flag: 'https://flagcdn.com/w320/mu.png' },
    //     { name: 'Morocco', flag: 'https://flagcdn.com/w320/ma.png' },
    //     { name: 'Mozambique', flag: 'https://flagcdn.com/w320/mz.png' },
    //     { name: 'Namibia', flag: 'https://flagcdn.com/w320/na.png' },
    //     { name: 'Niger', flag: 'https://flagcdn.com/w320/ne.png' },
    //     { name: 'Nigeria', flag: 'https://flagcdn.com/w320/ng.png' },
    //     { name: 'Rwanda', flag: 'https://flagcdn.com/w320/rw.png' },
    //     { name: 'São Tomé and Príncipe', flag: 'https://flagcdn.com/w320/st.png' },
    //     { name: 'Senegal', flag: 'https://flagcdn.com/w320/sn.png' },
    //     { name: 'Seychelles', flag: 'https://flagcdn.com/w320/sc.png' },
    //     { name: 'Sierra Leone', flag: 'https://flagcdn.com/w320/sl.png' },
    //     { name: 'Somalia', flag: 'https://flagcdn.com/w320/so.png' },
    //     { name: 'South Africa', flag: 'https://flagcdn.com/w320/za.png' },
    //     { name: 'South Sudan', flag: 'https://flagcdn.com/w320/ss.png' },
    //     { name: 'Sudan', flag: 'https://flagcdn.com/w320/sd.png' },
    //     { name: 'Tanzania', flag: 'https://flagcdn.com/w320/tz.png' },
    //     { name: 'Togo', flag: 'https://flagcdn.com/w320/tg.png' },
    //     { name: 'Tunisia', flag: 'https://flagcdn.com/w320/tn.png' },
    //     { name: 'Uganda', flag: 'https://flagcdn.com/w320/ug.png' },
    //     { name: 'Zambia', flag: 'https://flagcdn.com/w320/zm.png' },
    //     { name: 'Zimbabwe', flag: 'https://flagcdn.com/w320/zw.png' }
    // ];

    function togglePopup() {
        showPopup = !showPopup;
    }

    function closePopup() {
        showPopup = false;
    }
  
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

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">

<style>
    body, html {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
    }
  
    .container {
      font-family: 'Roboto', sans-serif;
      max-width: 420px;
      margin: 0 auto;
      padding: 20px;
      background-color: rgba(247, 248, 250, 0.9);
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
  
    .header h2 {
      font-size: 1.6rem;
      margin: 15px 0;
    }
  
    .search-section {
      margin: 20px 0;
    }
  
    .search-bar {
      width: 100%;
      padding: 12px;
      border: 1px solid #ddd;
      border-radius: 8px;
      font-size: 1rem;
      box-sizing: border-box;
    }
  
    .eSIM-options {
      display: flex;
      justify-content: space-between;
      margin: 10px 0;
      gap: 10px;
    }
  
    .esim-button {
      flex: 1;
      padding: 12px;
      border: none;
      border-radius: 8px;
      background-color: #87CEFA;
      color: white;
      cursor: pointer;
      font-size: 1rem;
      transition: background-color 0.3s ease;
    }
  
    .esim-button.active {
      background-color: #5DADE2;
    }
  
    .esim-button:hover {
      background-color: #3498DB;
    }
  
    .banner-slide {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 15px;
      border-radius: 10px;
      margin-top: 20px;
      transition: background-color 0.5s ease;
    }
  
    .banner-img {
      font-size: 2rem;
    }
  
    .banner-slide p {
      font-size: 1.1rem;
      font-weight: bold;
    }
  
    .popular-countries {
      margin-top: 30px;
      margin-bottom: 80px;
    }
  
    .popular-countries h3 {
      font-size: 1.2rem;
      margin-bottom: 10px;
    }
  
    .country-link {
      text-decoration: none;
    }
  
    .country {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 15px;
      background-color: white;
      border-radius: 10px;
      border: 1px solid #eee;
      margin-bottom: 10px;
      color: black; /* สีของข้อความประเทศเป็นสีดำ */
      transition: background-color 0.3s ease;
    }
  
    .country:hover {
      background-color: #f0f0f0;
    }
  
    .chevron {
      font-size: 1.5rem;
      color: #007bff;
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
    }
  
    .menu-item p {
      margin: 5px 0 0 0;
      font-size: 0.9rem;
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

    .global-package {
        margin-bottom: 80px;
    }
</style>
  
<!-- Container หลัก -->
<div class="container">
    
    <!-- ส่วนที่ 1: Header -->
    <div class="header">
      <h2>Hello, Aeknarin</h2>
  
      <div class="search-section">
        <input
          type="text"
          bind:value={searchQuery}
          placeholder="Search data packs for 200+ countries and regions"
          class="search-bar"
        />
      </div>
  
      <div class="eSIM-options">
        <button 
          class="esim-button {selectedTab === 'Local eSIMs' ? 'active' : ''}" 
          on:click={() => selectedTab = 'Local eSIMs'}>
          Local eSIMs
        </button>
        <button 
          class="esim-button {selectedTab === 'Regional eSIMs' ? 'active' : ''}" 
          on:click={() => selectedTab = 'Regional eSIMs'}>
          Regional eSIMs
        </button>
        <button 
          class="esim-button {selectedTab === 'Global eSIMs' ? 'active' : ''}" 
          on:click={() => selectedTab = 'Global eSIMs'}>
          Global eSIMs
        </button>
      </div>
  
      <div class="banner-slide" style="background-color: {banners[currentBanner].color}">
        <span class="banner-img">{banners[currentBanner].img}</span>
        <p>{banners[currentBanner].text}</p>
      </div>
    </div>
    
    <!-- ส่วนที่ 2: รายชื่อประเทศยอดนิยม -->
    {#if selectedTab === 'Local eSIMs'}
        <div class="popular-countries">
        <h3>Popular Countries</h3>
        <!-- {#each popularCountries as country}
            <a class="country-link" href="/local-esim-package/{country.id}" rel="external">
                <div class="country">
                    <img src="{country.flag}" alt="{country.name}" width="25" height="18" />
                    <span>{country.name}</span>
                    <span class="chevron">➔</span>
                </div>
            </a>
        {/each} -->
        {#each popularCountries as country}
            <div class="country-link" on:click={() => goto(`/local-esim-package/${country.id}`)} style="cursor: pointer;">
                <div class="country">
                    <img src="{country.flag}" alt="{country.name}" width="25" height="18" />
                    <span>{country.name}</span>
                    <span class="chevron">➔</span>
                </div>
            </div>
        {/each}
        </div>
    {/if}

    {#if selectedTab === 'Regional eSIMs'}
        <div class="popular-countries">
            <h3>Regional Countries</h3>
            {#each regionals as regional}
                <div class="country-link" on:click={() => goto(`/regional-esim-package/${regional.id}`)} style="cursor: pointer;">
                    <div class="country">
                        <img src="{regional.icon}" alt="{regional.name}" width="25" height="18" />
                        <span>{regional.name}</span>
                        <span class="chevron">➔</span>
                    </div>
                </div>
            {/each}
        </div>
    {/if}

    {#if selectedTab === 'Global eSIMs'}
        <div class="global-package">
            {#each globalPackages as packageData}
                <div class="card" style="background: linear-gradient(45deg, {packageData.gradient_start}, {packageData.gradient_end});">
                <h2>{packageData.brand_title}</h2>
                <img src="{packageData.package_img_url}" alt="Tourist SIM card with Tuk-Tuk and Thailand flag" />
                <div class="details-group">
                    <div class="details">
                    <div class="label-value">
                        <i class="fas fa-globe icon"></i>
                        <span>Coverage</span>
                    </div>
                    <div class="converage-button">
                        <button on:click={togglePopup}>{supportedGlobalCountries.length} COUNTRIES</button>
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
                </div>
                <div class="buy-now">
                    <button on:click={goToBuyPage(packageData.package_id,packageData.id)}>BUY NOW</button>
                </div>
                </div>
            {/each}
            <!-- การ์ดที่ 1 -->
            <!-- <div class="card" style="background: linear-gradient(45deg, #1E90FF, #00BFFF);">
                <h2>Discover</h2>
                <img src="https://placehold.co/100x60" alt="Tourist SIM card with Tuk-Tuk and Thailand flag" />
                <div class="details-group">
                {#each detailsGroup1 as detail}
                    <div class="details">
                    <div class="label-value">
                        <i class={detail.icon + " icon"}></i>
                        <span>{detail.label}</span>
                    </div>
                    {#if detail.label == 'Coverage'}
                        <div class="converage-button">
                        <button on:click={togglePopup}>135 COUNTRIES</button>
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

            <!-- การ์ดที่ 2 -->
            <!-- <div class="card" style="background: linear-gradient(45deg, #1E90FF, #00BFFF);">
                <h2>Discover</h2>
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
                        <button on:click={togglePopup}>135 COUNTRIES</button>
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
        </div>
    {/if}

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
    
    <!-- ส่วนที่ 3: เมนูด้านล่าง -->
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
  
</div>