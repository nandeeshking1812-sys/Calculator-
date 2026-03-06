<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
            justify-content: center;
            max-width: 1200px;
        }

        .calculator {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            overflow: hidden;
            width: 100%;
            max-width: 400px;
            animation: slideIn 0.3s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .display-panel {
            background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
            color: white;
            padding: 20px;
            min-height: 200px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .display-info {
            display: flex;
            justify-content: space-between;
            font-size: 12px;
            margin-bottom: 10px;
            opacity: 0.7;
        }

        .memory-info {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .info-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .info-label {
            font-weight: bold;
            color: #3498db;
        }

        .display {
            background: rgba(0, 0, 0, 0.3);
            border: 2px solid rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 32px;
            padding: 15px;
            border-radius: 10px;
            text-align: right;
            word-wrap: break-word;
            word-break: break-all;
            min-height: 50px;
            font-weight: 500;
            letter-spacing: 0.5px;
            transition: all 0.3s ease;
            font-family: 'Courier New', monospace;
            resize: none;
            border: none;
            outline: none;
        }

        .display:focus {
            outline: none;
            border: 2px solid #3498db;
            background: rgba(52, 152, 219, 0.2);
        }

        .buttons-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 8px;
            padding: 15px;
            background: #ecf0f1;
        }

        button {
            padding: 15px;
            font-size: 14px;
            font-weight: 600;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s ease;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        button:active {
            transform: translateY(0);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .btn-number {
            background: #ecf0f1;
            color: #2c3e50;
            border: 2px solid #bdc3c7;
        }

        .btn-number:hover {
            background: #d5dbdb;
        }

        .btn-operator {
            background: linear-gradient(135deg, #f39c12 0%, #e67e22 100%);
            color: white;
        }

        .btn-operator:hover {
            filter: brightness(1.1);
        }

        .btn-equals {
            background: linear-gradient(135deg, #27ae60 0%, #229954 100%);
            color: white;
            grid-column: span 2;
            font-size: 16px;
        }

        .btn-equals:hover {
            filter: brightness(1.1);
        }

        .btn-function {
            background: linear-gradient(135deg, #3498db 0%, #2980b9 100%);
            color: white;
            font-size: 12px;
        }

        .btn-function:hover {
            filter: brightness(1.1);
        }

        .btn-memory {
            background: linear-gradient(135deg, #9b59b6 0%, #8e44ad 100%);
            color: white;
            font-size: 12px;
        }

        .btn-memory:hover {
            filter: brightness(1.1);
        }

        .btn-clear {
            background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
            color: white;
        }

        .btn-clear:hover {
            filter: brightness(1.1);
        }

        .btn-scientific {
            background: linear-gradient(135deg, #16a085 0%, #138d75 100%);
            color: white;
            font-size: 12px;
        }

        .btn-scientific:hover {
            filter: brightness(1.1);
        }

        .tabs {
            display: flex;
            gap: 5px;
            padding: 10px;
            background: #ecf0f1;
            border-top: 1px solid #bdc3c7;
        }

        .tab-btn {
            flex: 1;
            padding: 10px;
            border: 2px solid #95a5a6;
            background: white;
            color: #2c3e50;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 12px;
            transition: all 0.3s ease;
        }

        .tab-btn.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-color: #667eea;
        }

        .tab-content {
            display: none;
            padding: 15px;
            background: white;
            border-top: 1px solid #bdc3c7;
            max-height: 300px;
            overflow-y: auto;
        }

        .tab-content.active {
            display: block;
        }

        .history-item {
            padding: 8px;
            background: #ecf0f1;
            border-radius: 5px;
            margin: 5px 0;
            font-family: 'Courier New', monospace;
            font-size: 12px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .history-item:hover {
            background: #d5dbdb;
            transform: translateX(5px);
        }

        .variable-item {
            padding: 8px;
            background: #ecf0f1;
            border-radius: 5px;
            margin: 5px 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 12px;
        }

        .var-delete {
            background: #e74c3c;
            color: white;
            border: none;
            padding: 3px 8px;
            border-radius: 3px;
            cursor: pointer;
            font-size: 10px;
        }

        .var-delete:hover {
            background: #c0392b;
        }

        .sidebar {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            width: 100%;
            max-width: 300px;
            overflow: hidden;
            animation: slideIn 0.3s ease-out 0.1s both;
        }

        .sidebar-header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px;
            font-weight: 600;
            font-size: 16px;
        }

        .sidebar-content {
            padding: 15px;
            max-height: 400px;
            overflow-y: auto;
        }

        .section {
            margin-bottom: 20px;
        }

        .section-title {
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 12px;
            text-transform: uppercase;
        }

        .constant-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
        }

        .constant-btn {
            padding: 10px;
            background: linear-gradient(135deg, #f39c12 0%, #e67e22 100%);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 600;
            transition: all 0.2s ease;
        }

        .constant-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        .const-value {
            font-size: 10px;
            opacity: 0.8;
        }

        .about-section {
            background: #ecf0f1;
            padding: 10px;
            border-radius: 8px;
            font-size: 11px;
            line-height: 1.5;
            color: #2c3e50;
        }

        .about-section p {
            margin: 5px 0;
        }

        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }

            .sidebar {
                max-width: 100%;
            }

            .buttons-grid {
                grid-template-columns: repeat(4, 1fr);
            }

            button {
                padding: 12px;
                font-size: 12px;
            }

            .display {
                font-size: 24px;
            }

            .btn-equals {
                grid-column: span 2;
            }
        }

        @media (max-width: 480px) {
            .buttons-grid {
                grid-template-columns: repeat(4, 1fr);
                gap: 6px;
                padding: 10px;
            }

            button {
                padding: 10px;
                font-size: 11px;
            }

            .display {
                font-size: 20px;
                padding: 10px;
            }

            .display-panel {
                padding: 15px;
                min-height: 150px;
            }
        }

        .error {
            color: #e74c3c;
            animation: shake 0.3s ease;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        .success {
            color: #27ae60;
        }

        .no-data {
            padding: 20px;
            text-align: center;
            color: #95a5a6;
            font-size: 12px;
        }

        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: #ecf0f1;
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb {
            background: #bdc3c7;
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #95a5a6;
        }

        textarea {
            resize: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Main Calculator -->
        <div class="calculator">
            <!-- Display Panel -->
            <div class="display-panel">
                <div class="display-info">
                    <div class="memory-info">
                        <div class="info-item">
                            <span class="info-label">M:</span>
                            <span id="memoryValue">0</span>
                        </div>
                        <div class="info-item">
                            <span class="info-label">H:</span>
                            <span id="historyCount">0</span>
                        </div>
                        <div class="info-item">
                            <span class="info-label">Mode:</span>
                            <span id="modeIndicator">Basic</span>
                        </div>
                    </div>
                </div>
                <textarea class="display" id="display" spellcheck="false">0</textarea>
            </div>

            <!-- Main Button Grid -->
            <div class="buttons-grid">
                <!-- Row 1 -->
                <button class="btn-clear" onclick="clearDisplay()">AC</button>
                <button class="btn-clear" onclick="deleteLastChar()">DEL</button>
                <button class="btn-operator" onclick="appendOperator('(')">( )</button>
                <button class="btn-operator" onclick="appendOperator('/')">/</button>
                <button class="btn-function" onclick="toggleMode()">Sci</button>

                <!-- Row 2 -->
                <button class="btn-number" onclick="appendNumber('7')">7</button>
                <button class="btn-number" onclick="appendNumber('8')">8</button>
                <button class="btn-number" onclick="appendNumber('9')">9</button>
                <button class="btn-operator" onclick="appendOperator('*')">×</button>
                <button class="btn-memory" onclick="memoryClear()">MC</button>

                <!-- Row 3 -->
                <button class="btn-number" onclick="appendNumber('4')">4</button>
                <button class="btn-number" onclick="appendNumber('5')">5</button>
                <button class="btn-number" onclick="appendNumber('6')">6</button>
                <button class="btn-operator" onclick="appendOperator('-')">−</button>
                <button class="btn-memory" onclick="memoryRecall()">MR</button>

                <!-- Row 4 -->
                <button class="btn-number" onclick="appendNumber('1')">1</button>
                <button class="btn-number" onclick="appendNumber('2')">2</button>
                <button class="btn-number" onclick="appendNumber('3')">3</button>
                <button class="btn-operator" onclick="appendOperator('+')">+</button>
                <button class="btn-memory" onclick="memoryAdd()">M+</button>

                <!-- Row 5 -->
                <button class="btn-number" style="grid-column: span 2;" onclick="appendNumber('0')">0</button>
                <button class="btn-number" onclick="appendNumber('.')">.</button>
                <button class="btn-equals" onclick="calculateResult()">=</button>
                <button class="btn-memory" onclick="memorySubtract()">M−</button>
            </div>

            <!-- Scientific Buttons (Hidden by default) -->
            <div id="scientificButtons" style="display: none;">
                <div class="buttons-grid" style="grid-template-columns: repeat(5, 1fr);">
                    <button class="btn-scientific" onclick="appendFunction('sin')">sin</button>
                    <button class="btn-scientific" onclick="appendFunction('cos')">cos</button>
                    <button class="btn-scientific" onclick="appendFunction('tan')">tan</button>
                    <button class="btn-scientific" onclick="appendFunction('sqrt')">√</button>
                    <button class="btn-scientific" onclick="appendFunction('abs')">|x|</button>

                    <button class="btn-scientific" onclick="appendFunction('asin')">asin</button>
                    <button class="btn-scientific" onclick="appendFunction('acos')">acos</button>
                    <button class="btn-scientific" onclick="appendFunction('atan')">atan</button>
                    <button class="btn-scientific" onclick="appendFunction('log')">log</button>
                    <button class="btn-scientific" onclick="appendFunction('ln')">ln</button>

                    <button class="btn-scientific" onclick="appendFunction('exp')">eˣ</button>
                    <button class="btn-operator" onclick="appendOperator('^')">xʸ</button>
                    <button class="btn-scientific" onclick="appendFunction('factorial')">n!</button>
                    <button class="btn-scientific" onclick="appendFunction('ceil')">⌈x⌉</button>
                    <button class="btn-scientific" onclick="appendFunction('floor')">⌊x⌋</button>

                    <button class="btn-scientific" onclick="appendConstant('π')">π</button>
                    <button class="btn-scientific" onclick="appendConstant('e')">e</button>
                    <button class="btn-scientific" onclick="appendConstant('φ')">φ</button>
                    <button class="btn-operator" onclick="appendOperator('%')">%</button>
                    <button class="btn-scientific" onclick="appendFunction('deg')">°→r</button>
                </div>
            </div>

            <!-- Tabs -->
            <div class="tabs">
                <button class="tab-btn active" onclick="switchTab('history')">History</button>
                <button class="tab-btn" onclick="switchTab('variables')">Variables</button>
                <button class="tab-btn" onclick="switchTab('info')">Info</button>
            </div>

            <!-- Tab Contents -->
            <div id="history" class="tab-content active"></div>
            <div id="variables" class="tab-content"></div>
            <div id="info" class="tab-content">
                <div class="about-section">
                    <p><strong>Advanced Calculator v2.0</strong></p>
                    <p>✓ Scientific functions (sin, cos, tan, sqrt, log, etc.)</p>
                    <p>✓ Memory operations (M+, M−, MR, MC)</p>
                    <p>✓ Calculation history</p>
                    <p>✓ Custom variables</p>
                    <p>✓ Mathematical constants (π, e, φ)</p>
                    <p>✓ Keyboard support</p>
                    <p>✓ CSP compliant (no unsafe-eval)</p>
                    <p style="margin-top: 10px; font-size: 10px; color: #7f8c8d;">Made with ❤️ for easy calculations</p>
                </div>
            </div>
        </div>

        <!-- Sidebar -->
        <div class="sidebar">
            <div class="sidebar-header">Quick Access</div>
            <div class="sidebar-content">
                <!-- Constants Section -->
                <div class="section">
                    <div class="section-title">Constants</div>
                    <div class="constant-grid">
                        <button class="constant-btn" onclick="appendConstant('π')">
                            π<br><span class="const-value">3.14159</span>
                        </button>
                        <button class="constant-btn" onclick="appendConstant('e')">
                            e<br><span class="const-value">2.71828</span>
                        </button>
                        <button class="constant-btn" onclick="appendConstant('φ')">
                            φ<br><span class="const-value">1.61803</span>
                        </button>
                        <button class="constant-btn" onclick="appendConstant('√2')">
                            √2<br><span class="const-value">1.41421</span>
                        </button>
                    </div>
                </div>

                <!-- Quick Functions Section -->
                <div class="section">
                    <div class="section-title">Quick Functions</div>
                    <div class="constant-grid">
                        <button class="constant-btn" onclick="appendFunction('sqrt')">Square Root</button>
                        <button class="constant-btn" onclick="appendFunction('sin')">Sine</button>
                        <button class="constant-btn" onclick="appendFunction('cos')">Cosine</button>
                        <button class="constant-btn" onclick="appendFunction('tan')">Tangent</button>
                        <button class="constant-btn" onclick="appendFunction('log')">Log10</button>
                        <button class="constant-btn" onclick="appendFunction('ln')">Ln</button>
                        <button class="constant-btn" onclick="appendFunction('abs')">Absolute</button>
                        <button class="constant-btn" onclick="appendFunction('factorial')">Factorial</button>
                    </div>
                </div>

                <!-- Variable Input Section -->
                <div class="section">
                    <div class="section-title">Set Variable</div>
                    <input type="text" id="varName" placeholder="Name (e.g., x)" style="width: 100%; padding: 8px; border: 1px solid #bdc3c7; border-radius: 5px; margin-bottom: 5px; font-size: 12px;">
                    <input type="text" id="varValue" placeholder="Value" style="width: 100%; padding: 8px; border: 1px solid #bdc3c7; border-radius: 5px; margin-bottom: 5px; font-size: 12px;">
                    <button onclick="setVariable()" style="width: 100%; padding: 8px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border: none; border-radius: 5px; cursor: pointer; font-weight: 600; font-size: 12px;">Set Var</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Safe Expression Evaluator (No eval() or Function())
        class Calculator {
            constructor() {
                this.display = document.getElementById('display');
                this.memory = 0;
                this.history = [];
                this.variables = {};
                this.isScientificMode = false;
                
                this.constants = {
                    'π': Math.PI,
                    'e': Math.E,
                    'φ': (1 + Math.sqrt(5)) / 2,
                    '√2': Math.sqrt(2)
                };

                this.mathFunctions = {
                    'sin': Math.sin,
                    'cos': Math.cos,
                    'tan': Math.tan,
                    'asin': Math.asin,
                    'acos': Math.acos,
                    'atan': Math.atan,
                    'sqrt': Math.sqrt,
                    'abs': Math.abs,
                    'log': Math.log10,
                    'ln': Math.log,
                    'exp': Math.exp,
                    'ceil': Math.ceil,
                    'floor': Math.floor,
                    'deg': (x) => x * Math.PI / 180,
                    'rad': (x) => x * 180 / Math.PI,
                    'factorial': this.factorial
                };

                this.display.value = '0';
                this.updateMemoryDisplay();
                this.updateHistoryDisplay();
                this.updateVariablesDisplay();
            }

            factorial(n) {
                if (n < 0) throw new Error('Factorial of negative number');
                if (n === 0 || n === 1) return 1;
                let result = 1;
                for (let i = 2; i <= n; i++) result *= i;
                return result;
            }

            tokenize(input) {
                const tokens = [];
                let current = '';
                let i = 0;

                while (i < input.length) {
                    const char = input[i];

                    // Skip whitespace
                    if (/\s/.test(char)) {
                        i++;
                        continue;
                    }

                    // Numbers
                    if (/[0-9]/.test(char) || (char === '.' && /[0-9]/.test(input[i - 1] || ''))) {
                        let num = '';
                        while (i < input.length && (/[0-9.]/.test(input[i]))) {
                            num += input[i];
                            i++;
                        }
                        tokens.push({ type: 'NUMBER', value: parseFloat(num) });
                        continue;
                    }

                    // Functions and constants (letters)
                    if (/[a-z]/i.test(char) || char === 'π' || char === 'φ') {
                        let name = '';
                        while (i < input.length && (/[a-z0-9π]|[φ]/.test(input[i]))) {
                            name += input[i];
                            i++;
                        }

                        if (this.constants[name]) {
                            tokens.push({ type: 'NUMBER', value: this.constants[name] });
                        } else if (this.mathFunctions[name]) {
                            tokens.push({ type: 'FUNCTION', value: name });
                        } else {
                            // Check if it's a variable
                            if (this.variables[name]) {
                                tokens.push({ type: 'NUMBER', value: this.variables[name] });
                            } else {
                                throw new Error(`Unknown function or variable: ${name}`);
                            }
                        }
                        continue;
                    }

                    // Operators
                    if (/[+\-*/%^]/.test(char)) {
                        tokens.push({ type: 'OPERATOR', value: char });
                        i++;
                        continue;
                    }

                    // Parentheses
                    if (char === '(') {
                        tokens.push({ type: 'LPAREN', value: '(' });
                        i++;
                        continue;
                    }

                    if (char === ')') {
                        tokens.push({ type: 'RPAREN', value: ')' });
                        i++;
                        continue;
                    }

                    throw new Error(`Invalid character: ${char}`);
                }

                return tokens;
            }

            parseExpression(tokens, pos = 0) {
                let [left, pos2] = this.parseTerm(tokens, pos);

                while (pos2 < tokens.length && (tokens[pos2].type === 'OPERATOR' && /[+\-]/.test(tokens[pos2].value))) {
                    const op = tokens[pos2].value;
                    const [right, pos3] = this.parseTerm(tokens, pos2 + 1);
                    left = op === '+' ? left + right : left - right;
                    pos2 = pos3;
                }

                return [left, pos2];
            }

            parseTerm(tokens, pos = 0) {
                let [left, pos2] = this.parseFactor(tokens, pos);

                while (pos2 < tokens.length && (tokens[pos2].type === 'OPERATOR' && /[*/%]/.test(tokens[pos2].value))) {
                    const op = tokens[pos2].value;
                    const [right, pos3] = this.parseFactor(tokens, pos2 + 1);

                    if (op === '*') left = left * right;
                    else if (op === '/') {
                        if (right === 0) throw new Error('Division by zero');
                        left = left / right;
                    }
                    else if (op === '%') {
                        if (right === 0) throw new Error('Modulo by zero');
                        left = left % right;
                    }
                    pos2 = pos3;
                }

                return [left, pos2];
            }

            parseFactor(tokens, pos = 0) {
                if (pos >= tokens.length) throw new Error('Unexpected end of expression');

                const token = tokens[pos];

                // Handle negative numbers
                if (token.type === 'OPERATOR' && token.value === '-') {
                    const [val, newPos] = this.parseFactor(tokens, pos + 1);
                    return [-val, newPos];
                }

                // Handle positive numbers
                if (token.type === 'OPERATOR' && token.value === '+') {
                    return this.parseFactor(tokens, pos + 1);
                }

                // Handle numbers
                if (token.type === 'NUMBER') {
                    return [token.value, pos + 1];
                }

                // Handle functions
                if (token.type === 'FUNCTION') {
                    const [val, newPos] = this.parseFactor(tokens, pos + 1);
                    return [this.mathFunctions[token.value](val), newPos];
                }

                // Handle parentheses
                if (token.type === 'LPAREN') {
                    const [val, newPos] = this.parseExpression(tokens, pos + 1);
                    if (newPos >= tokens.length || tokens[newPos].type !== 'RPAREN') {
                        throw new Error('Mismatched parentheses');
                    }
                    return [val, newPos + 1];
                }

                // Handle power operator
                if (token.type === 'OPERATOR' && token.value === '^') {
                    const [base, pos2] = this.parseFactor(tokens, pos - 1);
                    const [exp, pos3] = this.parseFactor(tokens, pos + 1);
                    return [Math.pow(base, exp), pos3];
                }

                throw new Error(`Unexpected token: ${token.value}`);
            }

            parseWithPower(tokens, pos = 0) {
                let [left, newPos] = this.parseFactor(tokens, pos);

                while (newPos < tokens.length && tokens[newPos].type === 'OPERATOR' && tokens[newPos].value === '^') {
                    const [right, pos2] = this.parseFactor(tokens, newPos + 1);
                    left = Math.pow(left, right);
                    newPos = pos2;
                }

                return [left, newPos];
            }

            evaluate(expression) {
                try {
                    const tokens = this.tokenize(expression);
                    const [result] = this.parseExpression(tokens);
                    
                    if (!isFinite(result)) {
                        throw new Error('Result is not a valid number');
                    }
                    
                    return result;
                } catch (error) {
                    throw new Error(error.message);
                }
            }

            appendNumber(num) {
                if (this.display.value === '0') {
                    this.display.value = num;
                } else {
                    this.display.value += num;
                }
            }

            appendOperator(op) {
                const text = this.display.value;
                if (op === '()') {
                    const openCount = (text.match(/\(/g) || []).length;
                    const closeCount = (text.match(/\)/g) || []).length;
                    if (openCount > closeCount) {
                        this.display.value += ')';
                    } else {
                        this.display.value += '(';
                    }
                } else if (!/[+\-*/%^(]$/.test(text)) {
                    this.display.value += op;
                }
            }

            appendFunction(func) {
                if (this.display.value === '0') {
                    this.display.value = func + '(';
                } else {
                    this.display.value += func + '(';
                }
            }

            appendConstant(constant) {
                if (this.display.value === '0') {
                    this.display.value = constant;
                } else {
                    this.display.value += constant;
                }
            }

            deleteLastChar() {
                const text = this.display.value;
                this.display.value = text.slice(0, -1) || '0';
            }

            clearDisplay() {
                this.display.value = '0';
            }

            calculateResult() {
                try {
                    const expression = this.display.value.trim();
                    const result = this.evaluate(expression);

                    let displayValue;
                    if (Number.isInteger(result)) {
                        displayValue = result.toString();
                    } else {
                        displayValue = parseFloat(result.toFixed(10)).toString();
                    }

                    this.display.value = displayValue;
                    this.addToHistory(displayValue);
                    this.updateHistoryDisplay();
                } catch (error) {
                    this.display.value = `Error: ${error.message}`;
                    this.display.classList.add('error');
                    setTimeout(() => this.display.classList.remove('error'), 500);
                }
            }

            // Memory functions
            memoryAdd() {
                try {
                    const value = parseFloat(this.display.value);
                    if (!isNaN(value)) {
                        this.memory += value;
                        this.updateMemoryDisplay();
                        this.display.value = '0';
                    }
                } catch (e) {
                    this.display.value = 'Error';
                }
            }

            memorySubtract() {
                try {
                    const value = parseFloat(this.display.value);
                    if (!isNaN(value)) {
                        this.memory -= value;
                        this.updateMemoryDisplay();
                        this.display.value = '0';
                    }
                } catch (e) {
                    this.display.value = 'Error';
                }
            }

            memoryRecall() {
                this.display.value = this.memory.toString();
            }

            memoryClear() {
                this.memory = 0;
                this.updateMemoryDisplay();
            }

            updateMemoryDisplay() {
                document.getElementById('memoryValue').textContent = this.memory === 0 ? '0' : this.memory.toFixed(4);
            }

            // History
            addToHistory(result) {
                const expression = this.display.value;
                this.history.unshift({
                    expression: expression,
                    timestamp: new Date().toLocaleTimeString()
                });
                if (this.history.length > 50) this.history.pop();
                document.getElementById('historyCount').textContent = this.history.length;
            }

            updateHistoryDisplay() {
                const historyDiv = document.getElementById('history');
                if (this.history.length === 0) {
                    historyDiv.innerHTML = '<div class="no-data">No calculations yet</div>';
                } else {
                    historyDiv.innerHTML = this.history.map((item, index) => 
                        `<div class="history-item" onclick="calc.recallHistory(${index})">${item.expression}</div>`
                    ).join('');
                }
            }

            recallHistory(index) {
                if (this.history[index]) {
                    this.display.value = this.history[index].expression;
                }
            }

            // Variables
            setVariable() {
                const name = document.getElementById('varName').value.trim();
                const value = document.getElementById('varValue').value.trim();

                if (name && value) {
                    try {
                        const result = this.evaluate(value);
                        this.variables[name] = result;
                        this.updateVariablesDisplay();
                        document.getElementById('varName').value = '';
                        document.getElementById('varValue').value = '';
                        this.display.classList.add('success');
                        setTimeout(() => this.display.classList.remove('success'), 300);
                    } catch (e) {
                        this.display.value = 'Invalid variable value';
                    }
                }
            }

            deleteVariable(name) {
                delete this.variables[name];
                this.updateVariablesDisplay();
            }

            updateVariablesDisplay() {
                const variablesDiv = document.getElementById('variables');
                const varNames = Object.keys(this.variables);
                if (varNames.length === 0) {
                    variablesDiv.innerHTML = '<div class="no-data">No variables set</div>';
                } else {
                    variablesDiv.innerHTML = varNames.map(name => 
                        `<div class="variable-item">
                            <span>${name} = ${this.variables[name].toFixed(4)}</span>
                            <button class="var-delete" onclick="calc.deleteVariable('${name}')">Delete</button>
                        </div>`
                    ).join('');
                }
            }

            toggleMode() {
                this.isScientificMode = !this.isScientificMode;
                const scientificButtons = document.getElementById('scientificButtons');
                scientificButtons.style.display = this.isScientificMode ? 'block' : 'none';
                document.getElementById('modeIndicator').textContent = this.isScientificMode ? 'Scientific' : 'Basic';
            }
        }

        // Global calculator instance
        const calc = new Calculator();

        // Event handlers
        function appendNumber(num) { calc.appendNumber(num); }
        function appendOperator(op) { calc.appendOperator(op); }
        function appendFunction(func) { calc.appendFunction(func); }
        function appendConstant(constant) { calc.appendConstant(constant); }
        function deleteLastChar() { calc.deleteLastChar(); }
        function clearDisplay() { calc.clearDisplay(); }
        function calculateResult() { calc.calculateResult(); }
        function memoryAdd() { calc.memoryAdd(); }
        function memorySubtract() { calc.memorySubtract(); }
        function memoryRecall() { calc.memoryRecall(); }
        function memoryClear() { calc.memoryClear(); }
        function setVariable() { calc.setVariable(); }
        function toggleMode() { calc.toggleMode(); }

        function switchTab(tabName) {
            const tabs = document.querySelectorAll('.tab-content');
            const buttons = document.querySelectorAll('.tab-btn');
            
            tabs.forEach(tab => tab.classList.remove('active'));
            buttons.forEach(btn => btn.classList.remove('active'));
            
            document.getElementById(tabName).classList.add('active');
            event.target.classList.add('active');
        }

        // Keyboard support
        document.addEventListener('keydown', (e) => {
            if (e.target === calc.display) return;
            
            const key = e.key;
            
            if (/[0-9.]/.test(key)) {
                appendNumber(key);
            } else if (key === '+') {
                e.preventDefault();
                appendOperator('+');
            } else if (key === '-') {
                e.preventDefault();
                appendOperator('−');
            } else if (key === '*') {
                e.preventDefault();
                appendOperator('×');
            } else if (key === '/') {
                e.preventDefault();
                appendOperator('/');
            } else if (key === '%') {
                e.preventDefault();
                appendOperator('%');
            } else if (key === '^') {
                e.preventDefault();
                appendOperator('^');
            } else if (key === 'Enter' || key === '=') {
                e.preventDefault();
                calculateResult();
            } else if (key === 'Backspace') {
                e.preventDefault();
                deleteLastChar();
            } else if (key === 'Delete') {
                e.preventDefault();
                clearDisplay();
            } else if (key === '(') {
                e.preventDefault();
                appendOperator('(');
            } else if (key === ')') {
                e.preventDefault();
                appendOperator(')');
            }
        });
    </script>
</body>
</html>
