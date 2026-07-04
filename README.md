# Calculadora-programaci-n-

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora Científica Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #f3f4f6; display: flex; justify-content: center; align-items: center; min-height: 100vh; margin: 0; font-family: sans-serif; }
        .calculator { width: 100%; max-width: 400px; background: white; padding: 20px; border-radius: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        .btn-sci { background-color: #4b5563; color: white; }
        .btn-sci:hover { background-color: #374151; }
        #history { max-height: 100px; overflow-y: auto; }
    </style>
</head>
<body>

<div class="calculator">
    <input type="text" id="display" class="w-full h-16 text-right text-2xl font-bold mb-2 p-4 bg-gray-100 rounded-lg outline-none" disabled placeholder="0">
    
    <!-- Historial Demo -->
    <div id="history" class="mb-4 text-xs text-gray-500 border-t pt-2 italic">
        <div class="text-gray-400">Historial:</div>
        <div id="history-items"></div>
    </div>
    
    <div class="grid grid-cols-4 gap-2 mb-2">
        <button onclick="appendFunc('sin(')" class="p-2 btn-sci rounded-lg text-xs">sin</button>
        <button onclick="appendFunc('cos(')" class="p-2 btn-sci rounded-lg text-xs">cos</button>
        <button onclick="appendFunc('tan(')" class="p-2 btn-sci rounded-lg text-xs">tan</button>
        <button onclick="appendFunc('Math.log(')" class="p-2 btn-sci rounded-lg text-xs">ln</button>
        <button onclick="appendFunc('Math.sqrt(')" class="p-2 btn-sci rounded-lg text-xs">√</button>
        <button onclick="appendFunc('**')" class="p-2 btn-sci rounded-lg text-xs">x^y</button>
        <button onclick="appendFunc('Math.PI')" class="p-2 btn-sci rounded-lg text-xs">π</button>
        <button onclick="appendFunc('Math.E')" class="p-2 btn-sci rounded-lg text-xs">e</button>
        <button onclick="appendFunc('(')" class="p-2 btn-sci rounded-lg text-xs">(</button>
        <button onclick="appendFunc(')')" class="p-2 btn-sci rounded-lg text-xs">)</button>
        <button onclick="appendFunc('!')" class="p-2 btn-sci rounded-lg text-xs">n!</button>
        <button onclick="deleteLast()" class="p-2 bg-gray-400 text-white rounded-lg text-xs">DEL</button>
    </div>

    <div class="grid grid-cols-4 gap-2">
        <button onclick="clearDisplay()" class="col-span-2 p-4 bg-red-400 text-white rounded-xl text-xl hover:bg-red-500">C</button>
        <button onclick="appendToDisplay('/')" class="p-4 bg-orange-400 text-white rounded-xl text-xl hover:bg-orange-500">/</button>
        <button onclick="appendToDisplay('*')" class="p-4 bg-orange-400 text-white rounded-xl text-xl hover:bg-orange-500">×</button>
        
        <button onclick="appendToDisplay('7')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">7</button>
        <button onclick="appendToDisplay('8')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">8</button>
        <button onclick="appendToDisplay('9')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">9</button>
        <button onclick="appendToDisplay('-')" class="p-4 bg-orange-400 text-white rounded-xl text-xl hover:bg-orange-500">-</button>
        
        <button onclick="appendToDisplay('4')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">4</button>
        <button onclick="appendToDisplay('5')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">5</button>
        <button onclick="appendToDisplay('6')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">6</button>
        <button onclick="appendToDisplay('+')" class="p-4 bg-orange-400 text-white rounded-xl text-xl hover:bg-orange-500">+</button>
        
        <button onclick="appendToDisplay('1')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">1</button>
        <button onclick="appendToDisplay('2')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">2</button>
        <button onclick="appendToDisplay('3')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">3</button>
        <button onclick="calculate()" class="row-span-2 p-4 bg-green-500 text-white rounded-xl text-xl hover:bg-green-600">=</button>
        
        <button onclick="appendToDisplay('0')" class="col-span-2 p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">0</button>
        <button onclick="appendToDisplay('.')" class="p-4 bg-gray-200 rounded-xl text-xl hover:bg-gray-300">.</button>
    </div>
</div>

<script>
    const display = document.getElementById('display');
    const historyContainer = document.getElementById('history-items');

    function factorial(n) {
        if (n === 0 || n === 1) return 1;
        let res = 1;
        for (let i = 2; i <= n; i++) res *= i;
        return res;
    }

    function addToHistory(op, res) {
        const item = document.createElement('div');
        item.textContent = `${op} = ${res}`;
        historyContainer.prepend(item);
    }

    function appendToDisplay(value) { display.value += value; }
    function appendFunc(func) { display.value += func; }
    function clearDisplay() { display.value = ''; }
    function deleteLast() { display.value = display.value.slice(0, -1); }
    
    function calculate() {
        try {
            const originalExpr = display.value;
            let expression = display.value
                .replace(/sin\(/g, 'Math.sin(')
                .replace(/cos\(/g, 'Math.cos(')
                .replace(/tan\(/g, 'Math.tan(')
                .replace(/(\d+)!/g, 'factorial($1)');
            
            const result = eval(expression);
            addToHistory(originalExpr, result);
            display.value = result;
        } catch (error) {
            display.value = 'Error';
            setTimeout(clearDisplay, 1000);
        }
    }
</script>

</body>
</html>

```
