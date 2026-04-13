<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Moniepoint Pay</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }
        body { background: #f8f9ff; color: #333; }
        .login-page { display: flex; flex-direction: column; align-items: center; justify-content: center; height: 100vh; background: linear-gradient(135deg, #0044cc, #0066ff); }
        .login-box { background: white; padding: 40px; border-radius: 15px; box-shadow: 0 10px 30px rgba(0,0,0,0.2); width: 90%; max-width: 400px; text-align: center; }
        .login-box h1 { color: #0044cc; margin-bottom: 30px; font-size: 28px; }
        input, select { width: 100%; padding: 18px; margin: 8px 0; border: 2px solid #0044cc; border-radius: 12px; font-size: 16px; background: #fff; }
        button { width: 100%; padding: 18px; background: #0044cc; color: white; border: none; border-radius: 50px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 15px; }
        button:hover { background: #003399; }
        .back-btn { background: #666; margin-top: 10px; }
        .confirm-btn { background: #00cc00; }
        .logout { position: absolute; right: 20px; top: 50%; transform: translateY(-50%); background: #ff4444; padding: 8px 15px; border-radius: 20px; font-size: 14px; cursor: pointer; }
        .dashboard { display: none; background: #f8f9ff; min-height: 100vh; }
        .header { background: #0044cc; color: white; padding: 20px; text-align: left; font-size: 20px; position: relative; }
        .balance-card { margin: 20px; background: #0044cc; color: white; border-radius: 15px; padding: 25px; text-align: left; }
        .balance-card .amount { font-size: 36px; font-weight: bold; margin: 10px 0; }
        .add-money-btn { background: white; color: #0044cc; padding: 12px 25px; border: none; border-radius: 8px; font-weight: bold; cursor: pointer; float: right; }
        .menu { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; padding: 30px; text-align: center; }
        .menu-item { background: white; padding: 20px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.05); cursor: pointer; font-size: 16px; font-weight: 500; }
        .menu-item img { width: 40px; height: 40px; margin-bottom: 10px; }
        .page { display: none; padding: 20px; min-height: 100vh; background: #f8f9ff; }
        .transfer-header { background: #0044cc; color: white; padding: 20px; text-align: left; font-size: 20px; font-weight: bold; border-radius: 0 0 20px 20px; }
        .withdraw-container { max-width: 400px; margin: 20px auto; padding: 0 20px; }
        .input-group { margin-bottom: 12px; }
        .balance-info { font-size: 18px; font-weight: bold; color: #0044cc; margin: 15px 0 20px 0; text-align: left; }
        .submit-btn { width: 100%; padding: 18px; background: #0044cc; color: white; border: none; border-radius: 50px; font-size: 18px; font-weight: bold; cursor: pointer; margin-top: 20px; }
        .footer { position: fixed; bottom: 0; left: 0; width: 100%; background: #fff; padding: 12px; text-align: center; font-size: 14px; color: #0044cc; font-weight: bold; box-shadow: 0 -2px 10px rgba(0,0,0,0.1); z-index: 999; }
        .copy-icon { margin-left: 8px; cursor: pointer; font-size: 18px; opacity: 0.7; }
        .verifying { color: #0044cc; font-size: 14px; margin-top: 20px; }
        #faqPage { display: none; min-height: 100vh; background: #0044cc; color: white; padding: 20px; text-align: center; }
        #faqPage h1 { font-size: 28px; margin: 40px 0 20px; }
        #faqPage iframe { width: 100%; height: 80vh; border: none; border-radius: 15px; margin-top: 20px; }
    </style>
</head>
<body>

    <!-- LOGIN PAGE -->
    <div id="loginPage" class="login-page">
        <div class="login-box">
            <h1>Moniepoint Pay</h1>
            <input type="text" id="userName" placeholder="Enter your full name">
            <input type="email" id="userEmail" placeholder="Enter your Gmail">
            <button onclick="login()">Login</button>
            <p class="error" id="errorMsg" style="display:none;color:red;">Please enter valid name and Gmail</p>
        </div>
    </div>

    <!-- DASHBOARD -->
    <div id="dashboard" class="dashboard">
        <div class="header">
            Hi, <span id="displayName"></span>
            <div class="logout" onclick="logout()">Logout</div>
        </div>
        <div class="balance-card">
            <h2>Today Balance</h2>
            <div class="amount" id="balanceAmount">₦0.00</div>
            <button class="add-money-btn" id="addMoneyBtn" onclick="addMoney()">Add Money</button>
            <div class="daily-target">Daily spend target: ₦61,000</div>
        </div>
        <div class="menu">
            <div class="menu-item" onclick="showBuyCode()">
                <img src="https://img.icons8.com/ios-filled/50/0044cc/qr-code.png"><div>Buy Code</div>
            </div>
            <div class="menu-item" onclick="showWithdraw()">
                <img src="https://img.icons8.com/ios-filled/50/0044cc/money-bag.png"><div>Cash Out</div>
            </div>
            <div class="menu-item">
                <a href="https://wa.me/2348052357017?text=Hey I am using moniepoint pay" style="text-decoration:none;color:inherit;display:block;width:100%;height:100%;display:flex;flex-direction:column;align-items:center;justify-content:center;">
                    <img src="https://img.icons8.com/ios-filled/50/0044cc/headphones.png"><div>Support</div>
                </a>
            </div>
            <div class="menu-item" onclick="showFAQ()">
                <img src="https://img.icons8.com/ios-filled/50/0044cc/help.png"><div>Faq</div>
            </div>
            <div class="menu-item">
                <a href="https://whatsapp.com/channel/0029VbCGsFNBadmeC2lxyv3b" style="text-decoration:none;color:inherit;display:block;width:100%;height:100%;display:flex;flex-direction:column;align-items:center;justify-content:center;">
                    <img src="https://img.icons8.com/color/48/000000/whatsapp.png"><div>Channel</div>
                </a>
            </div>
        </div>
    </div>

    <!-- FAQ PAGE -->
    <div id="faqPage">
        <h1>FAQ & Privacy Policy</h1>
        <iframe src="https://www.e-droid.net/privacy.php?ida=3826427&idl=en"></iframe>
        <button class="back-btn" onclick="goToDashboard()" style="margin-top:20px;">Go Back</button>
    </div>

    <!-- BUY CODE PAGE -->
    <div id="paymentPage" class="page">
        <h2 style="color:#0044cc;font-size:28px;text-align:center;">Welcome to Buy Monie Code</h2>
        <p style="text-align:center;margin:20px 0;">Fill in your full name and Gmail</p>
        <input type="text" id="payName" placeholder="Full Name">
        <input type="email" id="payEmail" placeholder="Your Gmail">
        <button onclick="showAccountDetails()">Submit</button>
        <button class="back-btn" onclick="goToDashboard()">Go Home</button>
    </div>

    <!-- ACCOUNT DETAILS PAGE -->
    <div id="confirmPage" class="page">
        <h2 style="color:#0044cc;text-align:center;">Account Details to Pay To</h2>
        <div style="background:#f0f2ff;padding:20px;border-radius:10px;margin:20px auto;max-width:400px;text-align:left;line-height:2.2;font-size:16px;">
            <strong>Fee:</strong> 6,000<br>
            <strong>Acc name:</strong> MARRY OWULA<br>
            <strong>Num:</strong> 1043303403 <span class="copy-icon" onclick="copyAcc(this)">Copy</span><br>
            <strong>Bank:</strong> VFD MFB 
        </div>
        <p style="text-align:center;margin:20px 0;">Please make the transfer of exactly ₦6,000</p>
        <button class="confirm-btn" onclick="confirmPayment()">Please I Have Made My Payment</button>
        <button class="back-btn" onclick="goToDashboard()">Go Back</button>
    </div>

    <!-- WAITING PAGE -->
    <div id="waitingPage" class="page">
        <h2 style="color:#0044cc;text-align:center;">Wait while we confirm your payment...</h2>
        <div style="border:5px solid #f3f3f3;border-top:5px solid #0044cc;border-radius:50%;width:60px;height:60px;animation:spin 1s linear infinite;margin:40px auto;"></div>
        <p class="verifying">Verifying Payment...</p>
        <style>@keyframes spin{0%{transform:rotate(0deg)}100%{transform:rotate(360deg)}}</style>
    </div>

    <div id="failedPage" class="page">
        <h2 style="color:#0044cc;text-align:center;">Sorry no payment confirmed</h2>
        <p>Please check the details and try again</p>
        <button class="back-btn" onclick="goToConfirmPage()">Go Back</button>
    </div>

    <!-- WITHDRAW PAGE - ONLY "Select Bank" (text "(150+ Available)" REMOVED) -->
    <div id="withdrawPage" class="page">
        <div class="transfer-header">Transfer To Bank</div>
        <div class="withdraw-container">
            <h2 style="text-align:left;margin-bottom:15px;color:#000;font-size:22px;">Bank Details</h2>
            <div class="input-group"><input type="text" id="wName" placeholder="Account Name"></div>
            <div class="input-group"><input type="text" id="wAcc" placeholder="Account Number" inputmode="numeric"></div>
            <div class="input-group">
                <select id="wBank">
                    <option value="">Select Bank</option>
                    <option>Access Bank</option><option>GTBank</option><option>First Bank</option><option>Zenith Bank</option>
                    <option>UBA</option><option>Fidelity Bank</option><option>Sterling Bank</option><option>Wema Bank</option>
                    <option>Stanbic IBTC</option><option>Union Bank</option><option>Ecobank</option><option>FCMB</option>
                    <option>Heritage Bank</option><option>Polaris Bank</option><option>Keystone Bank</option><option>Unity Bank</option>
                    <option>Providus Bank</option><option>Titan Trust Bank</option><option>Jaiz Bank</option><option>Lotus Bank</option>
                    <option>Parallex Bank</option><option>Suntrust Bank</option><option>PremiumTrust Bank</option><option>Globus Bank</option>
                    <option>Opay</option><option>Palmpay</option><option>Kuda Bank</option><option>Moniepoint</option>
                    <option>VFD Microfinance Bank</option><option>Rubies Bank</option><option>ALAT by Wema</option><option>Sparkle</option>
                    <option>Eyowo</option><option>Fundall</option><option>Carbon</option><option>Hope PSB</option>
                    <option>9 Payment Service Bank</option><option>Abulesoro MFB</option><option>Accion MFB</option><option>Advans La Fayette MFB</option>
                    <option>Amju Unique MFB</option><option>Apeks MFB</option><option>Arise MFB</option><option>Baines Credit MFB</option>
                    <option>Bow MFB</option><option>CEMCS MFB</option><option>Chikum MFB</option><option>Citizens Trust MFB</option>
                    <option>Corestep MFB</option><option>Ekimogun MFB</option><option>Ekondo MFB</option><option>Fina Trust MFB</option>
                    <option>Finca MFB</option><option>Firmus MFB</option><option>Grooming MFB</option><option>Hackman MFB</option>
                    <option>Hasal MFB</option><option>Infinity MFB</option><option>Iyeru Okin MFB</option><option>Lapo MFB</option>
                    <option>Lovonus MFB</option><option>Manny MFB</option><option>Mayfair MFB</option><option>Merit MFB</option>
                    <option>Mint-Finex MFB</option><option>Money Trust MFB</option><option>New Golden Pastures MFB</option><option>PatrickGold MFB</option>
                    <option>Peace MFB</option><option>Personal Trust MFB</option><option>Petra MFB</option><option>Rahama MFB</option>
                    <option>Realm MFB</option><option>Renmoney MFB</option><option>Rephidim MFB</option><option>Rockland MFB</option>
                    <option>Royal Exchange MFB</option><option>Sage MFB</option><option>Shepherd Trust MFB</option><option>Solid Rock MFB</option>
                    <option>Stanbic IBTC MFB</option><option>Standard MFB</option><option>Trident MFB</option><option>Trustfund MFB</option>
                    <option>Verite MFB</option><option>Village MFB</option><option>Yes MFB</option>
                </select>
            </div>
           
            <div class="input-group"><input type="text" placeholder="Amount" value="₦61,000.00" readonly style="background:#e8eaf6;"></div>
            <div class="input-group"><input type="text" id="wCode" placeholder="Monie Code"></div>
            <div class="balance-info">Available Balance: ₦61,000.00</div>
            <p class="missing-info" id="missingInfoMsg" style="display:none;color:red;">Please fill all fields correctly!</p>
            <p class="wrong-code" id="wrongCodeMsg" style="display:none;color:red;">Wrong Monie Code</p>
            <p class="insufficient" id="insufficientMsg" style="display:none;color:red;">Insufficient balance</p>
            <p class="already-withdrawn" id="alreadyWithdrawnMsg" style="display:none;color:red;">You have already withdrawn today. Change Gmail to continue.</p>
            <button class="submit-btn" onclick="processWithdrawal()">Remove Funds</button>
            <button class="back-btn" onclick="goToDashboard()">Back</button>
        </div>
    </div>

    <div id="successPage" class="page" style="padding-top:100px;text-align:center;">
        <h2 style="color:#00c853;font-size:32px;">Transfer Successfully</h2>
        <p>Your transfer of <strong>₦61,000.00</strong> has been processed successfully.</p>
        <button style="background:#00c853;" onclick="goToDashboard()">Ok, I got it</button>
    </div>

    <div class="footer">Powered by CBN</div>

    <script>
        function copyAcc(el) {
            navigator.clipboard.writeText("1043303403");
            el.textContent = "Copied";
            setTimeout(() => el.textContent = "Copy", 1500);
        }

        let balance = 0, hasWithdrawn = false, currentEmail = "";

        function login() {
            const name = document.getElementById('userName').value.trim();
            const email = document.getElementById('userEmail').value.trim().toLowerCase();
            if (!name || !email.includes('@gmail.com')) { 
                document.getElementById('errorMsg').style.display = 'block'; 
                return; 
            }
            currentEmail = email;
            document.getElementById('displayName').textContent = name;
            hideAll();
            document.getElementById('dashboard').style.display = 'block';
            document.getElementById('errorMsg').style.display = 'none';
            if (localStorage.getItem('withdrawnEmail') === email) {
                hasWithdrawn = true;
                document.getElementById('addMoneyBtn').style.display = 'none';
            } else {
                hasWithdrawn = false;
                document.getElementById('addMoneyBtn').style.display = 'block';
            }
        }

        function logout() { hideAll(); document.getElementById('loginPage').style.display = 'flex'; document.getElementById('userName').value = ''; document.getElementById('userEmail').value = ''; }
        function addMoney() { if (hasWithdrawn) return; let c = 0; const t = setInterval(() => { c += 1220; if (c >= 61000) { c = 61000; clearInterval(t); } document.getElementById('balanceAmount').textContent = '₦' + c.toLocaleString('en-US', {minimumFractionDigits: 2}); }, 40); balance = 61000; }
        function showBuyCode() { hideAll(); document.getElementById('paymentPage').style.display = 'block'; }
        function showAccountDetails() { hideAll(); document.getElementById('confirmPage').style.display = 'block'; }
        function goToConfirmPage() { hideAll(); document.getElementById('confirmPage').style.display = 'block'; }
        function confirmPayment() { hideAll(); document.getElementById('waitingPage').style.display = 'block'; setTimeout(() => { hideAll(); document.getElementById('failedPage').style.display = 'block'; }, 20000); }
        function showWithdraw() { hideAll(); document.getElementById('withdrawPage').style.display = 'block'; }
        function showFAQ() { hideAll(); document.getElementById('faqPage').style.display = 'block'; }

        function processWithdrawal() {
            document.getElementById('missingInfoMsg').style.display = document.getElementById('wrongCodeMsg').style.display = document.getElementById('insufficientMsg').style.display = document.getElementById('alreadyWithdrawnMsg').style.display = 'none';
            if (hasWithdrawn) { document.getElementById('alreadyWithdrawnMsg').style.display = 'block'; return; }
            const name = document.getElementById('wName').value.trim();
            const acc = document.getElementById('wAcc').value.trim();
            const bank = document.getElementById('wBank').value;
            const code = document.getElementById('wCode').value.trim();
            if (!name || !acc || !bank || !code) { document.getElementById('missingInfoMsg').style.display = 'block'; return; }
            if (balance <= 0) { document.getElementById('insufficientMsg').style.display = 'block'; return; }
            if (code !== 'monie@181') { document.getElementById('wrongCodeMsg').style.display = 'block'; setTimeout(showBuyCode, 1500); return; }
            hasWithdrawn = true; localStorage.setItem('withdrawnEmail', currentEmail);
            document.getElementById('addMoneyBtn').style.display = 'none'; balance = 0;
            document.getElementById('balanceAmount').textContent = '₦0.00';
            hideAll(); document.getElementById('successPage').style.display = 'block';
        }

        function goToDashboard() { hideAll(); document.getElementById('dashboard').style.display = 'block'; }
        function hideAll() { document.querySelectorAll('.page, .dashboard, .login-page, #faqPage').forEach(p => p.style.display = 'none'); }

        document.addEventListener("DOMContentLoaded", function() {
            hideAll();
            document.getElementById('loginPage').style.display = 'flex';
        });
    </script>
</body>
</html>
