<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  let packages = [];
  let countryName = ""
  onMount(async () => {
    const res = await fetch(`${import.meta.env.VITE_API_URL}/airalo/local-pack-data`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ id: $page.params.id })
    });
    const data = await res.json();
    packages = data.datas;
    countryName = packages[0].country_name
  });
  // const countryName = packages[0].country_name
  // packages = data.data.datas.map(packageData => ({
  //     id: packageData.id,
  //     gradient_end: packageData.gradient_end,
  //     gradient_start: packageData.gradient_start,
  //     is_unlimited: packageData.is_unlimited,
  //     package_airalo_id: packageData.package_airalo_id,
  //     package_data: packageData.package_data,
  //     package_day: packageData.package_day,
  //     package_id: packageData.package_id,
  //     package_img_url: packageData.package_img_url,
  //     package_name: packageData.package_name,
  //     package_price: packageData.package_price,
  //     package_text: packageData.package_text,
  //     package_voice: packageData.package_voice,
  //     plan_type: packageData.plan_type
  // }));
  // console.log(packages)
  // ข้อมูลของกล่องแรก
  let detailsGroup1 = [
    { icon: 'fas fa-globe', label: 'Coverage', value: 'Thailand' },
    { icon: 'fas fa-exchange-alt', label: 'Data', value: 'Unlimited' },
    { icon: 'fas fa-phone', label: 'Calls', value: 'Unlimited' },
    { icon: 'fas fa-calendar-alt', label: 'Validity', value: '15 Days' },
    { icon: 'fas fa-tag', label: 'Price', value: '$19.95 USD' }
  ];

  // ข้อมูลของกล่องที่สอง
  let detailsGroup2 = [
    { icon: 'fas fa-globe', label: 'Coverage', value: 'Thailand' },
    { icon: 'fas fa-exchange-alt', label: 'Data', value: '50 GB' },
    { icon: 'fas fa-phone', label: 'Calls', value: '100 Mins' },
    { icon: 'fas fa-calendar-alt', label: 'Validity', value: '10 Days' },
    { icon: 'fas fa-tag', label: 'Price', value: '$9.90 USD' }
  ];

  import { goto } from '$app/navigation';

  function goToBuyPage(packageId,id) {
    goto('/local-esim-package/'+packageId+'/buy-page/'+id);
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

  /* เพิ่มช่องว่างระหว่าง header และ body */
  .card {
    margin-top: 20px; /* เพิ่มช่องว่างด้านบนของ body */
  }

  /* สไตล์ของการ์ดที่สอง (พื้นหลังสีน้ำเงิน) */
  .card-blue {
    background: linear-gradient(45deg, #1e3a8a, #2563eb);
  }
</style>

<div class="top-menu">
  <a href="javascript:history.back()">
    <div class="back-arrow">
      <i class="fas fa-arrow-left"></i>
    </div>
  </a>
  <h1>{countryName}</h1>
</div>

<div class="container">
  <!-- Header พร้อมลูกศรสำหรับกลับ -->
  <!-- <div class="header">
    <a href="javascript:history.back()">
      <i class="fas fa-arrow-left"></i>
    </a>
    <h1>Thailand</h1>
  </div> -->
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
          <span>{packageData.country_name}</span>
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
            <i class="fas fa-phone icon"></i>
            <span>Calls</span>
          </div>
          <span>{packageData.package_voice} MINS</span>
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
  <!-- <div class="card" style="background: linear-gradient(45deg, #5a2e90, #933cad);">
    <h2>dtac</h2>
    <img src="https://placehold.co/100x60" alt="Tourist SIM card with Tuk-Tuk and Thailand flag" />
    <div class="details-group">
      {#each detailsGroup1 as detail}
        <div class="details">
          <div class="label-value">
            <i class={detail.icon + " icon"}></i>
            <span>{detail.label}</span>
          </div>
          <span>{detail.value}</span>
        </div>
      {/each}
    </div>
    <div class="buy-now">
      <button on:click={goToBuyPage}>BUY NOW</button>
    </div>
  </div> -->

  <!-- การ์ดที่ 2 -->
  <!-- <div class="card card-blue">
    <h2>dtac</h2>
    <img src="https://placehold.co/100x60" alt="Tourist SIM card with Tuk-Tuk and Thailand flag" />
    <div class="details-group">
      {#each detailsGroup2 as detail}
        <div class="details">
          <div class="label-value">
            <i class={detail.icon + " icon"}></i>
            <span>{detail.label}</span>
          </div>
          <span>{detail.value}</span>
        </div>
      {/each}
    </div>
    <div class="buy-now">
      <button on:click={goToBuyPage}>BUY NOW</button>
    </div>
  </div> -->
</div>