<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>The Method - Training Studio</title>
    <style>
        /* CSS for Styling the Application */
        :root {
            --primary-color: #28a745;
            --secondary-color: #f4f4f4;
            --accent-color: #ff4500;
            --text-color: #ff4500;
            --light-gray: #ccc;
            --success-green: #28a745;
            --error-red: #dc3545;
            --warning-pink: #ffc0cb;
        }

        body, html {
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            background-color: var(--secondary-color);
            color: var(--text-color);
            height: 100%;
            overflow: hidden; /* Prevent scrolling on the body */
            background-image: url('Screenshot (49).png'); /* Background image for the whole web */
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
        }

        .app-container {
            display: flex;
            flex-direction: column;
            height: 100vh;
        }

        header {
            background-color: var(--primary-color);
            color: white;
            padding: 10px 20px;
            text-align: center;
            flex-shrink: 0;
        }

        .logo-image {
            max-height: 80px; /* Adjust as needed */
            width: auto;
        }

        .sub-logo {
            font-size: 0.8em;
            letter-spacing: 1px;
        }
        
        main {
            flex-grow: 1;
            overflow-y: auto; /* Allow scrolling within the main content area */
            padding: 20px;
        }

        .page {
            display: none; /* Hide all pages by default */
            max-width: 800px;
            margin: 0 auto;
        }

        .page.active {
            display: block; /* Show the active page */
        }

        h1, h2 {
            color: var(--primary-color);
            text-align: center;
            border-bottom: 2px solid var(--accent-color);
            padding-bottom: 10px;
            margin-bottom: 20px;
        }
        
        /* Form & Input Styles */
        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }

        input[type="text"],
        input[type="email"],
        input[type="tel"],
        input[type="number"],
        input[type="password"],
        input[type="date"],
        input[type="time"],
        select,
        textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--light-gray);
            border-radius: 5px;
            box-sizing: border-box;
            font-size: 1em;
            background-color: #fff;
        }

        .btn {
            display: inline-block;
            background-color: var(--accent-color);
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1.1em;
            text-align: center;
            width: 100%;
            margin-top: 10px;
            text-transform: uppercase;
            font-weight: bold;
            transition: background-color 0.3s;
        }

        .btn-secondary {
            background-color: var(--primary-color);
        }
        
        .btn-danger {
            background-color: var(--error-red);
        }

        .btn:hover {
            opacity: 0.9;
        }
        
        /* Home Page Buttons */
        .home-buttons {
            display: flex;
            flex-direction: column;
            gap: 15px;
            max-width: 400px;
            margin: 40px auto;
        }

        /* Alerts */
        .alert {
            padding: 15px;
            margin: 20px 0;
            border-radius: 5px;
            text-align: center;
            font-weight: bold;
            color: white;
        }

        .alert-success { background-color: var(--success-green); }
        .alert-danger { background-color: var(--error-red); }
        .alert-warning { background-color: var(--warning-pink); color: var(--text-color); border: 1px solid var(--accent-color); }
        
        /* Report Table Styles */
        .report-table-container {
            overflow-x: auto;
        }
        .report-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        .report-table th, .report-table td {
            border: 1px solid var(--light-gray);
            padding: 12px;
            text-align: left;
        }

        .report-table th {
            background-color: var(--primary-color);
            color: white;
        }
        
        .report-table tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        
        .report-table tfoot {
            font-weight: bold;
        }
        
        /* Client Details */
        .client-info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .info-card {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        /* Password Modal */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.5);
        }

        .modal-content {
            background-color: #fefefe;
            margin: 15% auto;
            padding: 30px;
            border: 1px solid #888;
            width: 90%;
            max-width: 400px;
            border-radius: 10px;
            text-align: center;
        }

        .back-button {
            width: auto;
            margin-bottom: 20px;
            padding: 10px 15px;
        }

    </style>
</head>
<body>

    <div class="app-container">
        <header>
            <img src="Screenshot (48).png" alt="THE METHOD PERSONAL TRAINING STUDIO" class="logo-image">
        </header>

        <main>
            <div id="home-page" class="page active">
                <div class="home-buttons">
                    <button class="btn" onclick="app.navigateTo('client-checkin-page')">Client Check In</button>
                    <button class="btn btn-secondary" onclick="app.showAdminPassword()">Admin Panel</button>
                </div>
            </div>

            <div id="client-checkin-page" class="page">
                <button class="btn btn-secondary back-button" onclick="app.navigateTo('home-page')">Back to Home</button>
                <h2>CLIENT CHECK IN</h2>
                <div id="checkin-alert-container"></div>
                <form id="checkin-form">
                    <div class="form-group">
                        <label for="checkin-client-name">Client Name</label>
                        <input type="text" id="checkin-client-name" list="client-datalist" placeholder="Start typing client's name...">
                    </div>
                    <div class="form-group">
                        <label for="checkin-trainer-name">Trainer Name</label>
                        <select id="checkin-trainer-name" required></select>
                    </div>
                    <div class="form-group">
                        <label for="checkin-session-type">Session Type</label>
                        <select id="checkin-session-type" required></select>
                    </div>
                    <div class="form-group" id="checkin-partner-container" style="display: none;">
                        <label for="checkin-partner-name">Partner Name</label>
                        <input type="text" id="checkin-partner-name" list="client-datalist" placeholder="Start typing partner's name...">
                    </div>
                    <button type="submit" class="btn">Check In Client</button>
                </form>
            </div>
            
            <div id="admin-panel-page" class="page">
                <button class="btn btn-secondary back-button" onclick="app.navigateTo('home-page');">Logout</button>
                <h2>ADMIN PANEL</h2>
                <div class="home-buttons">
                    <button class="btn" onclick="app.navigateTo('add-client-page')">Add New Client</button>
                    <button class="btn" onclick="app.navigateTo('client-details-page')">Client Details</button>
                    <button class="btn" onclick="app.navigateTo('trainer-panel-page')">Trainer Panel</button>
                    <button class="btn" onclick="app.navigateTo('trainer-report-page')">Trainer Report</button>
                    <button class="btn" onclick="app.navigateTo('session-report-page')">Session Report</button>
                </div>
            </div>

            <div id="add-client-page" class="page">
                <button class="btn btn-secondary back-button" onclick="app.navigateTo('admin-panel-page')">Back to Admin Panel</button>
                <h2>ADD NEW CLIENT</h2>
                <form id="add-client-form">
                    <div class="form-group">
                        <label for="add-client-first-name">First Name</label>
                        <input type="text" id="add-client-first-name" required>
                    </div>
                    <div class="form-group">
                        <label for="add-client-last-name">Last Name</label>
                        <input type="text" id="add-client-last-name" required>
                    </div>
                    <div class="form-group">
                        <label for="add-client-email">Email</label>
                        <input type="email" id="add-client-email">
                    </div>
                     <div class="form-group">
                        <label for="add-client-phone">Phone Number</label>
                        <input type="tel" id="add-client-phone">
                    </div>
                    <div class="form-group">
                        <label for="add-client-session-type">Session Type</label>
                        <select id="add-client-session-type" required></select>
                    </div>
                    <div class="form-group">
                        <label for="add-client-session-amount">Starting Package Session Amount</label>
                        <input type="number" id="add-client-session-amount" min="1" required>
                    </div>
                    <div id="add-partner-container" style="display: none;">
                        <h3>Partner Details</h3>
                        <div class="form-group">
                            <label for="add-partner-first-name">Partner First Name</label>
                            <input type="text" id="add-partner-first-name">
                        </div>
                        <div class="form-group">
                            <label for="add-partner-last-name">Partner Last Name</label>
                            <input type="text" id="add-partner-last-name">
                        </div>
                         <div class="form-group">
                            <label for="add-partner-email">Partner Email</label>
                            <input type="email" id="add-partner-email">
                        </div>
                        <div class="form-group">
                            <label for="add-partner-phone">Partner Phone Number</label>
                            <input type="tel" id="add-partner-phone">
                        </div>
                    </div>
                    <button type="submit" class="btn">Add Client</button>
                </form>
            </div>
            
            <div id="client-details-page" class="page">
                    <button class="btn btn-secondary back-button" onclick="app.navigateTo('admin-panel-page')">Back to Admin Panel</button>
                    <h2>CLIENT DETAILS</h2>
                    <div class="form-group">
                        <label for="details-client-search">Select Client</label>
                        <input type="text" id="details-client-search" list="client-datalist" placeholder="Start typing to search for a client...">
                    </div>
                    <div id="client-details-content" style="display:none;">
                            <div class="client-info-grid">
                                <div class="info-card">
                                    <h3>Client Information</h3>
                                    <p><strong>Name:</strong> <span id="details-client-name"></span></p>
                                    <p><strong>Email:</strong> <span id="details-client-email"></span></p>
                                    <p><strong>Phone:</strong> <span id="details-client-phone"></span></p>
                                    <p><strong>Session Type:</strong> <span id="details-client-session-type"></span></p>
                                    <p><strong>Sessions Left:</strong> <span id="details-client-sessions-left"></span></p>
                                </div>
                                <div class="info-card">
                                    <h3>Notes</h3>
                                    <textarea id="details-client-notes" rows="5" placeholder="Add any notes about the client here..."></textarea>
                                    <button class="btn" id="save-notes-btn">Save Notes</button>
                                </div>
                                <div class="info-card">
                                    <h3>Manage Sessions</h3>
                                    <div class="form-group">
                                        <label for="details-recharge-sessions">Recharge Sessions</label>
                                        <input type="number" id="details-recharge-sessions" min="1" placeholder="e.g., 12">
                                        <button class="btn" id="recharge-btn">Recharge</button>
                                    </div>
                                    <div class="form-group">
                                        <label for="details-adjust-sessions">Adjust Sessions</label>
                                        <input type="number" id="details-adjust-sessions" placeholder="e.g., 1 or -1">
                                        <button class="btn" id="adjust-btn">Adjust</button>
                                    </div>
                                </div>
                            </div>
                            <h3>Client Log</h3>
                            <div class="form-group">
                                <label for="details-log-filter">Filter by:</label>
                                <select id="details-log-filter">
                                    <option value="all">All Time</option>
                                     <option value="7">Last 7 Days</option>
                                     <option value="30">Last 30 Days</option>
                                </select>
                            </div>
                            <div class="report-table-container">
                                    <table class="report-table">
                                            <thead>
                                                    <tr><th>Date</th><th>Time</th><th>Action</th></tr>
                                            </thead>
                                            <tbody id="client-log-body"></tbody>
                                    </table>
                            </div>
                            <hr style="margin: 30px 0;">
                            <button id="delete-client-btn" class="btn btn-danger">Delete This Client</button>
                    </div>
            </div>

            <div id="trainer-panel-page" class="page">
                <button class="btn btn-secondary back-button" onclick="app.navigateTo('admin-panel-page')">Back to Admin Panel</button>
                <h2>TRAINER PANEL</h2>
                <form id="trainer-panel-form">
                    <div class="form-group">
                        <label for="trainer-panel-select">Select or Add Trainer</label>
                        <select id="trainer-panel-select"></select>
                    </div>
                    <div id="add-new-trainer-fields" style="display:none;">
                        <h3>Add New Trainer Details</h3>
                        <div class="form-group">
                            <label for="new-trainer-name">New Trainer Name</label>
                            <input type="text" id="new-trainer-name">
                        </div>
                         <div class="form-group">
                            <label for="new-trainer-email">Email</label>
                            <input type="email" id="new-trainer-email">
                        </div>
                         <div class="form-group">
                            <label for="new-trainer-phone">Phone</label>
                            <input type="tel" id="new-trainer-phone">
                        </div>
                    </div>
                    <h3>Payroll Amounts Per Session</h3>
                    <div id="trainer-pay-rates">
                        </div>
                    <button type="submit" class="btn">Save Trainer Info</button>
                </form>
            </div>
            
            <div id="trainer-report-page" class="page">
                <button class="btn btn-secondary back-button" onclick="app.navigateTo('admin-panel-page')">Back to Admin Panel</button>
                <h2>TRAINER REPORT</h2>
                <div class="form-group">
                    <label for="report-trainer-select">Trainer Name</label>
                    <select id="report-trainer-select"></select>
                </div>
                     <div class="form-group">
                    <label for="report-trainer-filter">Time Frame</label>
                     <select id="report-trainer-filter">
                            <option value="7">Last 7 Days</option>
                            <option value="30">Last 30 Days</option>
                            <option value="custom">Custom Date Range</option>
                    </select>
                </div>
                <div id="trainer-custom-date-range" class="form-group" style="display:none;">
                     <label>Start Date:</label>
                     <input type="date" id="trainer-start-date">
                     <label>End Date:</label>
                     <input type="date" id="trainer-end-date">
                     <button type="button" class="btn" id="generate-trainer-report-btn">Generate Report</button>
                </div>
                     <div class="report-table-container">
                    <table class="report-table">
                            <thead>
                                    <tr><th>Client</th><th>Date</th><th>Time</th><th>Session Type</th><th>Pay Amount</th></tr>
                            </thead>
                            <tbody id="trainer-report-body"></tbody>
                            <tfoot>
                                    <tr><td colspan="4" style="text-align:right;"><strong>Total Pay:</strong></td><td id="trainer-report-total"></td></tr>
                            </tfoot>
                    </table>
                </div>
            </div>
            
            <div id="session-report-page" class="page">
                <button class="btn btn-secondary back-button" onclick="app.navigateTo('admin-panel-page')">Back to Admin Panel</button>
                <h2>SESSION REPORT</h2>
                     <div class="form-group">
                    <label for="report-session-filter">Time Frame</label>
                     <select id="report-session-filter">
                            <option value="7">Last 7 Days</option>
                            <option value="30">Last 30 Days</option>
                            <option value="custom">Custom Date Range</option>
                    </select>
                </div>
                <div id="session-custom-date-range" class="form-group" style="display:none;">
                     <label>Start Date:</label>
                     <input type="date" id="session-start-date">
                     <label>End Date:</label>
                     <input type="date" id="session-end-date">
                     <button type="button" class="btn" id="generate-session-report-btn">Generate Report</button>
                </div>
                <button type="button" class="btn" id="add-session-manual-btn">Add a Session Manually</button>
                     <div class="report-table-container">
                    <table class="report-table">
                            <thead>
                                    <tr><th>Trainer</th><th>Client</th><th>Date</th><th>Time</th><th>Session Type</th><th>Action</th></tr>
                            </thead>
                            <tbody id="session-report-body"></tbody>
                    </table>
                </div>
            </div>

            <div id="add-session-page" class="page">
                     <button class="btn btn-secondary back-button" onclick="app.navigateTo('session-report-page')">Back to Session Report</button>
                     <h2>ADD A SESSION</h2>
                     <form id="add-session-form">
                        <div class="form-group">
                            <label for="add-session-client-name">Client Name</label>
                            <input type="text" id="add-session-client-name" list="client-datalist" required>
                        </div>
                        <div class="form-group">
                            <label for="add-session-trainer-name">Trainer Name</label>
                            <select id="add-session-trainer-name" required></select>
                        </div>
                        <div class="form-group">
                            <label for="add-session-session-type">Session Type</label>
                            <select id="add-session-session-type" required></select>
                        </div>
                         <div class="form-group" id="add-session-partner-container" style="display: none;">
                            <label for="add-session-partner-name">Partner Name</label>
                            <input type="text" id="add-session-partner-name" list="client-datalist">
                        </div>
                         <div class="form-group">
                            <label for="add-session-date">Date</label>
                            <input type="date" id="add-session-date" required>
                        </div>
                         <div class="form-group">
                            <label for="add-session-time">Time</label>
                            <input type="time" id="add-session-time" required>
                        </div>
                        <button type="submit" class="btn">Add Session</button>
                     </form>
            </div>
            
        </main>
    </div>

    <div id="admin-password-modal" class="modal">
        <div class="modal-content">
            <h2>Admin Access</h2>
            <p>Please enter the password to access the admin panel.</p>
            <div class="form-group">
                <label for="admin-password" class="sr-only">Password</label>
                <input type="password" id="admin-password">
            </div>
            <p id="password-error" style="color:red; display:none;">Incorrect password.</p>
            <button class="btn" onclick="app.checkAdminPassword()">Login</button>
            <button type="button" class="btn btn-secondary" onclick="document.getElementById('admin-password-modal').style.display = 'none'">Cancel</button>
        </div>
    </div>
    
    <datalist id="client-datalist"></datalist>

    <script>
    // All JavaScript logic for the application
    class TrainingStudioApp {
        constructor() {
            // Use a hardcoded password for the admin panel.
            this.adminPassword = 'admin'; 
            this.sessionTypes = [
                "Single Session", //
                "Partner Session", //
                "Partner Session (Only 1 Party Showed)", //
                "Drop in Partner" //
            ];

            // Load data from localStorage or initialize with empty arrays
            this.clients = JSON.parse(localStorage.getItem('clients')) || [];
            this.trainers = JSON.parse(localStorage.getItem('trainers')) || [];
            this.sessionsLog = JSON.parse(localStorage.getItem('sessionsLog')) || [];

            this.init();
        }

        // --- CORE & INITIALIZATION ---
        init() {
            this.setupEventListeners();
            this.populateAll();
            this.navigateTo('home-page');
        }
        
        saveData() {
            localStorage.setItem('clients', JSON.stringify(this.clients));
            localStorage.setItem('trainers', JSON.stringify(this.trainers));
            localStorage.setItem('sessionsLog', JSON.stringify(this.sessionsLog));
        }
        
        setupEventListeners() {
            // Form submissions
            document.getElementById('checkin-form').addEventListener('submit', (e) => { e.preventDefault(); this.handleClientCheckIn(); });
            document.getElementById('add-client-form').addEventListener('submit', (e) => { e.preventDefault(); this.addNewClient(); });
            document.getElementById('trainer-panel-form').addEventListener('submit', (e) => { e.preventDefault(); this.saveTrainerInfo(); });
            document.getElementById('add-session-form').addEventListener('submit', (e) => { e.preventDefault(); this.addSessionManually(); });
            
            // Conditional "Partner" field display
            const setupPartnerField = (selectId, containerId) => {
                document.getElementById(selectId).addEventListener('change', (e) => {
                    const isPartner = e.target.value === 'Partner Session'; //
                    document.getElementById(containerId).style.display = isPartner ? 'block' : 'none';
                });
            };
            setupPartnerField('checkin-session-type', 'checkin-partner-container');
            setupPartnerField('add-client-session-type', 'add-partner-container');
            setupPartnerField('add-session-session-type', 'add-session-partner-container');
            
            // Trainer Panel dynamic fields
            document.getElementById('trainer-panel-select').addEventListener('change', (e) => this.populateTrainerPanel(e.target.value));
            
            // Report filters
            const setupReportGeneration = (selectId, filterId, customDivId, generateBtnId, generatorFunc) => {
                const boundGenerator = generatorFunc.bind(this);
                const filterSelect = document.getElementById(filterId);
                
                if (document.getElementById(selectId)) {
                    document.getElementById(selectId).addEventListener('change', boundGenerator);
                }
                filterSelect.addEventListener('change', () => {
                    document.getElementById(customDivId).style.display = filterSelect.value === 'custom' ? 'block' : 'none';
                    if (filterSelect.value !== 'custom') boundGenerator();
                });
                document.getElementById(generateBtnId).addEventListener('click', boundGenerator);
            };

            setupReportGeneration('report-trainer-select', 'report-trainer-filter', 'trainer-custom-date-range', 'generate-trainer-report-btn', this.generateTrainerReport);
            setupReportGeneration(null, 'report-session-filter', 'session-custom-date-range', 'generate-session-report-btn', this.generateSessionReport);

            // Client Details Page listeners
            document.getElementById('details-client-search').addEventListener('input', (e) => this.populateClientDetails(e.target.value));
            document.getElementById('save-notes-btn').addEventListener('click', () => this.saveClientNotes());
            document.getElementById('recharge-btn').addEventListener('click', () => this.rechargeClientSessions());
            document.getElementById('adjust-btn').addEventListener('click', () => this.adjustClientSessions());
            document.getElementById('details-log-filter').addEventListener('change', () => this.populateClientLog());
            document.getElementById('delete-client-btn').addEventListener('click', () => this.deleteClient());
            
            document.getElementById('add-session-manual-btn').addEventListener('click', () => this.navigateTo('add-session-page'));
        }

        // --- POPULATION ---
        populateAll() {
            this.populateClientDataList();
            this.populateTrainerDropdowns();
            this.populateSessionTypeDropdowns();
            this.populateTrainerPanel();
        }

        populateClientDataList() {
            const datalist = document.getElementById('client-datalist');
            datalist.innerHTML = '';
            this.clients.forEach(client => {
                const option = document.createElement('option');
                option.value = `${client.firstName} ${client.lastName}`;
                datalist.appendChild(option);
            });
        }

        populateTrainerDropdowns() {
            const selects = document.querySelectorAll('#checkin-trainer-name, #report-trainer-select, #add-session-trainer-name');
            selects.forEach(select => {
                select.innerHTML = '<option value="">Select Trainer</option>';
                this.trainers.forEach(trainer => {
                    select.innerHTML += `<option value="${trainer.id}">${trainer.name}</option>`;
                });
            });
        }

        populateSessionTypeDropdowns() {
            const selects = document.querySelectorAll('#checkin-session-type, #add-client-session-type, #add-session-session-type');
            selects.forEach(select => {
                select.innerHTML = '<option value="">Select Session Type</option>';
                this.sessionTypes.forEach(type => {
                    select.innerHTML += `<option value="${type}">${type}</option>`;
                });
            });
        }
        
        // --- NAVIGATION & UI ---
        navigateTo(pageId) {
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            document.querySelector('main').scrollTop = 0; // Scroll to top
            
            if (pageId.includes('report')) this.populateAll();
            if (pageId === 'client-details-page') {
                document.getElementById('details-client-search').value = '';
                document.getElementById('client-details-content').style.display = 'none';
            }
        }
        
        showAlert(containerId, message, type) {
            const container = document.getElementById(containerId);
            const alertDiv = document.createElement('div');
            alertDiv.className = `alert alert-${type}`;
            alertDiv.textContent = message;
            container.innerHTML = ''; 
            container.appendChild(alertDiv);
            setTimeout(() => {
                if (alertDiv) alertDiv.remove();
            }, 5000);
        }

        showAdminPassword() {
            document.getElementById('admin-password-modal').style.display = 'block';
            document.getElementById('admin-password').value = '';
            document.getElementById('password-error').style.display = 'none';
        }
        // ... (rest of the JavaScript code)
        checkAdminPassword() {
            const passwordInput = document.getElementById('admin-password').value;
            const passwordError = document.getElementById('password-error');

            if (passwordInput === this.adminPassword) {
                document.getElementById('admin-password-modal').style.display = 'none';
                this.navigateTo('admin-panel-page');
            } else {
                passwordError.style.display = 'block';
            }
        }

        // --- CLIENT MANAGEMENT ---
        handleClientCheckIn() {
            const clientName = document.getElementById('checkin-client-name').value.trim();
            const trainerId = document.getElementById('checkin-trainer-name').value;
            const sessionType = document.getElementById('checkin-session-type').value;
            let partnerName = document.getElementById('checkin-partner-name').value.trim();

            if (!clientName || !trainerId || !sessionType) {
                this.showAlert('checkin-alert-container', 'Please fill in all required fields (Client, Trainer, Session Type).', 'danger');
                return;
            }

            const client = this.findClientByName(clientName);
            if (!client) {
                this.showAlert('checkin-alert-container', 'Client not found. Please add the client first.', 'danger');
                return;
            }

            if (sessionType === 'Partner Session' && !partnerName) {
                this.showAlert('checkin-alert-container', 'For Partner Sessions, please provide a Partner Name.', 'danger');
                return;
            }

            let partner = null;
            if (partnerName) {
                partner = this.findClientByName(partnerName);
                if (!partner) {
                    this.showAlert('checkin-alert-container', 'Partner not found. Please add the partner as a client first.', 'danger');
                    return;
                }
            }

            if (client.sessionsLeft <= 0) {
                this.showAlert('checkin-alert-container', `${client.firstName} ${client.lastName} has no sessions left. Please recharge their package.`, 'warning');
                return;
            }

            // Deduct sessions for the main client
            client.sessionsLeft--;
            this.addLogEntry(client.id, `Checked in for a ${sessionType} with ${this.trainers.find(t => t.id === trainerId)?.name || 'N/A'}`);

            // Deduct sessions for partner if applicable
            if (sessionType === 'Partner Session' && partner) {
                if (partner.sessionsLeft <= 0) {
                    this.showAlert('checkin-alert-container', `${partner.firstName} ${partner.lastName} (Partner) has no sessions left. Please recharge their package.`, 'warning');
                    client.sessionsLeft++; // Revert client deduction if partner has no sessions
                    return;
                }
                partner.sessionsLeft--;
                this.addLogEntry(partner.id, `Checked in as partner for a ${sessionType} with ${this.trainers.find(t => t.id === trainerId)?.name || 'N/A'}`);
            }

            // Log the session
            this.sessionsLog.push({
                id: Date.now(),
                clientId: client.id,
                clientName: `${client.firstName} ${client.lastName}`,
                trainerId: trainerId,
                trainerName: this.trainers.find(t => t.id === trainerId)?.name || 'N/A',
                sessionType: sessionType,
                partnerId: partner ? partner.id : null,
                partnerName: partner ? `${partner.firstName} ${partner.lastName}` : null,
                date: new Date().toISOString().split('T')[0],
                time: new Date().toLocaleTimeString('en-GB', { hour: '2-digit', minute: '2-digit' })
            });

            this.saveData();
            this.populateAll(); // Refresh data displays
            this.showAlert('checkin-alert-container', `${client.firstName} ${client.lastName} checked in successfully! Sessions left: ${client.sessionsLeft}`, 'success');
            document.getElementById('checkin-form').reset();
            document.getElementById('checkin-partner-container').style.display = 'none';
        }

        addNewClient() {
            const firstName = document.getElementById('add-client-first-name').value.trim();
            const lastName = document.getElementById('add-client-last-name').value.trim();
            const email = document.getElementById('add-client-email').value.trim();
            const phone = document.getElementById('add-client-phone').value.trim();
            const sessionType = document.getElementById('add-client-session-type').value;
            const sessionAmount = parseInt(document.getElementById('add-client-session-amount').value);

            if (!firstName || !lastName || !sessionType || isNaN(sessionAmount) || sessionAmount <= 0) {
                this.showAlert('add-client-page', 'Please fill in all required client fields and ensure session amount is valid.', 'danger');
                return;
            }

            // Check if client already exists
            if (this.clients.some(c => c.firstName.toLowerCase() === firstName.toLowerCase() && c.lastName.toLowerCase() === lastName.toLowerCase())) {
                this.showAlert('add-client-page', 'A client with this name already exists.', 'warning');
                return;
            }

            const newClient = {
                id: Date.now(),
                firstName,
                lastName,
                email,
                phone,
                sessionType,
                sessionsLeft: sessionAmount,
                notes: '',
                log: []
            };
            this.clients.push(newClient);
            this.addLogEntry(newClient.id, `Initial package: ${sessionAmount} ${sessionType} sessions`);

            // Handle partner addition if session type is 'Partner Session'
            if (sessionType === 'Partner Session') {
                const partnerFirstName = document.getElementById('add-partner-first-name').value.trim();
                const partnerLastName = document.getElementById('add-partner-last-name').value.trim();
                const partnerEmail = document.getElementById('add-partner-email').value.trim();
                const partnerPhone = document.getElementById('add-partner-phone').value.trim();

                if (partnerFirstName && partnerLastName) {
                    // Check if partner already exists as a client
                    if (this.clients.some(c => c.firstName.toLowerCase() === partnerFirstName.toLowerCase() && c.lastName.toLowerCase() === partnerLastName.toLowerCase())) {
                        this.showAlert('add-client-page', 'The specified partner already exists as a client.', 'warning');
                    } else {
                        const newPartner = {
                            id: Date.now() + 1, // Ensure unique ID for partner
                            firstName: partnerFirstName,
                            lastName: partnerLastName,
                            email: partnerEmail,
                            phone: partnerPhone,
                            sessionType: sessionType, // Partner gets the same session type as main client
                            sessionsLeft: sessionAmount,
                            notes: '',
                            log: []
                        };
                        this.clients.push(newPartner);
                        this.addLogEntry(newPartner.id, `Initial package (as partner): ${sessionAmount} ${sessionType} sessions with ${firstName} ${lastName}`);
                        this.showAlert('add-client-page', `Client ${firstName} ${lastName} and partner ${partnerFirstName} ${partnerLastName} added successfully!`, 'success');
                    }
                } else if (partnerFirstName || partnerLastName) {
                    this.showAlert('add-client-page', 'Please fill both first and last names for the partner, or leave both empty.', 'warning');
                    return;
                }
            }

            this.saveData();
            this.populateAll();
            this.showAlert('add-client-page', `Client ${firstName} ${lastName} added successfully!`, 'success');
            document.getElementById('add-client-form').reset();
            document.getElementById('add-partner-container').style.display = 'none';
        }

        populateClientDetails(clientFullName) {
            const client = this.findClientByName(clientFullName);
            const clientDetailsContent = document.getElementById('client-details-content');

            if (client) {
                clientDetailsContent.style.display = 'block';
                document.getElementById('details-client-name').textContent = `${client.firstName} ${client.lastName}`;
                document.getElementById('details-client-email').textContent = client.email || 'N/A';
                document.getElementById('details-client-phone').textContent = client.phone || 'N/A';
                document.getElementById('details-client-session-type').textContent = client.sessionType;
                document.getElementById('details-client-sessions-left').textContent = client.sessionsLeft;
                document.getElementById('details-client-notes').value = client.notes;
                this.currentClient = client; // Store for other functions
                this.populateClientLog();
            } else {
                clientDetailsContent.style.display = 'none';
                this.currentClient = null;
            }
        }

        saveClientNotes() {
            if (this.currentClient) {
                this.currentClient.notes = document.getElementById('details-client-notes').value.trim();
                this.saveData();
                this.showAlert('client-details-page', 'Notes saved successfully!', 'success');
                this.addLogEntry(this.currentClient.id, `Notes updated.`);
            }
        }

        rechargeClientSessions() {
            if (this.currentClient) {
                const rechargeAmount = parseInt(document.getElementById('details-recharge-sessions').value);
                if (!isNaN(rechargeAmount) && rechargeAmount > 0) {
                    this.currentClient.sessionsLeft += rechargeAmount;
                    this.saveData();
                    this.populateClientDetails(`${this.currentClient.firstName} ${this.currentClient.lastName}`);
                    this.showAlert('client-details-page', `${rechargeAmount} sessions added! Total: ${this.currentClient.sessionsLeft}`, 'success');
                    this.addLogEntry(this.currentClient.id, `Recharged ${rechargeAmount} sessions.`);
                    document.getElementById('details-recharge-sessions').value = '';
                } else {
                    this.showAlert('client-details-page', 'Please enter a valid positive number for recharge.', 'danger');
                }
            }
        }

        adjustClientSessions() {
            if (this.currentClient) {
                const adjustAmount = parseInt(document.getElementById('details-adjust-sessions').value);
                if (!isNaN(adjustAmount) && this.currentClient.sessionsLeft + adjustAmount >= 0) {
                    this.currentClient.sessionsLeft += adjustAmount;
                    this.saveData();
                    this.populateClientDetails(`${this.currentClient.firstName} ${this.currentClient.lastName}`);
                    this.showAlert('client-details-page', `Sessions adjusted by ${adjustAmount}. Total: ${this.currentClient.sessionsLeft}`, 'success');
                    this.addLogEntry(this.currentClient.id, `Sessions adjusted by ${adjustAmount}.`);
                    document.getElementById('details-adjust-sessions').value = '';
                } else {
                    this.showAlert('client-details-page', 'Invalid adjustment amount or not enough sessions.', 'danger');
                }
            }
        }

        populateClientLog() {
            if (!this.currentClient) return;

            const logBody = document.getElementById('client-log-body');
            logBody.innerHTML = '';
            const filter = document.getElementById('details-log-filter').value;
            const now = new Date();

            const filteredLog = this.currentClient.log.filter(entry => {
                const entryDate = new Date(entry.date);
                if (filter === '7') {
                    return (now - entryDate) / (1000 * 60 * 60 * 24) <= 7;
                } else if (filter === '30') {
                    return (now - entryDate) / (1000 * 60 * 60 * 24) <= 30;
                }
                return true; // 'all' or no filter
            });

            filteredLog.sort((a, b) => new Date(b.date) - new Date(a.date) || b.timestamp - a.timestamp); // Sort by date then timestamp

            if (filteredLog.length === 0) {
                logBody.innerHTML = '<tr><td colspan="3">No log entries found for this client.</td></tr>';
            } else {
                filteredLog.forEach(entry => {
                    const row = logBody.insertRow();
                    row.insertCell().textContent = entry.date;
                    row.insertCell().textContent = entry.time;
                    row.insertCell().textContent = entry.action;
                });
            }
        }

        deleteClient() {
            if (this.currentClient && confirm(`Are you sure you want to delete ${this.currentClient.firstName} ${this.currentClient.lastName}? This action cannot be undone.`)) {
                this.clients = this.clients.filter(c => c.id !== this.currentClient.id);
                // Also remove their sessions from the log
                this.sessionsLog = this.sessionsLog.filter(s => s.clientId !== this.currentClient.id && s.partnerId !== this.currentClient.id);
                this.saveData();
                this.populateAll();
                this.showAlert('home-page', `${this.currentClient.firstName} ${this.currentClient.lastName} has been deleted.`, 'success');
                this.navigateTo('admin-panel-page'); // Go back to admin panel after deletion
            }
        }

        // --- TRAINER MANAGEMENT ---
        populateTrainerPanel(selectedTrainerId = null) {
            const select = document.getElementById('trainer-panel-select');
            const newTrainerFields = document.getElementById('add-new-trainer-fields');
            const payRatesDiv = document.getElementById('trainer-pay-rates');

            select.innerHTML = '<option value="">-- Add New Trainer --</option>';
            this.trainers.forEach(trainer => {
                const option = document.createElement('option');
                option.value = trainer.id;
                option.textContent = trainer.name;
                select.appendChild(option);
            });

            const currentTrainerId = selectedTrainerId || select.value;
            const selectedTrainer = this.trainers.find(t => t.id == currentTrainerId);

            if (selectedTrainer) {
                newTrainerFields.style.display = 'none';
                document.getElementById('new-trainer-name').value = '';
                document.getElementById('new-trainer-email').value = selectedTrainer.email || '';
                document.getElementById('new-trainer-phone').value = selectedTrainer.phone || '';
            } else {
                newTrainerFields.style.display = 'block';
                document.getElementById('new-trainer-name').value = '';
                document.getElementById('new-trainer-email').value = '';
                document.getElementById('new-trainer-phone').value = '';
            }
            
            // Populate pay rates
            payRatesDiv.innerHTML = '';
            this.sessionTypes.forEach(type => {
                const div = document.createElement('div');
                div.className = 'form-group';
                const trainerPay = selectedTrainer ? (selectedTrainer.payRates ? selectedTrainer.payRates[type] : '') : '';
                div.innerHTML = `
                    <label for="pay-rate-${type.replace(/\s/g, '-')}" style="font-size: 0.9em;">${type} Pay Amount</label>
                    <input type="number" id="pay-rate-${type.replace(/\s/g, '-')}" value="${trainerPay}" step="0.01">
                `;
                payRatesDiv.appendChild(div);
            });
            select.value = currentTrainerId; // Re-select the trainer after populating options
        }

        saveTrainerInfo() {
            const select = document.getElementById('trainer-panel-select');
            const selectedTrainerId = select.value;
            let trainer;

            if (selectedTrainerId) {
                // Editing existing trainer
                trainer = this.trainers.find(t => t.id == selectedTrainerId);
                if (!trainer) {
                    this.showAlert('trainer-panel-page', 'Selected trainer not found.', 'danger');
                    return;
                }
                trainer.name = document.getElementById('new-trainer-name').value.trim() || trainer.name; // Allow name edit even if not "new"
                trainer.email = document.getElementById('new-trainer-email').value.trim();
                trainer.phone = document.getElementById('new-trainer-phone').value.trim();

            } else {
                // Adding new trainer
                const newTrainerName = document.getElementById('new-trainer-name').value.trim();
                const newTrainerEmail = document.getElementById('new-trainer-email').value.trim();
                const newTrainerPhone = document.getElementById('new-trainer-phone').value.trim();

                if (!newTrainerName) {
                    this.showAlert('trainer-panel-page', 'Please enter a name for the new trainer.', 'danger');
                    return;
                }
                if (this.trainers.some(t => t.name.toLowerCase() === newTrainerName.toLowerCase())) {
                    this.showAlert('trainer-panel-page', 'A trainer with this name already exists.', 'warning');
                    return;
                }

                trainer = {
                    id: Date.now(),
                    name: newTrainerName,
                    email: newTrainerEmail,
                    phone: newTrainerPhone,
                    payRates: {}
                };
                this.trainers.push(trainer);
            }

            // Save pay rates
            this.sessionTypes.forEach(type => {
                const input = document.getElementById(`pay-rate-${type.replace(/\s/g, '-')}`);
                if (input) {
                    trainer.payRates[type] = parseFloat(input.value) || 0;
                }
            });

            this.saveData();
            this.populateAll();
            this.showAlert('trainer-panel-page', 'Trainer information saved successfully!', 'success');
            document.getElementById('trainer-panel-form').reset();
            this.populateTrainerPanel(trainer.id); // Re-populate to show updated info
        }

        // --- REPORTS ---
        generateTrainerReport() {
            const trainerId = document.getElementById('report-trainer-select').value;
            const filter = document.getElementById('report-trainer-filter').value;
            const startDateInput = document.getElementById('trainer-start-date').value;
            const endDateInput = document.getElementById('trainer-end-date').value;
            const reportBody = document.getElementById('trainer-report-body');
            const totalPayElement = document.getElementById('trainer-report-total');
            reportBody.innerHTML = '';
            totalPayElement.textContent = '';

            if (!trainerId) {
                reportBody.innerHTML = '<tr><td colspan="5">Please select a trainer to generate the report.</td></tr>';
                return;
            }

            const selectedTrainer = this.trainers.find(t => t.id == trainerId);
            if (!selectedTrainer) return;

            let filteredSessions = this.sessionsLog.filter(session => session.trainerId == trainerId);

            const now = new Date();
            if (filter === '7') {
                filteredSessions = filteredSessions.filter(session => (now - new Date(session.date)) / (1000 * 60 * 60 * 24) <= 7);
            } else if (filter === '30') {
                filteredSessions = filteredSessions.filter(session => (now - new Date(session.date)) / (1000 * 60 * 60 * 24) <= 30);
            } else if (filter === 'custom' && startDateInput && endDateInput) {
                const startDate = new Date(startDateInput);
                const endDate = new Date(endDateInput);
                filteredSessions = filteredSessions.filter(session => {
                    const sessionDate = new Date(session.date);
                    return sessionDate >= startDate && sessionDate <= endDate;
                });
            }

            let totalPay = 0;
            if (filteredSessions.length === 0) {
                reportBody.innerHTML = '<tr><td colspan="5">No sessions found for this trainer in the selected time frame.</td></tr>';
            } else {
                filteredSessions.sort((a, b) => new Date(a.date) - new Date(b.date) || a.time.localeCompare(b.time));
                filteredSessions.forEach(session => {
                    const payAmount = selectedTrainer.payRates[session.sessionType] || 0;
                    totalPay += payAmount;
                    const row = reportBody.insertRow();
                    row.insertCell().textContent = session.clientName + (session.partnerName ? ` & ${session.partnerName}` : '');
                    row.insertCell().textContent = session.date;
                    row.insertCell().textContent = session.time;
                    row.insertCell().textContent = session.sessionType;
                    row.insertCell().textContent = payAmount.toFixed(2);
                });
            }
            totalPayElement.textContent = totalPay.toFixed(2);
        }

        generateSessionReport() {
            const filter = document.getElementById('report-session-filter').value;
            const startDateInput = document.getElementById('session-start-date').value;
            const endDateInput = document.getElementById('session-end-date').value;
            const reportBody = document.getElementById('session-report-body');
            reportBody.innerHTML = '';

            let filteredSessions = [...this.sessionsLog]; // Create a copy

            const now = new Date();
            if (filter === '7') {
                filteredSessions = filteredSessions.filter(session => (now - new Date(session.date)) / (1000 * 60 * 60 * 24) <= 7);
            } else if (filter === '30') {
                filteredSessions = filteredSessions.filter(session => (now - new Date(session.date)) / (1000 * 60 * 60 * 24) <= 30);
            } else if (filter === 'custom' && startDateInput && endDateInput) {
                const startDate = new Date(startDateInput);
                const endDate = new Date(endDateInput);
                filteredSessions = filteredSessions.filter(session => {
                    const sessionDate = new Date(session.date);
                    return sessionDate >= startDate && sessionDate <= endDate;
                });
            }

            if (filteredSessions.length === 0) {
                reportBody.innerHTML = '<tr><td colspan="6">No sessions found for the selected time frame.</td></tr>';
            } else {
                filteredSessions.sort((a, b) => new Date(a.date) - new Date(b.date) || a.time.localeCompare(b.time));
                filteredSessions.forEach(session => {
                    const row = reportBody.insertRow();
                    row.insertCell().textContent = session.trainerName;
                    row.insertCell().textContent = session.clientName + (session.partnerName ? ` & ${session.partnerName}` : '');
                    row.insertCell().textContent = session.date;
                    row.insertCell().textContent = session.time;
                    row.insertCell().textContent = session.sessionType;

                    const actionCell = row.insertCell();
                    const deleteBtn = document.createElement('button');
                    deleteBtn.textContent = 'Delete';
                    deleteBtn.className = 'btn btn-danger';
                    deleteBtn.style.width = 'auto';
                    deleteBtn.style.padding = '5px 10px';
                    deleteBtn.onclick = () => this.deleteSession(session.id);
                    actionCell.appendChild(deleteBtn);
                });
            }
        }
        
        addSessionManually() {
            const clientName = document.getElementById('add-session-client-name').value.trim();
            const trainerId = document.getElementById('add-session-trainer-name').value;
            const sessionType = document.getElementById('add-session-session-type').value;
            let partnerName = document.getElementById('add-session-partner-name').value.trim();
            const date = document.getElementById('add-session-date').value;
            const time = document.getElementById('add-session-time').value;

            if (!clientName || !trainerId || !sessionType || !date || !time) {
                this.showAlert('add-session-page', 'Please fill in all required fields.', 'danger');
                return;
            }

            const client = this.findClientByName(clientName);
            if (!client) {
                this.showAlert('add-session-page', 'Client not found. Please add the client first.', 'danger');
                return;
            }

            let partner = null;
            if (sessionType === 'Partner Session' && !partnerName) {
                this.showAlert('add-session-page', 'For Partner Sessions, please provide a Partner Name.', 'danger');
                return;
            } else if (partnerName) {
                partner = this.findClientByName(partnerName);
                if (!partner) {
                    this.showAlert('add-session-page', 'Partner not found. Please add the partner as a client first.', 'danger');
                    return;
                }
            }

            // Deduct sessions for the main client (if not 'Drop in Partner')
            if (client.sessionType !== 'Drop in Partner') {
                if (client.sessionsLeft <= 0) {
                    this.showAlert('add-session-page', `${client.firstName} ${client.lastName} has no sessions left. Manual addition skipped for this client.`, 'warning');
                    return;
                }
                client.sessionsLeft--;
                this.addLogEntry(client.id, `Manual session added: ${sessionType} with ${this.trainers.find(t => t.id === trainerId)?.name || 'N/A'} on ${date} ${time}`);
            }

            // Deduct sessions for partner if applicable and not 'Drop in Partner'
            if (sessionType === 'Partner Session' && partner && partner.sessionType !== 'Drop in Partner') {
                if (partner.sessionsLeft <= 0) {
                    this.showAlert('add-session-page', `${partner.firstName} ${partner.lastName} (Partner) has no sessions left. Manual addition skipped for partner.`, 'warning');
                    if (client.sessionType !== 'Drop in Partner') client.sessionsLeft++; // Revert client deduction
                    return;
                }
                partner.sessionsLeft--;
                this.addLogEntry(partner.id, `Manual session added (as partner): ${sessionType} with ${this.trainers.find(t => t.id === trainerId)?.name || 'N/A'} on ${date} ${time}`);
            }

            // Log the session
            this.sessionsLog.push({
                id: Date.now(),
                clientId: client.id,
                clientName: `${client.firstName} ${client.lastName}`,
                trainerId: trainerId,
                trainerName: this.trainers.find(t => t.id === trainerId)?.name || 'N/A',
                sessionType: sessionType,
                partnerId: partner ? partner.id : null,
                partnerName: partner ? `${partner.firstName} ${partner.lastName}` : null,
                date: date,
                time: time
            });

            this.saveData();
            this.populateAll(); // Refresh data displays
            this.showAlert('add-session-page', 'Session added manually!', 'success');
            document.getElementById('add-session-form').reset();
            document.getElementById('add-session-partner-container').style.display = 'none';
            this.navigateTo('session-report-page');
        }

        deleteSession(sessionId) {
            if (confirm('Are you sure you want to delete this session? This will also re-add sessions to clients.')) {
                const sessionIndex = this.sessionsLog.findIndex(s => s.id === sessionId);
                if (sessionIndex > -1) {
                    const deletedSession = this.sessionsLog[sessionIndex];

                    // Re-add session to main client if not 'Drop in Partner'
                    const client = this.clients.find(c => c.id === deletedSession.clientId);
                    if (client && client.sessionType !== 'Drop in Partner') {
                        client.sessionsLeft++;
                        this.addLogEntry(client.id, `Session manually deleted: re-added 1 session. Old type: ${deletedSession.sessionType}`);
                    }

                    // Re-add session to partner if applicable and not 'Drop in Partner'
                    if (deletedSession.partnerId) {
                        const partner = this.clients.find(c => c.id === deletedSession.partnerId);
                        if (partner && partner.sessionType !== 'Drop in Partner') {
                            partner.sessionsLeft++;
                            this.addLogEntry(partner.id, `Partner session manually deleted: re-added 1 session. Old type: ${deletedSession.sessionType}`);
                        }
                    }

                    this.sessionsLog.splice(sessionIndex, 1);
                    this.saveData();
                    this.showAlert('session-report-page', 'Session deleted and client sessions re-added.', 'success');
                    this.generateSessionReport(); // Refresh the report
                }
            }
        }

        // --- UTILITY FUNCTIONS ---
        findClientByName(fullName) {
            const [firstName, ...lastNameParts] = fullName.split(' ');
            const lastName = lastNameParts.join(' ');
            return this.clients.find(c => 
                c.firstName.toLowerCase() === firstName.toLowerCase() && 
                c.lastName.toLowerCase() === lastName.toLowerCase()
            );
        }

        addLogEntry(clientId, action) {
            const client = this.clients.find(c => c.id === clientId);
            if (client) {
                client.log.push({
                    timestamp: Date.now(),
                    date: new Date().toISOString().split('T')[0],
                    time: new Date().toLocaleTimeString('en-GB', { hour: '2-digit', minute: '2-digit' }),
                    action: action
                });
                this.saveData();
            }
        }
    }

    const app = new TrainingStudioApp();
    </script>
</body>
</html>
