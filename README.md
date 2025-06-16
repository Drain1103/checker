
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Daraz 3D Style Page</title>

    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet" />

    <style>
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

        .header {
            background-color: #fef5ef;
            background-image: url('https://i.ibb.co/p3yZ6J3/daraz-background.png');
            background-size: cover;
            background-position: center bottom;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 150px;
        }

        .logo-container {
            position: relative;
        }

        /* Hidden file input */
        #logoUpload {
            display: none;
        }

        .logo-container img {
            max-width: 130px;
            width: 130px;
            height: 130px;
            border-radius: 50%;
            object-fit: cover;
            cursor: pointer;
            transition: transform 0.3s ease;
            border: 3px solid white;
            box-shadow: 0 2px 10px rgba(0,0,0,0.15);
        }

        .logo-container img:hover {
            transform: scale(1.1);
        }

        .main-content {
            padding: 0 20px 20px 20px;
            margin-top: -20px;
            position: relative;
            z-index: 2;
        }

        .action-buttons,
        .user-info-card,
        .commission-dynamics {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            transform: translateZ(20px);
        }

        .action-buttons:hover,
        .user-info-card:hover,
        .commission-dynamics:hover {
            transform: translateZ(50px) rotateX(5deg);
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
        }

        .action-buttons {
            display: flex;
            justify-content: space-between;
            padding: 15px;
        }

        .action-btn {
            background-color: #fdf5f5;
            border: 1px solid #fce5e5;
            border-radius: 8px;
            padding: 12px 8px;
            width: 32%;
            text-align: center;
            cursor: pointer;
            font-size: 13px;
            font-weight: 500;
            color: #333;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
            transition: transform 0.2s ease-out;
        }

        .action-btn:hover {
            transform: translateY(-5px) scale(1.05);
        }

        .action-btn i {
            font-size: 18px;
            color: #f36f21;
            background-color: #fff;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            line-height: 30px;
            text-align: center;
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
            grid-template-columns: 1fr 1fr;
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
        }

        .commission-dynamics h2 {
            font-size: 18px;
            font-weight: 700;
            margin-top: 0;
            margin-bottom: 20px;
            text-align: left;
            color: #333;
        }

        .commission-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .commission-user {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 15px;
        }

        .commission-user img {
            width: 24px;
            height: 24px;
            border-radius: 50%;
        }

        .commission-amount {
            text-align: right;
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
    </style>
</head>
<body>

    <div class="container">
        <header class="header">
            <div class="logo-container">
                <!-- Hidden input for file upload -->
                <input type="file" id="logoUpload" accept="image/*" />
                <!-- Image that triggers file input on click -->
                <img id="customLogo" src="https://img.uxwing.com/wp-content/themes/uxwing/download/brands-social-media/daraz-logo-icon.png" alt="Daraz Logo" onclick="document.getElementById('logoUpload').click();" />
            </div>
        </header>

        <main class="main-content">
            <section class="action-buttons">
                <button class="action-btn">
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

    <script>
        document.getElementById('logoUpload').addEventListener('change', function(event) {
            const file = event.target.files[0];
            if (file) {
                const img = document.getElementById('customLogo');
                img.src = URL.createObjectURL(file);
            }
        });
    </script>

</body>
</html>
