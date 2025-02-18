<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Cash Flow - Hard Mode (Vibrant Edition)</title>
  <!-- Import a playful Google Font -->
  <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    /* Reset & Basic Styling */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: 'Nunito', sans-serif;
      background: linear-gradient(135deg, #fdfbfb, #ebedee);
      color: #333;
      -webkit-tap-highlight-color: transparent;
      padding-bottom: 100px; /* So content isn't hidden by footer */
    }
    header {
      background: linear-gradient(135deg, #ff7f50, #ff6347);
      color: #fff;
      padding: 15px;
      text-align: center;
      border-bottom: 3px solid #fff;
    }
    header h1 {
      font-size: 26px;
      margin-bottom: 5px;
      font-weight: 600;
    }
    header .balance,
    header .health-container {
      font-size: 18px;
    }
    /* Health Bar Styles */
    .health-container {
      margin-top: 5px;
    }
    .health-bar {
      width: 80%;
      height: 10px;
      background: #ddd;
      border-radius: 5px;
      margin: 5px auto;
      overflow: hidden;
    }
    #healthBarFill, #healthBarFillFooter {
      height: 10px;
      background: #66bb6a;
      border-radius: 5px;
      width: 100%;
      transition: width 0.5s;
    }
    .container {
      max-width: 480px;
      margin: 20px auto;
      padding: 10px;
    }
    .dashboard {
      display: grid;
      grid-template-columns: 1fr;
      gap: 15px;
    }
    .card {
      background: #fff;
      border-radius: 15px;
      padding: 15px;
      border: 2px solid #fff;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
      animation: fadeIn 0.5s ease-in-out;
    }
    .card h2 {
      font-size: 20px;
      margin-bottom: 10px;
      color: #ff6347;
    }
    .card button, .card select {
      padding: 12px;
      font-size: 18px;
      margin-top: 10px;
      border: 2px solid #fff;
      border-radius: 30px;
      background: #00bcd4;
      color: #fff;
      transition: background 0.3s ease, transform 0.3s ease;
      cursor: pointer;
    }
    .card button:hover, .card select:hover {
      background: #2196f3;
    }
    .financial-overview ul {
      list-style: none;
    }
    .financial-overview li {
      margin-bottom: 8px;
      padding: 5px;
      border-bottom: 1px dashed #ff6347;
    }
    /* Hide sub-section titles */
    .sub-section h3 {
      display: none;
    }
    /* Grid layout for purchase option buttons */
    .options {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
      gap: 10px;
    }
    /* Vibrant buttons with pulsing borders and moderate zoom effect */
    .sub-section .options button {
      padding: 10px;
      font-size: 14px;
      border: 2px solid #fff;
      border-radius: 30px;
      background: #ff9800;
      color: #fff;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      cursor: pointer;
    }
    .sub-section .options button:hover {
      transform: scale(1.8);
      box-shadow: 0 0 15px rgba(255,255,255,0.8);
      animation: pulse 1.5s infinite;
    }
    @keyframes pulse {
      0% { box-shadow: 0 0 0 0 rgba(255,255,255,0.7); }
      70% { box-shadow: 0 0 0 10px rgba(255,255,255,0); }
      100% { box-shadow: 0 0 0 0 rgba(255,255,255,0); }
    }
    /* Additional vibrant styles for Liability and Health Booster buttons */
    .liability-btn {
      background: linear-gradient(45deg, #ff9a9e, #fad0c4);
    }
    .liability-btn:hover {
      background: linear-gradient(45deg, #f5576c, #f093fb);
    }
    .health-btn {
      background: linear-gradient(45deg, #a8e063, #56ab2f);
    }
    .health-btn:hover {
      background: linear-gradient(45deg, #56ab2f, #a8e063);
    }
    /* Owned Items – displayed as expanding bubbles */
    .owned-items-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
      gap: 10px;
    }
    .owned-items-grid .item {
      background: #2196f3;
      color: #fff;
      padding: 10px;
      border-radius: 10px;
      text-align: center;
      transition: transform 0.3s, box-shadow 0.3s;
      cursor: default;
    }
    .owned-items-grid .item:hover {
      transform: scale(1.1);
      box-shadow: 0 0 10px rgba(0,0,0,0.5);
    }
    /* Gambling Panel (Pop-out) */
    #gamblingPanel {
      position: fixed;
      right: 10px;
      bottom: 110px;
      width: 280px;
      background: #fff;
      border: 3px solid #ff9800;
      border-radius: 15px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.3);
      display: none;
      z-index: 200;
      animation: fadeIn 0.5s;
    }
    #gamblingPanel header {
      background: #ff9800;
      color: #fff;
      padding: 8px;
      border-top-left-radius: 15px;
      border-top-right-radius: 15px;
      font-size: 18px;
      position: relative;
    }
    #gamblingPanel header .close-btn {
      position: absolute;
      right: 8px;
      top: 8px;
      background: transparent;
      border: none;
      color: #fff;
      font-size: 20px;
      cursor: pointer;
    }
    #gamblingPanel .panel-content {
      padding: 10px;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    #gamblingPanel .panel-content button {
      padding: 10px;
      font-size: 16px;
      border: 2px solid #fff;
      border-radius: 30px;
      background: #ff9800;
      color: #fff;
      cursor: pointer;
      transition: background 0.3s ease, transform 0.3s ease;
    }
    #gamblingPanel .panel-content button:hover {
      background: #ff5722;
    }
    /* Sticky Footer */
    .sticky-footer {
      position: fixed;
      bottom: 0;
      left: 0;
      width: 100%;
      background: linear-gradient(135deg, #ff7f50, #ff6347);
      color: #fff;
      padding: 10px;
      text-align: center;
      border-top: 3px solid #fff;
      z-index: 100;
    }
    .footer-content {
      display: flex;
      flex-direction: column;
      align-items: center;
      font-size: 16px;
    }
    .footer-content .footer-stats {
      margin-bottom: 5px;
    }
    .footer-health-bar {
      width: 90%;
      height: 8px;
      background: #ddd;
      border-radius: 5px;
      overflow: hidden;
      margin: 0 auto;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.9); }
      to { opacity: 1; transform: scale(1); }
    }
    @keyframes slideDown {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @media (max-width: 480px) {
      .container { padding: 10px; }
      header h1 { font-size: 22px; }
      .card h2 { font-size: 18px; }
    }
  </style>
</head>
<body>
  <header>
    <h1>Cash Flow - Hard Mode</h1>
    <div class="balance">Bank: $<span id="bankBalance">1000.00</span></div>
    <div class="health-container">
      Health: <span id="playerHealthDisplay">100</span>%
      <div class="health-bar">
        <div id="healthBarFill"></div>
      </div>
    </div>
  </header>

  <div class="container">
    <div class="dashboard">
      <!-- Overview Card -->
      <div class="card financial-overview">
        <h2>Overview</h2>
        <ul>
          <li>Job: $<span id="jobIncomeDisplay">0.00</span></li>
          <li>Items: $<span id="itemsFlow">0.00</span></li>
          <li>Total: $<span id="totalFlow">0.00</span></li>
          <li>Net: $<span id="cashFlow">0.00</span></li>
        </ul>
      </div>
      <!-- Job Selection Card -->
      <div class="card job-selection">
        <h2>Job</h2>
        <select id="jobSelect">
          <option value="0" data-income="0" data-min="0">-- Pick Job --</option>
          <option value="1" data-income="100" data-min="0">Clerk ($100/tick)</option>
          <option value="2" data-income="200" data-min="500">Sales ($200/tick) – Min $500</option>
          <option value="3" data-income="300" data-min="1000">Engineer ($300/tick) – Min $1K</option>
          <option value="4" data-income="400" data-min="5000">Manager ($400/tick) – Min $5K</option>
          <option value="5" data-income="500" data-min="10000">Exec ($500/tick) – Min $10K</option>
          <option value="6" data-income="1000" data-min="50000">Director ($1000/tick) – Min $50K</option>
          <option value="7" data-income="2000" data-min="100000">CEO ($2000/tick) – Min $100K</option>
        </select>
        <button onclick="startJob()">Start</button>
      </div>
      <!-- Investments & Purchases Card -->
      <div class="card investment-section">
        <h2>Investments</h2>
        <div class="sub-section">
          <!-- Assets -->
          <div class="options" id="assetsOptions"></div>
        </div>
        <div class="sub-section">
          <!-- Liabilities -->
          <div class="options" id="liabilitiesOptions"></div>
        </div>
        <div class="sub-section">
          <!-- Misc -->
          <div class="options" id="miscOptions"></div>
        </div>
        <div class="sub-section">
          <!-- Health Boosters -->
          <div class="options" id="healthBoostersOptions"></div>
        </div>
      </div>
      <!-- Gambling Card -->
      <div class="card">
        <h2>Gamble</h2>
        <button onclick="openGamblingPanel()">Open Panel</button>
      </div>
      <!-- Owned Items Card -->
      <div class="card owned-items">
        <h2>Owned Items</h2>
        <div class="owned-items-grid" id="ownedItemsGrid"></div>
      </div>
    </div>
  </div>

  <!-- Sticky Footer -->
  <footer class="sticky-footer">
    <div class="footer-content">
      <div class="footer-stats">
        Bank: $<span id="bankBalanceFooter">1000.00</span> | Health: <span id="playerHealthFooter">100</span>%
      </div>
      <div class="footer-health-bar">
        <div id="healthBarFillFooter"></div>
      </div>
    </div>
  </footer>

  <!-- Gambling Panel (Pop-out) -->
  <div id="gamblingPanel">
    <header>
      Gambling Panel
      <button class="close-btn" onclick="closeGamblingPanel()">×</button>
    </header>
    <div class="panel-content">
      <button onclick="gambleFixed()">Try $100</button>
      <button onclick="gambleAllPopup()">All or Nothing</button>
    </div>
  </div>

  <!-- Modal for Confirmations & Gamble Popup -->
  <div id="modal" class="modal">
    <div class="modal-content">
      <span class="close" onclick="closeModal()">×</span>
      <div id="modalBody"></div>
    </div>
  </div>

  <script>
    /* Helper: Shuffle an array in place */
    function shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    }
    
    /**********************
     * Game Variables & Levels
     **********************/
    let bankBalance = 1000;
    let jobIncome = 0; // Income per tick
    let ownedItems = [];
    let gameActive = true;
    let playerHealth = 100; // Health from 0 to 100
    const healthDecay = 1;  // 1 per tick
    const tickInterval = 1500; // 1.5 seconds per tick for quicker income
    const distributionFactor = 5; // Faster income accumulation
    let level = 1;
    // Level goals: Level 1: $1M, Level 2: $10M, Level 3: $100M win
    const levelGoals = [1000000, 10000000, 100000000];

    /**********************
     * Purchase Options Arrays (Extended)
     **********************/
    const assetsOptions = shuffleArray([
      { name: "Small House", cost: 10000, flow: 100 },
      { name: "Duplex", cost: 25000, flow: 300 },
      { name: "Apartment Complex", cost: 50000, flow: 600 },
      { name: "Commercial Building", cost: 100000, flow: 1200 },
      { name: "Shopping Mall", cost: 200000, flow: 2500 },
      { name: "Office Tower", cost: 350000, flow: 4000 },
      { name: "Hotel", cost: 500000, flow: 6000 },
      { name: "Industrial Park", cost: 750000, flow: 9000 },
      { name: "Tech Campus", cost: 1000000, flow: 12000 },
      { name: "City Skyline", cost: 2000000, flow: 25000 },
      // Additional assets
      { name: "Luxury Condo", cost: 1500000, flow: 18000 },
      { name: "Resort", cost: 2500000, flow: 30000 }
    ]);
    const liabilitiesOptions = shuffleArray([
      { name: "Used Car", cost: 5000, flow: 200, healthBoost: 5 },
      { name: "Luxury Car", cost: 20000, flow: 800, healthBoost: 10 },
      { name: "Sports Car", cost: 50000, flow: 1500, healthBoost: 15 },
      { name: "Camper", cost: 15000, flow: 500, healthBoost: 7 },
      { name: "Jet Ski", cost: 25000, flow: 1000, healthBoost: 8 },
      { name: "Yacht", cost: 100000, flow: 5000, healthBoost: 20 },
      { name: "Private Jet", cost: 500000, flow: 20000, healthBoost: 30 },
      { name: "Designer Watch", cost: 10000, flow: 300, healthBoost: 5 },
      { name: "Expensive Art", cost: 30000, flow: 1000, healthBoost: 10 },
      { name: "Luxury Vacation", cost: 15000, flow: 600, healthBoost: 8 },
      // Additional liabilities
      { name: "High-End Car", cost: 75000, flow: 2000, healthBoost: 12 },
      { name: "Mega Yacht", cost: 200000, flow: 8000, healthBoost: 25 }
    ]);
    const miscOptions = shuffleArray([
      { name: "Antique Typewriter", cost: 500, flow: 0 },
      { name: "Rare Comic Book", cost: 1000, flow: 0 },
      { name: "Vintage Vinyl", cost: 1500, flow: 0 },
      { name: "Strange Sculpture", cost: 2000, flow: 0 },
      { name: "Magic Beans", cost: 300, flow: 50 },
      { name: "Mystery Box", cost: 1000, flow: 0 },
      { name: "Celebrity Autograph", cost: 2500, flow: 0 },
      { name: "Old Coin", cost: 800, flow: 20 },
      { name: "Signed Memorabilia", cost: 1200, flow: 0 },
      { name: "Rare Stamps", cost: 600, flow: 0 },
      // Additional misc
      { name: "Vintage Poster", cost: 700, flow: 0 },
      { name: "Classic Car Model", cost: 900, flow: 10 }
    ]);
    const healthBoostersOptions = shuffleArray([
      { name: "Meditation", cost: 50, healthBoost: 3 },
      { name: "Energy Bar", cost: 100, healthBoost: 5 },
      { name: "Fresh Fruit", cost: 150, healthBoost: 7 },
      { name: "Vitamin Drink", cost: 200, healthBoost: 10 },
      { name: "Smoothie", cost: 250, healthBoost: 12 },
      { name: "Healthy Meal", cost: 300, healthBoost: 15 },
      { name: "Supplement", cost: 350, healthBoost: 8 },
      { name: "Tracker", cost: 400, healthBoost: 10 },
      { name: "Yoga Class", cost: 500, healthBoost: 20 },
      { name: "Spa Voucher", cost: 750, healthBoost: 25 },
      // Additional boosters
      { name: "Mindfulness App", cost: 80, healthBoost: 4 },
      { name: "Herbal Tea", cost: 60, healthBoost: 3 }
    ]);

    /**********************
     * Utility Functions
     **********************/
    function getOwnedItemsFlow() {
      return ownedItems.reduce((sum, item) => sum + item.flow, 0);
    }
    function updateOwnedItemsList() {
      const grid = document.getElementById('ownedItemsGrid');
      grid.innerHTML = '';
      ownedItems.forEach(item => {
        const div = document.createElement('div');
        div.classList.add('item');
        div.innerHTML = `<strong>${item.name}</strong><br>${item.type}<br>$${item.cost.toFixed(2)}<br>${item.flow.toFixed(2)}/tick`;
        grid.appendChild(div);
      });
    }
    function updateOverview() {
      document.getElementById('bankBalance').innerText = bankBalance.toFixed(2);
      document.getElementById('jobIncomeDisplay').innerText = jobIncome.toFixed(2);
      const itemsFlow = getOwnedItemsFlow();
      document.getElementById('itemsFlow').innerText = itemsFlow.toFixed(2);
      const totalFlow = jobIncome + itemsFlow;
      document.getElementById('totalFlow').innerText = totalFlow.toFixed(2);
      document.getElementById('cashFlow').innerText = totalFlow.toFixed(2);
      document.getElementById('playerHealthDisplay').innerText = playerHealth.toFixed(0);
      document.getElementById('healthBarFill').style.width = playerHealth + '%';
      document.getElementById('bankBalanceFooter').innerText = bankBalance.toFixed(2);
      document.getElementById('playerHealthFooter').innerText = playerHealth.toFixed(0);
      document.getElementById('healthBarFillFooter').style.width = playerHealth + '%';
    }
    function renderPurchaseOptions() {
      // Randomize order by shuffling the arrays on each render
      shuffleArray(assetsOptions);
      shuffleArray(liabilitiesOptions);
      shuffleArray(miscOptions);
      shuffleArray(healthBoostersOptions);
      
      const assetsDiv = document.getElementById('assetsOptions');
      assetsDiv.innerHTML = '';
      assetsOptions.forEach(opt => {
        const btn = document.createElement('button');
        btn.innerHTML = `${opt.name}<br>$${opt.cost}<br>+${opt.flow}/tick`;
        btn.onclick = () => buyItem('Asset', opt.name, opt.cost, opt.flow);
        assetsDiv.appendChild(btn);
      });
      const liabDiv = document.getElementById('liabilitiesOptions');
      liabDiv.innerHTML = '';
      liabilitiesOptions.forEach(opt => {
        const btn = document.createElement('button');
        btn.classList.add('liability-btn');
        btn.innerHTML = `${opt.name}<br>$${opt.cost}<br>+${opt.flow}/tick<br>Health +${opt.healthBoost}`;
        btn.onclick = () => buyItem('Liability', opt.name, opt.cost, opt.flow, opt.healthBoost);
        liabDiv.appendChild(btn);
      });
      const miscDiv = document.getElementById('miscOptions');
      miscDiv.innerHTML = '';
      miscOptions.forEach(opt => {
        const btn = document.createElement('button');
        btn.innerHTML = `${opt.name}<br>$${opt.cost}<br>${opt.flow >= 0 ? '+'+opt.flow : opt.flow}/tick`;
        btn.onclick = () => buyItem('Misc', opt.name, opt.cost, opt.flow);
        miscDiv.appendChild(btn);
      });
      const healthDiv = document.getElementById('healthBoostersOptions');
      healthDiv.innerHTML = '';
      healthBoostersOptions.forEach(opt => {
        const btn = document.createElement('button');
        btn.classList.add('health-btn');
        btn.innerHTML = `${opt.name}<br>$${opt.cost}<br>Health +${opt.healthBoost}`;
        btn.onclick = () => buyItem('Health Booster', opt.name, opt.cost, 0, opt.healthBoost);
        healthDiv.appendChild(btn);
      });
    }
    function buyItem(type, name, cost, flow, healthBoost = 0) {
      let extraText = '';
      if (type === 'Liability' || type === 'Health Booster') {
        extraText = `<br>Health Boost: +${healthBoost}`;
      }
      openModal(`${type} Purchase`, 
        `Purchase ${name} for $${cost}?${extraText}<br><br>
         <button onclick="confirmPurchase('${type}', '${name}', ${cost}, ${flow}, ${healthBoost})">Confirm</button>`);
    }
    function confirmPurchase(type, name, cost, flow, healthBoost = 0) {
      closeModal();
      if (bankBalance >= cost) {
        bankBalance -= cost;
        ownedItems.push({ name, type, cost, flow });
        updateOwnedItemsList();
        if(type === 'Liability' || type === 'Health Booster'){
          playerHealth = Math.min(100, playerHealth + healthBoost);
        }
        updateOverview();
        alert(`${name} purchased! ${type === 'Asset' || type === 'Misc' ? 'Flow +' : 'Health Boost +'+healthBoost} $${Math.abs(flow)} per tick.`);
      } else {
        alert('Insufficient funds to purchase ' + name);
      }
    }
    function updateJobOptions() {
      const jobSelect = document.getElementById('jobSelect');
      for (let i = 0; i < jobSelect.options.length; i++) {
        const opt = jobSelect.options[i];
        const min = parseFloat(opt.getAttribute('data-min'));
        opt.disabled = bankBalance < min;
      }
    }
    function startJob() {
      const jobSelect = document.getElementById('jobSelect');
      const selectedOption = jobSelect.options[jobSelect.selectedIndex];
      const requiredMin = parseFloat(selectedOption.getAttribute('data-min'));
      const selectedIncome = parseFloat(selectedOption.getAttribute('data-income'));
      if (bankBalance < requiredMin) {
        alert(`Need at least $${requiredMin} for this job.`);
        return;
      }
      if (selectedIncome > 0) {
        jobIncome = selectedIncome;
        alert(`Job started! Earning $${selectedIncome} per tick.`);
      } else {
        alert('Select a valid job.');
      }
      updateOverview();
    }
    function gambleFixed() {
      const bet = 100;
      if (bankBalance >= bet) {
        if (confirm(`Gamble $${bet}?`)) {
          bankBalance -= bet;
          if (Math.random() < 0.5) {
            bankBalance += bet * 2;
            alert('Gamble won!');
          } else {
            alert('Gamble lost.');
          }
          updateOverview();
        }
      } else {
        alert('Not enough funds to gamble.');
      }
    }
    function gambleAllPopup() {
      openModal("All or Nothing Gamble", 
        `Risk it all: $${bankBalance.toFixed(2)}?<br><br>
         <button style="padding:12px; font-size:18px; margin-right:10px; background:#ff9671; border:none; border-radius:30px; color:#fff;" onclick="confirmGambleAll()">All or Nothing</button>
         <button style="padding:12px; font-size:18px; background:#fcb69f; border:none; border-radius:30px; color:#fff;" onclick="closeModal()">Cancel</button>`);
    }
    function confirmGambleAll() {
      closeModal();
      let betAmount = bankBalance;
      bankBalance = 0;
      if (Math.random() < 0.5) {
        bankBalance += betAmount * 2;
        alert('Big win!');
      } else {
        alert('Lost it all.');
      }
      updateOverview();
    }
    function openGamblingPanel() {
      document.getElementById('gamblingPanel').style.display = 'block';
    }
    function closeGamblingPanel() {
      document.getElementById('gamblingPanel').style.display = 'none';
    }
    function checkWinCondition() {
      if (level === 1 && bankBalance >= levelGoals[0]) {
        level = 2;
        alert("Level 1 complete! Welcome to Level 2.");
      } else if (level === 2 && bankBalance >= levelGoals[1]) {
        level = 3;
        alert("Level 2 complete! Welcome to Level 3.");
      } else if (level === 3 && bankBalance >= levelGoals[2]) {
        gameActive = false;
        alert("Congratulations! You've reached $100,000,000 and won the game!");
        clearInterval(gameTick);
      }
    }
    const gameTick = setInterval(() => {
      if (!gameActive) return;
      const tickIncome = jobIncome / distributionFactor;
      const tickItemsFlow = getOwnedItemsFlow() / distributionFactor;
      bankBalance += tickIncome + tickItemsFlow;
      playerHealth -= healthDecay;
      if (playerHealth < 0) playerHealth = 0;
      updateOverview();
      updateJobOptions();
      checkWinCondition();
      if (playerHealth <= 0) {
        alert("You're exhausted! Game Over.");
        gameActive = false;
        clearInterval(gameTick);
      }
    }, tickInterval);
    function openModal(title, content) {
      document.getElementById('modalBody').innerHTML = `<h2>${title}</h2><p>${content}</p>`;
      document.getElementById('modal').style.display = 'block';
    }
    function closeModal() {
      document.getElementById('modal').style.display = 'none';
    }
    renderPurchaseOptions();
    updateOverview();
    updateJobOptions();
  </script>
</body>
</html>
