<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Nysa Search Engine</title>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary-color: #3498db;
      --secondary-color: #2c3e50;
      --accent-color: #e74c3c;
      --text-color: #34495e;
      --background-dark: #0A0B0E;
      --border-color: #e0e0e0;
      --background-color: rgb(248, 228, 216);
      --border-radius: 12px;
      --box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      --active-color: #FFD700;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Poppins', sans-serif;
      background-color: var(--background-color);
      color: var(--text-color);
      line-height: 1.6;
      margin-bottom: 60px; /* Space for bottom navigation */
      min-height: 100vh;
      position: relative;
    }

    .container {
      width: 100%;
      max-width: 100%;
      padding: 10px;
      box-sizing: border-box;
    }

    main.container {
      padding-top: 10px;
      padding-bottom: 70px; /* Added padding for bottom nav */
    }

    .header {
    padding: 12px 20px;
    background: #1a1a1f;
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
    z-index: 1000;
    border-bottom: 2px solid #FFD700;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  }
  
  /* Bottom Navigation Styles */
  .bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: #1a1a1f;
    padding: 10px 0;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
    z-index: 1000;
  }

  .nav-container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    max-width: 600px;
    margin: 0 auto;
  }

  .nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-decoration: none;
    color: #fff;
    transition: all 0.3s ease;
    padding: 5px;
    cursor: pointer;
    flex: 1;
    text-align: center;
  }

  .nav-item i {
    font-size: 20px;
    margin-bottom: 4px;
    transition: all 0.3s ease;
  }

  .nav-item span {
    font-size: 12px;
    transition: all 0.3s ease;
  }

  .nav-item.active {
    color: var(--active-color);
  }

  .nav-item.active i {
    transform: translateY(-2px);
  }

  /* Content sections */
  .content {
    padding: 20px;
    display: none;
  }

  .content.active {
    display: block;
  }
  
  .header-content {
    max-width: 1400px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .header-ink {
    font-size: 1.8em;
    font-weight: 900;
    background: linear-gradient(135deg, #FFD700, #FDB931);  /* Royal gold gradient */
    -webkit-background-clip: text;
    color: transparent;
    letter-spacing: 1.2px;
  }

    .connect-wallet {
      padding: 12px 24px;
      background: linear-gradient(135deg, #FFD700, #FDB931);
      border: 1px solid rgba(255, 215, 0, 0.3);
      border-radius: 50px;
      color: #000000;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      font-size: 0.95em;
      letter-spacing: 0.5px;
    }

    .connect-wallet:hover {
      transform: translateY(-1px);
      background: linear-gradient(135deg, #FDB931, #FFD700);
      box-shadow: 0 4px 12px rgba(255, 215, 0, 0.15);
    }

    .connect-wallet:active {
      transform: translateY(0);
      box-shadow: 0 2px 8px rgba(255, 215, 0, 0.1);
    }

    .search-container {
      margin-top: 100px;
      position: relative;
      width: 95%;
      max-width: 800px;
      margin-left: auto;
      margin-right: auto;
      z-index: 100;
    }

    .search-wrapper {
      position: relative;
      width: 100%;
      background: rgba(255, 255, 255, 0.95);
      border-radius: 24px;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
      transition: all 0.3s ease;
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255, 215, 0, 0.2);
    }

    .search-wrapper:focus-within {
      transform: translateY(-2px);
      box-shadow: 0 12px 48px rgba(0, 0, 0, 0.15);
      border-color: rgba(255, 215, 0, 0.4);
    }

    .search-bar {
      width: 100%;
      height: 68px;
      padding: 12px 60px;
      font-size: 18px;
      color: #000000;
      background: transparent;
      border: 2px solid #000000;
      border-radius: 24px;
      transition: all 0.3s ease;
      font-family: 'Poppins', sans-serif;
      letter-spacing: 0.3px;
    }

    .search-bar:focus {
      outline: none;
    }

    .search-bar::placeholder {
      color: #090202;
      font-weight: 400;
    }

    .search-icon {
      position: absolute;
      left: 20px;
      top: 50%;
      transform: translateY(-50%);
      color: hsl(51, 51%, 23%);
      font-size: 24px;
      transition: all 0.3s ease;
    }

    .search-wrapper:focus-within .search-icon {
      color: #FDB931;
      transform: translateY(-50%) scale(1.1);
    }

    .search-suggestions {
      position: absolute;
      top: calc(100% + 5px);
      left: 0;
      right: 0;
      background-color: rgb(255, 255, 255);
      border-radius: 15px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      z-index: 1000;
      max-height: 300px;
      overflow-y: auto;
      display: none;
      border: 1px solid #e0e0e0;
    }

    .search-suggestions.active {
      display: block;
    }

    .suggestion-item {
      padding: 12px 20px;
      cursor: pointer;
      transition: background-color 0.2s ease;
      display: flex;
      align-items: center;
      gap: 10px;
      border-bottom: 1px solid #f0f0f0;
    }

    .suggestion-item:last-child {
      border-bottom: none;
    }

    .suggestion-item:hover {
      background-color: #f8f9fa;
    }

    .suggestion-icon {
      color: #666;
      font-size: 16px;
    }

    .suggestion-text {
      flex-grow: 1;
    }

    .suggestion-category {
      font-size: 12px;
      color: #666;
      background-color: #f0f0f0;
      padding: 2px 8px;
      border-radius: 12px;
    }

    .filter-container {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      overflow-x: auto;
      white-space: nowrap;
      -webkit-overflow-scrolling: touch;
      scrollbar-width: none;
      -ms-overflow-style: none;
      padding: 24px 20px 24px 40px;
      margin-top: 20px;
      gap: 0px;
      width: 100vw;
      position: relative;
      left: 50%;
      right: 50%;
      margin-left: -50vw;
      margin-right: -50vw;
      background-color: var(--background-color);
    }

    .filter-container::-webkit-scrollbar {
      display: none;
    }

    .filter-btn {
      padding: 14px 32px;
      font-family: 'Poppins', sans-serif;
      font-size: 15px;
      font-weight: 500;
      border: 1px solid rgba(0, 0, 0, 0.08);
      border-radius: 50px;
      background-color: #ffffff;
      color: #fff;
      cursor: pointer;
      transition: all 0.2s ease;
      margin-right: 12px;
      flex-shrink: 0;
      text-transform: capitalize;
      letter-spacing: 0.4px;
    }

    .filter-btn:hover {
      background-color: #f8f9fa;
      transform: translateY(-2px);
    }

    .filter-btn.active {
      background: linear-gradient(135deg, #4a90e2, #357abd);
      color: white;
      border: none;
    }

    .filter-btn:focus {
      outline: none;
      ring: 2px solid rgba(74, 144, 226, 0.5);
    }

    .separator-line {
      width: 100vw;
      height: 1px;
      background-color: #343333;
      margin: 20px 0;
      position: relative;
      left: 50%;
      right: 50%;
      margin-left: -50vw;
      margin-right: -50vw;
    }

    .notification-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 1000;
      opacity: 0;
      visibility: hidden;
      transition: opacity 0.3s ease, visibility 0.3s ease;
    }

    .notification-content {
      background-color: white;
      border-radius: 20px;
      padding: 20px;
      max-width: 80%;
      max-height: 80%;
      overflow-y: auto;
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
      transform: scale(0.9);
      transition: transform 0.3s ease;
    }

    .notification-overlay.active {
      opacity: 1;
      visibility: visible;
    }

    .notification-overlay.active .notification-content {
      transform: scale(1);
    }

    .notification-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
      padding-bottom: 10px;
      border-bottom: 1px solid #e0e0e0;
    }

    .notification-title {
      font-size: 18px;
      font-weight: 600;
      color: #333;
    }

    .notification-close {
      font-size: 24px;
      color: #999;
      cursor: pointer;
      transition: color 0.3s ease;
    }

    .notification-close:hover {
      color: #333;
    }

    .notification-body {
      font-size: 14px;
      line-height: 1.6;
      color: #666;
      max-height: 300px;
      overflow-y: auto;
    }

    .listing-form {
      background-color: #fff;
      border-radius: var(--border-radius);
      box-shadow: var(--box-shadow);
      padding: 20px;
      margin-bottom: 20px;
    }

    .listing-form h3 {
      color: var(--secondary-color);
      margin-bottom: 10px;
    }

    .listing-form p {
      margin-bottom: 15px;
    }

    .listing-form form {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      grid-gap: 20px;
    }

    .listing-form input,
    .listing-form textarea {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-family: 'Poppins', sans-serif;
      font-size: 14px;
    }

    .listing-form textarea {
      resize: vertical;
    }

    .listing-form button {
      grid-column: 1 / -1;
      background-color: #4CAF50;
      color: white;
      padding: 12px 20px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-family: 'Poppins', sans-serif;
      font-size: 16px;
    }

    .listing-form button:hover {
      background-color: #45a049;
    }

    @media (max-width: 768px) {
      .filter-container {
        padding: 5px 0 5px 14px;
      }

      .filter-btn {
        padding: 8px 16px;
        font-size: 14px;
        margin-right: 10px;
      }
    }

    @media (min-width: 769px) and (max-width: 1024px) {
      .filter-container {
        padding: 24px 20px 24px 30px;
      }

      .filter-btn {
        padding: 12px 20px;
        font-size: 16px;
        margin-right: 15px;
      }
    }

    @media (min-width: 1025px) {
      .filter-container {
        padding: 24px 20px 24px 40px;
      }

      .filter-btn {
        padding: 20px 40px;
        font-size: 20px;
        margin-right: 20px;
      }
    }
    @media (min-width: 768px) {
    .search-container {
        width: 70%; /* Tablet size */
    }
  
    .filter-btn {
        padding: 12px 24px;
        font-size: 16px;
        margin-right: 15px;
    }
  }
  
  @media (min-width: 1024px) {
    .search-container {
        width: 60%; /* Desktop size */
    }
    
    .search-bar {
        height: 65px;
        font-size: 18px;
    }
    
    .suggestion-item {
        padding: 14px 24px;
    }
  
    .filter-btn {
        padding: 20px 20px;
        font-size: 20px;
        margin-right: 20px;
    }
  }

  @media (max-width: 768px) {
    .heading {
        font-size: 2.5rem;
    }
  
    .subheading {
        font-size: 0.9rem;
    }
  
    .search-bar {
        font-size: 14px;
        padding: 10px 10px 10px 35px;
    }
  
    .search-icon {
        left: 10px;
    }
  
    .filter-container {
        padding: 5px 0;
    }
  
    .filter-btn {
        padding: 8px 16px;
        font-size: 14px;
        margin-right: 10px;
    }

    @media (min-width: 768px) {
    .search-container {
        width: 70%; /* Tablet size */
    }
  
    .filter-btn {
        padding: 12px 24px;
        font-size: 16px;
        margin-right: 15px;
    }
  }
  
  </style>
</head>
<body>
  <main class="container">
    <header class="header">
      <div class="header-content">
        <div class="header-ink">Nysa</div>
        <button class="connect-wallet">
          <i class="fas fa-wallet"></i>
          Connect
        </button>
      </div>
    </header>

    <div class="search-container">
      <i class="fas fa-search search-icon"></i>
      <input type="text" class="search-bar" id="searchBar" placeholder="Search for cryptocurrencies, NFTs, people, or smart contracts...">
      <div class="search-suggestions" id="searchSuggestions"></div>
    </div>

    <div class="filter-container">
      <button class="filter-btn active" data-filter="all" style="background-color: #4CAF50; color: white;">
        <i class="fas fa-globe"></i> All
      </button>
      <button class="filter-btn" data-filter="job" style="background-color: #1E90FF; color: white;">
        <i class="fas fa-user-tie"></i> Job
    </button>
    <button class="filter-btn" data-filter="education" style="background-color: #FFA500; color: white;">
      <i class="fas fa-graduation-cap"></i> Education
    </button>
    <button class="filter-btn" data-filter="crypto" style="background-color: #8A2BE2; color: white;">
      <i class="fas fa-coins"></i> Crypto
    </button>
  </div>

  <div class="separator-line"></div>

  <div class="content-container" id="contentContainer"></div>

  <div class="notification-overlay" id="notificationOverlay">
    <div class="notification-content">
      <div class="notification-header">
        <h2 class="notification-title" id="notificationTitle"></h2>
        <span class="notification-close" id="notificationClose">&times;</span>
      </div>
      <div class="notification-body" id="notificationBody"></div>
    </div>
  </div>
</main>

<!-- Bottom Navigation -->
<nav class="bottom-nav">
  <div class="nav-container">
    <div class="nav-item active" data-page="home">
      <i class="fas fa-home"></i>
      <span>Home</span>
    </div>
    <div class="nav-item" data-page="tournament">
      <i class="fas fa-trophy"></i>
      <span>Tournament</span>
    </div>
    <div class="nav-item" data-page="gallery">
      <i class="fas fa-vr-cardboard"></i>
      <span>Gallery</span>
    </div>
    <div class="nav-item" data-page="location">
      <i class="fas fa-map"></i>
      <span>Location</span>
    </div>
    <div class="nav-item" data-page="listings">
      <i class="fas fa-list"></i>
      <span>Listings</span>
    </div>
  </div>
</nav>

<script>
  const searchBar = document.getElementById('searchBar');
  const searchSuggestions = document.getElementById('searchSuggestions');
  const filterButtons = document.querySelectorAll('.filter-btn');
  const contentContainer = document.getElementById('contentContainer');

  // Sample listing form data
  const listingForms = [
    {
      type: 'job-application',
      title: 'Software Engineer',
      description: 'Join our team as a software engineer',
      formFields: [
        { name: 'name', label: 'Name', type: 'text', placeholder: 'Enter your name' },
        { name: 'email', label: 'Email', type: 'email', placeholder: 'Enter your email' },
        { name: 'resume', label: 'Resume', type: 'file', placeholder: 'Upload your resume' },
        { name: 'portfolio', label: 'Portfolio', type: 'text', placeholder: 'Enter your portfolio link' }
      ],
      category: 'job'
    },
    {
      type: 'education-course',
      title: 'Web Development Bootcamp',
      description: 'Learn to build modern web applications',
      formFields: [
        { name: 'name', label: 'Name', type: 'text', placeholder: 'Enter your name' },
        { name: 'email', label: 'Email', type: 'email', placeholder: 'Enter your email' },
        { name: 'education', label: 'Education', type: 'text', placeholder: 'Enter your education background' },
        { name: 'experience', label: 'Experience', type: 'text', placeholder: 'Enter your relevant experience' }
      ],
      category: 'education'
    },
    {
      type: 'crypto-atm',
      title: 'Install Crypto ATM',
      description: 'Apply to install a crypto ATM in your business',
      formFields: [
        { name: 'business-name', label: 'Business Name', type: 'text', placeholder: 'Enter your business name' },
        { name: 'location', label: 'Location', type: 'text', placeholder: 'Enter your business location' },
        { name: 'monthly-volume', label: 'Monthly Volume', type: 'number', placeholder: 'Enter your expected monthly volume' }
      ],
      category: 'crypto'
    }
  ];

  // Function to render listing forms
  function renderListingForms(filter = 'all') {
    contentContainer.innerHTML = '';

    listingForms.forEach(form => {
      if (filter === 'all' || form.category === filter) {
        const formElement = document.createElement('div');
        formElement.classList.add('listing-form');

        const formTitle = document.createElement('h3');
        formTitle.textContent = form.title;

        const formDescription = document.createElement('p');
        formDescription.textContent = form.description;

        const formFields = document.createElement('form');

        form.formFields.forEach(field => {
          const fieldLabel = document.createElement('label');
          fieldLabel.textContent = field.label;

          const fieldInput = document.createElement('input');
          fieldInput.type = field.type;
          fieldInput.name = field.name;
          fieldInput.placeholder = field.placeholder;

          formFields.appendChild(fieldLabel);
          formFields.appendChild(fieldInput);
        });

        const submitButton = document.createElement('button');
        submitButton.type = 'submit';
        submitButton.textContent = 'Submit';

        formFields.addEventListener('submit', (e) => {
          e.preventDefault();
          handleFormSubmission(form.type, Object.fromEntries(new FormData(e.target)));
        });

        formFields.appendChild(submitButton);

        formElement.appendChild(formTitle);
        formElement.appendChild(formDescription);
        formElement.appendChild(formFields);
        contentContainer.appendChild(formElement);
      }
    });
  }

  // Function to handle form submission
  function handleFormSubmission(formType, formData) {
    console.log(`Submitting ${formType} form:`, formData);
    // Add your custom logic here to handle the form submission
    // For example, you could send the form data to a backend server
    showNotification(`${formType} Form Submitted`, 'Thank you for your submission!');
  }

  // Search functionality
  searchBar.addEventListener('input', function() {
    const searchTerm = this.value.toLowerCase();
    const suggestions = listingForms
      .filter(form => form.title.toLowerCase().includes(searchTerm))
      .map(form => form.title);

    if (suggestions.length > 0 && searchTerm.length > 0) {
      searchSuggestions.innerHTML = suggestions.map(suggestion =>
        `<div class="suggestion-item">${suggestion}</div>`
      ).join('');
      searchSuggestions.style.display = 'block';
    } else {
      searchSuggestions.style.display = 'none';
    }
  });

  // Handle suggestion clicks
  searchSuggestions.addEventListener('click', function(e) {
    if (e.target.classList.contains('suggestion-item')) {
      searchBar.value = e.target.textContent;
      searchSuggestions.style.display = 'none';
      const selectedForm = listingForms.find(form => form.title === e.target.textContent);
      if (selectedForm) {
        showNotification(selectedForm.title, selectedForm.description);
      }
    }
  });

  // Filter functionality
  filterButtons.forEach(button => {
    button.addEventListener('click', function() {
      filterButtons.forEach(btn => btn.classList.remove('active'));
      this.classList.add('active');
      const filter = this.dataset.filter;
      renderListingForms(filter);
    });
  });

  // Close notification when clicking outside the notification content
  document.getElementById('notificationOverlay').addEventListener('click', function(e) {
    if (e.target === this) {
      this.classList.remove('active');
    }
  });

  // Function to show notifications
  function showNotification(title, content) {
    const notificationOverlay = document.getElementById('notificationOverlay');
    const notificationTitle = document.getElementById('notificationTitle');
    const notificationBody = document.getElementById('notificationBody');

    notificationTitle.textContent = title;
    notificationBody.innerHTML = content;

    notificationOverlay.classList.add('active');
  }

  // Initial render of listing forms
  renderListingForms();
</script>
</body>
 
