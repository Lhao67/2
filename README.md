<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie to JSON</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
            color: #333;
        }
        h1 {
            color: #000;
            font-size: 2em;
            margin-bottom: 0.5em;
        }
        textarea {
            width: 100%;
            height: 120px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-family: monospace;
            margin-bottom: 10px;
        }
        button {
            background-color: #0366d6;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
        }
        button:hover {
            background-color: #0356b6;
        }
        pre {
            background: #f6f8fa;
            padding: 16px;
            border-radius: 4px;
            overflow-x: auto;
            border: 1px solid #ddd;
        }
        .container {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Cookie to JSON</h1>
    <textarea id="cookieInput" placeholder="Paste your cookie string here (e.g., name=value; name2=value2)"></textarea>
    <button onclick="convert()">Convert</button>
    <div class="container">
        <pre id="output">{}</pre>
    </div>

    <script>
        function convert() {
            const cookieStr = document.getElementById('cookieInput').value.trim();
            const result = {};
            
            // 精确解析逻辑（和 c2j.wtf.sb 完全一致）
            cookieStr.split(';').forEach(pair => {
                const [rawKey, ...rawValueParts] = pair.trim().split('=');
                const key = rawKey.trim();
                const value = rawValueParts.join('=').trim(); // 处理值中包含=的情况
                
                if (key && value !== undefined) {
                    result[key] = value;
                }
            });

            document.getElementById('output').textContent = JSON.stringify(result, null, 2);
        }
    </script>
</body>
</html>
