<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fingt - Image Name Extractor</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            color: #333;
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
        }
        
        /* Menu Bar Styles */
        .menu-bar {
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            padding: 15px 30px;
            margin-bottom: 20px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 2rem;
            font-weight: 700;
            color: #2c3e50;
            display: flex;
            align-items: center;
        }
        
        .logo-icon {
            margin-right: 10px;
            font-size: 2.2rem;
        }
        
        .nav-links {
            display: flex;
            gap: 25px;
        }
        
        .nav-links a {
            text-decoration: none;
            color: #2c3e50;
            font-weight: 500;
            padding: 8px 15px;
            border-radius: 5px;
            transition: all 0.3s;
        }
        
        .nav-links a:hover {
            background-color: #f1f8ff;
            color: #3498db;
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            padding: 30px;
            overflow: hidden;
            flex: 1;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        h1 {
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 2.2rem;
        }
        
        .subtitle {
            color: #7f8c8d;
            font-size: 1.1rem;
        }
        
        .upload-area {
            border: 3px dashed #3498db;
            border-radius: 10px;
            padding: 40px 20px;
            text-align: center;
            margin-bottom: 30px;
            background-color: #f8fafc;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .upload-area:hover {
            background-color: #e8f4fc;
            border-color: #2980b9;
        }
        
        .upload-area.highlight {
            background-color: #d6eaf8;
            border-color: #1abc9c;
        }
        
        .upload-icon {
            font-size: 60px;
            color: #3498db;
            margin-bottom: 15px;
        }
        
        .upload-text {
            font-size: 1.2rem;
            margin-bottom: 15px;
            color: #2c3e50;
        }
        
        .browse-btn {
            display: inline-block;
            background-color: #3498db;
            color: white;
            padding: 10px 25px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
            transition: background-color 0.3s;
        }
        
        .browse-btn:hover {
            background-color: #2980b9;
        }
        
        #file-input {
            display: none;
        }
        
        .file-list {
            margin-top: 30px;
            max-height: 400px;
            overflow-y: auto;
            border-radius: 8px;
            background-color: #f8f9fa;
            padding: 15px;
        }
        
        .file-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 12px 15px;
            background-color: white;
            border-radius: 8px;
            margin-bottom: 10px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
            transition: transform 0.2s;
        }
        
        .file-item:hover {
            transform: translateX(5px);
        }
        
        .file-info {
            display: flex;
            align-items: center;
            flex: 1;
        }
        
        .file-icon {
            font-size: 24px;
            margin-right: 15px;
            color: #3498db;
        }
        
        .file-name {
            font-weight: 500;
            color: #2c3e50;
            word-break: break-all;
            cursor: pointer;
            padding: 5px 10px;
            border-radius: 4px;
            transition: background-color 0.2s;
        }
        
        .file-name:hover {
            background-color: #f1f8ff;
        }
        
        .file-name.copied {
            background-color: #e1f7e1;
            color: #2e7d32;
        }
        
        .copy-btn {
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 4px;
            padding: 6px 12px;
            cursor: pointer;
            font-size: 0.9rem;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .copy-btn:hover {
            background-color: #e9ecef;
        }
        
        .copy-btn.copied {
            background-color: #d4edda;
            border-color: #c3e6cb;
            color: #155724;
        }
        
        .no-files {
            text-align: center;
            padding: 40px;
            color: #7f8c8d;
            font-size: 1.2rem;
        }
        
        .actions {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
        }
        
        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 5px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .btn-primary {
            background-color: #2ecc71;
            color: white;
        }
        
        .btn-primary:hover {
            background-color: #27ae60;
        }
        
        .btn-secondary {
            background-color: #e74c3c;
            color: white;
        }
        
        .btn-secondary:hover {
            background-color: #c0392b;
        }
        
        .btn-copy-all {
            background-color: #3498db;
            color: white;
        }
        
        .btn-copy-all:hover {
            background-color: #2980b9;
        }
        
        .btn:disabled {
            background-color: #bdc3c7;
            cursor: not-allowed;
        }
        
        .notification {
            position: fixed;
            bottom: 80px;
            right: 20px;
            background-color: #2ecc71;
            color: white;
            padding: 15px 25px;
            border-radius: 5px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            transform: translateY(100px);
            opacity: 0;
            transition: all 0.3s ease;
            z-index: 1000;
        }
        
        .notification.show {
            transform: translateY(0);
            opacity: 1;
        }
        
        /* Footer Styles */
        footer {
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 10px;
            padding: 15px 30px;
            margin-top: 20px;
            text-align: center;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            color: #2c3e50;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .upload-area {
                padding: 30px 15px;
            }
            
            .file-item {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .copy-btn {
                align-self: flex-end;
                margin-top: 10px;
            }
            
            .nav-links {
                display: none;
            }
            
            .menu-bar {
                justify-content: center;
            }
        }
        
        @media (max-width: 480px) {
            .container {
                padding: 15px;
            }
            
            .actions {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <!-- Menu Bar -->
    <div class="menu-bar">
        <div class="logo">
            <span class="logo-icon">📸</span>
            Fingt
        </div>
        <div class="nav-links">
            <a href="#">Home</a>
            <a href="#">Features</a>
            <a href="#">About</a>
            <a href="#">Contact</a>
        </div>
    </div>

    <!-- Main Content -->
    <div class="container">
        <header>
            <h1>Image Name Extractor</h1>
            <p class="subtitle">Upload multiple images to extract and copy their file names</p>
        </header>
        
        <div class="upload-area" id="upload-area">
            <div class="upload-icon">📁</div>
            <p class="upload-text">Drag & drop images here or</p>
            <label for="file-input" class="browse-btn">Browse Files</label>
            <input type="file" id="file-input" accept="image/*" multiple>
        </div>
        
        <div class="file-list" id="file-list">
            <div class="no-files">No images uploaded yet</div>
        </div>
        
        <div class="actions">
            <button class="btn btn-copy-all" id="copy-all-btn" disabled>Copy All Names</button>
            <button class="btn btn-primary" id="extract-btn" disabled>Show All Names</button>
            <button class="btn btn-secondary" id="clear-btn" disabled>Clear All</button>
        </div>
    </div>

    <!-- Footer -->
    <footer>
        <p>All rights reserved by Prasanth</p>
    </footer>

    <div class="notification" id="notification">Copied to clipboard!</div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const fileInput = document.getElementById('file-input');
            const uploadArea = document.getElementById('upload-area');
            const fileList = document.getElementById('file-list');
            const extractBtn = document.getElementById('extract-btn');
            const clearBtn = document.getElementById('clear-btn');
            const copyAllBtn = document.getElementById('copy-all-btn');
            const notification = document.getElementById('notification');
            
            let uploadedFiles = [];
            
            // Handle drag and drop events
            ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(eventName => {
                uploadArea.addEventListener(eventName, preventDefaults, false);
            });
            
            function preventDefaults(e) {
                e.preventDefault();
                e.stopPropagation();
            }
            
            ['dragenter', 'dragover'].forEach(eventName => {
                uploadArea.addEventListener(eventName, highlight, false);
            });
            
            ['dragleave', 'drop'].forEach(eventName => {
                uploadArea.addEventListener(eventName, unhighlight, false);
            });
            
            function highlight() {
                uploadArea.classList.add('highlight');
            }
            
            function unhighlight() {
                uploadArea.classList.remove('highlight');
            }
            
            // Handle dropped files
            uploadArea.addEventListener('drop', handleDrop, false);
            
            function handleDrop(e) {
                const dt = e.dataTransfer;
                const files = dt.files;
                handleFiles(files);
            }
            
            // Handle file input change
            fileInput.addEventListener('change', function() {
                handleFiles(this.files);
            });
            
            // Handle browse button click
            uploadArea.addEventListener('click', function() {
                fileInput.click();
            });
            
            // Process uploaded files
            function handleFiles(files) {
                if (files.length === 0) return;
                
                for (let i = 0; i < files.length; i++) {
                    const file = files[i];
                    
                    // Check if file is an image
                    if (!file.type.match('image.*')) {
                        alert('Please upload only image files.');
                        continue;
                    }
                    
                    // Check if file already exists
                    if (uploadedFiles.some(f => f.name === file.name && f.size === file.size)) {
                        alert(`Image "${file.name}" is already uploaded.`);
                        continue;
                    }
                    
                    uploadedFiles.push(file);
                }
                
                updateFileList();
                updateButtons();
            }
            
            // Update the file list display
            function updateFileList() {
                if (uploadedFiles.length === 0) {
                    fileList.innerHTML = '<div class="no-files">No images uploaded yet</div>';
                    return;
                }
                
                fileList.innerHTML = '';
                
                uploadedFiles.forEach((file, index) => {
                    const fileItem = document.createElement('div');
                    fileItem.className = 'file-item';
                    
                    const fileInfo = document.createElement('div');
                    fileInfo.className = 'file-info';
                    
                    const fileIcon = document.createElement('div');
                    fileIcon.className = 'file-icon';
                    fileIcon.textContent = '🖼️';
                    
                    const fileName = document.createElement('div');
                    fileName.className = 'file-name';
                    fileName.textContent = file.name;
                    fileName.title = 'Click to copy';
                    
                    // Add click to copy functionality
                    fileName.addEventListener('click', function() {
                        copyToClipboard(file.name);
                        showNotification(`Copied: ${file.name}`);
                        
                        // Visual feedback
                        fileName.classList.add('copied');
                        setTimeout(() => {
                            fileName.classList.remove('copied');
                        }, 1000);
                    });
                    
                    fileInfo.appendChild(fileIcon);
                    fileInfo.appendChild(fileName);
                    
                    const copyBtn = document.createElement('button');
                    copyBtn.className = 'copy-btn';
                    copyBtn.innerHTML = '📋 Copy';
                    
                    copyBtn.addEventListener('click', function() {
                        copyToClipboard(file.name);
                        showNotification(`Copied: ${file.name}`);
                        
                        // Visual feedback
                        copyBtn.classList.add('copied');
                        copyBtn.innerHTML = '✓ Copied!';
                        setTimeout(() => {
                            copyBtn.classList.remove('copied');
                            copyBtn.innerHTML = '📋 Copy';
                        }, 1000);
                    });
                    
                    fileItem.appendChild(fileInfo);
                    fileItem.appendChild(copyBtn);
                    
                    fileList.appendChild(fileItem);
                });
            }
            
            // Copy text to clipboard
            function copyToClipboard(text) {
                const textarea = document.createElement('textarea');
                textarea.value = text;
                document.body.appendChild(textarea);
                textarea.select();
                document.execCommand('copy');
                document.body.removeChild(textarea);
            }
            
            // Show notification
            function showNotification(message) {
                notification.textContent = message;
                notification.classList.add('show');
                
                setTimeout(() => {
                    notification.classList.remove('show');
                }, 2000);
            }
            
            // Update button states
            function updateButtons() {
                extractBtn.disabled = uploadedFiles.length === 0;
                clearBtn.disabled = uploadedFiles.length === 0;
                copyAllBtn.disabled = uploadedFiles.length === 0;
            }
            
            // Handle extract button click
            extractBtn.addEventListener('click', function() {
                if (uploadedFiles.length === 0) return;
                
                // Create a list of file names
                const fileNames = uploadedFiles.map(file => file.name).join('\n');
                
                // Display the file names
                alert(`Extracted ${uploadedFiles.length} file name(s):\n\n${fileNames}`);
            });
            
            // Handle copy all button click
            copyAllBtn.addEventListener('click', function() {
                if (uploadedFiles.length === 0) return;
                
                // Create a list of file names
                const fileNames = uploadedFiles.map(file => file.name).join('\n');
                
                // Copy to clipboard
                copyToClipboard(fileNames);
                showNotification(`Copied ${uploadedFiles.length} file names to clipboard`);
                
                // Visual feedback
                copyAllBtn.classList.add('copied');
                copyAllBtn.textContent = '✓ All Copied!';
                setTimeout(() => {
                    copyAllBtn.classList.remove('copied');
                    copyAllBtn.textContent = 'Copy All Names';
                }, 1000);
            });
            
            // Handle clear button click
            clearBtn.addEventListener('click', function() {
                uploadedFiles = [];
                updateFileList();
                updateButtons();
                fileInput.value = '';
            });
        });
    </script>
</body>
</html>
