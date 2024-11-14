<script>
  let showPopup = false;
  let showPaymentPopup = false;
  let showCardPopup = false;
  let showApplyCodePopup = false; // เพิ่มตัวแปรสำหรับ popup Apply Code / Use Airmoney
  let showCountriesPopup = false;

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

  function toggleCountriesPopup() {
    showCountriesPopup = !showCountriesPopup;
    showPaymentPopup = false;
    showCardPopup = false;
    showApplyCodePopup = false;
    toggleBodyScroll(showPaymentPopup || showCardPopup || showApplyCodePopup || showCountriesPopup);
  }

  function closeCountriesPopup() {
    showCountriesPopup = false;
    showPaymentPopup = false;
    showCardPopup = false;
    showApplyCodePopup = false;
    toggleBodyScroll(showPaymentPopup || showCardPopup || showApplyCodePopup);
  }

  // Function to toggle payment method popup visibility
  const togglePaymentPopup = () => {
    showPaymentPopup = !showPaymentPopup;
    showCardPopup = false;
    showApplyCodePopup = false; // ปิด Apply Code Popup เมื่อเปิด Payment Popup
    toggleBodyScroll(showPaymentPopup || showCardPopup || showApplyCodePopup || showCountriesPopup);
  };

  // Function to open card popup and close payment method popup
  const openCardPopup = () => {
    showPaymentPopup = false;
    showCardPopup = true;
    toggleBodyScroll(showPaymentPopup || showCardPopup || showApplyCodePopup || showCountriesPopup);
  };

  // Function to go back to payment popup
  const backToPaymentPopup = () => {
    showCardPopup = false;
    showPaymentPopup = true;
    toggleBodyScroll(showPaymentPopup || showCardPopup || showApplyCodePopup || showCountriesPopup);
  };

  const toggleClosePopup = () => {
    showCardPopup = false;
    showPaymentPopup = false;
    toggleBodyScroll(showPaymentPopup || showCardPopup || showApplyCodePopup);
  };

  // Function to toggle apply code popup visibility
  const toggleApplyCodePopup = () => {
    showApplyCodePopup = !showApplyCodePopup;
    showPaymentPopup = false; // ปิด Payment Popup เมื่อเปิด Apply Code Popup
    toggleBodyScroll(showPaymentPopup || showCardPopup || showApplyCodePopup || showCountriesPopup);
  };

  // ปิดหรือเปิดการ scroll ของ body
  function toggleBodyScroll(isPopupOpen) {
    if (isPopupOpen) {
      document.body.style.overflow = 'hidden';
    } else {
      document.body.style.overflow = 'auto';
    }
  }

  import { goto } from '$app/navigation';

  function goToCompletePaymentPage() {
    goto('/global-esim-package/complete-payment-page');
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

  .back-arrow {
    font-size: 20px;
    cursor: pointer;
  }

  .container {
    max-width: 400px;
    margin: 0 auto;
    padding: 16px;
    margin-top: 80px; /* เพิ่ม margin-top เพื่อเว้นที่ให้ top-menu */
  }

  .checkout-container {
    position: relative;
    background: linear-gradient(45deg, #1E90FF, #00BFFF);
    border-radius: 16px;
    padding: 16px;
    color: white;
    margin-bottom: 16px;
  }

  .checkout-header {
    font-size: 20px;
    font-weight: bold;
    margin-bottom: 16px;
  }

  .details {
    padding: 16px 0;
    border-radius: 8px;
    color: white;
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

  .details span {
    display: flex;
    align-items: center;
    font-size: 16px;
  }

  .details i {
    margin-right: 8px; /* เพิ่มระยะห่างระหว่าง icon กับข้อความ */
  }

  .details span:first-child {
    flex: 1;
  }

  .details span:last-child {
    text-align: right;
    flex-shrink: 0;
  }

  /* รูป Package */
  .package-image {
    width: 150px; /* ขยายขนาดของรูปให้ใหญ่ขึ้น */
    border-radius: 8px;
    position: absolute;
    top: -25px; /* ปรับตำแหน่งให้เหมาะสมกับขนาดใหม่ */
    right: 16px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); /* เพิ่มเงาให้ดูโดดเด่น */
  }

  .payment-method {
    background-color: #fff;
    border-radius: 12px;
    padding: 16px;
    margin: 16px 0;
    color: #333;
    font-size: 14px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }

  .payment-method h2 {
    margin: 0 0 8px;
    font-size: 18px;
    font-weight: bold;
  }

  .payment-method button {
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

  .buy-button,
  .add-button {
    background-color: #333;
    color: white;
    padding: 12px 24px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 14px;
    flex-grow: 1;
    transition: background-color 0.3s;
    max-width: 400px;
  }

  .buy-button:hover,
  .add-button:hover {
    background-color: #555;
  }

  .price-section {
    font-size: 18px;
    font-weight: bold;
    color: #333;
    margin-right: 16px;
  }

  /* ลดขนาดฟอนต์เฉพาะข้อความ "AMOUNT TO BE PAID" */
  .amount-label {
    font-size: 10px;
    color: #333;
  }

  /* Section for Apply Code or Use Airmoney */
  .apply-code {
    background-color: #fff;
    border-radius: 12px;
    padding: 16px;
    margin: 16px 0;
    color: #333;
    font-size: 14px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }

  .apply-code h2 {
    margin: 0 0 8px;
    font-size: 18px;
    font-weight: bold;
  }

  .apply-code p {
    margin: 0 0 12px;
    color: #666;
    font-size: 14px;
  }

  .apply-code-button {
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
  }

  /* Confirmation Section */
  .confirmation-section {
    display: flex;
    align-items: flex-start;
    margin: 16px 0 70px 0; /* เพิ่ม margin-bottom 50px เพื่อเพิ่มระยะห่างกับ bottom-menu */
    font-size: 14px;
    color: #333;
  }

  .confirmation-section input {
    margin-right: 10px;
    margin-top: 3px;
  }

  .confirmation-section label {
    line-height: 1.5;
    color: #666;
  }

  .confirmation-section a {
    color: #007bff;
    text-decoration: none;
  }

  .confirmation-section a:hover {
    text-decoration: underline;
  }

  /* Popup สำหรับ Payment Method */
  /* ป้องกันการเลื่อนหน้าจอหลักเมื่อ popup เปิด */
  .popup-background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: flex-end;
    z-index: 20;
  }

  .payment-popup,
  .card-popup,
  .apply-code-popup {
    background-color: white;
    border-radius: 16px 16px 0 0;
    width: 95%;
    height: 80%;
    position: absolute;
    bottom: 0;
    padding: 20px;
    box-shadow: 0px -4px 12px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    overflow-y: auto; /* เปิดการ scroll ภายใน popup */
    padding-bottom: 100px; /* เพิ่ม padding-bottom ให้มีพื้นที่เพียงพอ */
  }

  .popup-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #eee;
    padding-bottom: 10px;
  }

  .popup-header h2 {
    font-size: 18px;
    font-weight: bold;
    margin: 0;
  }

  .close-button {
    background: none;
    border: none;
    font-size: 30px;
    cursor: pointer;
    color: gray;
  }

  .back-button {
    background: none;
    border: none;
    font-size: 20px;
    cursor: pointer;
    color: gray;
  }

  .payment-methods {
    margin-top: 20px;
  }

  .payment-method-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    margin-bottom: 10px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  .payment-method-item:hover {
    background-color: #f5f5f5;
  }

  .payment-method-item img {
    width: 24px;
    margin-right: 12px;
  }

  .payment-method-info {
    flex: 1;
  }

  .payment-method-info h3 {
    margin: 0;
    font-size: 16px;
  }

  .payment-method-info p {
    margin: 0;
    color: #666;
    font-size: 14px;
  }

  .card-form {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-top: 20px;
  }

  .card-form input {
    padding: 12px;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 14px;
    box-sizing: border-box; /* ป้องกัน padding ทำให้ input ล้นขอบ */
    width: 100%; /* เพิ่มให้ input ครอบคลุมขนาด container */
  }

  .card-form .input-group {
      display: flex;
      gap: 12px; /* เพิ่มช่องว่างระหว่าง input */
      width: 100%; /* ครอบคลุมขนาด container */
  }

  .card-form .input-group input {
      flex: 1; /* ให้ input ขยายเต็มพื้นที่ที่เหลือ */
      min-width: 0; /* ป้องกัน input ล้นขอบ */
  }

  /* ปรับการแสดงผลไอคอนบัตร */
  .card-icons {
    display: flex;
    gap: 8px; /* ปรับระยะห่างระหว่างไอคอน */
    margin: 12px 0;
    justify-content: flex-start; /* จัดชิดซ้าย */
  }

  .card-icons i {
    font-size: 24px;
    color: currentColor;
  }

  /* ให้แต่ละไอคอนมีสีเฉพาะตัว */
  .fa-cc-visa {
    color: #1a1f71; /* สีน้ำเงินของ Visa */
  }

  .fa-cc-mastercard {
    color: #eb001b; /* สีแดงของ Mastercard */
  }

  .fa-cc-amex {
    color: #007bc1; /* สีน้ำเงินของ American Express */
  }

  .fa-cc-jcb {
    color: #0033a0; /* สีของ JCB */
  }

  .fa-cc-unionpay {
    color: #d81f26; /* สีแดงของ UnionPay */
  }

  /* ใช้ไอคอนทั่วไปและปรับสีสำหรับ UnionPay */
  .fa-cc-unionpay-alt {
    color: #d81f26; /* สีแดงของ UnionPay */
  }

  .card-icons img {
    height: 24px;
  }

  /* Styles specific to Apply Code Popup */
  .apply-code-section {
    margin-top: 20px;
  }

  .apply-code-section h3 {
    font-size: 16px;
    margin-bottom: 8px;
    font-weight: bold;
  }

  .apply-code-section p {
    font-size: 14px;
    margin-bottom: 12px;
    color: #666;
  }

  .input-group {
    display: flex;
    gap: 12px;
  }

  .input-code {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    font-size: 14px;
  }

  .apply-button {
    background-color: #333;
    color: white;
    padding: 10px 16px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 14px;
    transition: background-color 0.3s;
  }

  .apply-button:hover {
    background-color: #555;
  }

  .alert-box {
    background-color: #2ecc71;
    color: white;
    padding: 12px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    font-size: 14px;
    margin-top: 12px;
  }

  .alert-icon {
    font-size: 18px;
    margin-right: 8px;
  }

  /* CSS สำหรับ Toggle Switch */
  .toggle-switch {
    position: relative;
    width: 50px;
    height: 24px;
    display: inline-block;
  }

  .toggle-switch input {
    opacity: 0;
    width: 0;
    height: 0;
  }

  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    border-radius: 34px;
    transition: 0.4s;
  }

  .slider:before {
    position: absolute;
    content: "";
    height: 16px;
    width: 16px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    border-radius: 50%;
    transition: 0.4s;
  }

  input:checked + .slider {
    background-color: #4caf50;
  }

  input:checked + .slider:before {
    transform: translateX(26px);
  }

  .toggle-save-card {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-top: 16px;
  }

  .toggle-save-card label {
    font-size: 14px;
    color: #666;
  }

  .toggle-save-card i {
    font-size: 16px;
    color: #666;
  }

  .learn-more {
    margin-top: 16px;
    font-size: 14px;
    color: #666;
    padding-bottom: 80px; /* เพิ่ม padding-bottom เพื่อไม่ให้ข้อความติด bottom-menu */
  }

  .learn-more a {
    color: #007bff;
    text-decoration: none;
  }

  .learn-more a:hover {
    text-decoration: underline;
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
  <h1>Secure Checkout</h1>
</div>

<!-- Main Container -->
<div class="container">
  <!-- Checkout Section -->
  <div class="checkout-container">
    <h2 class="checkout-header">Discover</h2>
    <img
      class="package-image"
      src="https://placehold.co/150x80"
      alt="SIM card image showing tourist package details"
    />

    <div class="details">
      <div>
        <span><i class="fas fa-globe"></i> COVERAGE</span>
        <div class="converage-button">
          <button on:click={toggleCountriesPopup}>135 COUNTRIES</button>
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

  <!-- Payment Method Section -->
  <div class="payment-method">
    <h2>Choose Payment Method</h2>
    <p>You can choose or change the payment method to complete your order.</p>
    <button on:click={togglePaymentPopup}>
      Choose Payment Method <i class="fas fa-chevron-right"></i>
    </button>
  </div>

  <!-- Section for Applying Code or Using Airmoney -->
  <div class="apply-code">
    <h2>Apply Code or Use Airmoney</h2>
    <p>You can apply your discount / referral code or use Airmoney with your purchase.</p>
    <button class="apply-code-button" on:click={toggleApplyCodePopup}>
      Apply Code / Use Airmoney <i class="fas fa-chevron-right"></i>
    </button>
  </div>

  <!-- Confirmation Checkbox Section -->
  <div class="confirmation-section">
    <input type="checkbox" id="confirm-check" />
    <label for="confirm-check">
      Before completing this order, please confirm your device is eSIM compatible and
      network-unlocked. <a href="#">Learn More</a>
    </label>
  </div>
</div>

<!-- Bottom Menu with Amount and Complete Order Button -->
<div class="bottom-menu">
  <div class="price-section">
    <span class="amount-label">AMOUNT TO BE PAID</span><br/> <!-- ลดขนาดฟอนต์เฉพาะข้อความนี้ -->
    <span>$9.00 USD</span>
  </div>
  <button class="buy-button" on:click={goToCompletePaymentPage}>COMPLETE ORDER</button>
</div>

<!-- Payment Method Popup -->
{#if showPaymentPopup}
<div class="popup-background" on:click={togglePaymentPopup}>
  <div class="payment-popup" on:click|stopPropagation>
    <!-- Header ของ Popup -->
    <div class="popup-header">
      <h2>Choose Payment Method</h2>
      <button class="close-button" on:click={togglePaymentPopup}>&times;</button>
    </div>

    <!-- ส่วนเนื้อหา Payment Methods -->
    <div class="payment-methods">
      <div class="payment-method-item" on:click={openCardPopup}>
        <img src="https://placehold.co/24x24" alt="Credit/Debit Card" />
        <div class="payment-method-info">
          <h3>Credit / Debit Card</h3>
          <p>Visa, Mastercard, AMEX, CUP, JCB</p>
        </div>
        <i class="fas fa-chevron-right"></i>
      </div>

      <!-- <div class="payment-method-item">
        <img src="https://placehold.co/24x24?text=PP" alt="PayPal" />
        <div class="payment-method-info">
          <h3>PayPal</h3>
        </div>
        <button class="select-button">SELECT</button>
      </div>

      <div class="payment-method-item">
        <img src="https://placehold.co/24x24?text=AP" alt="Alipay" />
        <div class="payment-method-info">
          <h3>Alipay</h3>
        </div>
        <button class="select-button">SELECT</button>
      </div> -->
    </div>
  </div>
</div>
{/if}

<!-- Add New Card Popup -->
{#if showCardPopup}
<div class="popup-background" on:click={backToPaymentPopup}>
  <div class="card-popup" on:click|stopPropagation>
    <div class="popup-header">
      <button class="back-button" on:click={backToPaymentPopup}>
        <i class="fas fa-arrow-left"></i>
      </button>
      <h2>Add New Card</h2>
      <!-- <button class="close-button" on:click={backToPaymentPopup}>&times;</button> -->
    </div>
    <div class="card-form">
      <input type="text" placeholder="Card Name" />
    
      <!-- แสดงไอคอนบัตรเครดิตแบบมีสี -->
      <div class="card-icons">
        <i class="fab fa-cc-visa"></i> <!-- Visa -->
        <i class="fab fa-cc-mastercard"></i> <!-- Mastercard -->
        <i class="fab fa-cc-amex"></i> <!-- AMEX -->
        <i class="fab fa-cc-jcb"></i> <!-- JCB -->
        <i class="fas fa-credit-card fa-cc-unionpay-alt"></i> <!-- UnionPay -->
      </div>
    
      <input type="text" placeholder="Card Number" />
      <input type="text" placeholder="Name on Card" />
    
      <!-- ใช้ flex เพื่อให้ input ของ CVV ไม่ล้นขอบ -->
      <div class="input-group">
        <input type="text" placeholder="Expiration Date" />
        <input type="text" placeholder="CVV" />
      </div>
    
      <div class="toggle-save-card">
        <label class="toggle-switch">
          <input type="checkbox" id="save-card" />
          <span class="slider"></span>
        </label>
        <label for="save-card">I'd like to save my card securely.</label>
        <i class="fas fa-info-circle"></i>
      </div>
    </div>
    <div class="learn-more">
      <p>Learn More About Security</p>
      <p>
        Stripe has been audited by a PCI-certified auditor and is certified to PCI Service Provider Level 1. This is the most stringent level of certification available in the payments industry. <a href="#">Learn More</a>
      </p>
    </div>
    <div class="bottom-menu">
      <button class="add-button" on:click={toggleClosePopup}>ADD</button>
    </div>
  </div>
</div>
{/if}

<!-- Apply Code / Use Airmoney Popup -->
{#if showApplyCodePopup}
<div class="popup-background" on:click={toggleApplyCodePopup}>
  <div class="apply-code-popup" on:click|stopPropagation>
    <!-- Header ของ Popup -->
    <div class="popup-header">
      <h2>Apply Code</h2>
      <button class="close-button" on:click={toggleApplyCodePopup}>&times;</button>
    </div>

    <!-- ส่วนเนื้อหา Apply Code / Use Airmoney -->
    <div class="apply-code-section">
      <h3>Apply Code</h3>
      <p>Please enter your discount or referral code to apply.</p>
      <div class="input-group">
        <input type="text" class="input-code" placeholder="Code" />
        <button class="apply-button">APPLY</button>
      </div>
    </div>
  </div>
</div>
{/if}

<!-- Popup Modal -->
{#if showCountriesPopup}
<div class="modal">
  <div class="modal-header">
    <h2>Supported Countries</h2>
    <i class="fas fa-times close-btn" on:click={closeCountriesPopup}></i>
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