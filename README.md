# web<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Image Generator | Create Stunning Art</title>
    <meta name="description" content="Generate beautiful AI-powered images with simple text prompts">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #6c63ff;
            --secondary-color: #4d44db;
            --dark-color: #2a2a2a;
            --light-color: #f8f9fa;
            --success-color: #28a745;
            --warning-color: #ffc107;
            --danger-color: #dc3545;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f5f5f7;
            color: var(--dark-color);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        header {
            background-color: white;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 20px 0;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 24px;
            font-weight: 700;
            color: var(--primary-color);
            text-decoration: none;
        }
        
        .logo span {
            color: var(--dark-color);
        }
        
        .hero {
            text-align: center;
            padding: 60px 0 40px;
        }
        
        .hero h1 {
            font-size: 2.5rem;
            margin-bottom: 20px;
            color: var(--dark-color);
        }
        
        .hero p {
            font-size: 1.1rem;
            color: #666;
            max-width: 700px;
            margin: 0 auto 30px;
        }
        
        .generator-container {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            padding: 30px;
            margin-bottom: 40px;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
        }
        
        .input-group input, 
        .input-group textarea, 
        .input-group select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-family: inherit;
            font-size: 16px;
            transition: border 0.3s;
        }
        
        .input-group input:focus, 
        .input-group textarea:focus, 
        .input-group select:focus {
            border-color: var(--primary-color);
            outline: none;
        }
        
        .input-group textarea {
            min-height: 100px;
            resize: vertical;
        }
        
        .options-row {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .options-row .input-group {
            flex: 1;
            margin-bottom: 0;
        }
        
        .btn {
            display: inline-block;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 5px;
            padding: 12px 25px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            text-align: center;
        }
        
        .btn:hover {
            background-color: var(--secondary-color);
            transform: translateY(-2px);
        }
        
        .btn:disabled {
            background-color: #ccc;
            cursor: not-allowed;
            transform: none;
        }
        
        .btn-block {
            display: block;
            width: 100%;
        }
        
        .result-container {
            display: none;
            margin-top: 30px;
            text-align: center;
        }
        
        .result-image {
            max-width: 100%;
            border-radius: 8px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }
        
        .loading {
            display: none;
            text-align: center;
            margin: 30px 0;
        }
        
        .spinner {
            width: 40px;
            height: 40px;
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-left-color: var(--primary-color);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto 15px;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .error-message {
            color: var(--danger-color);
            background-color: #f8d7da;
            padding: 15px;
            border-radius: 5px;
            margin: 20px 0;
            display: none;
        }
        
        .actions {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }
        
        .download-btn {
            background-color: var(--success-color);
        }
        
        .download-btn:hover {
            background-color: #218838;
        }
        
        footer {
            text-align: center;
            padding: 30px 0;
            color: #666;
            font-size: 14px;
            border-top: 1px solid #eee;
        }
        
        @media (max-width: 768px) {
            .options-row {
                flex-direction: column;
                gap: 15px;
            }
            
            .hero h1 {
                font-size: 2rem;
            }
            
            .hero p {
                font-size: 1rem;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <nav class="navbar">
                <a href="#" class="logo">AI<span>Art</span>Generator</a>
            </nav>
        </div>
    </header>
    
    <main class="container">
        <section class="hero">
            <h1>Create Stunning AI-Generated Art</h1>
            <p>Transform your ideas into beautiful images with our powerful AI image generator. Just describe what you want to see!</p>
        </section>
        
        <section class="generator-container">
            <div class="error-message" id="errorMessage"></div>
            
            <div class="input-group">
                <label for="prompt">Describe the image you want to generate</label>
                <textarea id="prompt" placeholder="e.g. A futuristic cityscape at sunset with flying cars and neon lights"></textarea>
            </div>
            
            <div class="options-row">
                <div class="input-group">
                    <label for="style">Art Style</label>
                    <select id="style">
                        <option value="digital-art">Digital Art</option>
                        <option value="photographic">Photographic</option>
                        <option value="fantasy-art">Fantasy Art</option>
                        <option value="anime">Anime</option>
                        <option value="3d-model">3D Model</option>
                        <option value="pixel-art">Pixel Art</option>
                    </select>
                </div>
                
                <div class="input-group">
                    <label for="quality">Quality</label>
                    <select id="quality">
                        <option value="standard">Standard</option>
                        <option value="hd">HD</option>
                    </select>
                </div>
            </div>
            
            <button id="generateBtn" class="btn btn-block">Generate Image</button>
            
            <div class="loading" id="loading">
                <div class="spinner"></div>
                <p>Generating your image... This may take a moment.</p>
            </div>
            
            <div class="result-container" id="resultContainer">
                <h2>Your Generated Image</h2>
                <img id="resultImage" class="result-image" src="" alt="Generated AI image">
                <div class="actions">
                    <button id="downloadBtn" class="btn download-btn">
                        <i class="fas fa-download"></i> Download
                    </button>
                    <button id="generateAnotherBtn" class="btn">
                        <i class="fas fa-sync-alt"></i> Generate Another
                    </button>
                </div>
            </div>
        </section>
    </main>
    
    <footer>
        <div class="container">
            <p>© 2023 AI Art Generator. All generated images are created by AI and may be used freely.</p>
        </div>
    </footer>
    
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const generateBtn = document.getElementById('generateBtn');
            const promptInput = document.getElementById('prompt');
            const styleSelect = document.getElementById('style');
            const qualitySelect = document.getElementById('quality');
            const loadingElement = document.getElementById('loading');
            const resultContainer = document.getElementById('resultContainer');
            const resultImage = document.getElementById('resultImage');
            const downloadBtn = document.getElementById('downloadBtn');
            const generateAnotherBtn = document.getElementById('generateAnotherBtn');
            const errorMessage = document.getElementById('errorMessage');
            
            // Using a free AI image generation API (Stable Diffusion via DeepAI)
            const API_KEY = 'quickstart-QUdJIGlzIGNvbWluZy4uLi4K'; // This is a placeholder key
            
            generateBtn.addEventListener('click', generateImage);
            generateAnotherBtn.addEventListener('click', resetGenerator);
            downloadBtn.addEventListener('click', downloadImage);
            
            async function generateImage() {
                const prompt = promptInput.value.trim();
                
                if (!prompt) {
                    showError('Please enter a description for the image you want to generate.');
                    return;
                }
                
                // Show loading state
                generateBtn.disabled = true;
                loadingElement.style.display = 'block';
                hideError();
                
                try {
                    // In a real implementation, you would call an AI image generation API here
                    // For this example, we'll simulate the API call with a timeout
                    
                    // Simulate API delay
                    await new Promise(resolve => setTimeout(resolve, 3000));
                    
                    // For demonstration purposes, we'll use a placeholder service
                    // In a real app, you would replace this with an actual API call
                    const style = styleSelect.value;
                    const quality = qualitySelect.value;
                    
                    // This is a simulation - in reality you would call:
                    // const response = await fetch('https://api.deepai.org/api/stable-diffusion', {
                    //     method: 'POST',
                    //     headers: {
                    //         'Content-Type': 'application/json',
                    //         'api-key': API_KEY
                    //     },
                    //     body: JSON.stringify({
                    //         text: prompt,
                    //         grid_size: '1',
                    //         width: '512',
                    //         height: '512'
                    //     })
                    // });
                    // const data = await response.json();
                    // const imageUrl = data.output_url;
                    
                    // For this demo, we'll use a placeholder image based on the style selected
                    const placeholderImages = {
                        'digital-art': 'https://via.placeholder.com/512/6c63ff/ffffff?text=Digital+Art',
                        'photographic': 'https://via.placeholder.com/512/4d44db/ffffff?text=Photographic',
                        'fantasy-art': 'https://via.placeholder.com/512/28a745/ffffff?text=Fantasy+Art',
                        'anime': 'https://via.placeholder.com/512/dc3545/ffffff?text=Anime',
                        '3d-model': 'https://via.placeholder.com/512/ffc107/000000?text=3D+Model',
                        'pixel-art': 'https://via.placeholder.com/512/2a2a2a/ffffff?text=Pixel+Art'
                    };
                    
                    const imageUrl = placeholderImages[style] || placeholderImages['digital-art'];
                    
                    // Display the result
                    resultImage.src = imageUrl;
                    resultContainer.style.display = 'block';
                    
                    // Scroll to result
                    resultContainer.scrollIntoView({ behavior: 'smooth' });
                    
                } catch (error) {
                    console.error('Error generating image:', error);
                    showError('Failed to generate image. Please try again later.');
                } finally {
                    loadingElement.style.display = 'none';
                    generateBtn.disabled = false;
                }
            }
            
            function resetGenerator() {
                resultContainer.style.display = 'none';
                promptInput.value = '';
                promptInput.focus();
            }
            
            function downloadImage() {
                if (!resultImage.src) return;
                
                const link = document.createElement('a');
                link.href = resultImage.src;
                link.download = `ai-image-${Date.now()}.jpg`;
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            }
            
            function showError(message) {
                errorMessage.textContent = message;
                errorMessage.style.display = 'block';
            }
            
            function hideError() {
                errorMessage.style.display = 'none';
            }
        });
    </script>
</body>
</html>
