<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Copy Phrases</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 40px;
            background-color: #f5f5f5;
            max-width: 600px;
            margin: 0 auto;
        }

        input[type="text"] {
            width: 100%;
            padding: 10px;
            font-size: 16px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        
        .phrase-container {
            background: white;
            padding: 20px;
            margin: 15px 0;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .phrase {
            font-size: 18px;
            font-weight: 500;
            flex: 1;
        }
        
        .copy-btn {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.2s;
        }
        
        .copy-btn:hover {
            background-color: #0056b3;
        }
        
        .copy-btn:active {
            background-color: #004085;
        }
        
        .feedback {
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: #28a745;
            color: white;
            padding: 10px 20px;
            border-radius: 4px;
            display: none;
            z-index: 1000;
        }
    </style>
</head>
<body>
    <h2>Copy Phrases</h2>
    
    <input type="text" id="inputText" placeholder="Type something...">

    <div class="phrase-container">
        <span class="phrase" id="goldenPhrase">(Golden)</span>
        <button class="copy-btn" onclick="copyToClipboard(document.getElementById('goldenPhrase').innerText)">Copy</button>
    </div>
    
    <div class="phrase-container">
        <span class="phrase" id="darkMatterPhrase">(Dark Matter)</span>
        <button class="copy-btn" onclick="copyToClipboard(document.getElementById('darkMatterPhrase').innerText)">Copy</button>
    </div>
    
    <div class="feedback" id="feedback">Copied to clipboard!</div>
    
    <script>
        const input = document.getElementById('inputText');
        const goldenPhrase = document.getElementById('goldenPhrase');
        const darkMatterPhrase = document.getElementById('darkMatterPhrase');

        input.addEventListener('input', () => {
            const value = input.value.trim();
            if (value) {
                goldenPhrase.innerText = value + ' (Golden)';
                darkMatterPhrase.innerText = value + ' (Dark Matter)';
            } else {
                goldenPhrase.innerText = '(Golden)';
                darkMatterPhrase.innerText = '(Dark Matter)';
            }
        });

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(function() {
                showFeedback();
            }).catch(function(err) {
                // Fallback for older browsers
                const textArea = document.createElement('textarea');
                textArea.value = text;
                document.body.appendChild(textArea);
                textArea.select();
                document.execCommand('copy');
                document.body.removeChild(textArea);
                showFeedback();
            });
        }
        
        function showFeedback() {
            const feedback = document.getElementById('feedback');
            feedback.style.display = 'block';
            setTimeout(() => {
                feedback.style.display = 'none';
            }, 2000);
        }
    </script>
</body>
</html>
