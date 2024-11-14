<script>
  import { onMount } from "svelte";

  import { goto } from '$app/navigation';

  function goToMyEsimDetailInstructionPage() {
    goto('/my-esim/detail/instruction');
  }

  let iccidNumber = "8965012405032477005";
  let coverage = "Vietnam";
  let remainingData = 1; // Remaining data in GB
  let usedData = 0; // Used data in MB
  let totalData = 1; // Total data in GB

  // ข้อมูลแพ็คเกจ
  let packageDetails = {
    status: "Not Activated",
    validity: "7 Days",
    data : "1 GB",
  };

  // ข้อมูลแพ็กเกจสำหรับการซื้อ
  let topUpPackages = [
    {
      data : "1 GB",
      validity: "7 Days",
      price: "$4.50 USD"
    },
    {
      data : "2 GB",
      validity: "15 Days",
      price: "$7.00 USD"
    }
  ];

  // คำนวณเปอร์เซ็นต์ที่เหลือของ data
  let remainingPercentage = (remainingData / totalData) * 100;

  onMount(() => {
    const circularProgress = document.querySelectorAll(".circular-progress");

    Array.from(circularProgress).forEach((progressBar) => {
      const progressValue = progressBar.querySelector(".percentage");
      const innerCircle = progressBar.querySelector(".inner-circle");
      let startValue = 0,
        endValue = Number(progressBar.getAttribute("data-percentage")),
        speed = 50,
        progressColor = progressBar.getAttribute("data-progress-color");

      const progress = setInterval(() => {
        startValue++;
        progressValue.textContent = `${startValue}%`;
        progressValue.style.color = `${progressColor}`;

        innerCircle.style.backgroundColor = `${progressBar.getAttribute(
          "data-inner-circle-color"
        )}`;

        progressBar.style.background = `conic-gradient(${progressColor} ${
          startValue * 3.6
        }deg,${progressBar.getAttribute("data-bg-color")} 0deg)`;

        if (startValue === endValue) {
          clearInterval(progress);
        }
      }, speed);
    });
  });
</script>

<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"
/>

<style>
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
    max-width: 420px;
    margin: 0 auto;
    padding: 16px;
    font-family: Arial, sans-serif;
    /* background-color: #f4f4f4; */
    margin-top: 50px;
  }

  /* Header Section */
  .header {
    background: linear-gradient(45deg, #d14141, #ef6e6e);
    color: white;
    padding: 20px;
    border-radius: 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
    position: relative;
  }

  .header div {
    max-width: 60%; /* จำกัดความกว้างของข้อความให้ไม่เกิน 60% ของ container เพื่อไม่ให้เกยกับรูป */
  }


  .header h2 {
    font-size: 24px;
    margin: 0;
  }

  .iccid-info {
    margin-top: 10px;
    font-size: 14px;
    opacity: 0.9;
  }

  .header img {
    width: 100px; /* ลดขนาดของรูป */
    height: auto;
    position: absolute;
    right: 20px;
    top: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }

  /* Warning Section */
  .warning {
    background-color: #ffedc2;
    color: #8a6d3b;
    border: 1px solid #faebcc;
    padding: 15px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    font-size: 14px;
    margin-bottom: 20px;
  }

  .warning i {
    font-size: 18px;
    margin-right: 10px;
  }

  /* Installation Section */
  .installation {
    background-color: #fff;
    padding: 15px;
    border-radius: 12px;
    margin-bottom: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }

  .installation p {
    font-size: 16px;
    font-weight: bold;
    margin: 0;
  }

  .installation button {
    background-color: #ef6e6e;
    color: white;
    padding: 10px 20px;
    border-radius: 8px;
    border: none;
    cursor: pointer;
  }

  .installation button:hover {
    background-color: #d9534f;
  }

  /* Data Usage Section */
  .data-usage {
    background-color: #fff;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
  }

  .data-header {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 20px;
    text-align: left;
  }

  .usage-details {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 40px;
  }

  .remaining-data {
    text-align: center;
    color: grey;
    font-size: 14px;
    margin-bottom: 10px;
  }

  .remaining-data .remaining {
    font-size: 24px;
    font-weight: bold;
    color: #d9534f;
  }

  .circular-progress {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }

  .inner-circle {
    position: absolute;
    width: calc(150px - 30px);
    height: calc(150px - 30px);
    border-radius: 50%;
    background-color: lightgrey;
  }

  .percentage {
    position: relative;
    font-size: 1.5rem;
    color: rgb(0, 0, 0, 0.8);
  }

  .data-info {
    text-align: left;
    font-size: 10px;
    color: grey;
  }

  .data-info p {
    margin: 4px 0;
  }

  .data-info strong {
    font-size: 13px;
    color: #333;
  }

  /* My Packages Section */
  .my-packages {
    background-color: #fff;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
  }

  .my-packages-header {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .package-status {
    background-color: #f0ad4e;
    color: white;
    padding: 5px 10px;
    border-radius: 4px;
    font-size: 12px;
    font-weight: bold;
    display: inline-block;      /* ทำให้กรอบขนาดตามเนื้อหา */
    width: auto;                /* กำหนดความกว้างตามเนื้อหา */
  }

  .package-details {
    display: flex;
    justify-content: space-between;
  }

  .package-details div {
    text-align: left;
  }

  /* Buy Top-up Packages Section */
  .top-up-section {
    background-color: #fff;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
  }

  .top-up-header {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 15px;
  }

  /* Buy Packages Section */
  .esim-card {
    background-color: #d9534f;
    border-radius: 16px;
    padding: 20px;
    color: white;
    margin-bottom: 20px;
    position: relative;
    min-height: 200px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  /* .esim-details {
    margin-top: 20px;
  } */

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
    gap: 60px; /* เพิ่ม gap เพื่อเพิ่มระยะห่างระหว่างปุ่ม */
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

  .price-info {
    font-size: 20px;
    font-weight: bold;
    margin-top: 8px;
  }
</style>

<div class="top-menu">
  <a href="/my-esim">
    <div class="back-arrow">
      <i class="fas fa-arrow-left"></i>
    </div>
  </a>
  <h1>Xin Chao</h1>
</div>

<div class="container">
  <!-- Header Section -->
  <div class="header">
    <div>
      <h2>Xin Chao</h2>
      <p class="iccid-info">ICCID NUMBER<br/>{iccidNumber}</p>
      <p class="iccid-info">COVERAGE<br/>{coverage}</p>
    </div>
    <img src="https://placehold.co/100x80" alt="SIM Image" />
  </div>

  <!-- Warning Section -->
  <div class="warning">
    <i class="fas fa-exclamation-triangle"></i>
    <p><strong>WARNING!</strong> Most eSIMs can only be installed once. If you remove the eSIM from your device, you cannot install it again.</p>
  </div>

  <!-- eSIM Installation Section -->
  <div class="installation">
    <p>eSIM Installation</p>
    <button on:click={goToMyEsimDetailInstructionPage}>View Instructions</button>
  </div>

  <!-- Data Usage Section -->
  <div class="data-usage">
    <div class="my-packages-header">
      <span>Usage</span>
    </div>
    
    <div class="usage-details">
      <div class="remaining-data">
        <div class="circular-progress" data-inner-circle-color="lightgrey" data-percentage="80" data-progress-color="crimson" data-bg-color="black">
          <div class="inner-circle"></div>
          <p class="percentage">0%</p>
        </div>
      </div>

      <!-- ข้อมูล data-info -->
      <div class="data-info">
        <p class="remaining-data">REMAINING DATA</p><br/>
        <p>Used Data<br/><strong>{usedData} MB</strong></p><br/>
        <p>Total Data<br/><strong>{totalData} GB</strong></p>
      </div>
    </div>
  </div>

  <!-- My Packages Section -->
  <div class="my-packages">
    <div class="my-packages-header">
      <span>MY PACKAGES</span>
      <i class="fas fa-cube"></i>
    </div>
    <div class="package-status">
      {packageDetails.status}
    </div>
    <div class="package-details">
      <div>
        <p><i class="fas fa-calendar-alt icon"></i> VALIDITY</p>
        <p><i class="fas fa-exchange-alt icon"></i> DATA</p>
      </div>
      <div>
        <p>{packageDetails.validity}</p>
        <p>{packageDetails.data}</p>
      </div>
    </div>
  </div>

  <!-- Top-up Packages Section -->
  <div class="top-up-section">
    <div class="top-up-header">Buy Top-up Packages</div>

    {#each topUpPackages as topUpPackage}
      <div class="esim-card">
        <div class="esim-details">
          <div>
            <span><i class="fas fa-exchange-alt"></i> DATA</span>
            <span>{topUpPackage.data}</span>
          </div>
          <div>
            <span><i class="fas fa-calendar-alt"></i> VALIDITY</span>
            <span>{topUpPackage.validity}</span>
          </div>
          <div>
            <span><i class="fas fa-tag"></i> PRICE</span>
            <span>{topUpPackage.price}</span>
          </div>
        </div>
        <div class="esim-actions">
          <div class="price-info">{topUpPackage.price}</div>
          <button class="action-button">BUY</button>
        </div>
      </div>
    {/each}
  </div>
</div>