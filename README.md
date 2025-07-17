<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Licznik Kart w Blackjacku</title>
    <style>
        :root {
            --primary: #0d3b2e;
            --secondary: #1a5c48;
            --accent: #e9c46a;
            --highlight: #f4a261;
            --text: #f0f0f0;
            --card-bg: #2a9d8f;
            --reset-btn: #e76f51;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0d3b2e, #0a2e23);
            color: var(--text);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .container {
            background: linear-gradient(to bottom, #1a5c48, #0d3b2e);
            border-radius: 15px;
            padding: 30px;
            width: 100%;
            max-width: 800px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            border: 2px solid var(--accent);
            position: relative;
            overflow: hidden;
        }
        
        .container::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 5px;
            background: linear-gradient(to right, #e9c46a, #f4a261, #e76f51);
        }
        
        h1 {
            text-align: center;
            color: var(--accent);
            margin: 0 0 20px 0;
            font-size: 2.5rem;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        .input-section {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 25px;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: var(--accent);
            font-size: 1.1rem;
        }
        
        .cards-input {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        #cards {
            flex: 1;
            min-height: 100px;
            padding: 15px;
            border: 2px solid var(--accent);
            border-radius: 8px;
            background-color: rgba(13, 59, 46, 0.7);
            color: var(--text);
            font-size: 1.1rem;
            resize: vertical;
        }
        
        .card-buttons {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
            margin-top: 15px;
        }
        
        .card-btn {
            padding: 12px;
            background: var(--card-bg);
            color: var(--text);
            border: none;
            border-radius: 8px;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .card-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 8px rgba(0, 0, 0, 0.2);
        }
        
        .card-btn:active {
            transform: translateY(1px);
        }
        
        .card-btn.low {
            background: #2a9d8f;
        }
        
        .card-btn.neutral {
            background: #5a7d9c;
        }
        
        .card-btn.high {
            background: #e76f51;
        }
        
        .decks-group {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
        }
        
        #decks {
            flex: 1;
            padding: 12px;
            border: 2px solid var(--accent);
            border-radius: 8px;
            background-color: rgba(13, 59, 46, 0.7);
            color: var(--text);
            font-size: 1.1rem;
            max-width: 200px;
        }
        
        .action-buttons {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }
        
        .btn {
            flex: 1;
            padding: 16px;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 10px rgba(0, 0, 0, 0.3);
        }
        
        .btn:active {
            transform: translateY(1px);
        }
        
        .btn.calculate {
            background: linear-gradient(to right, var(--accent), var(--highlight));
            color: var(--primary);
        }
        
        .btn.reset {
            background: linear-gradient(to right, var(--reset-btn), #d62828);
            color: white;
        }
        
        .result {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 25px;
            text-align: center;
            margin-bottom: 25px;
            border: 2px solid var(--accent);
        }
        
        .result-title {
            font-size: 1.4rem;
            margin-bottom: 5px;
            color: var(--accent);
            font-weight: bold;
        }
        
        .count-value {
            font-size: 3.5rem;
            font-weight: bold;
            margin: 10px 0;
            color: var(--accent);
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        .count-details {
            font-size: 1.1rem;
            opacity: 0.9;
            margin-top: 5px;
        }
        
        .explanation {
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            padding: 20px;
            font-size: 1.1rem;
            line-height: 1.6;
        }
        
        .explanation h3 {
            color: var(--accent);
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.5rem;
        }
        
        .explanation ul {
            padding-left: 25px;
            margin: 15px 0;
        }
        
        .explanation li {
            margin-bottom: 8px;
        }
        
        .card-types {
            display: flex;
            justify-content: space-around;
            margin: 20px 0;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .card-type {
            background: rgba(42, 157, 143, 0.3);
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            flex: 1;
            min-width: 150px;
            border: 1px solid var(--accent);
        }
        
        .card-type h4 {
            color: var(--accent);
            margin-bottom: 10px;
        }
        
        .card-type p {
            font-size: 1.1rem;
        }
        
        .footer {
            text-align: center;
            margin-top: 20px;
            font-size: 0.9rem;
            opacity: 0.7;
        }
        
        @media (max-width: 600px) {
            .card-buttons {
                grid-template-columns: repeat(4, 1fr);
            }
            
            .action-buttons {
                flex-direction: column;
            }
            
            h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Licznik Kart w Blackjacku</h1>
        
        <div class="input-section">
            <div class="input-group">
                <label for="cards">Wprowadź karty:</label>
                <div class="cards-input">
                    <textarea id="cards" rows="3" placeholder="Wpisz karty lub użyj przycisków poniżej..."></textarea>
                </div>
                
                <div class="card-buttons">
                    <button class="card-btn low" data-card="2">2</button>
                    <button class="card-btn low" data-card="3">3</button>
                    <button class="card-btn low" data-card="4">4</button>
                    <button class="card-btn low" data-card="5">5</button>
                    <button class="card-btn low" data-card="6">6</button>
                    <button class="card-btn neutral" data-card="7">7</button>
                    <button class="card-btn neutral" data-card="8">8</button>
                    <button class="card-btn neutral" data-card="9">9</button>
                    <button class="card-btn high" data-card="10">10</button>
                    <button class="card-btn high" data-card="J">J</button>
                    <button class="card-btn high" data-card="Q">Q</button>
                    <button class="card-btn high" data-card="K">K</button>
                    <button class="card-btn high" data-card="A">A</button>
                </div>
            </div>
            
            <div class="input-group">
                <label for="decks">Liczba talii:</label>
                <div class="decks-group">
                    <select id="decks">
                        <option value="1">1 talia</option>
                        <option value="2">2 talie</option>
                        <option value="4">4 talie</option>
                        <option value="6">6 talie</option>
                        <option value="8" selected>8 talii (standard)</option>
                    </select>
                    <div class="count-details">(52 karty na talię)</div>
                </div>
            </div>
            
            <div class="action-buttons">
                <button class="btn calculate" onclick="calculateCount()">
                    <span>Oblicz Licznik Kart</span>
                </button>
                <button class="btn reset" onclick="resetCounter()">
                    <span>Resetuj Karty</span>
                </button>
            </div>
        </div>
        
        <div class="result">
            <div class="result-title">Running Count:</div>
            <div id="runningCount" class="count-value">0</div>
            <div class="count-details">Suma wartości wszystkich kart</div>
            
            <div class="result-title" style="margin-top: 25px;">True Count:</div>
            <div id="trueCount" class="count-value">0.00</div>
            <div class="count-details">Running Count / pozostałe talie</div>
        </div>
        
        <div class="card-types">
            <div class="card-type">
                <h4>Karty Niskie (2-6)</h4>
                <p>+1</p>
                <p style="color: #2a9d8f; font-weight: bold;">Dobre dla gracza</p>
            </div>
            <div class="card-type">
                <h4>Karty Neutralne (7-9)</h4>
                <p>0</p>
                <p style="color: #5a7d9c; font-weight: bold;">Bez wpływu</p>
            </div>
            <div class="card-type">
                <h4>Karty Wysokie (10-A)</h4>
                <p>-1</p>
                <p style="color: #e76f51; font-weight: bold;">Dobre dla krupiera</p>
            </div>
        </div>
        
        <div class="explanation">
            <h3>Jak działa licznik kart w Blackjacku?</h3>
            <p>Licznik kart w systemie Hi-Lo to metoda używana przez graczy w blackjacka do śledzenia proporcji wysokich i niskich kart pozostałych w talii.</p>
            
            <p><strong>Interpretacja wyników:</strong></p>
            <ul>
                <li><strong style="color: var(--accent);">True Count > +3:</strong> Duża przewaga gracza - zwiększ stawkę</li>
                <li><strong style="color: var(--accent);">True Count +1 do +3:</strong> Przewaga gracza - możesz zwiększyć stawkę</li>
                <li><strong>True Count 0:</strong> Neutralna sytuacja</li>
                <li><strong style="color: var(--reset-btn);">True Count ujemny:</strong> Przewaga krupiera - zmniejsz stawkę</li>
            </ul>
            
            <p><strong>Strategia:</strong> Im wyższy True Count, tym większą przewagę ma gracz, ponieważ zwiększa się prawdopodobieństwo otrzymania blackjacka (as + 10) i korzystnych sytuacji przy dobieraniu kart.</p>
        </div>
        
        <div class="footer">
            Licznik kart w Blackjacku | System Hi-Lo | Domyślnie 8 talii
        </div>
    </div>

    <script>
        // Funkcja dodająca kartę do pola tekstowego
        document.querySelectorAll('.card-btn').forEach(button => {
            button.addEventListener('click', function() {
                const card = this.getAttribute('data-card');
                const textarea = document.getElementById('cards');
                const currentValue = textarea.value.trim();
                
                if (currentValue === '') {
                    textarea.value = card;
                } else {
                    // Dodaj przecinek tylko jeśli ostatni znak nie jest przecinkiem
                    if (currentValue.slice(-1) !== ',') {
                        textarea.value += ', ';
                    } else if (currentValue.slice(-1) === ',' && currentValue.slice(-2, -1) !== ' ') {
                        textarea.value += ' ';
                    }
                    textarea.value += card;
                }
                
                // Automatyczne przewijanie do końca
                textarea.scrollTop = textarea.scrollHeight;
            });
        });
        
        // Funkcja obliczająca licznik kart
        function calculateCount() {
            // Pobieranie danych od użytkownika
            const cardsInput = document.getElementById('cards').value;
            const decks = parseInt(document.getElementById('decks').value);
            
            // Czyszczenie danych wejściowych
            const cards = cardsInput
                .split(',')
                .map(card => card.trim().toUpperCase())
                .filter(card => card !== '');
            
            // Obliczanie Running Count
            let runningCount = 0;
            
            cards.forEach(card => {
                if (['2', '3', '4', '5', '6'].includes(card)) {
                    runningCount += 1;
                } else if (['10', 'J', 'Q', 'K', 'A'].includes(card)) {
                    runningCount -= 1;
                }
                // Karty 7,8,9 nie zmieniają licznika (0)
            });
            
            // Obliczanie True Count
            const totalCards = decks * 52;
            const remainingCards = totalCards - cards.length;
            const remainingDecks = Math.max(remainingCards / 52, 0.5); // Minimum 0.5 talii
            
            let trueCount;
            if (remainingDecks > 0) {
                trueCount = (runningCount / remainingDecks).toFixed(2);
            } else {
                trueCount = runningCount > 0 ? '∞' : '-∞';
            }
            
            // Aktualizacja wyników z animacją
            animateValue('runningCount', parseInt(document.getElementById('runningCount').textContent), runningCount, 800);
            animateValue('trueCount', parseFloat(document.getElementById('trueCount').textContent) || 0, trueCount, 800);
        }
        
        // Funkcja animująca zmianę wartości
        function animateValue(id, start, end, duration) {
            const obj = document.getElementById(id);
            let startTimestamp = null;
            const step = (timestamp) => {
                if (!startTimestamp) startTimestamp = timestamp;
                const progress = Math.min((timestamp - startTimestamp) / duration, 1);
                const value = progress * (end - start) + start;
                
                if (id === 'runningCount') {
                    obj.textContent = Math.floor(value);
                } else {
                    obj.textContent = progress === 1 ? end : value.toFixed(2);
                }
                
                if (progress < 1) {
                    window.requestAnimationFrame(step);
                }
            };
            window.requestAnimationFrame(step);
        }
        
        // Funkcja resetująca licznik
        function resetCounter() {
            document.getElementById('cards').value = '';
            animateValue('runningCount', parseInt(document.getElementById('runningCount').textContent), 0, 500);
            animateValue('trueCount', parseFloat(document.getElementById('trueCount').textContent), 0, 500);
        }
        
        // Inicjalizacja
        document.addEventListener('DOMContentLoaded', function() {
            // Dodanie obsługi klawisza Enter w polu tekstowym
            document.getElementById('cards').addEventListener('keydown', function(e) {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    calculateCount();
                }
            });
        });
    </script>
</body>
</html>
