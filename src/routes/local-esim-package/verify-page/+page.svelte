<script>
  let consent = false;
</script>

<style>
  html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #f8f8f8;
    font-family: Arial, sans-serif;
    overflow: hidden; /* Prevent body from scrolling */
  }

  .container {
    background-color: white;
    border-radius: 10px;
    padding: 20px;
    width: 100%;
    max-width: 400px;
    height: 100%; /* Take full screen height */
    display: flex;
    flex-direction: column;
    justify-content: flex-start; /* Start the content from the top */
    text-align: center;
    overflow-y: auto; /* Enable scrolling inside the container if content overflows */
  }

  .close-icon {
    align-self: flex-end;
    font-size: 18px;
    cursor: pointer;
    color: #666;
  }

  h1 {
    font-size: 20px;
    margin-bottom: 10px;
    color: #333;
  }

  p {
    font-size: 14px;
    color: #777;
    margin-bottom: 20px;
  }

  .checklist {
    text-align: left;
    margin-bottom: 20px;
    flex-grow: 1; /* Ensures the checklist can grow and take available space */
  }

  .checklist-item {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }

  .checkmark {
    color: #4CAF50;
    font-size: 16px;
    margin-right: 10px;
  }

  /* Consent and Start button at the bottom */
  .bottom-section {
    margin-top: auto; /* Pushes this section to the bottom */
    width: 100%;
  }

  .consent {
    font-size: 12px;
    text-align: left;
    margin-bottom: 20px;
  }

  .switch {
    display: inline-block;
    position: relative;
    width: 40px;
    height: 20px;
    margin-left: 10px;
  }

  .switch input {
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
    border-radius: 20px;
    transition: .4s;
  }

  .slider:before {
    position: absolute;
    content: "";
    height: 16px;
    width: 16px;
    border-radius: 50%;
    left: 2px;
    bottom: 2px;
    background-color: white;
    transition: .4s;
  }

  input:checked + .slider {
    background-color: #4CAF50;
  }

  input:checked + .slider:before {
    transform: translateX(20px);
  }

  .start-button {
    background-color: #ccc;
    color: white;
    padding: 10px;
    width: 100%;
    border: none;
    border-radius: 5px;
    cursor: not-allowed;
  }

  .start-button.active {
    background-color: #4CAF50;
    cursor: pointer;
  }
</style>

<!-- Add Font Awesome for the checkmarks -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">

<div class="container">
  <span class="close-icon">✖</span>
  <h1>Start verification</h1>
  <p>This process is designed to verify your identity and protect you from identity theft.</p>

  <div class="checklist">
    <div class="checklist-item">
      <i class="fas fa-check-circle checkmark"></i>
      <span>Use a valid document</span>
    </div>
    <div class="checklist-item">
      <i class="fas fa-check-circle checkmark"></i>
      <span>Find a well-lit surface</span>
    </div>
    <div class="checklist-item">
      <i class="fas fa-check-circle checkmark"></i>
      <span>Be ready to take a selfie</span>
    </div>
  </div>

  <!-- Bottom section for consent and start button -->
  <div class="bottom-section">
    <div class="consent">
      <label>
        I consent to Jumio collecting, processing, and sharing my personal information, which may include biometric data, as set out in its Privacy Notice.
        <label class="switch">
          <input type="checkbox" bind:checked={consent}>
          <span class="slider"></span>
        </label>
      </label>
    </div>

    <!-- Start button -->
    <button class="start-button {consent ? 'active' : ''}" disabled={!consent}>Start</button>
  </div>
</div>