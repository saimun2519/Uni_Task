<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>UniTask – Earn with Ads & Tasks</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Inter', 'Hind Siliguri', sans-serif;
            background: #f0f4f8;
            color: #1e293b;
            max-width: 640px;
            margin: 0 auto;
            min-height: 100vh;
            position: relative;
        }
        .loading-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(255,255,255,0.9); display: none;
            justify-content: center; align-items: center; z-index: 9999;
        }
        .spinner {
            width: 50px; height: 50px; border: 5px solid #e0e0e0;
            border-top: 5px solid #2e7d32; border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        
        .auth-container {
            min-height: 100vh; display: flex; align-items: center; justify-content: center;
            padding: 20px; background: linear-gradient(135deg, #f0f4f8, #e0eae0);
        }
        .auth-card {
            background: white; border-radius: 40px; padding: 40px 30px;
            width: 100%; max-width: 400px; box-shadow: 0 20px 40px rgba(0,40,0,0.1);
        }
        .auth-logo { font-size: 32px; font-weight: 700; color: #2e7d32; text-align: center; margin-bottom: 30px; }
        .auth-input {
            width: 100%; padding: 16px 20px; border: 2px solid #e0eae0;
            border-radius: 40px; font-size: 15px; margin-bottom: 15px;
        }
        .auth-input:focus { border-color: #2e7d32; outline: none; }
        .auth-btn {
            width: 100%; padding: 16px; background: #2e7d32; color: white;
            border: none; border-radius: 40px; font-size: 16px; font-weight: 600;
            cursor: pointer; margin: 10px 0;
        }
        .auth-btn:hover { background: #1b5e20; }
        .auth-link { text-align: center; margin-top: 20px; color: #64748b; cursor: pointer; }
        .auth-link span { color: #2e7d32; font-weight: 600; }
        .auth-error { color: #dc3545; text-align: center; margin: 10px 0; font-size: 14px; background: #ffe6e6; padding: 8px; border-radius: 20px; }
        .auth-success { color: #2e7d32; text-align: center; margin: 10px 0; font-size: 14px; background: #e6ffe6; padding: 8px; border-radius: 20px; }
        
        #mainApp { display: none; }
        
        .mini-header {
            display: flex; justify-content: space-between; align-items: center;
            padding: 12px 16px; background: transparent;
        }
        .logo-small { font-size: 20px; font-weight: 700; color: #2e7d32; }
        .header-right { display: flex; gap: 16px; align-items: center; position: relative; }
        .header-right i { font-size: 20px; color: #5e6f88; cursor: pointer; }
        .language-selector {
            background: #e8f5e9; border: none; padding: 6px 12px; border-radius: 30px;
            font-size: 14px; font-weight: 600; color: #2e7d32; cursor: pointer;
        }
        .notification-badge {
            position: absolute; top: -5px; right: 60px;
            background: #dc3545; color: white; border-radius: 50%;
            width: 18px; height: 18px; font-size: 11px;
            display: flex; align-items: center; justify-content: center; font-weight: bold;
        }
        
        .page { display: none; padding: 0 16px 80px; }
        .page.active { display: block; }
        
        .bottom-nav {
            position: fixed; bottom: 0; left: 0; right: 0; max-width: 640px; margin: 0 auto;
            background: white; display: flex; justify-content: space-around;
            padding: 8px 8px 18px; border-radius: 30px 30px 0 0;
            box-shadow: 0 -4px 15px rgba(0,20,0,0.05); border-top: 1px solid #e0eae0;
        }
        .nav-item {
            display: flex; flex-direction: column; align-items: center;
            color: #8a9cb0; font-size: 11px; font-weight: 500; cursor: pointer;
        }
        .nav-item i { font-size: 22px; margin-bottom: 2px; }
        .nav-item.active { color: #2e7d32; }
        
        .section-title {
            font-size: 18px; font-weight: 600; color: #1b4a2c;
            margin: 18px 0 14px; padding-left: 8px; border-left: 4px solid #f39c12;
        }
        
        .ad-card {
            background: white; border-radius: 24px; padding: 20px 22px; margin-bottom: 16px;
            display: flex; justify-content: space-between; align-items: center;
            box-shadow: 0 4px 12px rgba(0,20,0,0.05);
            border: 1px solid rgba(70,140,70,0.2); cursor: pointer; position: relative;
        }
        .ad-info h4 { font-size: 18px; font-weight: 600; color: #1b4a2c; margin-bottom: 6px; }
        .ad-info p { color: #64748b; font-size: 13px; display: flex; align-items: center; gap: 6px; }
        .ad-reward {
            background: #2e7d32; color: white; font-size: 18px; font-weight: 600;
            padding: 10px 20px; border-radius: 40px; display: flex; align-items: center; gap: 8px;
        }
        .ad-progress {
            position: absolute; bottom: -1px; left: 0; width: 100%; height: 5px;
            background: #e0eae0; border-radius: 0 0 24px 24px; overflow: hidden;
        }
        .ad-progress-fill { height: 100%; background: #2e7d32; width: 0%; transition: width 0.3s; }
        .ad-limit-text { font-size: 12px; color: #2e7d32; margin-left: 10px; font-weight: 500; }
        
        .task-card {
            background: white; border-radius: 20px; padding: 16px 20px; margin-bottom: 12px;
            display: flex; justify-content: space-between; align-items: center;
            box-shadow: 0 2px 8px rgba(0,40,0,0.05); border: 1px solid #c8e6c9;
            cursor: pointer; transition: 0.2s;
        }
        .task-card:hover { transform: translateY(-2px); }
        .task-info h4 { font-size: 16px; font-weight: 600; color: #1b4a2c; display: flex; align-items: center; gap: 8px; flex-wrap: wrap; }
        .task-reward {
            background: #f39c12; color: white; font-size: 14px; font-weight: 600;
            padding: 6px 14px; border-radius: 40px; display: flex; align-items: center; gap: 6px;
        }
        .status-badge {
            font-size: 11px; padding: 3px 10px; border-radius: 20px; font-weight: 500;
        }
        .status-badge.pending { background: #ff9800; color: white; }
        .status-badge.approved { background: #2e7d32; color: white; }
        .status-badge.rejected { background: #dc3545; color: white; }
        
        .social-strip {
            display: flex; justify-content: space-between; background: white;
            border-radius: 50px; padding: 12px 24px; margin: 15px 0 10px;
        }
        .social-icon {
            width: 42px; height: 42px; border-radius: 50%; display: flex;
            align-items: center; justify-content: center; font-size: 20px;
            color: white; cursor: pointer;
        }
        .telegram { background: #0088cc; }
        .youtube { background: #ff0000; }
        .facebook { background: #1877f2; }
        .tiktok { background: #010101; }
        .instagram { background: linear-gradient(45deg, #f09433, #d62976, #962fbf); }
        .support-btn {
            background: #2e7d32; color: white; padding: 12px 20px; border-radius: 40px;
            display: inline-block; text-align: center; font-weight: 600; cursor: pointer;
            margin: 15px 0; width: 100%;
        }
        
        .ref-card {
            background: white; border-radius: 26px; padding: 24px 18px;
            text-align: center; margin-bottom: 18px;
        }
        .ref-link-box, .ref-username-box {
            background: #e8f5e9; border: 1px dashed #2e7d32; border-radius: 40px;
            padding: 12px 15px; font-size: 13px; margin: 16px 0;
            display: flex; align-items: center; justify-content: space-between;
        }
        .copy-icon { color: #2e7d32; cursor: pointer; font-size: 18px; }
        .copy-btn {
            background: #2e7d32; color: white; border: none; padding: 10px 28px;
            border-radius: 40px; font-size: 14px; font-weight: 600;
            display: inline-flex; align-items: center; gap: 8px; cursor: pointer;
        }
        .stats-row { display: flex; gap: 12px; margin-bottom: 16px; }
        .stat-item {
            background: white; flex: 1; padding: 16px; border-radius: 22px;
            text-align: center; border: 1px solid #e0f0e0;
        }
        .stat-value { font-size: 26px; font-weight: 700; color: #2e7d32; }
        .stat-label { font-size: 13px; color: #64748b; }
        .ranking-table {
            background: white; border-radius: 26px; padding: 20px; margin: 20px 0;
        }
        .ranking-item {
            display: flex; align-items: center; justify-content: space-between;
            padding: 10px 0; border-bottom: 1px solid #e0eae0;
        }
        .rank-number { font-weight: 700; color: #2e7d32; width: 30px; }
        .rank-name { flex: 1; font-weight: 500; }
        .rank-value { font-weight: 600; color: #1b4a2c; }
        
        .vip-info-board {
            background: #ffffff; border-radius: 26px; padding: 20px;
            margin: 20px 0; border: 1px solid #c8e6c9;
        }
        .vip-list { display: flex; flex-direction: column; gap: 12px; }
        .vip-level-card {
            background: #f8fafc; border-radius: 20px; padding: 14px 18px;
            display: flex; justify-content: space-between; align-items: center;
            border: 1px solid #e0eae0;
        }
        .vip-level-name { font-weight: 700; color: #2e7d32; font-size: 16px; }
        .vip-level-details { font-size: 13px; color: #4b5563; margin-top: 4px; }
        .vip-level-stats { text-align: right; font-weight: 600; }
        .vip-note { font-size: 12px; color: #64748b; margin-top: 16px; padding-top: 10px; border-top: 1px dashed #c8e6c9; text-align: center; }
        .vip-summary { background: #f8fafc; border-radius: 20px; padding: 16px; margin: 16px 0; }
        
        .profile-card {
            background: white; border-radius: 26px; padding: 18px;
            display: flex; gap: 16px; align-items: center; margin-bottom: 16px;
            border: 1px solid #e0f0e0;
        }
        .profile-pic {
            width: 56px; height: 56px; border-radius: 50%; background: #c8e6c9;
            display: flex; align-items: center; justify-content: center;
            font-size: 30px; color: #2e7d32; border: 2px solid #2e7d32;
            overflow: hidden; cursor: pointer;
        }
        .profile-pic img { width: 100%; height: 100%; object-fit: cover; }
        .profile-info h3 { font-size: 18px; font-weight: 600; color: #1b3b2a; }
        .profile-info p { font-size: 13px; color: #5e768d; }
        .balance-box {
            background: #e8f5e9; border-radius: 40px; padding: 16px 20px;
            display: flex; justify-content: space-between; font-size: 18px;
            font-weight: 600; color: #1b5e20; margin: 16px 0;
            border: 1px solid #a5d6a7;
            transition: all 0.3s ease;
        }
        .balance-box.highlight {
            background: #c8e6c9;
            transform: scale(1.02);
        }
        .withdraw-btn {
            background: #d32f2f; color: white; border: none; padding: 15px;
            border-radius: 40px; font-size: 16px; font-weight: 600;
            width: 100%; cursor: pointer; margin-bottom: 16px;
        }
        
        .notice-board {
            background: #ffffff; border-radius: 24px; padding: 20px;
            margin: 20px 0; border: 1px solid #e0eae0;
        }
        
        .withdraw-form, .task-modal, .activation-modal, .fullscreen-modal, .edit-profile-modal {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5); z-index: 5000;
            justify-content: center; align-items: center; padding: 20px;
        }
        .withdraw-form-content, .task-modal-content, .activation-modal-content, .edit-profile-content {
            background: white; border-radius: 30px; padding: 25px;
            width: 100%; max-width: 450px; max-height: 80vh; overflow-y: auto;
        }
        .min-withdraw-info {
            background: #f8fafc; padding: 12px; border-radius: 20px;
            margin: 12px 0; font-size: 13px; text-align: center;
            color: #2e7d32; border: 1px solid #c8e6c9;
        }
        .method-selector { display: flex; gap: 10px; margin-bottom: 15px; }
        .method-btn {
            flex: 1; padding: 12px; border: 2px solid #e0eae0; border-radius: 40px;
            background: white; font-weight: 600; cursor: pointer;
        }
        .method-btn.active { border-color: #2e7d32; background: #e8f5e9; color: #2e7d32; }
        .input-field {
            width: 100%; padding: 14px 18px; border: 1px solid #d0e0d0;
            border-radius: 40px; margin-bottom: 12px; font-size: 14px;
        }
        .cancel-btn { background: #6c757d; margin-top: 8px; }
        
        .task-description-box {
            background: #f8fafc; padding: 15px; border-radius: 20px;
            margin: 15px 0; font-size: 14px; border: 1px solid #e0eae0;
        }
        .dropdown-menu {
            position: absolute; top: 55px; right: 16px; background: white;
            border-radius: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            display: none; z-index: 100; min-width: 200px;
            border: 1px solid #e0f0e0;
        }
        .dropdown-menu div {
            padding: 14px 18px; cursor: pointer; font-size: 14px;
            display: flex; align-items: center; gap: 12px;
            border-bottom: 1px solid #f0f7f0;
        }
        .dropdown-menu div:hover { background: #f5f5f5; }
        .dropdown-menu div i { width: 20px; color: #2e7d32; }
        
        .fullscreen-modal {
            background: #111; display: none; flex-direction: column; padding: 0;
        }
        .ad-header {
            display: flex; justify-content: space-between; align-items: center;
            padding: 16px 20px; background: rgba(0,0,0,0.7); color: white;
        }
        .ad-timer {
            font-size: 32px; font-weight: 700; color: #2e7d32;
            background: rgba(255,255,255,0.1); padding: 8px 20px; border-radius: 50px;
        }
        .ad-header-buttons { display: flex; gap: 12px; }
        .corner-btn {
            width: 48px; height: 48px; border-radius: 50%;
            background: rgba(255,255,255,0.2); backdrop-filter: blur(4px);
            color: white; font-size: 24px; display: flex;
            align-items: center; justify-content: center; cursor: pointer;
            border: 1px solid rgba(255,255,255,0.3);
        }
        .ad-content { flex: 1; display: flex; justify-content: center; align-items: center; padding: 20px; }
        .ad-iframe {
            width: 100%; height: 70vh; min-height: 400px;
            border: 2px solid #2e7d32; border-radius: 30px; background: white;
        }
        
        .notification {
            position: fixed; top: 20px; right: 20px; background: #2e7d32;
            color: white; padding: 12px 24px; border-radius: 40px;
            z-index: 9999; animation: slideIn 0.3s;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
            max-width: 300px;
        }
        .notification.error { background: #dc3545; }
        .notification.info { background: #2196f3; }
        .notification.warning { background: #ff9800; }
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        .activation-banner, .activation-pending { background: #fff3e0; padding: 12px; border-radius: 24px; margin-bottom: 20px; text-align: center; }
        .activate-now-btn { background: #f39c12; border: none; padding: 8px 16px; border-radius: 40px; margin-left: 12px; color: white; font-weight: bold; cursor: pointer; }
        
        .pending-count-badge {
            background: #ff9800;
            color: white;
            border-radius: 20px;
            padding: 2px 8px;
            font-size: 11px;
            margin-left: 8px;
        }
    </style>
</head>
<body>
    <div class="loading-overlay" id="loadingOverlay"><div class="spinner"></div></div>

    <div id="authPages">
        <div class="auth-container">
            <div class="auth-card">
                <div class="auth-logo">UniTask</div>
                <div id="loginForm">
                    <input type="email" id="loginEmail" class="auth-input" placeholder="Email Address / ইমেইল">
                    <input type="password" id="loginPassword" class="auth-input" placeholder="Password / পাসওয়ার্ড">
                    <div id="loginError" class="auth-error"></div>
                    <button class="auth-btn" onclick="handleLogin()">Login / লগইন</button>
                    <div class="auth-link" onclick="showRegister()">New user? <span>Create Account</span> / নতুন? <span>অ্যাকাউন্ট খুলুন</span></div>
                </div>
                <div id="registerForm" style="display:none;">
                    <input type="email" id="regEmail" class="auth-input" placeholder="Email Address / ইমেইল">
                    <input type="text" id="regUsername" class="auth-input" placeholder="Username / ইউজারনেম">
                    <input type="password" id="regPassword" class="auth-input" placeholder="Password / পাসওয়ার্ড">
                    <input type="password" id="regConfirmPassword" class="auth-input" placeholder="Confirm Password / পাসওয়ার্ড নিশ্চিত">
                    <input type="text" id="regReferral" class="auth-input" placeholder="Referral Username (optional) / রেফারেল ইউজারনেম (ঐচ্ছিক)">
                    <div id="registerError" class="auth-error"></div>
                    <div id="registerSuccess" class="auth-success"></div>
                    <button class="auth-btn" onclick="handleRegister()">Register / রেজিস্টার</button>
                    <div class="auth-link" onclick="showLogin()">Already have account? <span>Login</span> / ইতিমধ্যে অ্যাকাউন্ট আছে? <span>লগইন</span></div>
                </div>
            </div>
        </div>
    </div>

    <div id="mainApp">
        <div class="mini-header">
            <div class="logo-small">UniTask</div>
            <div class="header-right">
                <select class="language-selector" id="languageSelect" onchange="changeLanguage(this.value)">
                    <option value="en">English</option>
                    <option value="bn">বাংলা</option>
                </select>
                <i class="fas fa-bell" id="notificationBell"></i>
                <span class="notification-badge" id="notificationBadge" style="display:none;">0</span>
                <i class="fas fa-sliders-h" id="settingsIcon"></i>
            </div>
        </div>

        <div id="homePage" class="page active"></div>
        <div id="tasksPage" class="page"></div>
        <div id="sharePage" class="page"></div>
        <div id="profilePage" class="page"></div>

        <div class="bottom-nav">
            <div class="nav-item active" data-page="home"><i class="fas fa-home"></i><span id="navHome">HOME</span></div>
            <div class="nav-item" data-page="tasks"><i class="fas fa-tasks"></i><span id="navTask">TASK</span></div>
            <div class="nav-item" data-page="share"><i class="fas fa-share-alt"></i><span id="navShare">SHARE</span></div>
            <div class="nav-item" data-page="profile"><i class="fas fa-user"></i><span id="navProfile">PROFILE</span></div>
        </div>

        <div class="fullscreen-modal" id="adModal">
            <div class="ad-header">
                <div class="ad-timer" id="adTimerFull">00:00</div>
                <div class="ad-header-buttons">
                    <div class="corner-btn" id="skipAdCorner" style="display:none;">⏭</div>
                    <div class="corner-btn" id="closeAdCorner" style="display:none;">✕</div>
                </div>
            </div>
            <div class="ad-content">
                <iframe class="ad-iframe" id="adIframe" sandbox="allow-scripts allow-same-origin allow-popups allow-forms" src="about:blank"></iframe>
            </div>
        </div>

        <div class="task-modal" id="taskModal">
            <div class="task-modal-content">
                <h3 id="taskModalTitle">Submit Task Proof</h3>
                <div id="taskDescriptionDisplay" class="task-description-box"></div>
                <p id="taskRewardDisplay" style="font-weight:bold; margin-bottom:10px;"></p>
                <textarea id="taskProofText" placeholder="Write your proof here..." rows="4" class="input-field"></textarea>
                <button onclick="submitTaskProof()" class="auth-btn" id="submitTaskBtn">Submit for Review</button>
                <button onclick="closeTaskModal()" class="auth-btn cancel-btn" id="cancelTaskBtn">Cancel</button>
            </div>
        </div>

        <div class="activation-modal" id="activationModal">
            <div class="activation-modal-content">
                <h3>🔓 Activate Your Account</h3>
                <div class="activation-info">
                    <p><strong>Activation Fee:</strong> <span id="activationFee">100</span> BDT</p>
                    <p><strong>bKash:</strong> <span id="bkashNumber">01700000000</span></p>
                    <p><strong>Nagad:</strong> <span id="nagadNumber">01700000001</span></p>
                    <p style="color:#d32f2f;">After payment, fill the form. Activation within 24 hours.</p>
                </div>
                <div class="method-selector">
                    <button class="method-btn" onclick="selectActivationMethod(this, 'bkash')">bKash</button>
                    <button class="method-btn" onclick="selectActivationMethod(this, 'nagad')">Nagad</button>
                </div>
                <input type="text" id="activationTransactionId" class="input-field" placeholder="Transaction ID (TrxID)">
                <input type="number" id="activationAmount" class="input-field" placeholder="Amount (BDT)" readonly value="100">
                <button onclick="submitActivationRequest()" class="auth-btn">Submit Payment Info</button>
                <button onclick="closeActivationModal()" class="auth-btn cancel-btn">Cancel</button>
            </div>
        </div>

        <div id="withdrawForm" class="withdraw-form">
            <div class="withdraw-form-content">
                <h3>Withdraw Balance</h3>
                <div id="minWithdrawInfo" class="min-withdraw-info"></div>
                <div class="method-selector">
                    <button class="method-btn" onclick="selectWithdrawMethod(this, 'bkash')">Bkash</button>
                    <button class="method-btn" onclick="selectWithdrawMethod(this, 'nagad')">Nagad</button>
                    <button class="method-btn" onclick="selectWithdrawMethod(this, 'binance')">Binance</button>
                </div>
                <input type="text" id="withdrawAccount" class="input-field" placeholder="Account Number">
                <input type="number" id="withdrawAmount" class="input-field" placeholder="Amount (BDT)">
                <button onclick="submitWithdraw()" class="auth-btn">Submit Request</button>
                <button onclick="closeWithdrawForm()" class="auth-btn cancel-btn">Cancel</button>
            </div>
        </div>

        <div class="dropdown-menu" id="profileMenu">
            <div onclick="editProfile()"><i class="fas fa-user-edit"></i> Edit Profile</div>
            <div onclick="contactSupport()"><i class="fas fa-headset"></i> Contact</div>
            <div onclick="aboutApp()"><i class="fas fa-info-circle"></i> About</div>
            <div onclick="logout()"><i class="fas fa-sign-out-alt"></i> Log Out</div>
        </div>

        <div class="edit-profile-modal" id="editProfileModal">
            <div class="edit-profile-content">
                <h3>Edit Profile</h3>
                <input type="text" id="editName" class="input-field" placeholder="Full Name">
                <input type="text" id="editUsername" class="input-field" placeholder="Username">
                <input type="password" id="editPassword" class="input-field" placeholder="New Password (optional)">
                <button onclick="saveProfileChanges()" class="auth-btn">Save Changes</button>
                <button onclick="closeEditProfile()" class="auth-btn cancel-btn">Cancel</button>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, onAuthStateChanged, signOut, updatePassword } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getFirestore, collection, query, where, getDocs, addDoc, updateDoc, doc, getDoc, onSnapshot, orderBy, limit, increment, setDoc, serverTimestamp, runTransaction } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";
        import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-storage.js";

        const firebaseConfig = {
            apiKey: "AIzaSyDp5ptxuQaZ8xMSDu4ZlRJ0P3UV5TQD3fE",
            authDomain: "uni-da9b5.firebaseapp.com",
            projectId: "uni-da9b5",
            storageBucket: "uni-da9b5.appspot.com",
            messagingSenderId: "828115344512",
            appId: "1:828115344512:web:aa1cdb6e6b52567a8b9a65"
        };
        
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);
        const storage = getStorage(app);

        let currentUser = null, currentUserDoc = null, currentAd = null, adStep = 1, timerInterval = null, timeLeft = 0;
        let withdrawMethod = 'bkash', activationMethod = 'bkash', currentTask = null;
        let adBoxes = [], networks = [], socialLinks = {}, tasks = [], userSubmissions = [], adWatchCounts = {}, activationPending = false;
        let settings = { minWithdraw: 2000, referralBonus: 200, announcement: "Welcome to UniTask!", aboutUs: "UniTask - Earn money", activationFee: 100, bkashNumber: "01700000000", nagadNumber: "01700000001" };
        let supportGroupLink = 'https://t.me/+i7ubfptv0wBiZDc9';
        let currentLanguage = 'en';
        let translations = {
            en: {
                home: "HOME", task: "TASK", share: "SHARE", profile: "PROFILE",
                submitTask: "Submit for Review", cancel: "Cancel",
                taskSubmitted: "✅ Task submitted successfully!",
                approvalWait: "Admin will review within 24 hours."
            },
            bn: {
                home: "হোম", task: "টাস্ক", share: "শেয়ার", profile: "প্রোফাইল",
                submitTask: "জমা দিন", cancel: "বাতিল",
                taskSubmitted: "✅ টাস্ক সফলভাবে জমা হয়েছে!",
                approvalWait: "এডমিন ২৪ ঘন্টার মধ্যে রিভিউ করবেন।"
            }
        };
        let vipLevels = [
            { name: "UniStart", minReferrals: 0, commission: 2, salary: 0, salaryDay: 30 },
            { name: "UniStep", minReferrals: 10, commission: 3, salary: 40, salaryDay: 30 },
            { name: "UniEdge", minReferrals: 25, commission: 4, salary: 90, salaryDay: 30 },
            { name: "UniPulse", minReferrals: 52, commission: 5, salary: 140, salaryDay: 30 },
            { name: "UniPrime", minReferrals: 90, commission: 5, salary: 210, salaryDay: 30 },
            { name: "UniPro", minReferrals: 150, commission: 5, salary: 320, salaryDay: 30 },
            { name: "UniElite", minReferrals: 200, commission: 5, salary: 450, salaryDay: 30 }
        ];
        
        function showLoading() { document.getElementById('loadingOverlay').style.display = 'flex'; }
        function hideLoading() { document.getElementById('loadingOverlay').style.display = 'none'; }
        function formatBDT(amt) { return Number(amt).toFixed(2); }
        
        function showNotification(msg, type = 'success') { 
            const n = document.createElement('div'); 
            n.className = 'notification ' + type; 
            n.innerHTML = `<i class="fas ${type === 'error' ? 'fa-exclamation-circle' : type === 'info' ? 'fa-info-circle' : 'fa-check-circle'}"></i> ${msg}`; 
            document.body.appendChild(n); 
            setTimeout(() => n.remove(), 4000); 
        }
        
        function animateBalance() {
            const balanceBox = document.querySelector('.balance-box');
            if (balanceBox) {
                balanceBox.classList.add('highlight');
                setTimeout(() => balanceBox.classList.remove('highlight'), 500);
            }
        }
        
        function escapeHtml(str) {
            if (!str) return '';
            return str.replace(/[&<>]/g, function(m) {
                if (m === '&') return '&amp;';
                if (m === '<') return '&lt;';
                if (m === '>') return '&gt;';
                return m;
            });
        }
        
        async function loadSettings() { 
            try { 
                const gen = await getDoc(doc(db, "settings", "general")); 
                if (gen.exists()) { 
                    settings.minWithdraw = gen.data().minWithdraw || 2000; 
                    settings.referralBonus = gen.data().referralBonus || 200; 
                } 
                const notice = await getDoc(doc(db, "settings", "notice")); 
                if (notice.exists()) settings.announcement = notice.data().message; 
                const act = await getDoc(doc(db, "settings", "activation")); 
                if (act.exists()) { 
                    settings.activationFee = act.data().fee || 100; 
                    settings.bkashNumber = act.data().bkash || "01700000000"; 
                    settings.nagadNumber = act.data().nagad || "01700000001"; 
                } 
            } catch(e) { console.error(e); } 
        }
        
        async function loadAdBoxes() { 
            try { 
                const snap = await getDocs(query(collection(db, "adboxes"), where("status", "==", "active"))); 
                adBoxes = snap.docs.map(d => ({ id: d.id, ...d.data() })); 
            } catch(e) { console.error("Ad boxes error:", e); } 
        }
        
        async function loadNetworks() { 
            try { 
                const snap = await getDocs(collection(db, "networks")); 
                networks = snap.docs.map(d => ({ id: d.id, ...d.data() })); 
            } catch(e) { console.error("Networks error:", e); } 
        }
        
        async function loadSocialLinks() { 
            try { 
                const s = await getDoc(doc(db, "settings", "social")); 
                if (s.exists()) socialLinks = s.data(); 
            } catch(e) { console.error(e); } 
        }
        
        async function loadTasks() { 
            try { 
                const snap = await getDocs(query(collection(db, "tasks"), where("status", "==", "active"))); 
                tasks = snap.docs.map(d => ({ id: d.id, ...d.data() })); 
            } catch(e) { console.error("Tasks error:", e); } 
        }
        
        async function loadUserSubmissions() { 
            if (!currentUserDoc) return; 
            try { 
                const snap = await getDocs(query(
                    collection(db, "taskSubmissions"), 
                    where("userId", "==", currentUserDoc.id), 
                    orderBy("submittedAt", "desc")
                )); 
                userSubmissions = snap.docs.map(d => ({ id: d.id, ...d.data() })); 
                updatePendingBadge();
                updateTaskStatuses();
            } catch(e) { 
                console.warn("Submissions error:", e); 
                userSubmissions = []; 
            } 
        }
        
        function updatePendingBadge() {
            const pendingCount = userSubmissions.filter(s => s.status === 'pending').length;
            const badge = document.getElementById('notificationBadge');
            if (pendingCount > 0) {
                badge.style.display = 'flex';
                badge.innerText = pendingCount;
            } else {
                badge.style.display = 'none';
            }
        }
        
        function updateTaskStatuses() {
            if (document.getElementById('tasksPage').classList.contains('active')) {
                renderTasks();
            }
        }
        
        window.submitTaskProof = async () => { 
            if (!currentTask) {
                showNotification(currentLanguage === 'bn' ? 'কোন টাস্ক নির্বাচন করা হয়নি' : 'No task selected', 'error');
                return; 
            }
            
            const text = document.getElementById('taskProofText').value.trim(); 
            if (!text) { 
                showNotification(currentLanguage === 'bn' ? 'প্রমাণ দিন' : 'Please provide proof', 'error'); 
                return; 
            } 
            
            showLoading(); 
            try { 
                if (!currentUserDoc || !currentUserDoc.id) {
                    throw new Error('User not properly loaded');
                }
                
                const submissionData = {
                    userId: currentUserDoc.id,
                    userEmail: currentUser.email,
                    userName: currentUserDoc.name || currentUserDoc.username,
                    taskId: currentTask.id, 
                    taskTitle: currentTask.title, 
                    taskDescription: currentTask.description || '',
                    textProof: text, 
                    reward: currentTask.reward, 
                    status: 'pending', 
                    credited: false,   // <-- NEW: prevent double crediting
                    submittedAt: new Date().toISOString(),
                    timestamp: serverTimestamp()
                };
                
                await addDoc(collection(db, "taskSubmissions"), submissionData); 
                
                const t = translations[currentLanguage];
                showNotification(`${t.taskSubmitted} ${t.approvalWait}`, 'success'); 
                closeTaskModal(); 
                await loadUserSubmissions();
                renderTasks(); 
                renderProfile(); 
                
            } catch(e) { 
                console.error('Submission error:', e);
                showNotification(currentLanguage === 'bn' ? 'জমা দিতে ব্যর্থ: ' + e.message : 'Submission failed: ' + e.message, 'error'); 
            } finally { 
                hideLoading(); 
            } 
        };
        
        window.submitWithdraw = async () => { 
            const acc = document.getElementById('withdrawAccount').value.trim(); 
            const amt = parseFloat(document.getElementById('withdrawAmount').value); 
            
            if (!acc) { 
                showNotification(currentLanguage === 'bn' ? 'একাউন্ট নম্বর দিন' : 'Enter account number', 'error'); 
                return; 
            }
            
            if (!amt || amt <= 0) { 
                showNotification(currentLanguage === 'bn' ? 'সঠিক পরিমাণ দিন' : 'Enter valid amount', 'error'); 
                return; 
            } 
            
            if (amt > (currentUserDoc.balance || 0)) { 
                showNotification(currentLanguage === 'bn' ? 'পর্যাপ্ত ব্যালেন্স নেই' : 'Insufficient balance', 'error'); 
                return; 
            } 
            
            if (amt < settings.minWithdraw) { 
                showNotification(currentLanguage === 'bn' ? `সর্বনিম্ন উত্তোলন ৳${settings.minWithdraw}` : `Minimum withdraw is ৳${settings.minWithdraw}`, 'error'); 
                return; 
            } 
            
            showLoading(); 
            try { 
                const withdrawData = {
                    userId: currentUserDoc.id,
                    userEmail: currentUser.email,
                    userName: currentUserDoc.name || currentUserDoc.username,
                    method: withdrawMethod, 
                    accountNumber: acc, 
                    amount: amt, 
                    status: 'pending', 
                    requestedAt: new Date().toISOString(),
                    timestamp: serverTimestamp()
                };
                
                await addDoc(collection(db, "withdrawals"), withdrawData); 
                
                await updateDoc(doc(db, "users", currentUserDoc.id), { 
                    balance: increment(-amt) 
                }); 
                
                currentUserDoc.balance -= amt; 
                showNotification(currentLanguage === 'bn' ? `💰 ৳${formatBDT(amt)} উত্তোলন আবেদন জমা! ব্যালেন্স কেটে নেওয়া হয়েছে।` : `💰 Withdrawal request of ৳${formatBDT(amt)} submitted! Balance deducted.`, 'success'); 
                animateBalance();
                closeWithdrawForm(); 
                renderProfile(); 
                
            } catch(e) { 
                console.error('Withdrawal error:', e);
                showNotification(currentLanguage === 'bn' ? 'এরর: ' + e.message : 'Error: ' + e.message, 'error'); 
            } finally { 
                hideLoading(); 
            } 
        };
        
        window.submitActivationRequest = async () => { 
            const trx = document.getElementById('activationTransactionId').value.trim(); 
            const amount = parseFloat(document.getElementById('activationAmount').value);
            
            if (!trx) { 
                showNotification(currentLanguage === 'bn' ? 'ট্রানজেকশন আইডি দিন' : 'Enter transaction ID', 'error'); 
                return; 
            } 
            
            if (amount !== settings.activationFee) {
                showNotification(currentLanguage === 'bn' ? `পরিমাণ ৳${settings.activationFee} হতে হবে` : `Amount must be ৳${settings.activationFee}`, 'error');
                return;
            }
            
            showLoading(); 
            try { 
                const existingRequests = await getDocs(query(
                    collection(db, "activationRequests"), 
                    where("userId", "==", currentUserDoc.id),
                    where("status", "==", "pending")
                ));
                
                if (!existingRequests.empty) {
                    showNotification(currentLanguage === 'bn' ? 'আপনার ইতিমধ্যে একটি pending অনুরোধ আছে' : 'You already have a pending activation request', 'error');
                    closeActivationModal();
                    hideLoading();
                    return;
                }
                
                const activationData = {
                    userId: currentUserDoc.id,
                    userEmail: currentUser.email,
                    userName: currentUserDoc.name || currentUserDoc.username,
                    method: activationMethod, 
                    transactionId: trx, 
                    amount: amount, 
                    status: 'pending', 
                    createdAt: new Date().toISOString(),
                    timestamp: serverTimestamp()
                };
                
                await addDoc(collection(db, "activationRequests"), activationData); 
                
                activationPending = true; 
                showNotification(currentLanguage === 'bn' ? '📝 এক্টিভেশন অনুরোধ জমা! এডমিন ২৪ ঘন্টার মধ্যে যাচাই করবেন।' : '📝 Activation request submitted! Admin will verify within 24 hours.', 'info'); 
                closeActivationModal(); 
                renderHome(); 
                
            } catch(e) { 
                console.error('Activation error:', e);
                showNotification(currentLanguage === 'bn' ? 'এরর: ' + e.message : 'Error: ' + e.message, 'error'); 
            } finally { 
                hideLoading(); 
            } 
        };
        
        window.saveProfileChanges = async () => { 
            const name = document.getElementById('editName').value.trim(); 
            const uname = document.getElementById('editUsername').value.trim(); 
            const pw = document.getElementById('editPassword').value; 
            
            if (!name || !uname) { 
                showNotification(currentLanguage === 'bn' ? 'নাম এবং ইউজারনেম প্রয়োজন' : 'Name and username required', 'error'); 
                return; 
            }
            
            showLoading(); 
            try { 
                const unameQuery = query(
                    collection(db, "users"), 
                    where("username", "==", uname)
                ); 
                const unameSnap = await getDocs(unameQuery);
                
                if (!unameSnap.empty && unameSnap.docs[0].id !== currentUserDoc.id) {
                    showNotification(currentLanguage === 'bn' ? 'ইউজারনেম ইতিমধ্যে নেওয়া হয়েছে' : 'Username already taken', 'error');
                    hideLoading();
                    return;
                }
                
                const updateData = { 
                    name: name, 
                    username: uname 
                };
                
                await updateDoc(doc(db, "users", currentUserDoc.id), updateData); 
                
                currentUserDoc.name = name; 
                currentUserDoc.username = uname; 
                
                if (pw && pw.length >= 6) {
                    await updatePassword(auth.currentUser, pw);
                    showNotification(currentLanguage === 'bn' ? 'প্রোফাইল আপডেট! পাসওয়ার্ড পরিবর্তন হয়েছে।' : 'Profile updated! Password changed.', 'success');
                } else {
                    showNotification(currentLanguage === 'bn' ? 'প্রোফাইল সফলভাবে আপডেট হয়েছে!' : 'Profile updated successfully!', 'success');
                }
                
                renderProfile(); 
                renderShare(); 
                closeEditProfile(); 
                
            } catch(e) { 
                console.error('Profile update error:', e);
                showNotification(currentLanguage === 'bn' ? 'আপডেট ব্যর্থ: ' + e.message : 'Update failed: ' + e.message, 'error'); 
            } finally { 
                hideLoading(); 
            } 
        };
        
        function renderHome() { 
            const home = document.getElementById('homePage'); 
            let html = ''; 
            if (!currentUserDoc.activated) { 
                if (activationPending) html += `<div class="activation-pending"><i class="fas fa-hourglass-half"></i> ⏳ ${currentLanguage === 'bn' ? 'এক্টিভেশন অপেক্ষমান। এডমিন অনুমোদনের জন্য অপেক্ষা করুন।' : 'Activation pending. Wait for admin approval.'}</div>`; 
                else html += `<div class="activation-banner"><span>🔒 ${currentLanguage === 'bn' ? 'একাউন্ট এক্টিভেট হয়নি!' : 'Account not activated!'}</span><button class="activate-now-btn" onclick="openActivationModal()">${currentLanguage === 'bn' ? 'এক্টিভেট করুন' : 'Activate Now'}</button></div>`; 
            } 
            html += `<div class="section-title">${currentLanguage === 'bn' ? '📢 আজকের অফার' : '📢 Today\'s Offers'}</div>`; 
            if(adBoxes.length === 0) html += `<div style="text-align:center;padding:40px;">${currentLanguage === 'bn' ? 'কোনো বিজ্ঞাপন নেই' : 'No ads available'}</div>`;
            adBoxes.forEach(ad => { 
                const limit = ad.dailyLimit || 10; 
                const watched = adWatchCounts[ad.id] || 0; 
                const remaining = limit - watched; 
                const progress = (watched / limit) * 100; 
                html += `<div class="ad-card" onclick="${currentUserDoc.activated ? `openAdModal('${ad.id}')` : `showNotification('${currentLanguage === 'bn' ? 'প্রথমে এক্টিভেট করুন' : 'Activate first'}','error')`}"><div class="ad-info"><h4>${escapeHtml(ad.title || 'Special Offer')}</h4><p><i class="fas fa-clock"></i> ${ad.time || 20} sec</p></div><div class="ad-reward"><i class="fas fa-coins"></i> ৳${formatBDT(ad.coins || 0)}</div><div class="ad-progress"><div class="ad-progress-fill" style="width:${progress}%;"></div></div><span class="ad-limit-text">${remaining}/${limit}</span></div>`; 
            }); 
            html += `<div class="section-title">${currentLanguage === 'bn' ? '📱 অফিসিয়াল চ্যানেল' : '📱 Official Channels'}</div><div class="social-strip">`; 
            const chans = [{ name: 'telegram', icon: 'telegram', link: socialLinks.telegram || '#' }, { name: 'youtube', icon: 'youtube', link: socialLinks.youtube || '#' }, { name: 'facebook', icon: 'facebook', link: socialLinks.facebook || '#' }, { name: 'tiktok', icon: 'tiktok', link: socialLinks.tiktok || '#' }, { name: 'instagram', icon: 'instagram', link: socialLinks.instagram || '#' }]; 
            chans.forEach(ch => html += `<div class="social-icon ${ch.icon}" onclick="window.open('${ch.link}', '_blank')"><i class="fab fa-${ch.name}"></i></div>`); 
            html += `</div><div class="support-btn" onclick="window.open('${supportGroupLink}', '_blank')"><i class="fab fa-telegram"></i> ${currentLanguage === 'bn' ? 'সাপোর্ট গ্রুপে যোগ দিন' : 'Join Support Group'}</div>`; 
            home.innerHTML = html; 
        }
        
        function renderTasks() { 
            const page = document.getElementById('tasksPage'); 
            if (!currentUserDoc.activated) { page.innerHTML = `<div class="activation-pending">🔒 ${currentLanguage === 'bn' ? 'টাস্ক দেখতে একাউন্ট এক্টিভেট করুন' : 'Activate account to access tasks'}</div>`; return; } 
            
            const pendingSubmissions = userSubmissions.filter(s => s.status === 'pending');
            const pendingCount = pendingSubmissions.length;
            
            let html = `<div class="section-title">📋 ${currentLanguage === 'bn' ? 'উপলব্ধ টাস্ক' : 'Available Tasks'}`;
            if (pendingCount > 0) {
                html += `<span class="pending-count-badge">${pendingCount} ${currentLanguage === 'bn' ? 'অপেক্ষমান' : 'Pending'}</span>`;
            }
            html += `</div>`;
            
            if(pendingCount > 0) {
                html += `<div style="background:#fff3e0; padding:12px; border-radius:20px; margin-bottom:16px; text-align:center;">
                    <i class="fas fa-clock"></i> ${currentLanguage === 'bn' ? `আপনার ${pendingCount}টি টাস্ক পেন্ডিং আছে। এডমিন রিভিউ করার জন্য অপেক্ষা করুন।` : `You have ${pendingCount} pending task submission(s). Wait for admin review.`}
                </div>`;
            }
            
            if(tasks.length === 0) html += `<div style="text-align:center;padding:40px;">✨ ${currentLanguage === 'bn' ? 'বর্তমানে কোনো টাস্ক নেই। পরে আবার চেক করুন!' : 'No tasks available currently. Check back later!'}</div>`;
            
            tasks.forEach(task => { 
                const existingSubmission = userSubmissions.find(s => s.taskId === task.id);
                const hasPending = existingSubmission && existingSubmission.status === 'pending';
                const hasApproved = existingSubmission && existingSubmission.status === 'approved';
                const hasRejected = existingSubmission && existingSubmission.status === 'rejected';
                
                let statusBadge = '';
                let clickable = true;
                let message = '';
                
                if (hasPending) {
                    statusBadge = '<span class="status-badge pending">⏳ ' + (currentLanguage === 'bn' ? 'অপেক্ষমান' : 'Pending') + '</span>';
                    clickable = false;
                    message = currentLanguage === 'bn' ? 'এই টাস্কের জন্য আপনার একটি পেন্ডিং সাবমিশন আছে। এডমিন রিভিউ করার জন্য অপেক্ষা করুন।' : 'You have a pending submission for this task. Wait for admin review.';
                } else if (hasApproved) {
                    statusBadge = '<span class="status-badge approved">✅ ' + (currentLanguage === 'bn' ? 'সম্পন্ন' : 'Completed') + '</span>';
                    clickable = false;
                    message = currentLanguage === 'bn' ? 'আপনি ইতিমধ্যে এই টাস্ক সম্পন্ন করেছেন।' : 'You have already completed this task.';
                } else if (hasRejected) {
                    statusBadge = '<span class="status-badge rejected">❌ ' + (currentLanguage === 'bn' ? 'বাতিল' : 'Rejected') + '</span>';
                    clickable = true;
                    message = currentLanguage === 'bn' ? 'আপনার আগের সাবমিশন বাতিল হয়েছে। আবার চেষ্টা করতে পারেন।' : 'Your previous submission was rejected. You can try again.';
                }
                
                html += `<div class="task-card" onclick="${clickable && currentUserDoc.activated ? `openTaskModal('${task.id}')` : `showNotification('${message}', 'error')`}">
                    <div class="task-info">
                        <h4>${escapeHtml(task.title)} ${statusBadge}</h4>
                    </div>
                    <div class="task-reward"><i class="fas fa-coins"></i> ৳${formatBDT(task.reward)}</div>
                </div>`; 
            }); 
            page.innerHTML = html; 
        }
        
        function renderProfile() { 
            const page = document.getElementById('profilePage'); 
            if (!currentUserDoc.activated) { page.innerHTML = `<div class="activation-pending">🔒 ${currentLanguage === 'bn' ? 'প্রোফাইল দেখতে একাউন্ট এক্টিভেট করুন' : 'Activate account to see profile'}</div>`; return; } 
            
            page.innerHTML = `<div class="profile-card">
                <div class="profile-pic" onclick="uploadProfilePic()">${currentUserDoc.profilePic ? `<img src="${currentUserDoc.profilePic}">` : '<i class="fas fa-user"></i>'}</div>
                <div class="profile-info">
                    <h3>${escapeHtml(currentUserDoc.name || currentUserDoc.username)}</h3>
                    <p>@${escapeHtml(currentUserDoc.username)} • ID: ${currentUserDoc.id.slice(0,8)}</p>
                </div>
            </div>
            <div class="balance-box"><span><i class="fas fa-coins"></i> ${currentLanguage === 'bn' ? 'ব্যালেন্স (বিডিটি)' : 'Balance (BDT)'}</span><span>৳${formatBDT(currentUserDoc.balance || 0)}</span></div>
            <button class="withdraw-btn" onclick="openWithdrawForm()"><i class="fas fa-arrow-up"></i> ${currentLanguage === 'bn' ? 'উত্তোলন করুন' : 'Withdraw'}</button>
            <div class="notice-board">
                <h3><i class="fas fa-bullhorn"></i> ${currentLanguage === 'bn' ? 'ঘোষণা' : 'Announcement'}</h3>
                <p>${escapeHtml(settings.announcement)}</p>
            </div>`; 
        }
        
        async function renderShare() { 
            const page = document.getElementById('sharePage'); 
            if (!currentUserDoc.activated) { page.innerHTML = `<div class="activation-pending">🔒 ${currentLanguage === 'bn' ? 'রেফারেল ফিচার ব্যবহার করতে একাউন্ট এক্টিভেট করুন' : 'Activate account to use referral features'}</div>`; return; } 
            
            const vip = vipLevels.find(l => (currentUserDoc.referrals || 0) >= l.minReferrals) || vipLevels[0];
            let rankHTML = ''; 
            try { 
                const snap = await getDocs(query(collection(db, "users"), orderBy("referrals", "desc"), limit(12))); 
                let r = 1; 
                rankHTML = '<div class="ranking-table"><h3>🏆 Top 12 Referrers</h3>'; 
                snap.forEach(d => { const u = d.data(); rankHTML += `<div class="ranking-item"><span class="rank-number">#${r}</span><span class="rank-name">${escapeHtml(u.name || u.username)}</span><span class="rank-value">${u.referrals || 0}</span></div>`; r++; }); 
                rankHTML += '</div>'; 
            } catch(e) { rankHTML = '<p>Unable to load ranking</p>'; } 
            
            const referralLink = `${window.location.origin}${window.location.pathname}?ref=${encodeURIComponent(currentUserDoc.username)}`;
            
            let levelsHtml = ''; 
            vipLevels.sort((a,b)=>a.minReferrals-b.minReferrals).forEach(lvl => { 
                levelsHtml += `<div class="vip-level-card"><div class="vip-level-info"><div class="vip-level-name">${lvl.name}</div><div class="vip-level-details">${lvl.minReferrals}+ referrals • ${lvl.commission}% commission</div></div><div class="vip-level-stats"><span>৳${lvl.salary} / month</span></div></div>`; 
            }); 
            
            page.innerHTML = `<div class="ref-card"><h3>👥 Invite Friends</h3><p>💰 ${settings.referralBonus} BDT per referral</p>
                <div class="ref-link-box"><span id="refLink">${referralLink}</span><i class="fas fa-copy copy-icon" onclick="copyText('refLink')"></i></div>
                <div class="ref-username-box"><span id="refUsername">${currentUserDoc.username}</span><i class="fas fa-copy copy-icon" onclick="copyText('refUsername')"></i></div>
                <button class="copy-btn" onclick="copyText('refLink')"><i class="fas fa-copy"></i> Copy Link</button>
            </div>
            <div class="stats-row"><div class="stat-item"><div class="stat-value">${currentUserDoc.referrals || 0}</div><div class="stat-label">Referrals</div></div><div class="stat-item"><div class="stat-value">৳${formatBDT(currentUserDoc.referralEarnings || 0)}</div><div class="stat-label">Earned</div></div></div>
            <div class="vip-summary"><div><strong>Your Level:</strong> ${vip.name}</div><div><strong>Commission Rate:</strong> ${vip.commission}%</div><div><strong>Monthly Salary:</strong> ৳${vip.salary}</div></div>
            ${rankHTML}<div class="vip-info-board"><h4><i class="fas fa-crown"></i> Uni Level System</h4><div class="vip-list">${levelsHtml}</div><p class="vip-note">Commission from referrals' earnings. Salary on day ${vip.salaryDay}</p></div>`; 
        }
        
        window.openTaskModal = (id) => { 
            if (!currentUserDoc?.activated) { showNotification(currentLanguage === 'bn' ? 'প্রথমে একাউন্ট এক্টিভেট করুন' : 'Activate account first!', 'error'); return; } 
            const task = tasks.find(t => t.id === id); 
            if (!task) return; 
            
            const existingSubmission = userSubmissions.find(s => s.taskId === task.id);
            if (existingSubmission && existingSubmission.status === 'pending') { 
                showNotification(currentLanguage === 'bn' ? 'এই টাস্কের জন্য আপনার একটি পেন্ডিং সাবমিশন আছে। এডমিন রিভিউ করার জন্য অপেক্ষা করুন।' : 'You have a pending submission for this task. Wait for admin review.', 'warning'); 
                return; 
            }
            if (existingSubmission && existingSubmission.status === 'approved') { 
                showNotification(currentLanguage === 'bn' ? 'আপনি ইতিমধ্যে এই টাস্ক সম্পন্ন করেছেন!' : 'You have already completed this task!', 'info'); 
                return; 
            }
            
            currentTask = task; 
            document.getElementById('taskModalTitle').innerText = task.title; 
            document.getElementById('taskDescriptionDisplay').innerHTML = `<strong>📝 ${currentLanguage === 'bn' ? 'বিবরণ:' : 'Description:'}</strong><br>${escapeHtml(task.description || (currentLanguage === 'bn' ? 'কোন বিবরণ নেই।' : 'No description.'))}`; 
            document.getElementById('taskRewardDisplay').innerHTML = `💰 ${currentLanguage === 'bn' ? 'পুরস্কার:' : 'Reward:'} ৳${formatBDT(task.reward)}`; 
            document.getElementById('taskProofText').value = ''; 
            document.getElementById('taskModal').style.display = 'flex'; 
        };
        
        window.openActivationModal = () => { 
            if (currentUserDoc.activated) { showNotification(currentLanguage === 'bn' ? 'একাউন্ট ইতিমধ্যে এক্টিভেটেড' : 'Account already activated', 'info'); return; } 
            if (activationPending) { showNotification(currentLanguage === 'bn' ? 'এক্টিভেশন অনুরোধ ইতিমধ্যে পেন্ডিং' : 'Activation request already pending', 'info'); return; } 
            document.getElementById('activationFee').innerText = settings.activationFee; 
            document.getElementById('bkashNumber').innerText = settings.bkashNumber; 
            document.getElementById('nagadNumber').innerText = settings.nagadNumber; 
            document.getElementById('activationAmount').value = settings.activationFee;
            document.getElementById('activationModal').style.display = 'flex'; 
        };
        
        window.closeTaskModal = () => { document.getElementById('taskModal').style.display = 'none'; currentTask = null; };
        window.closeActivationModal = () => document.getElementById('activationModal').style.display = 'none';
        window.closeWithdrawForm = () => document.getElementById('withdrawForm').style.display = 'none';
        window.openWithdrawForm = () => { 
            if (!currentUserDoc.activated) { showNotification(currentLanguage === 'bn' ? 'প্রথমে একাউন্ট এক্টিভেট করুন!' : 'Activate account first!', 'error'); return; } 
            if ((currentUserDoc.balance || 0) < settings.minWithdraw) {
                showNotification(currentLanguage === 'bn' ? `সর্বনিম্ন উত্তোলন ৳${settings.minWithdraw}. আপনার ব্যালেন্স: ৳${formatBDT(currentUserDoc.balance || 0)}` : `Minimum withdrawal amount is ৳${settings.minWithdraw}. Your balance: ৳${formatBDT(currentUserDoc.balance || 0)}`, 'error');
                return;
            }
            document.getElementById('minWithdrawInfo').innerHTML = `💰 ${currentLanguage === 'bn' ? 'সর্বনিম্ন উত্তোলন:' : 'Minimum withdrawal:'} ৳${settings.minWithdraw}<br>💳 ${currentLanguage === 'bn' ? 'আপনার ব্যালেন্স:' : 'Your balance:'} ৳${formatBDT(currentUserDoc.balance || 0)}`; 
            document.getElementById('withdrawForm').style.display = 'flex'; 
        };
        window.selectWithdrawMethod = (btn, method) => { withdrawMethod = method; document.querySelectorAll('#withdrawForm .method-btn').forEach(b => b.classList.remove('active')); btn.classList.add('active'); };
        window.selectActivationMethod = (btn, method) => { activationMethod = method; document.querySelectorAll('#activationModal .method-btn').forEach(b => b.classList.remove('active')); btn.classList.add('active'); };
        window.copyText = (id) => { const txt = document.getElementById(id).innerText; navigator.clipboard.writeText(txt).then(() => showNotification('📋 ' + (currentLanguage === 'bn' ? 'কপি করা হয়েছে!' : 'Copied!'))); };
        window.editProfile = () => { document.getElementById('editName').value = currentUserDoc.name || ''; document.getElementById('editUsername').value = currentUserDoc.username || ''; document.getElementById('editProfileModal').style.display = 'flex'; };
        window.closeEditProfile = () => document.getElementById('editProfileModal').style.display = 'none';
        window.contactSupport = () => alert("📧 Email: saimunahmad67@gmail.com\n📞 Phone: 01798792581");
        window.aboutApp = () => alert(settings.aboutUs);
        window.logout = async () => { try { await signOut(auth); showNotification(currentLanguage === 'bn' ? 'লগআউট সফল' : 'Logged out successfully', 'info'); } catch(e){} };
        window.changeLanguage = (lang) => {
            currentLanguage = lang;
            updateLanguage();
            renderHome();
            renderTasks();
            renderShare();
            renderProfile();
        };
        
        function updateLanguage() {
            const t = translations[currentLanguage];
            document.getElementById('navHome').innerText = t.home;
            document.getElementById('navTask').innerText = t.task;
            document.getElementById('navShare').innerText = t.share;
            document.getElementById('navProfile').innerText = t.profile;
            if (document.getElementById('submitTaskBtn')) {
                document.getElementById('submitTaskBtn').innerText = t.submitTask;
                document.getElementById('cancelTaskBtn').innerText = t.cancel;
            }
        }
        
        window.openAdModal = (id) => { 
            if (!currentUserDoc?.activated) { showNotification(currentLanguage === 'bn' ? 'প্রথমে একাউন্ট এক্টিভেট করুন' : 'Activate account first!', 'error'); return; } 
            const ad = adBoxes.find(a => a.id === id); 
            if (!ad) return; 
            if ((adWatchCounts[ad.id] || 0) >= (ad.dailyLimit || 10)) { showNotification(currentLanguage === 'bn' ? 'দৈনিক সীমা শেষ' : 'Daily limit reached', 'error'); return; } 
            currentAd = ad; adStep = 1; 
            const link1 = (networks[ad.networkIndex]?.link1) || 'about:blank'; 
            document.getElementById('adIframe').src = link1; 
            document.getElementById('adTimerFull').innerText = formatTime(ad.time || 20); 
            document.getElementById('skipAdCorner').style.display = 'none'; 
            document.getElementById('closeAdCorner').style.display = 'none'; 
            document.getElementById('adModal').style.display = 'flex'; 
            timeLeft = ad.time || 20; 
            startAdTimer(); 
        };
        
        function formatTime(s) { let m = Math.floor(s/60).toString().padStart(2,'0'); let sec = (s%60).toString().padStart(2,'0'); return `${m}:${sec}`; }
        
        function startAdTimer() { 
            if (timerInterval) clearInterval(timerInterval); 
            timerInterval = setInterval(() => { 
                timeLeft--; 
                document.getElementById('adTimerFull').innerText = formatTime(timeLeft); 
                if (adStep === 1 && timeLeft <= Math.floor((currentAd.time || 20)/2)) document.getElementById('skipAdCorner').style.display = 'flex'; 
                if (timeLeft <= 0) { 
                    clearInterval(timerInterval); 
                    if (adStep === 1) { 
                        adStep = 2; 
                        timeLeft = Math.ceil((currentAd.time || 20)/2); 
                        document.getElementById('adTimerFull').innerText = formatTime(timeLeft); 
                        document.getElementById('skipAdCorner').style.display = 'none'; 
                        const link2 = networks[currentAd.networkIndex]?.link2 || 'about:blank'; 
                        document.getElementById('adIframe').src = link2; 
                        startAdTimer(); 
                    } else { 
                        document.getElementById('closeAdCorner').style.display = 'flex'; 
                    } 
                } 
            }, 1000); 
        }
        
        document.getElementById('skipAdCorner').onclick = () => { 
            if (adStep === 1 && currentAd) { 
                adStep = 2; 
                timeLeft = Math.ceil((currentAd.time || 20)/2); 
                document.getElementById('adTimerFull').innerText = formatTime(timeLeft); 
                document.getElementById('skipAdCorner').style.display = 'none'; 
                const link2 = networks[currentAd.networkIndex]?.link2 || 'about:blank'; 
                document.getElementById('adIframe').src = link2; 
                startAdTimer(); 
            } 
        };
        
        document.getElementById('closeAdCorner').onclick = async () => { 
            if (currentAd && currentUserDoc) { 
                const reward = currentAd.coins || 0; 
                await updateDoc(doc(db, "users", currentUserDoc.id), { 
                    balance: increment(reward), 
                    [`adWatchCounts.${currentAd.id}`]: increment(1) 
                }); 
                currentUserDoc.balance += reward; 
                adWatchCounts[currentAd.id] = (adWatchCounts[currentAd.id] || 0) + 1; 
                showNotification(`🎉 ${currentLanguage === 'bn' ? `আপনি বিজ্ঞাপন দেখে ৳${formatBDT(reward)} আয় করেছেন!` : `You earned ৳${formatBDT(reward)} from watching ad!`}`, 'success'); 
                animateBalance();
                renderHome(); 
                renderProfile(); 
            } 
            document.getElementById('adModal').style.display = 'none'; 
            clearInterval(timerInterval); 
            document.getElementById('adIframe').src = 'about:blank'; 
        };
        
        window.uploadProfilePic = async () => { 
            const inp = document.createElement('input'); inp.type = 'file'; inp.accept = 'image/*'; 
            inp.onchange = async (e) => { 
                const f = e.target.files[0]; if (!f) return; 
                showLoading(); 
                try { 
                    const fileRef = ref(storage, `profilePics/${currentUserDoc.id}`); 
                    await uploadBytes(fileRef, f); 
                    const url = await getDownloadURL(fileRef); 
                    await updateDoc(doc(db, "users", currentUserDoc.id), { profilePic: url }); 
                    currentUserDoc.profilePic = url; 
                    renderProfile(); 
                    showNotification(currentLanguage === 'bn' ? 'প্রোফাইল ছবি আপডেট হয়েছে!' : 'Profile picture updated!', 'success'); 
                } catch(e) { showNotification(currentLanguage === 'bn' ? 'আপলোড ব্যর্থ' : 'Upload failed', 'error'); } 
                finally { hideLoading(); } 
            }; 
            inp.click(); 
        };
        
        // Navigation
        document.querySelectorAll('.nav-item').forEach(item => { 
            item.addEventListener('click', function() { 
                document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); 
                this.classList.add('active'); 
                const page = this.dataset.page; 
                document.querySelectorAll('.page').forEach(p => p.classList.remove('active')); 
                document.getElementById(page + 'Page').classList.add('active'); 
                if (page === 'home') renderHome(); 
                if (page === 'tasks') renderTasks(); 
                if (page === 'share') renderShare(); 
                if (page === 'profile') renderProfile(); 
            }); 
        });
        
        document.getElementById('settingsIcon')?.addEventListener('click', (e) => { e.stopPropagation(); const m = document.getElementById('profileMenu'); m.style.display = m.style.display === 'block' ? 'none' : 'block'; });
        document.addEventListener('click', (e) => { const m = document.getElementById('profileMenu'); const s = document.getElementById('settingsIcon'); if (!s?.contains(e.target) && !m?.contains(e.target)) m.style.display = 'none'; });
        
        window.showLogin = () => { document.getElementById('loginForm').style.display = 'block'; document.getElementById('registerForm').style.display = 'none'; };
        window.showRegister = () => { document.getElementById('loginForm').style.display = 'none'; document.getElementById('registerForm').style.display = 'block'; };
        
        window.handleLogin = async () => { 
            const email = document.getElementById('loginEmail').value.trim(); 
            const pw = document.getElementById('loginPassword').value; 
            if (!email || !pw) { document.getElementById('loginError').innerText = currentLanguage === 'bn' ? 'ইমেইল এবং পাসওয়ার্ড দিন' : 'Enter email and password'; return; } 
            showLoading(); 
            try { 
                await signInWithEmailAndPassword(auth, email, pw); 
            } catch(err) { 
                hideLoading(); 
                document.getElementById('loginError').innerText = err.code === 'auth/user-not-found' ? (currentLanguage === 'bn' ? 'ইউজার পাওয়া যায়নি' : 'User not found') : err.code === 'auth/wrong-password' ? (currentLanguage === 'bn' ? 'ভুল পাসওয়ার্ড' : 'Wrong password') : (currentLanguage === 'bn' ? 'লগইন ব্যর্থ' : 'Login failed'); 
            } 
        };
        
        window.handleRegister = async () => { 
            const email = document.getElementById('regEmail').value.trim(); 
            const username = document.getElementById('regUsername').value.trim(); 
            const pw = document.getElementById('regPassword').value; 
            const cpw = document.getElementById('regConfirmPassword').value; 
            const refUsername = document.getElementById('regReferral').value.trim(); 
            if (!email || !username || !pw || !cpw) { document.getElementById('registerError').innerText = currentLanguage === 'bn' ? 'সব ফিল্ড পূরণ করুন' : 'Fill all fields'; return; } 
            if (pw !== cpw) { document.getElementById('registerError').innerText = currentLanguage === 'bn' ? 'পাসওয়ার্ড মেলে না' : 'Passwords do not match'; return; } 
            if (pw.length < 6) { document.getElementById('registerError').innerText = currentLanguage === 'bn' ? 'পাসওয়ার্ড ৬+ অক্ষর হতে হবে' : 'Password must be 6+ characters'; return; } 
            showLoading(); 
            try { 
                const unameQuery = query(collection(db, "users"), where("username", "==", username)); 
                const unameSnap = await getDocs(unameQuery); 
                if (!unameSnap.empty) { document.getElementById('registerError').innerText = currentLanguage === 'bn' ? 'ইউজারনেম নেওয়া হয়েছে' : 'Username taken'; hideLoading(); return; } 
                const cred = await createUserWithEmailAndPassword(auth, email, pw); 
                let referrerId = null; 
                if (refUsername) { 
                    const refQuery = query(collection(db, "users"), where("username", "==", refUsername)); 
                    const refSnap = await getDocs(refQuery); 
                    if (!refSnap.empty) referrerId = refSnap.docs[0].id; 
                } 
                const newUser = { 
                    uid: cred.user.uid, 
                    email: email, 
                    name: username, 
                    username: username, 
                    referredBy: referrerId, 
                    balance: 0, 
                    referrals: 0, 
                    referralEarnings: 0, 
                    totalCommissionEarned: 0, 
                    vipLevel: "UniStart", 
                    commissionRate: 2, 
                    monthlySalary: 0, 
                    salaryDay: 30, 
                    lastSalaryDate: null, 
                    createdAt: new Date().toISOString(), 
                    profilePic: '', 
                    adWatchCounts: {}, 
                    lastAdReset: new Date().toDateString(), 
                    activated: false 
                }; 
                await setDoc(doc(db, "users", cred.user.uid), newUser); 
                if (referrerId) { 
                    await updateDoc(doc(db, "users", referrerId), { 
                        referrals: increment(1), 
                        referralEarnings: increment(settings.referralBonus),
                        balance: increment(settings.referralBonus)
                    }); 
                } 
                document.getElementById('registerSuccess').innerText = currentLanguage === 'bn' ? '✅ রেজিস্ট্রেশন সফল! এখন লগইন করুন।' : '✅ Registration successful! You can now login.'; 
                setTimeout(() => showLogin(), 2000); 
            } catch(err) { 
                hideLoading(); 
                console.error('Registration error:', err);
                document.getElementById('registerError').innerText = err.code === 'auth/email-already-in-use' ? (currentLanguage === 'bn' ? 'ইমেইল ইতিমধ্যে ব্যবহৃত' : 'Email already used') : (currentLanguage === 'bn' ? 'রেজিস্ট্রেশন ব্যর্থ: ' + err.message : 'Registration failed: ' + err.message); 
            } finally {
                hideLoading();
            }
        };
        
        // Auth State Listener with Real-time Balance Updates
        onAuthStateChanged(auth, async (user) => {
            if (user) {
                showLoading();
                try {
                    const userSnap = await getDoc(doc(db, "users", user.uid));
                    if (!userSnap.exists()) { 
                        await signOut(auth); 
                        hideLoading(); 
                        return; 
                    }
                    currentUserDoc = { id: userSnap.id, ...userSnap.data() };
                    currentUser = user;
                    
                    await loadSettings(); 
                    await loadAdBoxes(); 
                    await loadNetworks(); 
                    await loadSocialLinks(); 
                    await loadTasks(); 
                    await loadUserSubmissions();
                    
                    adWatchCounts = currentUserDoc.adWatchCounts || {};
                    const today = new Date().toDateString();
                    if (currentUserDoc.lastAdReset !== today) { 
                        adWatchCounts = {}; 
                        await updateDoc(doc(db, "users", currentUserDoc.id), { adWatchCounts: {}, lastAdReset: today }); 
                    }
                    
                    const actSnap = await getDocs(query(
                        collection(db, "activationRequests"), 
                        where("userId", "==", currentUserDoc.id), 
                        where("status", "==", "pending")
                    ));
                    activationPending = !actSnap.empty;
                    
                    document.getElementById('authPages').style.display = 'none';
                    document.getElementById('mainApp').style.display = 'block';
                    updateLanguage();
                    renderHome(); 
                    renderTasks(); 
                    renderShare(); 
                    renderProfile();
                    
                    // Real-time user data listener with balance animation
                    onSnapshot(doc(db, "users", currentUserDoc.id), (d) => { 
                        if (d.exists()) { 
                            const oldBalance = currentUserDoc.balance || 0;
                            currentUserDoc = { id: d.id, ...d.data() }; 
                            const newBalance = currentUserDoc.balance || 0;
                            
                            if (newBalance > oldBalance) {
                                animateBalance();
                                showNotification(`💰 ${currentLanguage === 'bn' ? `ব্যালেন্স ৳${formatBDT(newBalance - oldBalance)} বেড়েছে!` : `Balance increased by ৳${formatBDT(newBalance - oldBalance)}!`}`, 'success');
                            } else if (newBalance < oldBalance) {
                                animateBalance();
                                showNotification(`💸 ${currentLanguage === 'bn' ? `ব্যালেন্স ৳${formatBDT(oldBalance - newBalance)} কমেছে` : `Balance decreased by ৳${formatBDT(oldBalance - newBalance)}`}`, 'info');
                            }
                            
                            renderHome(); 
                            renderTasks(); 
                            renderShare(); 
                            renderProfile(); 
                        } 
                    });
                    
                    // Real-time tasks listener
                    onSnapshot(query(collection(db, "tasks"), where("status", "==", "active")), () => { 
                        loadTasks(); 
                        if (document.getElementById('tasksPage').classList.contains('active')) renderTasks(); 
                    });
                    
                    // Real-time submissions listener with balance update on approval (using transaction)
                    onSnapshot(query(collection(db, "taskSubmissions"), where("userId", "==", currentUserDoc.id)), async (snapshot) => {
                        for (const change of snapshot.docChanges()) {
                            const docId = change.doc.id;
                            const newData = change.doc.data();
                            
                            if (change.type === 'modified') {
                                const oldData = userSubmissions.find(s => s.id === docId);
                                // Only process if status changed to 'approved' and not already credited
                                if (oldData && oldData.status !== newData.status && newData.status === 'approved' && !newData.credited) {
                                    const reward = Number(newData.reward) || 0;
                                    if (reward > 0) {
                                        try {
                                            const userRef = doc(db, "users", currentUserDoc.id);
                                            const submissionRef = doc(db, "taskSubmissions", docId);
                                            await runTransaction(db, async (transaction) => {
                                                const userDocSnap = await transaction.get(userRef);
                                                if (!userDocSnap.exists()) return;
                                                const newBalance = (userDocSnap.data().balance || 0) + reward;
                                                transaction.update(userRef, { balance: newBalance });
                                                transaction.update(submissionRef, { credited: true });
                                            });
                                            // Update local balance immediately
                                            currentUserDoc.balance = (currentUserDoc.balance || 0) + reward;
                                            showNotification(
                                                `✅ ${currentLanguage === 'bn' ? `টাস্ক "${newData.taskTitle}" অনুমোদিত! +৳${formatBDT(reward)} আপনার ব্যালেন্সে যোগ হয়েছে!` : `Task "${newData.taskTitle}" approved! +৳${formatBDT(reward)} added to your balance!`}`,
                                                'success'
                                            );
                                            animateBalance();
                                            renderHome();
                                            renderTasks();
                                            renderShare();
                                            renderProfile();
                                        } catch (err) {
                                            console.error('Error crediting reward:', err);
                                            showNotification(
                                                currentLanguage === 'bn' ? 'রিওয়ার্ড ক্রেডিট করতে ব্যর্থ হয়েছে। প্রশাসককে জানান।' : 'Failed to credit reward. Please contact admin.',
                                                'error'
                                            );
                                        }
                                    }
                                } else if (newData.status === 'rejected' && oldData && oldData.status !== 'rejected') {
                                    showNotification(
                                        `❌ ${currentLanguage === 'bn' ? `টাস্ক "${newData.taskTitle}" বাতিল করা হয়েছে। আপনি আবার চেষ্টা করতে পারেন।` : `Task "${newData.taskTitle}" rejected. You can try again.`}`,
                                        'error'
                                    );
                                }
                            }
                        }
                        // Reload submissions to keep local cache consistent
                        await loadUserSubmissions();
                        if (document.getElementById('tasksPage').classList.contains('active')) renderTasks();
                        if (document.getElementById('profilePage').classList.contains('active')) renderProfile();
                    });
                    
                    // Check for activation approval
                    onSnapshot(query(
                        collection(db, "activationRequests"), 
                        where("userId", "==", currentUserDoc.id), 
                        where("status", "==", "approved")
                    ), async (snap) => { 
                        if (!snap.empty && currentUserDoc && !currentUserDoc.activated) { 
                            await updateDoc(doc(db, "users", currentUserDoc.id), { activated: true }); 
                            showNotification("🎉 " + (currentLanguage === 'bn' ? 'অভিনন্দন! আপনার একাউন্ট এক্টিভেট হয়েছে! এখন আপনি আয় করতে পারবেন।' : 'Congratulations! Your account has been activated! Now you can start earning.'), "success"); 
                            renderHome(); 
                            renderTasks(); 
                            renderProfile();
                        } 
                    });
                    
                } catch(e) { 
                    console.error('Auth error:', e); 
                } finally { 
                    hideLoading(); 
                }
            } else {
                document.getElementById('authPages').style.display = 'block';
                document.getElementById('mainApp').style.display = 'none';
                hideLoading();
            }
        });
        
        document.getElementById('notificationBell').addEventListener('click', () => { 
            const pendingCount = userSubmissions.filter(s => s.status === 'pending').length;
            const approvedCount = userSubmissions.filter(s => s.status === 'approved').length;
            const rejectedCount = userSubmissions.filter(s => s.status === 'rejected').length;
            if (currentLanguage === 'bn') {
                alert(`📢 নোটিফিকেশন সারাংশ:\n\n⏳ অপেক্ষমান টাস্ক: ${pendingCount}\n✅ অনুমোদিত টাস্ক: ${approvedCount}\n❌ বাতিল টাস্ক: ${rejectedCount}\n💰 ব্যালেন্স: ৳${formatBDT(currentUserDoc?.balance || 0)}\n\n💡 টিপ: আরো আয় করতে টাস্ক সম্পন্ন করুন এবং বিজ্ঞাপন দেখুন!`);
            } else {
                alert(`📢 Notification Summary:\n\n⏳ Pending Tasks: ${pendingCount}\n✅ Approved Tasks: ${approvedCount}\n❌ Rejected Tasks: ${rejectedCount}\n💰 Balance: ৳${formatBDT(currentUserDoc?.balance || 0)}\n\n💡 Tip: Complete tasks and watch ads to earn more!`);
            }
        });
    </script>
</body>
</html>
