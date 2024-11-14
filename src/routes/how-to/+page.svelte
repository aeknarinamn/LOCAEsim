<script>
  // ข้อมูลขั้นตอนการติดตั้ง eSIM
  let installationSteps = [
    {
      step: 1,
      title: "Download the Airalo App",
      description: "Download and install the Airalo app from the App Store or Google Play.",
      icon: "fas fa-download",
    },
    {
      step: 2,
      title: "Select Your eSIM",
      description: "Choose your desired eSIM plan and purchase it from the app.",
      icon: "fas fa-sim-card",
    },
    {
      step: 3,
      title: "Install the eSIM",
      description: "Go to your phone's settings and follow the instructions to install the eSIM.",
      icon: "fas fa-cog",
    },
    {
      step: 4,
      title: "Activate the eSIM",
      description: "Activate your eSIM in the Airalo app and start using mobile data.",
      icon: "fas fa-check-circle",
    },
    {
      step: 5,
      title: "Enjoy Seamless Connectivity",
      description: "Enjoy internet access without worrying about SIM cards or roaming fees!",
      icon: "fas fa-wifi",
    },
  ];
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
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
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

  .how-to-header {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
    text-align: center;
    color: #d9534f;
  }

  .step-card {
    background-color: #fff;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 20px;
    display: flex;
    gap: 16px;
    align-items: center;
  }

  .step-card i {
    font-size: 36px;
    color: #d9534f;
  }

  .step-content {
    flex: 1;
  }

  .step-title {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 5px;
  }

  .step-description {
    font-size: 14px;
    color: #666;
  }

  .footer {
    margin-top: 40px;
    text-align: center;
    color: #666;
  }

  .footer a {
    color: #d9534f;
    text-decoration: none;
  }

  .footer a:hover {
    text-decoration: underline;
  }
</style>

<!-- Top Menu/Header -->
<div class="top-menu">
  <h1>How to Install Airalo eSIM</h1>
</div>

<!-- Main Container -->
<div class="container">
  <div class="how-to-header">Installation Steps</div>

  <!-- Loop through the steps -->
  {#each installationSteps as step}
    <div class="step-card">
      <i class={step.icon}></i>
      <div class="step-content">
        <div class="step-title">Step {step.step}: {step.title}</div>
        <div class="step-description">{step.description}</div>
      </div>
    </div>
  {/each}

  <!-- Footer Section -->
  <div class="footer">
    <p>Need more help? Visit the <a href="https://www.airalo.com/help" target="_blank">Airalo Help Center</a></p>
  </div>
</div>