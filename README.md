
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Daraz Style Page Responsive</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet" />
  <style>
    /* Reset and base */
    * {
      box-sizing: border-box;
    }
    body {
      font-family: 'Roboto', sans-serif;
      margin: 0;
      background-color: #f4f4f4;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      padding: 40px 20px;
      perspective: 1000px;
    }
    .container {
      width: 100%;
      max-width: 400px;
      background-color: #ffffff;
      box-shadow: 0 10px 30px rgba(0,0,0,0.15);
      border-radius: 12px;
      overflow: hidden;
      transition: transform 0.4s ease-in-out;
      transform-style: preserve-3d;
    }
    /* Header with background images */
    .header {
      height: 180px;
      background-size: cover;
      background-position: center center;
      background-repeat: no-repeat;
      transition: background-image 1s ease-in-out;
    }
    .main-content {
      padding: 0 20px 20px 20px;
      margin-top: -20px;
      position: relative;
      z-index: 2;
    }
    /* Action buttons container */
    .action-buttons {
      background: white;
      padding: 15px;
      border-radius: 12px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      margin-bottom: 25px;
      display: flex;
      justify-content: space-between;
      gap: 10px;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      transform: translateZ(20px);
    }
    .action-buttons:hover {
      transform: translateZ(50px) rotateX(5deg);
      box-shadow: 0 15px 40px rgba(0,0,0,0.2);
    }
    /* Individual buttons */
    .action-btn {
      background-color: #fdf5f5;
      border: 1px solid #fce5e5;
      border-radius: 8px;
      padding: 12px 8px;
      flex: 1; /* equal width */
      text-align: center;
      cursor: pointer;
      font-size: 14px;
      font-weight: 500;
      color: #333;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 8px;
      transition: transform 0.2s ease-out;
      min-width: 0; /* for flex shrinking */
    }
    .action-btn:hover {
      transform: translateY(-5px) scale(1.05);
    }
    .action-btn i {
      font-size: 20px;
      color: #f36f21;
      background-color: #fff;
      border-radius: 50%;
      width: 34px;
      height: 34px;
      line-height: 34px;
      text-align: center;
    }
    /* User info card */
    .user-info-card {
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      margin-bottom: 25px;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      transform: translateZ(20px);
    }
    .user-info-card:hover {
      transform: translateZ(50px) rotateX(5deg);
      box-shadow: 0 15px 40px rgba(0,0,0,0.2);
    }
    .info-row {
      display: flex;
      justify-content: space-between;
      padding: 12px 0;
      font-size: 15px;
      color: #555;
      border-bottom: 1px solid #f0f0f0;
    }
    .info-row span:first-child {
      color: #333;
      font-weight: 500;
    }
    .info-row:last-of-type {
      border-bottom: none;
    }
    .info-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: 20px 15px;
      margin-top: 20px;
      padding-top: 15px;
      border-top: 1px solid #f0f0f0;
    }
    .info-item {
      display: flex;
      flex-direction: column;
    }
    .info-item .label {
      font-size: 14px;
      color: #777;
      margin-bottom: 4px;
    }
    .info-item .value {
      font-size: 18px;
      font-weight: 700;
      color: #d9534f;
      word-wrap: break-word;
    }
    /* Commission dynamics section */
    .commission-dynamics {
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      transform: translateZ(20px);
    }
    .commission-dynamics:hover {
      transform: translateZ(50px) rotateX(5deg);
      box-shadow: 0 15px 40px rgba(0,0,0,0.2);
    }
    .commission-dynamics h2 {
      font-size: 18px;
      font-weight: 700;
      margin-top: 0;
      margin-bottom: 20px;
      color: #333;
    }
    .commission-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
    }
    .commission-user {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 15px;
      flex: 1 1 auto;
      min-width: 140px;
    }
    .commission-user img {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      object-fit: cover;
    }
    .commission-amount {
      text-align: right;
      flex: 1 1 auto;
      min-width: 140px;
    }
    .commission-amount span {
      display: block;
      font-size: 14px;
    }
    .commission-amount span:first-child {
      color: #777;
      margin-bottom: 2px;
    }
    .commission-amount span:last-child {
      font-weight: 700;
      font-size: 15px;
      color: #333;
    }
    /* Payment Modal */
    .payment-modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      z-index: 1000;
      justify-content: center;
      align-items: center;
    }
    .modal-content {
      background-color: white;
      border-radius: 12px;
      width: 90%;
      max-width: 400px;
      max-height: 90vh;
      overflow-y: auto;
      padding: 20px;
      box-shadow: 0 5px 30px rgba(0, 0, 0, 0.2);
      animation: modalFadeIn 0.3s ease-out;
    }
    @keyframes modalFadeIn {
      from {
        opacity: 0;
        transform: translateY(-20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
      padding-bottom: 10px;
      border-bottom: 1px solid #f0f0f0;
    }
    .modal-title {
      font-size: 20px;
      font-weight: 700;
      color: #333;
    }
    .close-modal {
      background: none;
      border: none;
      font-size: 24px;
      cursor: pointer;
      color: #777;
      transition: color 0.2s;
    }
    .close-modal:hover {
      color: #f36f21;
    }
    .payment-methods {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 15px;
      margin-bottom: 20px;
    }
    .payment-method {
      border: 1px solid #e0e0e0;
      border-radius: 8px;
      padding: 15px;
      cursor: pointer;
      transition: all 0.2s;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }
    .payment-method:hover {
      border-color: #f36f21;
      background-color: #fdf5f5;
    }
    .payment-method.selected {
      border-color: #f36f21;
      background-color: #fdf5f5;
      box-shadow: 0 2px 8px rgba(243, 111, 33, 0.2);
    }
    .payment-method i {
      font-size: 28px;
      color: #f36f21;
    }
    .payment-method-name {
      font-weight: 500;
      color: #333;
    }
    .amount-section {
      background-color: #f9f9f9;
      border-radius: 8px;
      padding: 15px;
      margin-bottom: 20px;
    }
    .amount-input {
      width: 100%;
      padding: 12px;
      border: 1px solid #e0e0e0;
      border-radius: 6px;
      font-size: 16px;
      margin-bottom: 10px;
    }
    .amount-input:focus {
      outline: none;
      border-color: #f36f21;
    }
    .confirm-btn {
      width: 100%;
      padding: 14px;
      background-color: #f36f21;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      font-weight: 500;
      cursor: pointer;
      transition: background-color 0.2s;
    }
    .confirm-btn:hover {
      background-color: #e05d18;
    }
    .confirm-btn:disabled {
      background-color: #ccc;
      cursor: not-allowed;
    }
    /* Responsive adjustments */
    @media (max-width: 480px) {
      body {
        padding: 20px 10px;
      }
      .container {
        max-width: 100%;
        border-radius: 0;
        box-shadow: none;
        min-height: 100vh;
      }
      .header {
        height: 160px;
      }
      .main-content {
        margin-top: -15px;
        padding: 0 15px 15px 15px;
      }
      .action-buttons {
        flex-direction: column;
        gap: 12px;
        padding: 10px;
      }
      .action-btn {
        width: 100%;
        font-size: 15px;
        padding: 14px 0;
      }
      .action-btn i {
        width: 36px;
        height: 36px;
        line-height: 36px;
        font-size: 22px;
      }
      .info-row {
        flex-direction: column;
        align-items: flex-start;
        padding: 8px 0;
        font-size: 14px;
      }
      .info-row span:last-child {
        margin-top: 4px;
        font-weight: 600;
        font-size: 16px;
      }
      .info-grid {
        grid-template-columns: 1fr;
        gap: 12px 0;
        margin-top: 15px;
        padding-top: 10px;
      }
      .info-item .value {
        font-size: 16px;
      }
      .commission-dynamics h2 {
        font-size: 16px;
        margin-bottom: 15px;
      }
      .commission-row {
        flex-direction: column;
        gap: 10px;
      }
      .commission-user {
        min-width: auto;
        font-size: 14px;
      }
      .commission-user img {
        width: 24px;
        height: 24px;
      }
      .commission-amount {
        min-width: auto;
        text-align: left;
      }
      .commission-amount span:last-child {
        font-size: 16px;
      }
      .payment-methods {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <header class="header">
      <!-- Background images rotate by JS -->
    </header>
    <main class="main-content">
      <section class="action-buttons">
        <button class="action-btn" id="rechargeBtn">
          <span>Recharge now</span>
          <i class="fas fa-wifi"></i>
        </button>
        <button class="action-btn">
          <span>Quick cash withdrawal</span>
          <i class="fas fa-dollar-sign"></i>
        </button>
        <button class="action-btn">
          <span>Invite friends</span>
          <i class="fas fa-user-plus"></i>
        </button>
      </section>
      <section class="user-info-card">
        <div class="info-row">
          <span>Username</span>
          <span>59162140451</span>
        </div>
        <div class="info-row">
          <span>Promotion code</span>
          <span>KdJtim</span>
        </div>
        <div class="info-grid">
          <div class="info-item">
            <span class="label">Account Balance</span>
            <span class="value">Rs. 300.00</span>
          </div>
          <div class="info-item">
            <span class="label">Mission funds</span>
            <span class="value">Rs. 300.00</span>
          </div>
          <div class="info-item">
            <span class="label">Today's earnings</span>
            <span class="value">Rs. 0.00</span>
          </div>
          <div class="info-item">
            <span class="label">Yesterday's earnings</span>
            <span class="value">Rs. 0.00</span>
          </div>
          <div class="info-item">
            <span class="label">Cumulative income</span>
            <span class="value">Rs. 0.00</span>
          </div>
          <div class="info-item">
            <span class="label">Team benefits</span>
            <span class="value">Rs. 0.00</span>
          </div>
        </div>
      </section>
      <section class="commission-dynamics">
        <h2>User commission income dynamics</h2>
        <div class="commission-row">
          <div class="commission-user">
            <img src="https://i.ibb.co/L1g3S3s/daraz-icon.png" alt="User Icon" />
            <span>923****60381</span>
          </div>
          <div class="commission-amount">
            <span>Commission</span>
            <span>Rs. 52,610.73</span>
          </div>
        </div>
      </section>
    </main>
  </div>

  <!-- Payment Modal -->
  <div class="payment-modal" id="paymentModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3 class="modal-title">Recharge Account</h3>
        <button class="close-modal" id="closeModal">&times;</button>
      </div>
      <div class="amount-section">
        <input type="number" class="amount-input" id="rechargeAmount" placeholder="Enter amount" min="1" step="1">
      </div>
      <div class="payment-methods">
        <div class="payment-method" data-method="credit-card">
          <i class="fas fa-credit-card"></i>
          <span class="payment-method-name">Credit Card</span>
        </div>
        <div class="payment-method" data-method="debit-card">
          <i class="fas fa-money-check-alt"></i>
          <span class="payment-method-name">Debit Card</span>
        </div>
        <div class="payment-method" data-method="paypal">
          <i class="fab fa-paypal"></i>
          <span class="payment-method-name">PayPal</span>
        </div>
        <div class="payment-method" data-method="bank-transfer">
          <i class="fas fa-university"></i>
          <span class="payment-method-name">Bank Transfer</span>
        </div>
        <div class="payment-method" data-method="upi">
          <i class="fas fa-mobile-alt"></i>
          <span class="payment-method-name">UPI</span>
        </div>
        <div class="payment-method" data-method="e-wallet">
          <i class="fas fa-wallet"></i>
          <span class="payment-method-name">E-Wallet</span>
        </div>
      </div>
      <button class="confirm-btn" id="confirmPayment" disabled>Confirm Payment</button>
    </div>
  </div>

  <script>
    const header = document.querySelector('.header');
 const images = [
      "https://picsum.photos/seed/daraz1/400/180.jpg",
      "https://picsum.photos/seed/daraz2/400/180.jpg",
      "https://picsum.photos/seed/daraz3/400/180.jpg"
    ];
    let currentIndex = 0;
    
    function changeBackground() {
      header.style.backgroundImage = `url(${images[currentIndex]})`;
      currentIndex = (currentIndex + 1) % images.length;
    }
    changeBackground(); // initial load
    setInterval(changeBackground, 5000); // change every 5 seconds

    // Payment modal functionality
    const rechargeBtn = document.getElementById('rechargeBtn');
    const paymentModal = document.getElementById('paymentModal');
    const closeModal = document.getElementById('closeModal');
    const paymentMethods = document.querySelectorAll('.payment-method');
    const confirmPayment = document.getElementById('confirmPayment');
    const rechargeAmount = document.getElementById('rechargeAmount');

    rechargeBtn.addEventListener('click', () => {
      paymentModal.style.display = 'flex';
    });

    closeModal.addEventListener('click', () => {
      paymentModal.style.display = 'none';
    });

    // Close modal when clicking outside
    paymentModal.addEventListener('click', (e) => {
      if (e.target === paymentModal) {
        paymentModal.style.display = 'none';
      }
    });

    // Payment method selection
    let selectedMethod = null;
    paymentMethods.forEach(method => {
      method.addEventListener('click', () => {
        // Remove selected class from all methods
        paymentMethods.forEach(m => m.classList.remove('selected'));
        // Add selected class to clicked method
        method.classList.add('selected');
        selectedMethod = method.dataset.method;
        validateForm();
      });
    });

    // Amount input validation
    rechargeAmount.addEventListener('input', validateForm);

    function validateForm() {
      if (rechargeAmount.value && rechargeAmount.value > 0 && selectedMethod) {
        confirmPayment.disabled = false;
      } else {
        confirmPayment.disabled = true;
      }
    }

    // Confirm payment
    confirmPayment.addEventListener('click', () => {
      const amount = rechargeAmount.value;
      const method = selectedMethod;
      
      // Here you would typically send this data to your server
      console.log(`Processing payment of Rs. ${amount} using ${method}`);
      
      // Show success message
      alert(`Payment of Rs. ${amount} via ${method} has been processed successfully!`);
      
      // Close modal
      paymentModal.style.display = 'none';
      
      // Reset form
      rechargeAmount.value = '';
      paymentMethods.forEach(m => m.classList.remove('selected'));
      selectedMethod = null;
      confirmPayment.disabled = true;
    });
  </script>
</body>
</html>
