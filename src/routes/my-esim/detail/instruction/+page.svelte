<script>
  let selectedTab = "Direct"; // เก็บค่าแท็บที่ถูกเลือก
  const tabs = ["Direct", "QR Code", "Manual"]; // แท็บที่มีให้เลือก

  // ฟังก์ชันสำหรับเปลี่ยนแท็บ
  function selectTab(tab) {
    selectedTab = tab;
  }

  // ฟังก์ชันสำหรับคัดลอกข้อมูล
  function copyText(text) {
    navigator.clipboard.writeText(text);
    alert("Copied to clipboard!");
  }

  // ข้อมูลที่ต้องการคัดลอก
  let smdpAddress = "sin.prod.ondemandconnectivity.com";
  let activationCode = "0C19CCA5F1908CF89D73BE8204B7D9926B8367D0FF5FA8680C6804E91E33417E";
</script>

<!-- Font Awesome CDN for Icons -->
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"
/>

<style>
  html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
  }

  /* Top Header Section */
  .top-header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    background-color: white;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    z-index: 100;
  }

  .top-menu {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px;
  }

  .top-menu h1 {
    font-size: 18px;
    font-weight: bold;
    margin: 0;
  }

  .top-menu a {
    text-decoration: none;
    color: inherit; /* ให้สีตรงกับ parent */
    margin-right: 10px;
    display: flex;
    align-items: center;
  }

  .back-button {
    background: none;
    border: none;
    font-size: 24px;
    cursor: pointer;
    color: #333;
  }

  .more-options {
    font-size: 24px;
    cursor: pointer;
    color: #333;
  }

  /* Tabs Section */
  .tabs {
    display: flex;
    justify-content: space-around;
    padding: 10px 0;
    background-color: white; /* พื้นหลังสีขาว */
    border-bottom: 1px solid #ddd;
  }

  .tab {
    flex: 1;
    text-align: center;
    padding: 10px;
    cursor: pointer;
    font-size: 16px;
    font-weight: bold;
    color: #888;
    border-bottom: 3px solid transparent;
    transition: all 0.3s ease;
  }

  .tab:hover {
    color: #333;
    background-color: #f2f2f2; /* สีเทาอ่อนเมื่อ hover */
  }

  /* Main Container */
  .container {
    max-width: 420px;
    margin: 0 auto;
    padding: 16px;
    margin-top: 120px; /* เพิ่ม margin-top สำหรับ header */
    font-family: Arial, sans-serif;
    /* background-color: #f4f4f4; */
  }

  .steps {
    margin-top: 20px;
    padding: 20px;
    background-color: white;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }

  .step-header {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 10px;
  }

  .step-content {
    text-align: left; /* ทำให้ข้อความทั้งหมดชิดซ้าย */
    margin-bottom: 20px;
    color: #555;
  }

  .step-content ol {
    padding-left: 0px; /* เพิ่ม padding ทางด้านซ้ายให้รายการ */
    margin-left: 0; /* กำหนด margin ให้เริ่มต้นจากซ้าย */
    list-style-position: inside; /* ทำให้ตัวเลขของรายการอยู่ชิดซ้าย */
  }

  .step-content ol li {
    margin-bottom: 10px; /* เพิ่มระยะห่างระหว่างแต่ละรายการ */
    text-align: left; /* ชิดซ้ายตัวข้อความของแต่ละรายการ */
  }

  .network-info {
    background-color: white;
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
  }

  .network-info p {
    font-size: 14px;
    color: #333;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #ddd;
    padding-bottom: 10px;
    margin-bottom: 10px;
  }

  .network-info p:last-child {
    border-bottom: none;
    margin-bottom: 0;
  }

  .info-icon {
    font-size: 16px;
    color: #333;
  }

  .install-button {
    width: 100%;
    background-color: #333;
    color: white;
    border: none;
    padding: 15px;
    font-size: 16px;
    font-weight: bold;
    border-radius: 10px;
    cursor: pointer;
    margin-top: 20px;
  }

  .install-button:hover {
    background-color: #555;
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

  .qr-code-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }

  .qr-code-image {
    width: 200px;
    height: 200px;
    margin-bottom: 20px;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }

  .share-button {
    background-color: #fff;
    border: 2px solid #333;
    padding: 10px 20px;
    border-radius: 8px;
    cursor: pointer;
    color: #333;
    font-weight: bold;
    margin-top: 10px;
    transition: background-color 0.3s ease;
  }

  .share-button:hover {
    background-color: #f0f0f0;
  }

  /* Manual Input Section */
  .manual-input {
    background-color: white;
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
    position: relative;
  }

  .manual-input p {
    font-size: 14px;
    color: #333;
    display: block;
    padding: 10px 0;
    padding-right: 40px; /* เพิ่ม padding ขวาให้ข้อความไม่ทับปุ่ม */
    border-bottom: 1px solid #ddd;
    word-wrap: break-word;
    position: relative;
  }

  .manual-input p span {
    display: block; /* ทำให้ span ขึ้นบรรทัดใหม่ */
    margin-top: 5px;
    word-wrap: break-word;
  }

  .manual-input p:last-child {
    border-bottom: none;
  }

  .copy-button {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 18px;
    color: #888;
    position: absolute;
    right: 0;
    top: 50%;
    transform: translateY(-50%);
  }

  .copy-button:hover {
    color: #333;
  }
</style>

<!-- Top Header Section -->
<div class="top-header">
  <!-- Top Menu/Header -->
  <div class="top-menu">
    <a href="/my-esim/detail">
      <div class="back-arrow">
        <i class="fas fa-arrow-left"></i>
      </div>
    </a>
    <h1>View Instructions</h1>
    <div class="more-options">⋮</div>
  </div>

  <!-- Tabs for Direct, QR Code, Manual -->
  <div class="tabs">
    {#each tabs as tab}
      <div
        class="tab {selectedTab === tab ? 'active' : ''}"
        on:click={() => (selectedTab = tab)}
      >
        {tab}
      </div>
    {/each}
  </div>
</div>

<!-- Main Container -->
<div class="container">
  <!-- Warning Section -->
  <div class="warning">
    <i class="fas fa-exclamation-triangle"></i>
    <p><strong>WARNING!</strong> Most eSIMs can only be installed once. If you remove the eSIM from your device, you cannot install it again.</p>
  </div>

  <!-- เงื่อนไขเมื่อแท็บที่เลือกเป็น Direct -->
  {#if selectedTab === "Direct"}

    <!-- Step 1/2 - Install eSIM -->
    <div class="steps">
      <div class="step-header">Step 1/2 - Install eSIM</div>
      <div class="step-content">
        *Note that the eSIM installation process must not be interrupted and make
        sure your device has a stable internet connection before installing.
      </div>
      <div class="step-content">
        <ol>
          <li>Tap “Install eSIM”, tap “Continue” twice and wait for a while. Your eSIM will connect to the network, this may take a few minutes, then tap “Done”.</li>
          <li>Choose a label for your new eSIM plan.</li>
          <li>Choose “Primary” for your default line, then tap “Continue”.</li>
          <li>Choose the “Primary” you want to use with iMessage and FaceTime for your Apple ID, then tap “Continue”.</li>
          <li>Choose your new eSIM plan for cellular/mobile data, then tap “Continue”.</li>
        </ol>
      </div>
    </div>

    <!-- Step 2/2 - Access Data -->
    <div class="steps">
      <div class="step-header">Step 2/2 - Access Data</div>
      
      <!-- Network and Data Info -->
      <div class="network-info">
        <p>
          <strong>NETWORK</strong>
          <span>Mobifone <i class="fas fa-info-circle info-icon"></i></span>
        </p>
        <p>
          <strong>NETWORK</strong>
          <span>Viettel <i class="fas fa-info-circle info-icon"></i></span>
        </p>
        <p>
          <strong>APN</strong>
          <span>The APN is set automatically.</span>
        </p>
        <p>
          <strong>DATA ROAMING</strong>
          <span>ON <i class="fas fa-info-circle info-icon"></i></span>
        </p>
      </div>
      <div class="step-content">
        <ol>
          <li>Go to "Cellular/Mobile Data", then select the recently downloaded eSIM on your device. Enable the "Turn On This Line" toggle, then select your new eSIM plan for cellular/mobile data.</li>
          <li>Tap "Network Selection", disable the "Automatic" toggle, then select the supported network manually if your eSIM has connected to the wrong network.</li>
          <li>Enable the "Data Roaming" toggle for your new eSIM plan.</li>
        </ol>
      </div>
    </div>
  {/if}

  <!-- เงื่อนไขเมื่อแท็บที่เลือกเป็น QR Code -->
  {#if selectedTab === "QR Code"}
    <div class="steps">
      <div class="step-header">Step 1/2 - Install eSIM</div>
      <div class="qr-code-section">
        <img class="qr-code-image" src="https://placehold.co/200x200" alt="QR Code" />
        <div class="step-content">
          Scan the QR code by printing out or displaying the code on another device to
          install your eSIM. *Make sure your device has a stable internet connection
          before installing.
        </div>
        <button class="share-button">SHARE QR CODE</button>
      </div>
      
      <div class="step-content">
        <ol>
          <li>Go to Settings > Cellular/Mobile Data > Add eSIM or Set up Cellular/Mobile Service > Use QR Code on your device.</li>
          <li>Scan the QR code or take a screenshot (available up to
            ¡OS 17.3), tap "Open Photos" , select it from your camera roll, tap "Next", then tap "Continue" twice and wait for a while. Your eSIM will connect to the network, this may take a few minutes, then tap "Done".</li>
          <li>Choose a label for your new eSIM plan.</li>
          <li>Choose “Primary” for your default line, then tap “Continue”.</li>
          <li>Choose the "Primary" you want to use with iMessage and FaceTime for your Apple ID, then tap "Continue".</li>
          <li>Choose your new eSIM plan for cellular/mobile data, then tap “Continue”.</li>
        </ol>
      </div>
    </div>

    <!-- Step 2/2 - Access Data -->
    <div class="steps">
      <div class="step-header">Step 2/2 - Access Data</div>
      
      <!-- Network and Data Info -->
      <div class="network-info">
        <p>
          <strong>NETWORK</strong>
          <span>Mobifone <i class="fas fa-info-circle info-icon"></i></span>
        </p>
        <p>
          <strong>NETWORK</strong>
          <span>Viettel <i class="fas fa-info-circle info-icon"></i></span>
        </p>
        <p>
          <strong>APN</strong>
          <span>The APN is set automatically.</span>
        </p>
        <p>
          <strong>DATA ROAMING</strong>
          <span>ON <i class="fas fa-info-circle info-icon"></i></span>
        </p>
      </div>
      <div class="step-content">
        <ol>
          <li>Go to "Cellular/Mobile Data", then select the recently downloaded eSIM on your device. Enable the "Turn On This Line" toggle, then select your new eSIM plan for cellular/mobile data.</li>
          <li>Tap "Network Selection", disable the "Automatic" toggle, then select the supported network manually if your eSIM has connected to the wrong network.</li>
          <li>Enable the "Data Roaming" toggle for your new eSIM plan.</li>
        </ol>
      </div>
    </div>
  {/if}

  <!-- เงื่อนไขเมื่อแท็บที่เลือกเป็น Manual -->
  {#if selectedTab === "Manual"}
    <div class="steps">
      <div class="step-header">Step 1/2 - Install eSIM</div>
      
      <!-- SM-DP+ Address and Activation Code Section -->
      <div class="manual-input">
        <p>
          <strong>SM-DP+ ADDRESS</strong>
          <span>{smdpAddress}</span>
          <button class="copy-button" on:click={() => copyText(smdpAddress)}>
            <i class="fas fa-copy"></i>
          </button>
        </p>
        <p>
          <strong>ACTIVATION CODE</strong>
          <span>{activationCode}</span>
          <button class="copy-button" on:click={() => copyText(activationCode)}>
            <i class="fas fa-copy"></i>
          </button>
        </p>
        <p class="step-content">
          Copy this information and enter details manually to install your eSIM. *Make sure your device has a stable internet connection before installing.
        </p>
      </div>

      <div class="step-content">
        <ol>
          <li>Go to Settings > Cellular/Mobile Data > Add eSIM or Set up Cellular/Mobile Service > Enter Details Manually.</li>
          <li>Enter the SM-DP+ Address and Activation Code, then tap "Next".</li>
          <li>Tap “Continue” twice and wait for a while. Your eSIM will connect to the network, this may take a few minutes, then tap “Done”.</li>
          <li>Choose a label for your new eSIM plan.</li>
          <li>Choose “Primary” for your default line, then tap “Continue”.</li>
          <li>Choose your new eSIM plan for cellular/mobile data, then tap “Continue”.</li>
        </ol>
      </div>
    </div>

    <!-- Step 2/2 - Access Data -->
    <div class="steps">
      <div class="step-header">Step 2/2 - Access Data</div>
      
      <!-- Network and Data Info -->
      <div class="network-info">
        <p>
          <strong>NETWORK</strong>
          <span>Mobifone <i class="fas fa-info-circle info-icon"></i></span>
        </p>
        <p>
          <strong>NETWORK</strong>
          <span>Viettel <i class="fas fa-info-circle info-icon"></i></span>
        </p>
        <p>
          <strong>APN</strong>
          <span>The APN is set automatically.</span>
        </p>
        <p>
          <strong>DATA ROAMING</strong>
          <span>ON <i class="fas fa-info-circle info-icon"></i></span>
        </p>
      </div>
      <div class="step-content">
        <ol>
          <li>Go to "Cellular/Mobile Data", then select the recently downloaded eSIM on your device. Enable the "Turn On This Line" toggle, then select your new eSIM plan for cellular/mobile data.</li>
          <li>Tap "Network Selection", disable the "Automatic" toggle, then select the supported network manually if your eSIM has connected to the wrong network.</li>
          <li>Enable the "Data Roaming" toggle for your new eSIM plan.</li>
        </ol>
      </div>
    </div>
  {/if}
</div>