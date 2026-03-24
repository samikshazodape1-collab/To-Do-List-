<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TaskFlow • Professional Task Manager</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&amp;display=swap');
        
        :root {
            --blue: #0066ff;
            --pink: #ff2d95;
            --white: #ffffff;
            --dark: #1a1a2e;
            --light-gray: #f8f9ff;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Poppins', system-ui, -apple-system, sans-serif;
            background: linear-gradient(135deg, #0066ff 0%, #ff2d95 100%);
            color: var(--dark);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        
        body::before {
            content: '';
            position: absolute;
            top: -20%;
            left: -10%;
            width: 400px;
            height: 400px;
            background: rgba(255,255,255,0.15);
            border-radius: 50%;
            filter: blur(80px);
            z-index: 0;
            animation: float 25s infinite linear;
        }
        
        body::after {
            content: '';
            position: absolute;
            bottom: -30%;
            right: -15%;
            width: 500px;
            height: 500px;
            background: rgba(255,255,255,0.12);
            border-radius: 50%;
            filter: blur(100px);
            z-index: 0;
            animation: float 30s infinite linear reverse;
        }
        
        @keyframes float {
            0% { transform: translate(0, 0) rotate(0deg); }
            100% { transform: translate(30px, 30px) rotate(360deg); }
        }
        
        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 0 20px;
            position: relative;
            z-index: 1;
        }
        
        /* HEADER */
        header {
            background: rgba(255,255,255,0.95);
            backdrop-filter: blur(20px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            padding: 15px 0;
            position: sticky;
            top: 0;
            z-index: 100;
            border-bottom: 1px solid rgba(255,255,255,0.3);
        }
        
        .header-content {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        
        .logo {
            font-size: 28px;
            font-weight: 700;
            background: linear-gradient(90deg, var(--blue), var(--pink));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: -1px;
        }
        
        .nav-buttons {
            display: flex;
            gap: 8px;
            background: white;
            padding: 6px;
            border-radius: 50px;
            box-shadow: 0 4px 15px rgba(0, 102, 255, 0.15);
        }
        
        .nav-btn {
            padding: 12px 24px;
            border: none;
            background: transparent;
            font-weight: 600;
            font-size: 15px;
            border-radius: 50px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            align-items: center;
            gap: 8px;
            color: #555;
        }
        
        .nav-btn.active,
        .nav-btn:hover {
            background: linear-gradient(90deg, var(--blue), var(--pink));
            color: white;
            transform: translateY(-1px);
            box-shadow: 0 10px 20px rgba(255, 45, 149, 0.3);
        }
        
        .user-section {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .clock {
            font-weight: 600;
            font-size: 18px;
            background: linear-gradient(90deg, #0066ff, #ff2d95);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            padding: 8px 18px;
            border-radius: 30px;
            box-shadow: 0 4px 15px rgba(0, 102, 255, 0.2);
        }
        
        .user-pill {
            background: var(--light-gray);
            padding: 8px 20px;
            border-radius: 50px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
        }
        
        .logout-btn {
            background: #ff2d95;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 50px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .logout-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(255, 45, 149, 0.4);
        }
        
        /* PAGES */
        .page {
            display: none;
            min-height: calc(100vh - 80px);
            padding: 40px 0;
        }
        
        .page.active {
            display: block;
            animation: fadeIn 0.4s ease forwards;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* AUTH PAGE */
        #auth-page {
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #0066ff 0%, #ff2d95 100%);
        }
        
        .auth-card {
            background: white;
            width: 100%;
            max-width: 420px;
            border-radius: 24px;
            padding: 50px 40px;
            box-shadow: 0 25px 60px rgba(0, 0, 0, 0.2);
            position: relative;
            z-index: 10;
        }
        
        .auth-tabs {
            display: flex;
            margin-bottom: 30px;
            border-radius: 50px;
            background: #f1f3f9;
            padding: 6px;
        }
        
        .auth-tab {
            flex: 1;
            padding: 14px;
            text-align: center;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .auth-tab.active {
            background: linear-gradient(90deg, var(--blue), var(--pink));
            color: white;
            box-shadow: 0 10px 25px rgba(255, 45, 149, 0.3);
        }
        
        .form-group {
            margin-bottom: 25px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #444;
            font-size: 14px;
        }
        
        input {
            width: 100%;
            padding: 16px 20px;
            border: 2px solid #e5e7eb;
            border-radius: 16px;
            font-size: 16px;
            font-weight: 500;
            transition: all 0.3s ease;
        }
        
        input:focus {
            outline: none;
            border-color: var(--blue);
            box-shadow: 0 0 0 4px rgba(0, 102, 255, 0.15);
        }
        
        .auth-btn {
            width: 100%;
            padding: 18px;
            background: linear-gradient(90deg, var(--blue), var(--pink));
            color: white;
            border: none;
            border-radius: 16px;
            font-size: 17px;
            font-weight: 700;
            cursor: pointer;
            margin-top: 10px;
            transition: all 0.3s ease;
            box-shadow: 0 15px 30px rgba(255, 45, 149, 0.3);
        }
        
        .auth-btn:hover {
            transform: translateY(-3px);
        }
        
        .error {
            color: #ff2d95;
            font-size: 14px;
            margin-top: 8px;
            display: none;
        }
        
        /* DASHBOARD */
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
        }
        
        .card {
            background: white;
            border-radius: 24px;
            padding: 28px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.08);
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 25px 50px rgba(0, 102, 255, 0.15);
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .card-title {
            font-size: 18px;
            font-weight: 600;
            color: #555;
        }
        
        .card-value {
            font-size: 42px;
            font-weight: 700;
            background: linear-gradient(90deg, var(--blue), var(--pink));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .progress-container {
            margin-top: 30px;
            background: #f1f3f9;
            border-radius: 50px;
            height: 14px;
            overflow: hidden;
            position: relative;
        }
        
        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #0066ff, #ff2d95);
            border-radius: 50px;
            transition: width 1s cubic-bezier(0.34, 1.56, 0.64, 1);
            position: relative;
        }
        
        .progress-bar::after {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 30%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.6));
            animation: shimmer 2s infinite linear;
        }
        
        @keyframes shimmer {
            100% { transform: translateX(-100%); }
        }
        
        .reminders-section {
            margin-top: 40px;
        }
        
        .reminder-card {
            background: white;
            border-radius: 20px;
            padding: 20px;
            margin-bottom: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.06);
        }
        
        .overdue {
            border-left: 6px solid #ff2d95;
        }
        
        .near {
            border-left: 6px solid #ffaa00;
        }
        
        /* ADD / WRITE PAGES */
        .form-container {
            max-width: 720px;
            margin: 0 auto;
            background: white;
            border-radius: 28px;
            padding: 40px;
            box-shadow: 0 20px 50px rgba(0, 102, 255, 0.12);
        }
        
        .title-input {
            font-size: 24px;
            font-weight: 700;
            color: #111;
            border: none;
            border-bottom: 3px solid #0066ff;
            width: 100%;
            padding: 12px 0;
            margin-bottom: 30px;
            outline: none;
        }
        
        .editor {
            border: 3px solid #e5e7eb;
            border-radius: 20px;
            min-height: 420px;
            padding: 25px;
            font-size: 18px;
            line-height: 1.6;
            color: #111;
            font-weight: 700;
            background: #fff;
            box-shadow: inset 0 4px 15px rgba(0, 0, 0, 0.03);
            overflow-y: auto;
        }
        
        .toolbar {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
            margin-bottom: 20px;
            background: #f8f9ff;
            padding: 14px;
            border-radius: 16px;
        }
        
        .toolbar select,
        .toolbar input,
        .toolbar button {
            padding: 10px 16px;
            border-radius: 12px;
            border: 2px solid #ddd;
            font-weight: 600;
        }
        
        .toolbar button {
            background: white;
            cursor: pointer;
        }
        
        .toolbar button.active {
            background: linear-gradient(90deg, var(--blue), var(--pink));
            color: white;
        }
        
        /* LIST & SUBMIT */
        .task-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 24px;
        }
        
        .task-card {
            background: white;
            border-radius: 24px;
            padding: 24px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.08);
            transition: all 0.3s ease;
            position: relative;
        }
        
        .task-card:hover {
            transform: scale(1.03);
        }
        
        .task-title {
            font-size: 22px;
            font-weight: 700;
            margin-bottom: 12px;
            line-height: 1.3;
        }
        
        .task-meta {
            display: flex;
            gap: 12px;
            margin-bottom: 18px;
        }
        
        .badge {
            font-size: 12px;
            padding: 4px 14px;
            border-radius: 50px;
            font-weight: 700;
            text-transform: uppercase;
        }
        
        .pending { background: #fff3cd; color: #b37c00; }
        .submitted { background: #d4edda; color: #006600; }
        
        .task-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        /* MODAL */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(26, 26, 46, 0.85);
            z-index: 9999;
            align-items: center;
            justify-content: center;
            animation: modalPop 0.3s ease;
        }
        
        .modal-content {
            background: white;
            width: 100%;
            max-width: 820px;
            border-radius: 28px;
            max-height: 92vh;
            overflow-y: auto;
            box-shadow: 0 30px 80px rgba(0, 0, 0, 0.3);
        }
        
        .modal-header {
            padding: 24px 32px;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            background: white;
            z-index: 10;
        }
        
        .toast {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: #111;
            color: white;
            padding: 16px 24px;
            border-radius: 16px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
            display: none;
            align-items: center;
            gap: 12px;
            font-weight: 600;
            z-index: 10000;
        }
        
        /* RESPONSIVE */
        @media (max-width: 768px) {
            .nav-buttons { flex-wrap: wrap; }
            .nav-btn { padding: 10px 16px; font-size: 14px; }
            .dashboard-grid { grid-template-columns: 1fr; }
            .form-container { padding: 25px; }
        }
    </style>
</head>
<body>
    <!-- AUTH PAGE -->
    <div id="auth-page">
        <div class="container">
            <div class="auth-card">
                <div class="text-center mb-8">
                    <h1 style="font-size: 42px; font-weight: 700; background: linear-gradient(90deg, #0066ff, #ff2d95); -webkit-background-clip: text; -webkit-text-fill-color: transparent;">TaskFlow</h1>
                    <p style="font-size: 18px; color: #666; margin-top: 8px;">Modern • Clean • Professional</p>
                </div>
                
                <div class="auth-tabs">
                    <div onclick="switchAuthTab(0)" id="login-tab" class="auth-tab active">Login</div>
                    <div onclick="switchAuthTab(1)" id="signup-tab" class="auth-tab">Sign Up</div>
                </div>
                
                <!-- Login Form -->
                <div id="login-form">
                    <div class="form-group">
                        <label>Name</label>
                        <input type="text" id="login-name" placeholder="Enter your name" autocomplete="off">
                    </div>
                    <div class="form-group">
                        <label>Password</label>
                        <input type="password" id="login-password" placeholder="••••••••">
                    </div>
                    <div class="error" id="login-error">Invalid credentials</div>
                    <button onclick="handleLogin()" class="auth-btn">Login to Dashboard</button>
                    <p class="text-center" style="margin-top: 20px; color: #777; font-size: 14px;">
                        New here? <span onclick="switchAuthTab(1)" style="color: var(--pink); cursor: pointer; font-weight: 600;">Create account</span>
                    </p>
                </div>
                
                <!-- Signup Form -->
                <div id="signup-form" style="display: none;">
                    <div class="form-group">
                        <label>Name</label>
                        <input type="text" id="signup-name" placeholder="Choose a name" autocomplete="off">
                    </div>
                    <div class="form-group">
                        <label>Password</label>
                        <input type="password" id="signup-password" placeholder="Create password">
                    </div>
                    <div class="error" id="signup-error">Name already exists</div>
                    <button onclick="handleSignup()" class="auth-btn">Create Account &amp; Start</button>
                    <p class="text-center" style="margin-top: 20px; color: #777; font-size: 14px;">
                        Already have an account? <span onclick="switchAuthTab(0)" style="color: var(--pink); cursor: pointer; font-weight: 600;">Login</span>
                    </p>
                </div>
            </div>
        </div>
    </div>
    
    <!-- MAIN APP -->
    <div id="main-app" style="display: none;">
        
        <!-- HEADER -->
        <header>
            <div class="container header-content">
                <div class="logo">TaskFlow</div>
                
                <div class="nav-buttons">
                    <button onclick="navigateTo('dashboard')" id="nav-dashboard" class="nav-btn active">
                        <span>🏠</span> Home
                    </button>
                    <button onclick="navigateTo('add')" id="nav-add" class="nav-btn">
                        <span>📤</span> Add
                    </button>
                    <button onclick="navigateTo('write')" id="nav-write" class="nav-btn">
                        <span>✍️</span> Write
                    </button>
                    <button onclick="navigateTo('submit')" id="nav-submit" class="nav-btn">
                        <span>✅</span> Submit
                    </button>
                    <button onclick="navigateTo('list')" id="nav-list" class="nav-btn">
                        <span>📋</span> List
                    </button>
                </div>
                
                <div class="user-section">
                    <div id="live-clock" class="clock"></div>
                    <div class="user-pill">
                        <span id="user-name-display" style="font-weight: 700;"></span>
                        <span style="width: 8px; height: 8px; background: #00ff88; border-radius: 50%; display: inline-block;"></span>
                    </div>
                    <button onclick="logout()" class="logout-btn">Logout</button>
                </div>
            </div>
        </header>
        
        <!-- DASHBOARD PAGE -->
        <div id="dashboard" class="page active">
            <div class="container">
                <div style="margin-bottom: 30px;">
                    <h1 style="font-size: 38px; font-weight: 700; color: white; text-shadow: 0 4px 20px rgba(0,0,0,0.2);">Task Management / To-Do List</h1>
                    <p style="font-size: 22px; color: rgba(255,255,255,0.95); font-weight: 500;">Welcome to Your Task Manager</p>
                </div>
                
                <div class="dashboard-grid">
                    <!-- Total Tasks -->
                    <div class="card">
                        <div class="card-header">
                            <div class="card-title">Total Tasks</div>
                            <div style="font-size: 32px;">📊</div>
                        </div>
                        <div id="total-tasks" class="card-value">0</div>
                        <p style="color: #666; font-size: 15px;">All tasks in your workspace</p>
                    </div>
                    
                    <!-- Submitted -->
                    <div class="card">
                        <div class="card-header">
                            <div class="card-title">Submitted Tasks</div>
                            <div style="font-size: 32px;">✅</div>
                        </div>
                        <div id="submitted-tasks" class="card-value">0</div>
                        <p style="color: #666; font-size: 15px;">Successfully delivered</p>
                    </div>
                    
                    <!-- Pending -->
                    <div class="card">
                        <div class="card-header">
                            <div class="card-title">Pending Tasks</div>
                            <div style="font-size: 32px;">⏳</div>
                        </div>
                        <div id="pending-tasks" class="card-value">0</div>
                        <p style="color: #666; font-size: 15px;">Awaiting your action</p>
                    </div>
                    
                    <!-- Progress -->
                    <div class="card" style="grid-column: span 1;">
                        <div class="card-header">
                            <div class="card-title">Completion Progress</div>
                        </div>
                        <div style="margin: 15px 0;">
                            <div class="progress-container">
                                <div id="progress-bar" class="progress-bar" style="width: 0%"></div>
                            </div>
                        </div>
                        <div style="display: flex; justify-content: space-between; font-weight: 600; font-size: 15px;">
                            <span id="progress-text">0% Complete</span>
                            <span id="progress-ratio">0 / 0</span>
                        </div>
                    </div>
                </div>
                
                <!-- Reminders -->
                <div class="reminders-section">
                    <h2 style="font-size: 24px; font-weight: 700; color: white; margin-bottom: 20px;">🔔 Upcoming Reminders &amp; Deadlines</h2>
                    <div id="reminders-list"></div>
                </div>
            </div>
        </div>
        
        <!-- ADD PAGE (File Upload) -->
        <div id="add" class="page">
            <div class="container">
                <div class="form-container">
                    <h2 style="font-size: 28px; font-weight: 700; margin-bottom: 10px;">📤 Add New File Task</h2>
                    <p style="color: #666; margin-bottom: 30px;">Upload documents, images or PDFs</p>
                    
                    <input type="text" id="add-title" class="title-input" placeholder="Task Title (must be unique)" maxlength="80">
                    
                    <div style="margin-bottom: 30px;">
                        <label style="font-weight: 600; font-size: 15px; display: block; margin-bottom: 12px;">Attach File</label>
                        <div onclick="document.getElementById('file-input').click()" 
                             style="border: 3px dashed #0066ff; border-radius: 20px; padding: 40px; text-align: center; cursor: pointer; transition: all .3s;">
                            <div style="font-size: 48px; margin-bottom: 12px;">📎</div>
                            <p style="font-weight: 600; color: #0066ff;">Click or drag to upload</p>
                            <p style="font-size: 14px; color: #888;">PDF, DOC, DOCX, JPG, PNG supported</p>
                            <input type="file" id="file-input" accept=".pdf,.doc,.docx,.jpg,.jpeg,.png" style="display: none;" onchange="handleFileSelect(event)">
                        </div>
                        <div id="selected-file-name" style="margin-top: 12px; font-weight: 600; color: #0066ff; display: none;"></div>
                    </div>
                    
                    <div style="margin-bottom: 30px;">
                        <label style="font-weight: 600;">Deadline (optional)</label>
                        <input type="datetime-local" id="add-deadline" style="width: 100%; padding: 16px; border-radius: 16px; border: 2px solid #e5e7eb; margin-top: 8px;">
                    </div>
                    
                    <button onclick="saveFileTask()" 
                            style="width: 100%; padding: 20px; background: linear-gradient(90deg, #0066ff, #ff2d95); color: white; border: none; border-radius: 20px; font-size: 18px; font-weight: 700;">
                        💾 Save Task
                    </button>
                </div>
            </div>
        </div>
        
        <!-- WRITE PAGE -->
        <div id="write" class="page">
            <div class="container">
                <div class="form-container">
                    <h2 style="font-size: 28px; font-weight: 700; margin-bottom: 10px;">✍️ Write New Text Task</h2>
                    <p style="color: #666; margin-bottom: 20px;">Rich text editor – fully formatted</p>
                    
                    <input type="text" id="write-title" class="title-input" placeholder="Task Title (must be unique)">
                    
                    <div class="toolbar">
                        <select id="font-select" onchange="applyFont()">
                            <option value="Poppins">Poppins</option>
                            <option value="Arial">Arial</option>
                            <option value="Verdana">Verdana</option>
                            <option value="Times New Roman">Times New Roman</option>
                            <option value="Courier New">Courier</option>
                        </select>
                        
                        <input type="number" id="size-input" value="18" min="12" max="48" style="width: 80px;" onchange="applySize()">
                        
                        <button onclick="formatText('bold')" title="Bold">𝐁</button>
                        <button onclick="formatText('italic')" title="Italic">𝐼</button>
                        <button onclick="formatHeading(1)">H1</button>
                        <button onclick="formatHeading(2)">H2</button>
                        <button onclick="formatText('justifyLeft')">⇤</button>
                        <button onclick="formatText('justifyCenter')">⇶</button>
                        <button onclick="formatText('justifyRight')">⇥</button>
                    </div>
                    
                    <div id="write-editor" contenteditable="true" class="editor"></div>
                    
                    <div style="margin-top: 30px; display: flex; gap: 15px;">
                        <div style="flex: 1;">
                            <label>Deadline (optional)</label>
                            <input type="datetime-local" id="write-deadline" style="width: 100%; padding: 16px; border: 2px solid #e5e7eb; border-radius: 16px;">
                        </div>
                        <button onclick="saveWrittenTask()" 
                                style="flex: 1; padding: 18px; background: linear-gradient(90deg, #0066ff, #ff2d95); color: white; border: none; border-radius: 20px; font-weight: 700; font-size: 18px;">
                            💾 Save Written Task
                        </button>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- SUBMIT PAGE -->
        <div id="submit" class="page">
            <div class="container">
                <h2 style="font-size: 32px; font-weight: 700; color: white; margin-bottom: 30px;">✅ Submit Your Saved Tasks</h2>
                <div id="submit-list" class="task-grid"></div>
                <div id="submit-empty" style="display: none; text-align: center; padding: 80px 40px; background: rgba(255,255,255,0.15); border-radius: 24px; color: white;">
                    <h3 style="font-size: 28px;">No pending tasks to submit</h3>
                    <p style="margin-top: 12px;">Tasks created via Add or Write will appear here</p>
                </div>
            </div>
        </div>
        
        <!-- LIST PAGE -->
        <div id="list" class="page">
            <div class="container">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 30px;">
                    <h2 style="font-size: 32px; font-weight: 700; color: white;">📋 All Tasks</h2>
                    
                    <div style="display: flex; background: white; border-radius: 50px; padding: 6px; box-shadow: 0 8px 25px rgba(0,0,0,0.1);">
                        <button onclick="filterList('all')" id="filter-all" class="nav-btn active" style="padding: 10px 28px;">All</button>
                        <button onclick="filterList('pending')" id="filter-pending" class="nav-btn">Pending</button>
                        <button onclick="filterList('submitted')" id="filter-submitted" class="nav-btn">Submitted</button>
                    </div>
                </div>
                
                <div id="list-grid" class="task-grid"></div>
                <div id="list-empty" style="display: none; text-align: center; padding: 100px; color: white; font-size: 20px;">No tasks yet. Create your first task!</div>
            </div>
        </div>
    </div>
    
    <!-- TASK DETAIL MODAL -->
    <div id="task-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 id="modal-title" style="font-weight: 700; font-size: 24px;"></h3>
                <button onclick="closeModal()" style="background: none; border: none; font-size: 32px; cursor: pointer; color: #999;">×</button>
            </div>
            
            <div id="modal-body" style="padding: 30px;">
                <!-- Dynamic content injected by JS -->
            </div>
            
            <div id="modal-footer" style="padding: 24px 32px; border-top: 1px solid #eee; display: flex; gap: 12px; justify-content: flex-end;">
                <!-- Buttons injected by JS -->
            </div>
        </div>
    </div>
    
    <!-- TOAST -->
    <div id="toast" class="toast">
        <span id="toast-icon"></span>
        <span id="toast-message"></span>
    </div>
    
    <script>
        // ======================
        // GLOBAL STATE
        // ======================
        let currentUser = null;
        let currentTasks = [];
        
        // ======================
        // LOCALSTORAGE HELPERS
        // ======================
        function getUsers() {
            const users = localStorage.getItem('taskflow_users');
            return users ? JSON.parse(users) : [];
        }
        
        function saveUsers(users) {
            localStorage.setItem('taskflow_users', JSON.stringify(users));
        }
        
        function getUserTasks(username) {
            const key = `taskflow_tasks_${username}`;
            const tasks = localStorage.getItem(key);
            return tasks ? JSON.parse(tasks) : [];
        }
        
        function saveUserTasks(username, tasks) {
            const key = `taskflow_tasks_${username}`;
            localStorage.setItem(key, JSON.stringify(tasks));
        }
        
        function generateId() {
            return 'task-' + Date.now().toString(36) + Math.random().toString(36).substr(2, 5);
        }
        
        // ======================
        // AUTH FUNCTIONS
        // ======================
        function switchAuthTab(tab) {
            const loginTab = document.getElementById('login-tab');
            const signupTab = document.getElementById('signup-tab');
            const loginForm = document.getElementById('login-form');
            const signupForm = document.getElementById('signup-form');
            
            if (tab === 0) {
                loginTab.classList.add('active');
                signupTab.classList.remove('active');
                loginForm.style.display = 'block';
                signupForm.style.display = 'none';
            } else {
                loginTab.classList.remove('active');
                signupTab.classList.add('active');
                loginForm.style.display = 'none';
                signupForm.style.display = 'block';
            }
        }
        
        function handleLogin() {
            const name = document.getElementById('login-name').value.trim();
            const password = document.getElementById('login-password').value;
            
            if (!name || !password) {
                showToast('❌', 'Please fill both fields', true);
                return;
            }
            
            const users = getUsers();
            const user = users.find(u => u.name === name && u.password === password);
            
            if (user) {
                currentUser = name;
                currentTasks = getUserTasks(name);
                document.getElementById('auth-page').style.display = 'none';
                document.getElementById('main-app').style.display = 'block';
                document.getElementById('user-name-display').textContent = name;
                renderAll();
                startClock();
                showToast('🚀', `Welcome back, ${name}!`, false);
            } else {
                document.getElementById('login-error').style.display = 'block';
                setTimeout(() => {
                    document.getElementById('login-error').style.display = 'none';
                }, 3000);
            }
        }
        
        function handleSignup() {
            const name = document.getElementById('signup-name').value.trim();
            const password = document.getElementById('signup-password').value;
            
            if (!name || !password) {
                showToast('❌', 'Name and password are required', true);
                return;
            }
            
            const users = getUsers();
            if (users.find(u => u.name === name)) {
                document.getElementById('signup-error').style.display = 'block';
                setTimeout(() => {
                    document.getElementById('signup-error').style.display = 'none';
                }, 3000);
                return;
            }
            
            users.push({ name, password });
            saveUsers(users);
            
            currentUser = name;
            currentTasks = [];
            saveUserTasks(name, []);
            
            document.getElementById('auth-page').style.display = 'none';
            document.getElementById('main-app').style.display = 'block';
            document.getElementById('user-name-display').textContent = name;
            renderAll();
            startClock();
            showToast('🎉', `Account created! Welcome, ${name}`, false);
        }
        
        function logout() {
            currentUser = null;
            currentTasks = [];
            document.getElementById('main-app').style.display = 'none';
            document.getElementById('auth-page').style.display = 'flex';
            document.getElementById('login-name').value = '';
            document.getElementById('login-password').value = '';
            showToast('👋', 'Logged out successfully', false);
        }
        
        // ======================
        // CLOCK
        // ======================
        function startClock() {
            const clockEl = document.getElementById('live-clock');
            setInterval(() => {
                const now = new Date();
                clockEl.textContent = now.toLocaleTimeString('en-US', { 
                    hour: '2-digit', 
                    minute: '2-digit', 
                    second: '2-digit' 
                });
            }, 1000);
        }
        
        // ======================
        // TOAST
        // ======================
        function showToast(icon, message, isError) {
            const toast = document.getElementById('toast');
            const toastIcon = document.getElementById('toast-icon');
            const toastMsg = document.getElementById('toast-message');
            
            toastIcon.innerHTML = icon;
            toastMsg.textContent = message;
            
            if (isError) toast.style.background = '#ff2d95';
            else toast.style.background = '#0066ff';
            
            toast.style.display = 'flex';
            
            setTimeout(() => {
                toast.style.transform = 'translateY(30px)';
                toast.style.opacity = '0';
                setTimeout(() => {
                    toast.style.display = 'none';
                    toast.style.transform = '';
                    toast.style.opacity = '';
                }, 400);
            }, 3500);
        }
        
        // ======================
        // RENDER DASHBOARD
        // ======================
        function renderDashboard() {
            const total = currentTasks.length;
            const submitted = currentTasks.filter(t => t.status === 'submitted').length;
            const pending = total - submitted;
            
            document.getElementById('total-tasks').textContent = total;
            document.getElementById('submitted-tasks').textContent = submitted;
            document.getElementById('pending-tasks').textContent = pending;
            
            const progress = total === 0 ? 0 : Math.round((submitted / total) * 100);
            document.getElementById('progress-bar').style.width = `${progress}%`;
            document.getElementById('progress-text').textContent = `${progress}% Complete`;
            document.getElementById('progress-ratio').textContent = `${submitted} / ${total}`;
            
            // Reminders
            const now = new Date();
            const remindersHTML = currentTasks
                .filter(task => task.deadline)
                .sort((a, b) => new Date(a.deadline) - new Date(b.deadline))
                .slice(0, 5)
                .map(task => {
                    const deadlineDate = new Date(task.deadline);
                    const diffMs = deadlineDate - now;
                    const diffDays = Math.ceil(diffMs / (1000 * 60 * 60 * 24));
                    
                    let badge = '';
                    if (diffMs < 0) badge = `<span class="badge" style="background:#ff2d95;color:white;">OVERDUE</span>`;
                    else if (diffDays <= 2) badge = `<span class="badge" style="background:#ffaa00;color:white;">SOON</span>`;
                    
                    return `
                    <div class="reminder-card ${diffMs < 0 ? 'overdue' : diffDays <= 2 ? 'near' : ''}">
                        <div>
                            <div style="font-weight:700;font-size:18px;">${task.title}</div>
                            <div style="color:#666;font-size:13px;">${task.type.toUpperCase()} • ${deadlineDate.toLocaleDateString('en-US', {month:'short', day:'numeric', hour:'numeric', minute:'2-digit'})}</div>
                        </div>
                        <div style="text-align:right;">
                            ${badge}
                            <div style="font-size:13px;color:#666;margin-top:4px;">${diffMs < 0 ? 'Passed' : diffDays + ' day' + (diffDays !== 1 ? 's' : '')}</div>
                        </div>
                    </div>`;
                }).join('');
            
            document.getElementById('reminders-list').innerHTML = remindersHTML || `
                <div style="background:white;border-radius:24px;padding:40px;text-align:center;color:#888;">
                    No deadlines set yet.<br><span style="font-size:14px;">Create tasks with deadlines to see reminders here</span>
                </div>`;
        }
        
        // ======================
        // FILE UPLOAD HANDLER
        // ======================
        let selectedFileData = null;
        let selectedFileName = '';
        let selectedFileType = '';
        
        function handleFileSelect(e) {
            const file = e.target.files[0];
            if (!file) return;
            
            selectedFileName = file.name;
            selectedFileType = file.type;
            
            document.getElementById('selected-file-name').innerHTML = `
                <span style="background:#e5f0ff;color:#0066ff;padding:8px 16px;border-radius:12px;">📄 ${selectedFileName}</span>
            `;
            document.getElementById('selected-file-name').style.display = 'block';
            
            const reader = new FileReader();
            reader.onload = function(ev) {
                selectedFileData = ev.target.result; // data URL
            };
            reader.readAsDataURL(file);
        }
        
        function saveFileTask() {
            const title = document.getElementById('add-title').value.trim();
            
            if (!title) {
                showToast('⚠️', 'Title is required', true);
                return;
            }
            
            if (currentTasks.some(t => t.title.toLowerCase() === title.toLowerCase())) {
                showToast('❌', 'Task with this title already exists', true);
                return;
            }
            
            if (!selectedFileData) {
                showToast('⚠️', 'Please select a file', true);
                return;
            }
            
            const deadline = document.getElementById('add-deadline').value || null;
            
            const newTask = {
                id: generateId(),
                title: title,
                type: 'file',
                status: 'pending',
                deadline: deadline,
                createdAt: new Date().toISOString(),
                fileName: selectedFileName,
                fileType: selectedFileType,
                fileData: selectedFileData
            };
            
            currentTasks.push(newTask);
            saveUserTasks(currentUser, currentTasks);
            
            // Reset form
            document.getElementById('add-title').value = '';
            document.getElementById('add-deadline').value = '';
            document.getElementById('selected-file-name').style.display = 'none';
            selectedFileData = null;
            selectedFileName = '';
            
            renderAll();
            navigateTo('dashboard');
            showToast('✅', 'File task saved successfully!', false);
        }
        
        // ======================
        // WRITE / EDITOR
        // ======================
        function applyFont() {
            const font = document.getElementById('font-select').value;
            document.execCommand('fontName', false, font);
        }
        
        function applySize() {
            const size = document.getElementById('size-input').value;
            document.execCommand('fontSize', false, size);
        }
        
        function formatText(cmd) {
            document.execCommand(cmd, false, null);
        }
        
        function formatHeading(level) {
            const tag = level === 1 ? 'h1' : 'h2';
            document.execCommand('formatBlock', false, tag);
        }
        
        function saveWrittenTask() {
            const title = document.getElementById('write-title').value.trim();
            const editorContent = document.getElementById('write-editor').innerHTML.trim();
            
            if (!title) {
                showToast('⚠️', 'Title is required', true);
                return;
            }
            
            if (currentTasks.some(t => t.title.toLowerCase() === title.toLowerCase())) {
                showToast('❌', 'Task with this title already exists', true);
                return;
            }
            
            if (!editorContent || editorContent === '<br>') {
                showToast('⚠️', 'Please write something', true);
                return;
            }
            
            const deadline = document.getElementById('write-deadline').value || null;
            
            const newTask = {
                id: generateId(),
                title: title,
                type: 'written',
                status: 'pending',
                deadline: deadline,
                createdAt: new Date().toISOString(),
                content: editorContent
            };
            
            currentTasks.push(newTask);
            saveUserTasks(currentUser, currentTasks);
            
            // Reset
            document.getElementById('write-title').value = '';
            document.getElementById('write-editor').innerHTML = '';
            document.getElementById('write-deadline').value = '';
            
            renderAll();
            navigateTo('dashboard');
            showToast('✅', 'Written task saved!', false);
        }
        
        // ======================
        // SUBMIT PAGE
        // ======================
        function renderSubmitPage() {
            const pendingTasks = currentTasks.filter(t => t.status === 'pending');
            
            const container = document.getElementById('submit-list');
            const empty = document.getElementById('submit-empty');
            
            if (pendingTasks.length === 0) {
                container.innerHTML = '';
                empty.style.display = 'block';
                return;
            }
            
            empty.style.display = 'none';
            
            container.innerHTML = pendingTasks.map(task => `
                <div class="task-card">
                    <div class="task-title">${task.title}</div>
                    <div class="task-meta">
                        <span class="badge pending">${task.type.toUpperCase()}</span>
                        ${task.deadline ? `<span style="font-size:13px;color:#666;">⏰ ${new Date(task.deadline).toLocaleDateString()}</span>` : ''}
                    </div>
                    <div class="task-footer">
                        <button onclick="submitSingleTask('${task.id}')" 
                                style="background:linear-gradient(90deg,#0066ff,#ff2d95);color:white;border:none;padding:10px 24px;border-radius:50px;font-weight:700;">
                            Submit Now
                        </button>
                        <button onclick="viewTask('${task.id}')" 
                                style="background:#f1f3f9;color:#444;border:none;padding:10px 18px;border-radius:12px;">
                            👁️ View
                        </button>
                    </div>
                </div>
            `).join('');
        }
        
        function submitSingleTask(id) {
            const task = currentTasks.find(t => t.id === id);
            if (!task || task.status === 'submitted') return;
            
            task.status = 'submitted';
            saveUserTasks(currentUser, currentTasks);
            renderAll();
            showToast('✅', `Task “${task.title}” submitted!`, false);
        }
        
        // ======================
        // LIST PAGE + FILTERS
        // ======================
        let currentFilter = 'all';
        
        function renderListPage() {
            let filtered = currentTasks;
            
            if (currentFilter === 'pending') {
                filtered = currentTasks.filter(t => t.status === 'pending');
            } else if (currentFilter === 'submitted') {
                filtered = currentTasks.filter(t => t.status === 'submitted');
            }
            
            const container = document.getElementById('list-grid');
            const empty = document.getElementById('list-empty');
            
            if (filtered.length === 0) {
                container.innerHTML = '';
                empty.style.display = 'block';
                return;
            }
            
            empty.style.display = 'none';
            
            container.innerHTML = filtered.map(task => {
                const deadlineHTML = task.deadline 
                    ? `<div style="font-size:13px;color:#666;margin-top:8px;">📅 ${new Date(task.deadline).toLocaleString('en-US', {month:'short',day:'numeric',hour:'numeric',minute:'2-digit'})}</div>` 
                    : '';
                
                return `
                <div class="task-card" onclick="viewTask('${task.id}')">
                    <div class="task-title">${task.title}</div>
                    <div class="task-meta">
                        <span class="badge ${task.status === 'pending' ? 'pending' : 'submitted'}">${task.type.toUpperCase()}</span>
                        <span class="badge" style="background:#ddd;color:#444;">${task.status.toUpperCase()}</span>
                    </div>
                    ${deadlineHTML}
                    <div class="task-footer" style="margin-top:20px;">
                        <button onclick="event.stopImmediatePropagation();deleteTask('${task.id}');" 
                                style="background:#ff2d95;color:white;border:none;padding:8px 18px;border-radius:50px;font-size:13px;">
                            🗑️ Delete
                        </button>
                    </div>
                </div>`;
            }).join('');
        }
        
        function filterList(mode) {
            currentFilter = mode;
            
            // Update active filter button
            document.querySelectorAll('#list .nav-btn').forEach(btn => btn.classList.remove('active'));
            if (mode === 'all') document.getElementById('filter-all').classList.add('active');
            else if (mode === 'pending') document.getElementById('filter-pending').classList.add('active');
            else if (mode === 'submitted') document.getElementById('filter-submitted').classList.add('active');
            
            renderListPage();
        }
        
        function deleteTask(id) {
            if (!confirm('Delete this task permanently?')) return;
            
            currentTasks = currentTasks.filter(t => t.id !== id);
            saveUserTasks(currentUser, currentTasks);
            renderAll();
            showToast('🗑️', 'Task deleted', false);
            
            // If modal is open, close it
            if (document.getElementById('task-modal').style.display === 'flex') {
                closeModal();
            }
        }
        
        // ======================
        // TASK VIEW MODAL
        // ======================
        function viewTask(id) {
            const task = currentTasks.find(t => t.id === id);
            if (!task) return;
            
            const modal = document.getElementById('task-modal');
            const titleEl = document.getElementById('modal-title');
            const bodyEl = document.getElementById('modal-body');
            const footerEl = document.getElementById('modal-footer');
            
            titleEl.textContent = task.title;
            
            let bodyHTML = '';
            let footerHTML = '';
            
            if (task.type === 'written') {
                const isEditable = task.status === 'pending';
                
                bodyHTML = `
                    <div style="font-size:18px;line-height:1.7;color:#111;font-weight:700;background:#fafaff;padding:24px;border-radius:18px;min-height:340px;border:3px solid #e5e7eb;">
                        ${task.content}
                    </div>`;
                
                if (isEditable) {
                    footerHTML = `
                        <button onclick="updateWrittenTask('${task.id}')" 
                                style="padding:14px 32px;background:linear-gradient(90deg,#0066ff,#ff2d95);color:white;border:none;border-radius:50px;font-weight:700;">
                            💾 Update &amp; Save
                        </button>
                        <button onclick="closeModal()" style="padding:14px 32px;background:#eee;color:#444;border:none;border-radius:50px;">Cancel</button>`;
                } else {
                    footerHTML = `<button onclick="closeModal()" style="padding:14px 32px;background:#0066ff;color:white;border:none;border-radius:50px;">Close</button>`;
                }
            } 
            else if (task.type === 'file') {
                let preview = '';
                
                if (task.fileType.includes('pdf')) {
                    preview = `<iframe src="${task.fileData}" style="width:100%;height:520px;border:3px solid #ddd;border-radius:16px;"></iframe>`;
                } 
                else if (task.fileType.includes('image')) {
                    preview = `<img src="${task.fileData}" style="max-width:100%;max-height:520px;border-radius:16px;box-shadow:0 10px 30px rgba(0,0,0,0.1);">`;
                } 
                else {
                    preview = `
                        <div style="background:#f8f9ff;padding:50px;border-radius:20px;text-align:center;">
                            <p style="font-size:60px;margin-bottom:20px;">📄</p>
                            <p style="font-weight:700;font-size:20px;">${task.fileName}</p>
                            <p style="color:#666;">Cannot preview this file type in browser.</p>
                            <a href="${task.fileData}" download="${task.fileName}" 
                               style="margin-top:20px;display:inline-block;background:#0066ff;color:white;padding:14px 40px;border-radius:50px;text-decoration:none;font-weight:700;">
                                ⬇️ Download File
                            </a>
                        </div>`;
                }
                
                bodyHTML = preview;
                footerHTML = `
                    <button onclick="closeModal()" style="padding:14px 32px;background:#0066ff;color:white;border:none;border-radius:50px;">Close Preview</button>`;
            }
            
            bodyEl.innerHTML = bodyHTML;
            footerEl.innerHTML = footerHTML;
            
            modal.style.display = 'flex';
        }
        
        function updateWrittenTask(id) {
            const task = currentTasks.find(t => t.id === id);
            if (!task) return;
            
            // Re-open editor inside modal with current content
            const currentContent = task.content;
            
            const bodyEl = document.getElementById('modal-body');
            bodyEl.innerHTML = `
                <div class="toolbar" style="margin-bottom:20px;">
                    <select id="modal-font" onchange="applyFontModal()">
                        <option value="Poppins">Poppins</option>
                        <option value="Arial">Arial</option>
                        <option value="Verdana">Verdana</option>
                        <option value="Times New Roman">Times New Roman</option>
                        <option value="Courier New">Courier</option>
                    </select>
                    <input type="number" id="modal-size" value="18" onchange="applySizeModal()" style="width:80px;">
                    <button onclick="formatTextModal('bold')">𝐁</button>
                    <button onclick="formatTextModal('italic')">𝐼</button>
                    <button onclick="formatHeadingModal(1)">H1</button>
                    <button onclick="formatHeadingModal(2)">H2</button>
                </div>
                <div id="modal-editor" contenteditable="true" class="editor" style="min-height:380px;">${currentContent}</div>`;
            
            const footerEl = document.getElementById('modal-footer');
            footerEl.innerHTML = `
                <button onclick="saveUpdatedWritten('${id}')" style="padding:14px 32px;background:linear-gradient(90deg,#0066ff,#ff2d95);color:white;border:none;border-radius:50px;font-weight:700;">Save Changes</button>
                <button onclick="closeModal()" style="padding:14px 32px;background:#eee;color:#444;border:none;border-radius:50px;">Cancel</button>`;
        }
        
        function applyFontModal() {
            const font = document.getElementById('modal-font').value;
            document.execCommand('fontName', false, font);
        }
        
        function applySizeModal() {
            const size = document.getElementById('modal-size').value;
            document.execCommand('fontSize', false, size);
        }
        
        function formatTextModal(cmd) {
            document.execCommand(cmd, false, null);
        }
        
        function formatHeadingModal(level) {
            const tag = level === 1 ? 'h1' : 'h2';
            document.execCommand('formatBlock', false, tag);
        }
        
        function saveUpdatedWritten(id) {
            const task = currentTasks.find(t => t.id === id);
            if (!task) return;
            
            const newContent = document.getElementById('modal-editor').innerHTML;
            task.content = newContent;
            
            saveUserTasks(currentUser, currentTasks);
            closeModal();
            renderAll();
            showToast('✅', 'Task updated successfully', false);
        }
        
        function closeModal() {
            const modal = document.getElementById('task-modal');
            modal.style.display = 'none';
        }
        
        // ======================
        // NAVIGATION
        // ======================
        function navigateTo(page) {
            // Remove active from all nav buttons
            document.querySelectorAll('.nav-btn').forEach(btn => btn.classList.remove('active'));
            
            // Activate the clicked one
            if (page === 'dashboard') document.getElementById('nav-dashboard').classList.add('active');
            else if (page === 'add') document.getElementById('nav-add').classList.add('active');
            else if (page === 'write') document.getElementById('nav-write').classList.add('active');
            else if (page === 'submit') document.getElementById('nav-submit').classList.add('active');
            else if (page === 'list') document.getElementById('nav-list').classList.add('active');
            
            // Hide all pages
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            
            // Show requested page
            const target = document.getElementById(page);
            if (target) target.classList.add('active');
            
            // Render specific pages
            if (page === 'submit') renderSubmitPage();
            else if (page === 'list') {
                currentFilter = 'all';
                document.querySelectorAll('#list .nav-btn').forEach(b => b.classList.remove('active'));
                document.getElementById('filter-all').classList.add('active');
                renderListPage();
            }
        }
        
        // ======================
        // GLOBAL RENDER
        // ======================
        function renderAll() {
            renderDashboard();
            if (document.getElementById('submit').classList.contains('active')) renderSubmitPage();
            if (document.getElementById('list').classList.contains('active')) renderListPage();
        }
        
        // ======================
        // DEADLINE CHECKER (runs every 30 seconds)
        // ======================
        function checkDeadlines() {
            const now = new Date();
            let alerted = false;
            
            currentTasks.forEach(task => {
                if (!task.deadline || task.status === 'submitted') return;
                
                const deadline = new Date(task.deadline);
                const minutesLeft = (deadline - now) / 60000;
                
                if (minutesLeft < 0 && !task.notifiedOverdue) {
                    showToast('🔴', `OVERDUE: ${task.title}`, true);
                    task.notifiedOverdue = true;
                    saveUserTasks(currentUser, currentTasks);
                    alerted = true;
                } else if (minutesLeft > 0 && minutesLeft < 60 && !task.notifiedNear) {
                    showToast('🟠', `Deadline in < 1 hour: ${task.title}`, false);
                    task.notifiedNear = true;
                    saveUserTasks(currentUser, currentTasks);
                    alerted = true;
                }
            });
            
            // Refresh dashboard if needed
            if (alerted && document.getElementById('dashboard').classList.contains('active')) {
                renderDashboard();
            }
        }
        
        // ======================
        // APP INITIALIZATION
        // ======================
        window.onload = function() {
            // Ensure editor has default styling
            const editor = document.getElementById('write-editor');
            if (editor) {
                editor.style.fontWeight = '700';
                editor.style.color = '#111';
            }
            
            // Check deadlines every 30 seconds
            setInterval(checkDeadlines, 30000);
            
            console.log('%c✅ TaskFlow SPA loaded successfully – fully functional, no backend required!', 'background:#0066ff;color:white;padding:4px 8px;border-radius:6px;font-weight:700');
        };
    </script>
</body>
</html>
