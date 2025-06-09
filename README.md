# My-website-
NikText is a fast, offline text editor like MS Word. Write anything, change font style, size, and color. Use Undo, Redo, Clear, and Delete with ease. Works on all devices with a clean, responsive design. Perfect for notes, documents, and more—anytime, without internet.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NikText Pro - Advanced Offline Word Processor</title>
  <style>
    :root {
      --bg-dark: #1e1e2f;
      --bg-light: #f8f9fa;
      --primary: #4361ee;
      --primary-dark: #3a0ca3;
      --secondary: #edf2f4;
      --text-dark: #2b2d42;
      --text-light: #ffffff;
      --toolbar-bg: #ffffff;
      --border-color: #e0e0e0;
      --hover-color: #f0f0f0;
      --active-color: #e0e0e0;
      --success: #4caf50;
      --warning: #ff9800;
      --danger: #f44336;
      --sidebar-width: 250px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
      background-color: var(--bg-light);
      color: var(--text-dark);
      height: 100vh;
      display: flex;
      flex-direction: column;
      line-height: 1.5;
      overflow: hidden;
    }

    header {
      background: linear-gradient(135deg, var(--primary), var(--primary-dark));
      padding: 12px 24px;
      color: var(--text-light);
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
      position: relative;
      z-index: 10;
    }

    header h1 {
      margin: 0;
      font-size: 1.5rem;
      font-weight: 600;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .logo-icon {
      font-size: 1.2em;
    }

    .main-container {
      display: flex;
      flex: 1;
      overflow: hidden;
    }

    .sidebar {
      width: var(--sidebar-width);
      background: var(--toolbar-bg);
      border-right: 1px solid var(--border-color);
      padding: 16px;
      overflow-y: auto;
      transition: transform 0.3s ease;
      box-shadow: 2px 0 5px rgba(0,0,0,0.05);
      z-index: 5;
    }

    .sidebar-collapsed {
      transform: translateX(calc(-1 * var(--sidebar-width)));
    }

    .sidebar-section {
      margin-bottom: 24px;
    }

    .sidebar-section h3 {
      font-size: 14px;
      color: #666;
      margin-bottom: 12px;
      padding-bottom: 6px;
      border-bottom: 1px solid var(--border-color);
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .sidebar-item {
      display: flex;
      align-items: center;
      padding: 8px 12px;
      border-radius: 4px;
      cursor: pointer;
      margin-bottom: 4px;
      font-size: 14px;
    }

    .sidebar-item:hover {
      background: var(--hover-color);
    }

    .sidebar-item.active {
      background: var(--primary);
      color: white;
    }

    .sidebar-item-icon {
      margin-right: 8px;
      font-size: 16px;
    }

    .content-area {
      flex: 1;
      display: flex;
      flex-direction: column;
      overflow: hidden;
    }

    .toolbar {
      background: var(--toolbar-bg);
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      padding: 8px 16px;
      border-bottom: 1px solid var(--border-color);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
      justify-content: flex-start;
      align-items: center;
    }

    .toolbar-section {
      display: flex;
      gap: 6px;
      padding: 0 12px;
      border-right: 1px solid var(--border-color);
      align-items: center;
    }

    .toolbar-section:last-child {
      border-right: none;
    }

    .toolbar-section-title {
      font-size: 12px;
      color: #666;
      margin-right: 8px;
      font-weight: 500;
    }

    .toolbar button,
    .toolbar select {
      padding: 6px 10px;
      border: 1px solid var(--border-color);
      border-radius: 4px;
      background: white;
      cursor: pointer;
      font-size: 13px;
      min-width: 32px;
      height: 32px;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: all 0.15s ease;
    }

    .toolbar button:hover,
    .toolbar select:hover {
      background: var(--hover-color);
    }

    .toolbar button:active {
      background: var(--active-color);
    }

    .toolbar button.active {
      background: var(--primary);
      color: white;
    }

    .toolbar input[type="color"] {
      width: 32px;
      height: 32px;
      border: 1px solid var(--border-color);
      border-radius: 4px;
      cursor: pointer;
      padding: 2px;
      background: white;
    }

    .toolbar select {
      min-width: 100px;
      padding: 6px 8px;
    }

    #editor-container {
      flex: 1;
      display: flex;
      flex-direction: column;
      overflow: hidden;
      margin: 16px;
      border-radius: 6px;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
      border: 1px solid var(--border-color);
      background: white;
      position: relative;
    }

    #editor {
      flex: 1;
      padding: 24px;
      overflow-y: auto;
      outline: none;
      font-size: 16px;
      line-height: 1.6;
    }

    #editor:focus {
      border-color: var(--primary);
    }

    .view-options {
      display: flex;
      padding: 8px 16px;
      background: var(--secondary);
      border-top: 1px solid var(--border-color);
      gap: 12px;
      flex-wrap: wrap;
    }

    .view-options button {
      padding: 6px 12px;
      border: 1px solid var(--border-color);
      border-radius: 4px;
      background: white;
      cursor: pointer;
      font-size: 13px;
      transition: all 0.15s ease;
    }

    .view-options button:hover {
      background: var(--hover-color);
    }

    .view-options button.active {
      background: var(--primary);
      color: white;
      border-color: var(--primary);
    }

    footer {
      background: var(--primary);
      color: white;
      text-align: center;
      padding: 10px;
      font-size: 12px;
      margin-top: auto;
    }

    .bottom-bar {
      display: flex;
      justify-content: space-between;
      padding: 10px 16px;
      background: var(--toolbar-bg);
      border-top: 1px solid var(--border-color);
    }

    .action-buttons {
      display: flex;
      gap: 12px;
    }

    .bottom-bar button {
      padding: 8px 16px;
      border: none;
      border-radius: 4px;
      background: var(--primary);
      color: white;
      cursor: pointer;
      font-size: 13px;
      display: flex;
      align-items: center;
      gap: 6px;
      transition: all 0.15s ease;
    }

    .bottom-bar button.secondary {
      background: #6c757d;
    }

    .bottom-bar button.warning {
      background: var(--warning);
    }

    .bottom-bar button.danger {
      background: var(--danger);
    }

    .bottom-bar button:hover {
      opacity: 0.9;
    }

    .bottom-bar button:active {
      transform: translateY(1px);
    }

    .status-bar {
      padding: 6px 12px;
      background: var(--toolbar-bg);
      border-top: 1px solid var(--border-color);
      font-size: 12px;
      color: #666;
      display: flex;
      justify-content: space-between;
    }

    /* Dark mode styles */
    body.dark-mode {
      --bg-light: #121212;
      --text-dark: #e0e0e0;
      --secondary: #2d2d2d;
      --toolbar-bg: #1e1e1e;
      --border-color: #333;
      --hover-color: #333;
      --active-color: #444;
    }

    body.dark-mode #editor-container {
      background: #1e1e1e;
    }

    body.dark-mode .sidebar {
      background: #1e1e1e;
      border-right-color: #333;
    }

    body.dark-mode .toolbar button,
    body.dark-mode .toolbar select,
    body.dark-mode .view-options button {
      background: #2d2d2d;
      color: #e0e0e0;
      border-color: #444;
    }

    body.dark-mode .toolbar button.active,
    body.dark-mode .view-options button.active,
    body.dark-mode .sidebar-item.active {
      background: var(--primary);
      color: white;
    }

    /* Zoom controls */
    .zoom-controls {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .zoom-controls button {
      width: 28px;
      height: 28px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .zoom-percentage {
      min-width: 40px;
      text-align: center;
    }

    /* Mobile dropdown menu */
    .mobile-menu-btn {
      display: none;
      background: none;
      border: none;
      font-size: 24px;
      cursor: pointer;
      color: var(--text-light);
    }

    .mobile-menu {
      display: none;
      position: absolute;
      top: 60px;
      right: 20px;
      background: var(--toolbar-bg);
      border: 1px solid var(--border-color);
      border-radius: 6px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      z-index: 1000;
      padding: 10px;
      width: 200px;
    }

    .mobile-menu button {
      width: 100%;
      padding: 8px 12px;
      text-align: left;
      background: none;
      border: none;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .mobile-menu button:hover {
      background: var(--hover-color);
    }

    /* View mode styles */
    #preview {
      display: none;
      padding: 24px;
      overflow-y: auto;
      flex: 1;
    }

    .fullscreen {
      position: fixed !important;
      top: 0 !important;
      left: 0 !important;
      right: 0 !important;
      bottom: 0 !important;
      width: 100% !important;
      height: 100% !important;
      margin: 0 !important;
      border-radius: 0 !important;
      z-index: 9999 !important;
    }

    .fullscreen-btn {
      position: absolute;
      top: 10px;
      right: 10px;
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 4px;
      padding: 6px 10px;
      cursor: pointer;
      z-index: 10000;
    }

    /* Code block styling */
    pre {
      background: #f5f5f5;
      padding: 12px;
      border-radius: 4px;
      overflow-x: auto;
      font-family: 'Courier New', monospace;
    }

    code {
      font-family: 'Courier New', monospace;
      background: #f5f5f5;
      padding: 2px 4px;
      border-radius: 2px;
    }

    body.dark-mode pre,
    body.dark-mode code {
      background: #2d2d2d;
      color: #f8f8f2;
    }

    /* Document templates */
    .template-preview {
      border: 1px solid var(--border-color);
      border-radius: 4px;
      padding: 10px;
      margin-bottom: 10px;
      cursor: pointer;
      transition: all 0.2s;
    }

    .template-preview:hover {
      border-color: var(--primary);
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .template-preview h4 {
      margin-bottom: 6px;
      color: var(--primary);
    }

    .template-preview p {
      font-size: 12px;
      color: #666;
    }

    body.dark-mode .template-preview p {
      color: #aaa;
    }

    /* Document history */
    .history-item {
      padding: 8px;
      border-bottom: 1px solid var(--border-color);
      cursor: pointer;
      font-size: 13px;
    }

    .history-item:hover {
      background: var(--hover-color);
    }

    .history-item-time {
      font-size: 11px;
      color: #666;
    }

    body.dark-mode .history-item-time {
      color: #aaa;
    }

    /* Focus mode */
    .focus-mode {
      max-width: 800px;
      margin: 0 auto;
      padding: 40px 20px;
      line-height: 1.8;
      font-size: 18px;
    }

    /* Typewriter mode */
    .typewriter-mode {
      background: #f5f5f5;
      padding: 40px;
      max-width: 800px;
      margin: 0 auto;
      border-left: 6px solid var(--primary);
    }

    body.dark-mode .typewriter-mode {
      background: #2d2d2d;
    }

    /* Markdown shortcuts panel */
    .markdown-panel {
      background: #f8f9fa;
      padding: 10px;
      border-radius: 4px;
      margin-top: 10px;
      font-size: 13px;
    }

    body.dark-mode .markdown-panel {
      background: #2d2d2d;
    }

    .markdown-panel code {
      background: rgba(0,0,0,0.1);
      padding: 2px 4px;
      border-radius: 3px;
      font-family: monospace;
    }

    body.dark-mode .markdown-panel code {
      background: rgba(255,255,255,0.1);
    }

    /* Responsive styles */
    @media (max-width: 1024px) {
      .sidebar {
        position: absolute;
        left: 0;
        top: 0;
        bottom: 0;
        z-index: 20;
        background: var(--toolbar-bg);
        box-shadow: 2px 0 10px rgba(0,0,0,0.1);
      }
      
      .sidebar-collapsed {
        transform: translateX(-100%);
      }
      
      .content-area {
        margin-left: 0;
      }
    }

    @media (max-width: 768px) {
      header h1 {
        font-size: 1.2rem;
      }
      
      .toolbar {
        padding: 8px;
        gap: 4px;
        overflow-x: auto;
        flex-wrap: nowrap;
      }
      
      .toolbar-section {
        padding: 0 8px;
        flex-shrink: 0;
      }
      
      #editor {
        padding: 16px;
      }

      #editor-container {
        margin: 8px;
      }

      .toolbar-section-title {
        display: none;
      }

      .bottom-bar {
        flex-direction: column;
        gap: 8px;
      }

      .action-buttons {
        justify-content: space-between;
        width: 100%;
      }

      .bottom-bar button {
        flex: 1;
        padding: 8px;
      }

      .mobile-menu-btn {
        display: block;
      }

      .desktop-only {
        display: none;
      }

      .view-options {
        gap: 6px;
        padding: 8px;
      }

      .view-options button {
        padding: 6px 8px;
        font-size: 12px;
      }

      .zoom-controls {
        margin-left: auto;
      }
    }

    @media (max-width: 480px) {
      .view-options button span {
        display: none;
      }
      
      .view-options button {
        min-width: 36px;
        justify-content: center;
      }
      
      .status-bar {
        font-size: 11px;
        flex-wrap: wrap;
        gap: 8px;
        justify-content: center;
      }
      
      .sidebar {
        width: 280px;
      }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeOut {
      from { opacity: 1; transform: translateY(0); }
      to { opacity: 0; transform: translateY(10px); }
    }
    
    /* Floating action button */
    .fab {
      position: fixed;
      bottom: 30px;
      right: 30px;
      width: 56px;
      height: 56px;
      border-radius: 50%;
      background: var(--primary);
      color: white;
      border: none;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      z-index: 100;
      transition: all 0.3s;
    }
    
    .fab:hover {
      transform: scale(1.1);
      box-shadow: 0 6px 16px rgba(0,0,0,0.3);
    }
    
    .fab-options {
      position: absolute;
      bottom: 70px;
      right: 0;
      background: var(--toolbar-bg);
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      padding: 8px;
      display: none;
      flex-direction: column;
      gap: 8px;
      min-width: 200px;
    }
    
    .fab-options.show {
      display: flex;
      animation: fadeIn 0.3s;
    }
    
    .fab-option {
      padding: 10px 16px;
      border-radius: 4px;
      background: var(--toolbar-bg);
      border: none;
      text-align: left;
      display: flex;
      align-items: center;
      gap: 10px;
      cursor: pointer;
      font-size: 14px;
    }
    
    .fab-option:hover {
      background: var(--hover-color);
    }
    
    /* Speech to text indicator */
    .recording-indicator {
      position: fixed;
      bottom: 30px;
      left: 30px;
      background: var(--danger);
      color: white;
      padding: 10px 16px;
      border-radius: 50px;
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 14px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      z-index: 100;
      animation: pulse 1.5s infinite;
    }
    
    @keyframes pulse {
      0% { opacity: 1; }
      50% { opacity: 0.7; }
      100% { opacity: 1; }
    }
    
    /* Document statistics panel */
    .stats-panel {
      background: var(--toolbar-bg);
      padding: 16px;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      margin-top: 16px;
    }
    
    .stats-panel h4 {
      margin-bottom: 12px;
      color: var(--primary);
    }
    
    .stat-item {
      display: flex;
      justify-content: space-between;
      margin-bottom: 8px;
      font-size: 14px;
    }
    
    .stat-value {
      font-weight: 600;
    }
    
    /* Custom scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    
    ::-webkit-scrollbar-track {
      background: #f1f1f1;
    }
    
    ::-webkit-scrollbar-thumb {
      background: #c1c1c1;
      border-radius: 4px;
    }
    
    ::-webkit-scrollbar-thumb:hover {
      background: #a8a8a8;
    }
    
    body.dark-mode ::-webkit-scrollbar-track {
      background: #2d2d2d;
    }
    
    body.dark-mode ::-webkit-scrollbar-thumb {
      background: #555;
    }
    
    body.dark-mode ::-webkit-scrollbar-thumb:hover {
      background: #666;
    }
  </style>
</head>
<body>
  <header>
    <h1><span class="logo-icon">✍️</span> NikText Pro</h1>
    <small class="desktop-only">Advanced Offline Word Processor</small>
    <button class="mobile-menu-btn" onclick="toggleMobileMenu()">☰</button>
    <div class="mobile-menu" id="mobile-menu">
      <button onclick="toggleSidebar()"><span>📁</span> Documents</button>
      <button onclick="saveText()"><span>💾</span> Save</button>
      <button onclick="newDocument()"><span>📄</span> New</button>
      <button onclick="toggleTheme()"><span>🌓</span> Toggle Theme</button>
      <button onclick="toggleFullscreen()"><span>⛶</span> Fullscreen</button>
      <button onclick="insertCodeBlock()"><span>&lt;/&gt;</span> Code Block</button>
      <button onclick="startSpeechToText()"><span>🎤</span> Voice Typing</button>
      <button onclick="toggleViewMode(isPreviewMode ? 'edit' : 'preview')">
        <span>👁️</span> Toggle View
      </button>
    </div>
  </header>

  <div class="main-container">
    <div class="sidebar" id="sidebar">
      <div class="sidebar-section">
        <h3><span>📂</span> Documents</h3>
        <div class="sidebar-item active" onclick="showPanel('templates')">
          <span class="sidebar-item-icon">📄</span> New Document
        </div>
        <div class="sidebar-item" onclick="showPanel('history')">
          <span class="sidebar-item-icon">🕒</span> Recent
        </div>
        <div class="sidebar-item" onclick="showPanel('saved')">
          <span class="sidebar-item-icon">📁</span> Saved Files
        </div>
      </div>
      
      <div class="sidebar-section">
        <h3><span>✨</span> Features</h3>
        <div class="sidebar-item" onclick="toggleFocusMode()">
          <span class="sidebar-item-icon">🔍</span> Focus Mode
        </div>
        <div class="sidebar-item" onclick="toggleTypewriterMode()">
          <span class="sidebar-item-icon">⌨️</span> Typewriter
        </div>
        <div class="sidebar-item" onclick="showPanel('markdown')">
          <span class="sidebar-item-icon">📝</span> Markdown Help
        </div>
        <div class="sidebar-item" onclick="showDocumentStats()">
          <span class="sidebar-item-icon">📊</span> Document Stats
        </div>
      </div>
      
      <div id="templates-panel" class="sidebar-panel">
        <h3>Choose a Template</h3>
        <div class="template-preview" onclick="loadTemplate('blank')">
          <h4>Blank Document</h4>
          <p>Start with a clean slate</p>
        </div>
        <div class="template-preview" onclick="loadTemplate('business-letter')">
          <h4>Business Letter</h4>
          <p>Professional letter format</p>
        </div>
        <div class="template-preview" onclick="loadTemplate('report')">
          <h4>Report</h4>
          <p>Structured report template</p>
        </div>
        <div class="template-preview" onclick="loadTemplate('meeting-notes')">
          <h4>Meeting Notes</h4>
          <p>Template for meeting minutes</p>
        </div>
        <div class="template-preview" onclick="loadTemplate('blog-post')">
          <h4>Blog Post</h4>
          <p>Structure for online articles</p>
        </div>
      </div>
      
      <div id="history-panel" class="sidebar-panel" style="display:none;">
        <h3>Recent Documents</h3>
        <div class="history-item">
          <div>Document 1</div>
          <div class="history-item-time">Today, 10:30 AM</div>
        </div>
        <div class="history-item">
          <div>Project Proposal</div>
          <div class="history-item-time">Yesterday, 3:45 PM</div>
        </div>
        <div class="history-item">
          <div>Meeting Notes</div>
          <div class="history-item-time">Monday, 9:15 AM</div>
        </div>
      </div>
      
      <div id="markdown-panel" class="sidebar-panel" style="display:none;">
        <h3>Markdown Shortcuts</h3>
        <div class="markdown-panel">
          <p><code># Heading 1</code></p>
          <p><code>## Heading 2</code></p>
          <p><code>**bold**</code> or <code>__bold__</code></p>
          <p><code>*italic*</code> or <code>_italic_</code></p>
          <p><code>- List item</code></p>
          <p><code>1. Numbered item</code></p>
          <p><code>[Link](url)</code></p>
          <p><code>![Image](url)</code></p>
          <p><code>`code`</code></p>
          <p><code>```code block```</code></p>
        </div>
      </div>
      
      <div id="stats-panel" class="sidebar-panel" style="display:none;">
        <h3>Document Statistics</h3>
        <div class="stats-panel">
          <div class="stat-item">
            <span>Words:</span>
            <span class="stat-value" id="stat-words">0</span>
          </div>
          <div class="stat-item">
            <span>Characters:</span>
            <span class="stat-value" id="stat-chars">0</span>
          </div>
          <div class="stat-item">
            <span>Paragraphs:</span>
            <span class="stat-value" id="stat-paragraphs">0</span>
          </div>
          <div class="stat-item">
            <span>Reading Time:</span>
            <span class="stat-value" id="stat-reading-time">0 min</span>
          </div>
          <div class="stat-item">
            <span>Created:</span>
            <span class="stat-value" id="stat-created">Just now</span>
          </div>
          <div class="stat-item">
            <span>Last Modified:</span>
            <span class="stat-value" id="stat-modified">Just now</span>
          </div>
        </div>
      </div>
    </div>
    
    <div class="content-area">
      <div class="toolbar">
        <div class="toolbar-section">
          <span class="toolbar-section-title desktop-only">File</span>
          <button onclick="toggleSidebar()" title="Documents (Ctrl+D)">📁<span class="desktop-only"> Documents</span></button>
          <button onclick="saveText()" title="Save (Ctrl+S)">💾<span class="desktop-only"> Save</span></button>
          <button onclick="newDocument()" title="New (Ctrl+N)">📄<span class="desktop-only"> New</span></button>
        </div>
        
        <div class="toolbar-section">
          <span class="toolbar-section-title desktop-only">Edit</span>
          <button onclick="format('undo')" title="Undo (Ctrl+Z)">↶<span class="desktop-only"> Undo</span></button>
          <button onclick="format('redo')" title="Redo (Ctrl+Y)">↷<span class="desktop-only"> Redo</span></button>
          <button onclick="format('cut')" title="Cut (Ctrl+X)">✂️<span class="desktop-only"> Cut</span></button>
          <button onclick="format('copy')" title="Copy (Ctrl+C)">📋<span class="desktop-only"> Copy</span></button>
          <button onclick="format('paste')" title="Paste (Ctrl+V)">📌<span class="desktop-only"> Paste</span></button>
        </div>
        
        <div class="toolbar-section">
          <span class="toolbar-section-title desktop-only">Format</span>
          <button onclick="toggleFormat('bold')" title="Bold (Ctrl+B)" id="bold-btn"><b>B</b></button>
          <button onclick="toggleFormat('italic')" title="Italic (Ctrl+I)" id="italic-btn"><i>I</i></button>
          <button onclick="toggleFormat('underline')" title="Underline (Ctrl+U)" id="underline-btn"><u>U</u></button>
          <button onclick="toggleFormat('strikeThrough')" title="Strikethrough" id="strike-btn"><s>S</s></button>
        </div>
        
        <div class="toolbar-section">
          <select onchange="format('fontName', this.value)" title="Font Family">
            <option value="Arial">Arial</option>
            <option value="Georgia">Georgia</option>
            <option value="Times New Roman">Times New Roman</option>
            <option value="Courier New">Courier New</option>
            <option value="Verdana">Verdana</option>
            <option value="Segoe UI">Segoe UI</option>
          </select>
          <select onchange="format('fontSize', this.value)" title="Font Size">
            <option value="1">8pt</option>
            <option value="2">10pt</option>
            <option value="3" selected>12pt</option>
            <option value="4">14pt</option>
            <option value="5">18pt</option>
            <option value="6">24pt</option>
            <option value="7">36pt</option>
          </select>
        </div>
        
        <div class="toolbar-section">
          <input type="color" onchange="format('foreColor', this.value)" value="#000000" title="Text Color" />
          <input type="color" onchange="format('hiliteColor', this.value)" value="#ffff00" title="Highlight Color" />
        </div>
        
        <div class="toolbar-section">
          <button onclick="format('justifyLeft')" title="Align Left">⇤<span class="desktop-only"> Left</span></button>
          <button onclick="format('justifyCenter')" title="Align Center">☰<span class="desktop-only"> Center</span></button>
          <button onclick="format('justifyRight')" title="Align Right">⇥<span class="desktop-only"> Right</span></button>
        </div>
        
        <div class="toolbar-section">
          <button onclick="format('insertUnorderedList')" title="Bullet List">•<span class="desktop-only"> List</span></button>
          <button onclick="format('insertOrderedList')" title="Numbered List">1.<span class="desktop-only"> List</span></button>
          <button onclick="insertCodeBlock()" title="Insert Code Block">&lt;/&gt;</button>
          <button onclick="insertTable()" title="Insert Table">🅃</button>
        </div>
        
        <div class="toolbar-section">
          <button onclick="toggleFocusMode()" title="Focus Mode (Ctrl+F)" id="focus-btn">🔍</button>
          <button onclick="toggleTypewriterMode()" title="Typewriter Mode (Ctrl+T)" id="typewriter-btn">⌨️</button>
        </div>
      </div>

      <div id="editor-container">
        <div class="view-options">
          <button onclick="toggleViewMode('edit')" class="active" id="edit-view-btn">
            <span>✏️</span><span class="desktop-only"> Edit Mode</span>
          </button>
          <button onclick="toggleViewMode('preview')" id="preview-view-btn">
            <span>👀</span><span class="desktop-only"> Preview Mode</span>
          </button>
          <button onclick="toggleFullscreen()" id="fullscreen-btn">
            <span>⛶</span><span class="desktop-only"> Fullscreen</span>
          </button>
          <div class="zoom-controls">
            <button onclick="adjustZoom(-10)" title="Zoom Out">🔍-</button>
            <span class="zoom-percentage" id="zoom-percentage">100%</span>
            <button onclick="adjustZoom(10)" title="Zoom In">🔍+</button>
          </div>
        </div>
        
        <div id="editor" contenteditable="true" spellcheck="true">
          <p>Start typing your document here...</p>
        </div>
        
        <div id="preview"></div>
      </div>

      <div class="status-bar">
        <span>Words: <span id="word-count">0</span></span>
        <span>Characters: <span id="char-count">0</span></span>
        <span>Zoom: <span id="zoom-display">100%</span></span>
        <span>Mode: <span id="current-mode">Standard</span></span>
      </div>
    </div>
  </div>

  <div class="bottom-bar">
    <div class="action-buttons">
      <button onclick="toggleSidebar()"><span>📁</span> <span class="desktop-only">Documents</span></button>
      <button onclick="saveText()"><span>💾</span> <span class="desktop-only">Save</span></button>
      <button onclick="newDocument()"><span>📄</span> <span class="desktop-only">New</span></button>
      <button onclick="toggleTheme()"><span>🌓</span> <span class="desktop-only">Theme</span></button>
      <button onclick="toggleFullscreen()"><span>⛶</span> <span class="desktop-only">Fullscreen</span></button>
    </div>
    <button onclick="clearEditor()" class="danger"><span>🗑</span> <span class="desktop-only">Clear Document</span></button>
  </div>

  <footer>
    &copy; 2025 NikText Pro | Advanced Offline Word Processor | <span id="current-date"></span> | <span id="document-status">Ready</span>
  </footer>
  
  <button class="fab" onclick="toggleFabOptions()" id="fab-btn">
    <span>+</span>
  </button>
  
  <div class="fab-options" id="fab-options">
    <button class="fab-option" onclick="insertTable()">
      <span>📊</span> Insert Table
    </button>
    <button class="fab-option" onclick="insertCodeBlock()">
      <span>&lt;/&gt;</span> Insert Code
    </button>
    <button class="fab-option" onclick="insertComment()">
      <span>💬</span> Add Comment
    </button>
    <button class="fab-option" onclick="startSpeechToText()">
      <span>🎤</span> Voice Typing
    </button>
    <button class="fab-option" onclick="showDocumentStats()">
      <span>📊</span> Document Stats
    </button>
  </div>
  
  <div class="recording-indicator" id="recording-indicator" style="display: none;">
    <span>●</span> Recording...
    <button onclick="stopSpeechToText()" style="background: none; border: none; color: white; margin-left: 10px;">Stop</button>
  </div>

  <script>
    let darkMode = false;
    let currentZoom = 100;
    let isPreviewMode = false;
    let isFullscreen = false;
    let isFocusMode = false;
    let isTypewriterMode = false;
    let isSidebarOpen = true;
    let lastSaveTime = new Date();
    let documentCreated = new Date();
    let recognition;
    const editor = document.getElementById('editor');
    const preview = document.getElementById('preview');
    const editorContainer = document.getElementById('editor-container');
    const mobileMenu = document.getElementById('mobile-menu');
    const sidebar = document.getElementById('sidebar');
    const fabOptions = document.getElementById('fab-options');
    const recordingIndicator = document.getElementById('recording-indicator');
    
    // Initialize current date in footer
    document.getElementById('current-date').textContent = new Date().toLocaleDateString();
    updateDocumentStatus('Ready');

    // Formatting functions
    function format(command, value = null) {
      document.execCommand(command, false, value);
      editor.focus();
      updateCounts();
      updateActiveButtons();
    }
    
    // Toggle format and button state
    function toggleFormat(command) {
      document.execCommand(command, false, null);
      editor.focus();
      updateCounts();
      updateActiveButtons();
    }
    
    // Update active formatting buttons
    function updateActiveButtons() {
      const commands = ['bold', 'italic', 'underline', 'strikeThrough'];
      commands.forEach(cmd => {
        const btn = document.getElementById(`${cmd}-btn`);
        if (btn) {
          btn.classList.toggle('active', document.queryCommandState(cmd));
        }
      });
      
      // Update focus and typewriter mode buttons
      document.getElementById('focus-btn').classList.toggle('active', isFocusMode);
      document.getElementById('typewriter-btn').classList.toggle('active', isTypewriterMode);
    }

    // Save functionality
    function saveText() {
      const content = isPreviewMode ? preview.innerHTML : editor.innerHTML;
      const blob = new Blob([content], { type: 'text/html' });
      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = `document-${new Date().toISOString().slice(0,10)}.html`;
      a.click();
      
      lastSaveTime = new Date();
      updateDocumentStatus('Saved');
      showNotification('Document saved successfully', 'success');
      closeMobileMenu();
    }
    
    // New document
    function newDocument() {
      if (editor.innerHTML.trim() === '<p>Start typing your document here...</p>' || 
          confirm("Are you sure you want to create a new document? Unsaved changes will be lost.")) {
        editor.innerHTML = '<p>Start typing your document here...</p>';
        documentCreated = new Date();
        updateCounts();
        updateDocumentStatus('New document');
        showNotification('New document created', 'success');
        closeMobileMenu();
      }
    }

    // Clear editor with confirmation
    function clearEditor() {
      if (confirm("Are you sure you want to clear the entire document?")) {
        editor.innerHTML = '<p><br></p>';
        updateCounts();
        updateDocumentStatus('Cleared');
        showNotification('Document cleared', 'warning');
        closeMobileMenu();
      }
    }

    // Theme toggle
    function toggleTheme() {
      darkMode = !darkMode;
      document.body.classList.toggle('dark-mode', darkMode);
      showNotification(darkMode ? 'Dark mode enabled' : 'Light mode enabled', 'success');
      closeMobileMenu();
    }
    
    // View mode toggle
    function toggleViewMode(mode) {
      isPreviewMode = mode === 'preview';
      if (isPreviewMode) {
        preview.innerHTML = editor.innerHTML;
        document.getElementById('preview-view-btn').classList.add('active');
        document.getElementById('edit-view-btn').classList.remove('active');
        editor.style.display = 'none';
        preview.style.display = 'block';
      } else {
        document.getElementById('edit-view-btn').classList.add('active');
        document.getElementById('preview-view-btn').classList.remove('active');
        editor.style.display = 'block';
        preview.style.display = 'none';
        editor.focus();
      }
      closeMobileMenu();
    }
    
    // Zoom functionality
    function adjustZoom(amount) {
      currentZoom = Math.max(50, Math.min(200, currentZoom + amount));
      editor.style.fontSize = `${currentZoom}%`;
      preview.style.fontSize = `${currentZoom}%`;
      document.getElementById('zoom-percentage').textContent = `${currentZoom}%`;
      document.getElementById('zoom-display').textContent = `${currentZoom}%`;
    }

    // Fullscreen toggle
    function toggleFullscreen() {
      if (!isFullscreen) {
        editorContainer.classList.add('fullscreen');
        document.getElementById('fullscreen-btn').innerHTML = '<span>✕</span><span class="desktop-only"> Exit Fullscreen</span>';
        isFullscreen = true;
      } else {
        editorContainer.classList.remove('fullscreen');
        document.getElementById('fullscreen-btn').innerHTML = '<span>⛶</span><span class="desktop-only"> Fullscreen</span>';
        isFullscreen = false;
      }
      closeMobileMenu();
    }

    // Insert code block
    function insertCodeBlock() {
      const codeBlock = '<pre><code>// Your code here\nconsole.log("Hello World!");</code></pre>';
      format('insertHTML', codeBlock);
      showNotification('Code block inserted', 'success');
      closeMobileMenu();
      closeFabOptions();
    }
    
    // Insert table
    function insertTable() {
      const tableHTML = `
        <table border="1" style="width:100%; border-collapse: collapse;">
          <tr>
            <th>Header 1</th>
            <th>Header 2</th>
            <th>Header 3</th>
          </tr>
          <tr>
            <td>Data 1</td>
            <td>Data 2</td>
            <td>Data 3</td>
          </tr>
          <tr>
            <td>Data 4</td>
            <td>Data 5</td>
            <td>Data 6</td>
          </tr>
        </table>
      `;
      format('insertHTML', tableHTML);
      showNotification('Table inserted', 'success');
      closeFabOptions();
    }
    
    // Insert comment
    function insertComment() {
      const commentText = prompt("Enter your comment:");
      if (commentText) {
        const commentHTML = `<span style="background: #fff9c4; padding: 2px 4px; border-radius: 3px; border-left: 3px solid #ffd600;" title="${commentText}">💬</span>`;
        format('insertHTML', commentHTML);
        showNotification('Comment added', 'success');
      }
      closeFabOptions();
    }

    // Word and character count
    function updateCounts() {
      const text = editor.innerText || "";
      const words = text.trim() ? text.trim().split(/\s+/).length : 0;
      const chars = text.length;
      const paragraphs = editor.querySelectorAll('p').length;
      
      document.getElementById('word-count').textContent = words;
      document.getElementById('char-count').textContent = chars;
      
      // Update stats panel if visible
      if (document.getElementById('stats-panel').style.display === 'block') {
        document.getElementById('stat-words').textContent = words;
        document.getElementById('stat-chars').textContent = chars;
        document.getElementById('stat-paragraphs').textContent = paragraphs;
        document.getElementById('stat-reading-time').textContent = Math.ceil(words / 200) + ' min';
        document.getElementById('stat-modified').textContent = new Date().toLocaleTimeString();
      }
    }
    
    // Update document status
    function updateDocumentStatus(status) {
      document.getElementById('document-status').textContent = status;
      document.getElementById('stat-created').textContent = documentCreated.toLocaleString();
      document.getElementById('stat-modified').textContent = new Date().toLocaleString();
    }

    // Notification system
    function showNotification(message, type = 'info') {
      const notification = document.createElement('div');
      notification.textContent = message;
      notification.style.position = 'fixed';
      notification.style.bottom = '20px';
      notification.style.right = '20px';
      notification.style.backgroundColor = type === 'success' ? '#4caf50' : 
                                          type === 'warning' ? '#ff9800' : 
                                          type === 'danger' ? '#f44336' :
                                          darkMode ? '#333' : '#4361ee';
      notification.style.color = 'white';
      notification.style.padding = '12px 20px';
      notification.style.borderRadius = '6px';
      notification.style.boxShadow = '0 4px 12px rgba(0,0,0,0.15)';
      notification.style.zIndex = '1000';
      notification.style.animation = 'fadeIn 0.3s';
      notification.style.fontSize = '14px';
      notification.style.fontWeight = '500';
      
      document.body.appendChild(notification);
      
      setTimeout(() => {
        notification.style.animation = 'fadeOut 0.3s';
        setTimeout(() => notification.remove(), 300);
      }, 3000);
    }
    
    // Mobile menu functions
    function toggleMobileMenu() {
      if (mobileMenu.style.display === 'block') {
        closeMobileMenu();
      } else {
        openMobileMenu();
      }
    }
    
    function openMobileMenu() {
      mobileMenu.style.display = 'block';
      mobileMenu.style.animation = 'fadeIn 0.3s';
    }
    
    function closeMobileMenu() {
      mobileMenu.style.animation = 'fadeOut 0.3s';
      setTimeout(() => {
        mobileMenu.style.display = 'none';
      }, 300);
    }
    
    // Close mobile menu when clicking outside
    document.addEventListener('click', (e) => {
      if (!mobileMenu.contains(e.target) && e.target.className !== 'mobile-menu-btn') {
        closeMobileMenu();
      }
    });
    
    // Sidebar functions
    function toggleSidebar() {
      isSidebarOpen = !isSidebarOpen;
      sidebar.classList.toggle('sidebar-collapsed', !isSidebarOpen);
    }
    
    function showPanel(panelId) {
      // Hide all panels
      document.querySelectorAll('.sidebar-panel').forEach(panel => {
        panel.style.display = 'none';
      });
      
      // Show selected panel
      document.getElementById(`${panelId}-panel`).style.display = 'block';
      
      // Update active item
      document.querySelectorAll('.sidebar-item').forEach(item => {
        item.classList.remove('active');
      });
      event.currentTarget.classList.add('active');
    }
    
    // Load template
    function loadTemplate(templateName) {
      let templateContent = '<p>Start typing your document here...</p>';
      
      switch(templateName) {
        case 'business-letter':
          templateContent = `
            <div style="font-family: 'Times New Roman', serif; max-width: 800px; margin: 0 auto;">
              <p style="text-align: right;">Your Address<br>City, State ZIP<br>Date: ${new Date().toLocaleDateString()}</p>
              
              <p style="margin-top: 40px;">Recipient's Name<br>Company Name<br>Address<br>City, State ZIP</p>
              
              <p style="margin-top: 20px;">Dear Recipient,</p>
              
              <p style="text-indent: 40px; margin-top: 20px;">I am writing to you regarding...</p>
              
              <p style="margin-top: 20px;">Sincerely,</p>
              
              <p style="margin-top: 60px;">Your Name</p>
            </div>
          `;
          break;
          
        case 'report':
          templateContent = `
            <div style="font-family: Arial, sans-serif; max-width: 800px; margin: 0 auto;">
              <h1 style="text-align: center; margin-bottom: 10px;">Report Title</h1>
              <h3 style="text-align: center; color: #666; margin-top: 0;">Prepared by: Your Name</h3>
              
              <h2 style="border-bottom: 1px solid #ddd; padding-bottom: 5px;">1. Introduction</h2>
              <p>Provide background information and objectives of the report.</p>
              
              <h2 style="border-bottom: 1px solid #ddd; padding-bottom: 5px;">2. Methodology</h2>
              <p>Describe how the information was gathered and analyzed.</p>
              
              <h2 style="border-bottom: 1px solid #ddd; padding-bottom: 5px;">3. Findings</h2>
              <p>Present the results of your research or analysis.</p>
              
              <h2 style="border-bottom: 1px solid #ddd; padding-bottom: 5px;">4. Conclusions</h2>
              <p>Summarize the key points and implications.</p>
              
              <h2 style="border-bottom: 1px solid #ddd; padding-bottom: 5px;">5. Recommendations</h2>
              <p>Suggest actions based on your conclusions.</p>
            </div>
          `;
          break;
          
        case 'meeting-notes':
          templateContent = `
            <div style="font-family: 'Segoe UI', sans-serif; max-width: 800px; margin: 0 auto;">
              <h1 style="text-align: center;">Meeting Notes</h1>
              
              <table style="width: 100%; margin-bottom: 20px;">
                <tr>
                  <td><strong>Date:</strong> ${new Date().toLocaleDateString()}</td>
                  <td><strong>Time:</strong> ${new Date().toLocaleTimeString()}</td>
                </tr>
                <tr>
                  <td><strong>Location:</strong> Virtual/Physical</td>
                  <td><strong>Facilitator:</strong> Your Name</td>
                </tr>
              </table>
              
              <h3>Attendees:</h3>
              <ul>
                <li>Person 1</li>
                <li>Person 2</li>
                <li>Person 3</li>
              </ul>
              
              <h3>Agenda Items:</h3>
              <ol>
                <li>
                  <strong>Topic 1</strong>
                  <p>Discussion points...</p>
                  <p><em>Action items:</em> Person responsible - Deadline</p>
                </li>
                <li>
                  <strong>Topic 2</strong>
                  <p>Discussion points...</p>
                  <p><em>Action items:</em> Person responsible - Deadline</p>
                </li>
              </ol>
              
              <h3>Next Meeting:</h3>
              <p>Date: [Next meeting date]</p>
              <p>Agenda items to prepare:</p>
              <ul>
                <li>Item 1</li>
                <li>Item 2</li>
              </ul>
            </div>
          `;
          break;
          
        case 'blog-post':
          templateContent = `
            <div style="font-family: 'Segoe UI', sans-serif; max-width: 800px; margin: 0 auto; line-height: 1.6;">
              <h1 style="margin-bottom: 10px;">Blog Post Title</h1>
              <p style="color: #666; font-style: italic;">By Your Name | ${new Date().toLocaleDateString()}</p>
              
              <p style="font-size: 1.2em;">This is the introduction paragraph that hooks the reader and explains what the post is about.</p>
              
              <h2 style="border-bottom: 1px solid #eee; padding-bottom: 5px;">Section Heading</h2>
              <p>Your content goes here. Break it into paragraphs for readability.</p>
              
              <h2 style="border-bottom: 1px solid #eee; padding-bottom: 5px;">Another Section</h2>
              <p>More content with supporting details.</p>
              
              <blockquote style="border-left: 4px solid #4361ee; padding-left: 15px; margin: 20px 0; color: #555;">
                This is a pull quote or important point you want to highlight.
              </blockquote>
              
              <h2 style="border-bottom: 1px solid #eee; padding-bottom: 5px;">Conclusion</h2>
              <p>Wrap up your post with key takeaways and a call to action.</p>
              
              <div style="background: #f5f5f5; padding: 15px; border-radius: 5px; margin-top: 30px;">
                <h3 style="margin-top: 0;">About the Author</h3>
                <p>Your bio and links to your social profiles or website.</p>
              </div>
            </div>
          `;
          break;
      }
      
      editor.innerHTML = templateContent;
      updateCounts();
      updateDocumentStatus('Template loaded');
      showNotification(`${templateName.replace('-', ' ')} template loaded`, 'success');
      toggleSidebar();
    }
    
    // Focus mode
    function toggleFocusMode() {
      isFocusMode = !isFocusMode;
      
      if (isFocusMode) {
        editor.classList.add('focus-mode');
        document.getElementById('current-mode').textContent = 'Focus';
        showNotification('Focus mode enabled - minimal interface for distraction-free writing', 'success');
      } else {
        editor.classList.remove('focus-mode');
        document.getElementById('current-mode').textContent = 'Standard';
        showNotification('Focus mode disabled', 'info');
      }
      
      updateActiveButtons();
    }
    
    // Typewriter mode
    function toggleTypewriterMode() {
      isTypewriterMode = !isTypewriterMode;
      
      if (isTypewriterMode) {
        editor.classList.add('typewriter-mode');
        document.getElementById('current-mode').textContent = 'Typewriter';
        showNotification('Typewriter mode enabled - classic writing experience', 'success');
      } else {
        editor.classList.remove('typewriter-mode');
        document.getElementById('current-mode').textContent = 'Standard';
        showNotification('Typewriter mode disabled', 'info');
      }
      
      updateActiveButtons();
    }
    
    // Show document statistics
    function showDocumentStats() {
      showPanel('stats');
      updateCounts();
      closeFabOptions();
    }
    
    // Floating action button functions
    function toggleFabOptions() {
      fabOptions.classList.toggle('show');
    }
    
    function closeFabOptions() {
      fabOptions.classList.remove('show');
    }
    
    // Speech to text functionality
    function startSpeechToText() {
      if (!('webkitSpeechRecognition' in window)) {
        showNotification('Speech recognition not supported in your browser', 'danger');
        return;
      }
      
      recognition = new webkitSpeechRecognition();
      recognition.continuous = true;
      recognition.interimResults = true;
      
      recognition.onstart = function() {
        recordingIndicator.style.display = 'flex';
        updateDocumentStatus('Recording...');
        showNotification('Speech recognition started. Speak now.', 'success');
      };
      
      recognition.onerror = function(event) {
        console.error('Speech recognition error', event.error);
        stopSpeechToText();
        showNotification('Speech recognition error: ' + event.error, 'danger');
      };
      
      recognition.onend = function() {
        recordingIndicator.style.display = 'none';
        updateDocumentStatus('Ready');
      };
      
      recognition.onresult = function(event) {
        let interimTranscript = '';
        let finalTranscript = '';
        
        for (let i = event.resultIndex; i < event.results.length; i++) {
          const transcript = event.results[i][0].transcript;
          if (event.results[i].isFinal) {
            finalTranscript += transcript;
          } else {
            interimTranscript += transcript;
          }
        }
        
        if (finalTranscript) {
          format('insertText', finalTranscript);
        }
      };
      
      recognition.start();
      closeFabOptions();
    }
    
    function stopSpeechToText() {
      if (recognition) {
        recognition.stop();
        recordingIndicator.style.display = 'none';
        updateDocumentStatus('Ready');
      }
    }

    // Keyboard shortcuts
    document.addEventListener('keydown', (e) => {
      if (e.ctrlKey || e.metaKey) {
        switch (e.key.toLowerCase()) {
          case 's':
            e.preventDefault();
            saveText();
            break;
          case 'b':
            e.preventDefault();
            toggleFormat('bold');
            break;
          case 'i':
            e.preventDefault();
            toggleFormat('italic');
            break;
          case 'u':
            e.preventDefault();
            toggleFormat('underline');
            break;
          case 'n':
            e.preventDefault();
            newDocument();
            break;
          case 'f':
            e.preventDefault();
            toggleFocusMode();
            break;
          case 't':
            e.preventDefault();
            toggleTypewriterMode();
            break;
          case 'd':
            e.preventDefault();
            toggleSidebar();
            break;
          case 'm':
            e.preventDefault();
            toggleMobileMenu();
            break;
          case 'k':
            e.preventDefault();
            insertCodeBlock();
            break;
          case 'l':
            e.preventDefault();
            insertTable();
            break;
        }
      }
      
      // Escape key closes mobile menu, fullscreen, and fab options
      if (e.key === 'Escape') {
        if (mobileMenu.style.display === 'block') {
          closeMobileMenu();
        }
        if (isFullscreen) {
          toggleFullscreen();
        }
        if (fabOptions.classList.contains('show')) {
          closeFabOptions();
        }
        if (recordingIndicator.style.display === 'flex') {
          stopSpeechToText();
        }
      }
    });

    // Initialize counts and event listeners
    editor.addEventListener('input', () => {
      updateCounts();
      updateActiveButtons();
      updateDocumentStatus('Editing...');
    });
    
    editor.addEventListener('click', updateActiveButtons);
    editor.addEventListener('keyup', updateActiveButtons);
    
    // Handle paste events to clean up formatting
    editor.addEventListener('paste', (e) => {
      e.preventDefault();
      const text = (e.clipboardData || window.clipboardData).getData('text/plain');
      document.execCommand('insertText', false, text);
    });
    
    // Close fab options when clicking outside
    document.addEventListener('click', (e) => {
      if (!fabOptions.contains(e.target) && e.target.id !== 'fab-btn') {
        closeFabOptions();
      }
    });
    
    updateCounts();
    updateActiveButtons();
  </script>
</body>
</html>
