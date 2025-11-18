<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minimal Marksheet</title>
    <!-- Load Inter font -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        /* --- 1. Base & Reset --- */
        *, *::before, *::after {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        /* Hide number input spinners */
        input[type=number] {
            -moz-appearance: textfield;
            appearance: textfield;
        }
        input[type=number]::-webkit-inner-spin-button,
        input[type=number]::-webkit-outer-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }

        html, body {
            min-height: 100%;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            /* New background to see glass effect */
            background: linear-gradient(135deg, #024950 0%, #0FA4AF 100%); /* Changed */
            display: flex;
            justify-content: center;
            align-items: flex-start;
            padding: 40px 20px;
            min-height: 100vh;
        }

        ::selection {
            background: rgba(0, 122, 255, 0.2);
        }

        /* --- 2. Layout & Main Container --- */
        .container {
            width: 100%;
            max-width: 1400px;
            margin: 0 auto;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
            flex-wrap: wrap;
            gap: 16px;
        }

        header h1 {
            font-size: 2.75rem; /* Changed */
            font-weight: 800; /* Changed */
            color: #FFFFFF; /* Changed */
            letter-spacing: -0.5px;
        }

        .button-group {
            display: flex;
            gap: 12px;
        }

        /* --- 3. Buttons --- */
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            -webkit-tap-highlight-color: transparent;
        }

        .btn-primary {
            /* Golden Ratio Gradient */
            background-image: linear-gradient(135deg, #00E0FF 0%, #007AFF 61.8%, #005ECF 100%);
            color: white;
            box-shadow: 0 4px 15px rgba(0, 122, 255, 0.25);
        }
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 122, 255, 0.3);
        }
        .btn-primary:active {
            transform: translateY(0);
            box-shadow: 0 2px 10px rgba(0, 122, 255, 0.2);
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.2); /* Changed */
            color: #007aff;
            border: 1px solid rgba(255, 255, 255, 0.2); /* Changed */
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
        }
        .btn-secondary:hover {
            transform: translateY(-2px);
            background: rgba(255, 255, 255, 0.9);
            box-shadow: 0 6px 16px rgba(0, 0, 0, 0.08);
        }
        .btn-secondary:active {
            transform: translateY(0);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
        }

        /* --- 4. Glassmorphism Card Style --- */
        .glass-card {
            background: rgba(255, 255, 255, 0.15); /* Changed */
            /* Frosted glass effect */
            backdrop-filter: blur(25px); /* Changed */
            -webkit-backdrop-filter: blur(25px); /* Changed */
            /* Soft border */
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 16px;
            /* Soft shadow */
            box-shadow: 0 10px 40px 0 rgba(0, 0, 0, 0.1); /* Changed */
        }

        /* --- 5. Marksheet Table --- */
        .marksheet-container {
            /* Apply glass card style to container */
            padding: 0;
            overflow: hidden;
            /* Key for mobile responsiveness */
            overflow-x: auto;
        }

        .marksheet-table {
            width: 100%;
            border-collapse: collapse;
            min-width: 900px; /* Force scroll on smaller screens */
        }

        .marksheet-table th, 
        .marksheet-table td {
            padding: 16px 20px;
            text-align: left;
            white-space: nowrap;
        }

        /* Table Header */
        .marksheet-table thead {
            background: rgba(255, 255, 255, 0.1); /* Changed */
        }

        .marksheet-table thead th {
            font-weight: 600;
            color: #AFDDE5; /* Changed */
            font-size: 0.8rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        /* Table Body */
        .marksheet-table tbody tr {
            border-bottom: 1px solid rgba(0, 0, 0, 0.05); /* Faint grid line */
        }

        .marksheet-table tbody tr:last-child {
            border-bottom: none;
        }

        /* Sticky Subject Column */
        .marksheet-table th:first-child,
        .marksheet-table td:first-child {
            position: sticky;
            left: 0;
            background: rgba(255, 255, 255, 0.15); /* Changed */
            text-align: left;
            font-weight: 600;
            color: #FFFFFF; /* Changed */
            /* Add a faint shadow to show it's on top */
            box-shadow: 4px 0 8px rgba(0, 0, 0, 0.03);
            border-right: 1px solid rgba(255, 255, 255, 0.1); /* Changed */
        }
        .marksheet-table th:first-child {
            background: rgba(255, 255, 255, 0.1); /* Changed */
        }

        /* Table Footer */
        .marksheet-table tfoot tr {
            border-top: 2px solid rgba(0, 0, 0, 0.1);
            background: rgba(245, 245, 247, 0.8);
        }

        .marksheet-table tfoot th,
        .marksheet-table tfoot td {
            font-weight: 700;
            font-size: 1.1rem;
            color: #FFFFFF; /* Changed */
        }
        .marksheet-table tfoot td {
            text-align: center;
        }

        /* --- 6. Input & Calculated Cells --- */
        .mark-input {
            width: 60px;
            padding: 10px;
            border: 1px solid rgba(255, 255, 255, 0.2); /* Changed */
            border-radius: 8px;
            background: rgba(255, 255, 255, 0.2); /* Changed */
            font-size: 1rem;
            text-align: center;
            font-weight: 500;
            transition: all 0.2s ease;
            color: #FFFFFF; /* Changed */
        }

        .mark-input::placeholder {
            color: #AFDDE5; /* Changed */
            font-weight: 400;
            opacity: 0.8; /* Added */
        }

        .mark-input:focus {
            outline: none;
            border-color: #007aff;
            background: rgba(255, 255, 255, 0.4); /* Changed */
            box-shadow: 0 0 0 4px rgba(0, 122, 255, 0.15);
        }

        /* Validation & Color Coding */
        .mark-input.invalid {
            border-color: #ff3b30;
            background: #fff0f0;
            color: #d90000;
        }
        .mark-input.valid-green {
            border-color: #34c759;
            background: #f0fff5;
            color: #00631d;
        }
        .mark-input.valid-yellow {
            border-color: #ffcc00;
            background: #fffcf0;
            color: #7a5f00;
        }

        .cell-total, .cell-perc, .cell-grade {
            font-weight: 600;
            text-align: center;
            font-size: 1rem;
            color: #FFFFFF; /* Changed */
        }

        .cell-grade {
            font-weight: 700;
            font-size: 1.1rem;
            color: #FFFFFF; /* Changed */
        }

        /* --- 7. Custom Modal (for Clear All) --- */
        .modal-backdrop {
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(4px);
            -webkit-backdrop-filter: blur(4px);
            z-index: 100;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.2s ease;
        }
        
        .modal-content {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 101;
            /* Re-use glass card style */
            background: rgba(255, 255, 255, 0.8); /* Changed */
            backdrop-filter: blur(25px); /* Changed */
            -webkit-backdrop-filter: blur(25px); /* Changed */
            border: 1px solid rgba(255, 255, 255, 0.3); /* Changed */
            border-radius: 16px;
            box-shadow: 0 10px 40px 0 rgba(0, 0, 0, 0.15);
            padding: 24px;
            width: 90%;
            max-width: 400px;
            opacity: 0;
            visibility: hidden;
            transform: translate(-50%, -45%);
            transition: all 0.2s ease;
        }

        .modal-content h3 {
            font-weight: 700;
            font-size: 1.25rem;
            margin-bottom: 12px;
        }

        .modal-content p {
            font-size: 1rem;
            color: #555;
            margin-bottom: 24px;
        }

        .modal-buttons {
            display: flex;
            justify-content: flex-end;
            gap: 12px;
        }
        .btn-danger {
            background: #ff3b30;
            color: white;
            box-shadow: 0 4px 12px rgba(255, 59, 48, 0.2);
        }
        .btn-danger:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 16px rgba(255, 59, 48, 0.3);
        }

        /* Modal active state */
        .modal-backdrop.active,
        .modal-content.active {
            opacity: 1;
            visibility: visible;
        }
        .modal-content.active {
             transform: translate(-50%, -50%);
        }

        /* --- 8. Mobile Responsiveness --- */
        @media (max-width: 768px) {
            body {
                padding: 20px 10px;
            }

            header {
                flex-direction: column;
                align-items: flex-start;
                margin-bottom: 20px;
            }

            header h1 {
                font-size: 2rem;
            }

            .marksheet-table {
                min-width: 0; /* Allow table to be smaller */
            }

            .marksheet-container {
                /* Container is now the scroller */
                width: 100%;
            }

            .marksheet-table th, 
            .marksheet-table td {
                padding: 12px 14px;
                font-size: 0.9rem;
            }

            .mark-input {
                width: 100%;
                min-width: 50px; /* Ensure tap target */
                padding: 12px 8px;
                font-size: 1rem;
            }

            .cell-total, .cell-perc, .cell-grade {
                font-size: 0.9rem;
            }
            .cell-grade {
                font-size: 1rem;
            }
        }

        /* --- 9. Print Styles --- */
        @media print {
            @page {
                size: A4 landscape;
                margin: 1cm;
            }

            body {
                background: #fff;
                padding: 0;
                font-family: sans-serif;
            }

            header, .button-group, .modal-backdrop, .modal-content {
                display: none !important;
            }

            .container {
                max-width: 100%;
                width: 100%;
                padding: 0;
                margin: 0;
            }

            .marksheet-container {
                box-shadow: none;
                border: 1px solid #ccc;
                backdrop-filter: none;
                background: #fff;
                padding: 0;
                overflow: visible;
            }

            .marksheet-table {
                font-size: 10pt;
                width: 100%;
                min-width: 0;
                border: 1px solid #ccc;
            }

            .marksheet-table th, 
            .marksheet-table td {
                padding: 8px 12px;
                color: #000;
                border: 1px solid #eee;
            }

            /* Remove sticky positioning for print */
            .marksheet-table th:first-child,
            .marksheet-table td:first-child {
                position: static;
                background: #fff;
                box-shadow: none;
                border-right: 1px solid #eee;
            }

            .marksheet-table thead {
                background: #f8f8f8;
            }

            .mark-input {
                border: none;
                background: transparent;
                padding: 0;
                text-align: center;
                width: auto;
                color: #000;
                font-weight: 500;
                font-size: 10pt;
            }
            
            /* Remove validation colors for print */
            .mark-input.invalid,
            .mark-input.valid-green,
            .mark-input.valid-yellow {
                border: none;
                background: transparent;
                color: #000;
            }

            .marksheet-table tfoot tr {
                border-top: 2px solid #000;
            }
        }
    </style>
</head>
<body>

    <main class="container">
        <header>
            <h1>Marksheet</h1>
            <div class="button-group">
                <button id="clear-btn" class="btn btn-secondary">Clear All</button>
                <button id="export-btn" class="btn btn-primary">Export PDF</button>
            </div>
        </header>

        <div class="marksheet-container glass-card">
            <table class="marksheet-table">
                <thead>
                    <tr>
                        <th>Subject</th>
                        <th>1st Sum (40)</th>
                        <th>Proj 1 (10)</th>
                        <th>2nd Sum (40)</th>
                        <th>Proj 2 (10)</th>
                        <th>3rd Sum (90)</th>
                        <th>Proj 3 (10)</th>
                        <th>Total (200)</th>
                        <th>Percent (%)</th>
                        <th>Grade</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Row: Bengali -->
                    <tr id="row-bengali">
                        <td>Bengali</td>
                        <td><input type="number" id="bengali-s1" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="bengali-p1" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="bengali-s2" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="bengali-p2" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="bengali-s3" class="mark-input" placeholder="—" data-max="90"></td>
                        <td><input type="number" id="bengali-p3" class="mark-input" placeholder="—" data-max="10"></td>
                        <td id="bengali-total" class="cell-total">— / 200</td>
                        <td id="bengali-perc" class="cell-perc">—</td>
                        <td id="bengali-grade" class="cell-grade">—</td>
                    </tr>
                    <!-- Row: English -->
                    <tr id="row-english">
                        <td>English</td>
                        <td><input type="number" id="english-s1" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="english-p1" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="english-s2" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="english-p2" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="english-s3" class="mark-input" placeholder="—" data-max="90"></td>
                        <td><input type="number" id="english-p3" class="mark-input" placeholder="—" data-max="10"></td>
                        <td id="english-total" class="cell-total">— / 200</td>
                        <td id="english-perc" class="cell-perc">—</td>
                        <td id="english-grade" class="cell-grade">—</td>
                    </tr>
                    <!-- Row: Geography -->
                    <tr id="row-geography">
                        <td>Geography</td>
                        <td><input type="number" id="geography-s1" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="geography-p1" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="geography-s2" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="geography-p2" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="geography-s3" class="mark-input" placeholder="—" data-max="90"></td>
                        <td><input type="number" id="geography-p3" class="mark-input" placeholder="—" data-max="10"></td>
                        <td id="geography-total" class="cell-total">— / 200</td>
                        <td id="geography-perc" class="cell-perc">—</td>
                        <td id="geography-grade" class="cell-grade">—</td>
                    </tr>
                    <!-- Row: History -->
                    <tr id="row-history">
                        <td>History</td>
                        <td><input type="number" id="history-s1" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="history-p1" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="history-s2" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="history-p2" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="history-s3" class="mark-input" placeholder="—" data-max="90"></td>
                        <td><input type="number" id="history-p3" class="mark-input" placeholder="—" data-max="10"></td>
                        <td id="history-total" class="cell-total">— / 200</td>
                        <td id="history-perc" class="cell-perc">—</td>
                        <td id="history-grade" class="cell-grade">—</td>
                    </tr>
                    <!-- Row: Physics -->
                    <tr id="row-physics">
                        <td>Physics</td>
                        <td><input type="number" id="physics-s1" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="physics-p1" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="physics-s2" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="physics-p2" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="physics-s3" class="mark-input" placeholder="—" data-max="90"></td>
                        <td><input type="number" id="physics-p3" class="mark-input" placeholder="—" data-max="10"></td>
                        <td id="physics-total" class="cell-total">— / 200</td>
                        <td id="physics-perc" class="cell-perc">—</td>
                        <td id="physics-grade" class="cell-grade">—</td>
                    </tr>
                    <!-- Row: Biology -->
                    <tr id="row-biology">
                        <td>Biology</td>
                        <td><input type="number" id="biology-s1" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="biology-p1" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="biology-s2" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="biology-p2" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="biology-s3" class="mark-input" placeholder="—" data-max="90"></td>
                        <td><input type="number" id="biology-p3" class="mark-input" placeholder="—" data-max="10"></td>
                        <td id="biology-total" class="cell-total">— / 200</td>
                        <td id="biology-perc" class="cell-perc">—</td>
                        <td id="biology-grade" class="cell-grade">—</td>
                    </tr>
                    <!-- Row: Math -->
                    <tr id="row-math">
                        <td>Math</td>
                        <td><input type="number" id="math-s1" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="math-p1" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="math-s2" class="mark-input" placeholder="—" data-max="40"></td>
                        <td><input type="number" id="math-p2" class="mark-input" placeholder="—" data-max="10"></td>
                        <td><input type="number" id="math-s3" class="mark-input" placeholder="—" data-max="90"></td>
                        <td><input type="number" id="math-p3" class="mark-input" placeholder="—" data-max="10"></td>
                        <td id="math-total" class="cell-total">— / 200</td>
                        <td id="math-perc" class="cell-perc">—</td>
                        <td id="math-grade" class="cell-grade">—</td>
                    </tr>
                </tbody>
                <tfoot>
                    <tr>
                        <th>Overall Total</th>
                        <td colspan="6"></td> <!-- Empty cells to push total over -->
                        <td id="overall-total" class="cell-total">— / 1400</td>
                        <td id="overall-perc" class="cell-perc">—</td>
                        <td id="overall-grade" class="cell-grade">—</td>
                    </tr>
                </tfoot>
            </table>
        </div>
    </main>

    <!-- Custom Modal for Clear All -->
    <div class="modal-backdrop" id="modal-backdrop"></div>
    <div class="modal-content" id="modal-content">
        <h3>Clear All Data</h3>
        <p>Are you sure you want to clear all marks? This action cannot be undone and will remove all saved data.</p>
        <div class="modal-buttons">
            <button id="modal-cancel-btn" class="btn btn-secondary">Cancel</button>
            <button id="modal-confirm-btn" class="btn btn-danger">Clear Data</button>
        </div>
    </div>


    <script>
        document.addEventListener('DOMContentLoaded', () => {

            // --- 1. Constants ---
            const SUBJECTS = ['bengali', 'english', 'geography', 'history', 'physics', 'biology', 'math'];
            const INPUT_IDS = ['s1', 'p1', 's2', 'p2', 's3', 'p3'];
            const MAX_MARKS = { 's1': 40, 'p1': 10, 's2': 40, 'p2': 10, 's3': 90, 'p3': 10 };
            const SUBJECT_TOTAL_MAX = 200;
            const GRAND_TOTAL_MAX = 1400;

            // --- 2. Selectors ---
            const allInputs = document.querySelectorAll('.mark-input');
            const clearBtn = document.getElementById('clear-btn');
            const exportBtn = document.getElementById('export-btn');
            const modalBackdrop = document.getElementById('modal-backdrop');
            const modalContent = document.getElementById('modal-content');
            const modalCancelBtn = document.getElementById('modal-cancel-btn');
            const modalConfirmBtn = document.getElementById('modal-confirm-btn');

            // --- 3. Utility Functions ---

            /**
             * Debounce function to limit API calls or expensive operations
             */
            function debounce(func, delay) {
                let timeout;
                return function(...args) {
                    clearTimeout(timeout);
                    timeout = setTimeout(() => func.apply(this, args), delay);
                };
            }

            /**
             * Gets grade based on percentage
             */
            function getGrade(percentage) {
                if (percentage === null || isNaN(percentage)) return '—';
                if (percentage >= 90) return 'A+';
                if (percentage >= 80) return 'A';
                if (percentage >= 70) return 'B+';
                if (percentage >= 60) return 'B';
                if (percentage >= 45) return 'C+';
                if (percentage >= 25) return 'C';
                if (percentage >= 0) return 'D';
                return '—';
            }

            // --- 4. Modal Logic ---
            function showModal() {
                modalBackdrop.classList.add('active');
                modalContent.classList.add('active');
            }

            function hideModal() {
                modalBackdrop.classList.remove('active');
                modalContent.classList.remove('active');
            }

            // --- 5. Core Calculation Logic ---

            /**
             * Validates a single input, styles it, and returns its value
             */
            function validateAndStyleInput(input) {
                const max = parseFloat(input.dataset.max);
                const value = input.value;

                // Reset styles
                input.classList.remove('invalid', 'valid-green', 'valid-yellow');

                if (value === '') {
                    return { valid: true, value: null }; // Blank is valid
                }

                const numValue = parseFloat(value);

                if (isNaN(numValue) || numValue < 0 || numValue > max) {
                    input.classList.add('invalid');
                    return { valid: false, value: null }; // Invalid
                }

                // Apply valid color coding
                const perc = (numValue / max) * 100;
                if (perc >= 75) {
                    input.classList.add('valid-green');
                } else if (perc >= 50) {
                    input.classList.add('valid-yellow');
                }

                return { valid: true, value: numValue };
            }

            /**
             * Calculates total, percentage, and grade for a single subject
             */
            function calculateSubject(subject) {
                let total = 0;
                let allValid = true;
                let allBlank = true;

                for (const id of INPUT_IDS) {
                    const inputEl = document.getElementById(`${subject}-${id}`);
                    const { valid, value } = validateAndStyleInput(inputEl);

                    if (!valid) {
                        allValid = false;
                    }
                    if (value !== null) {
                        allBlank = false;
                        total += value;
                    }
                }

                // Get UI elements to update
                const totalEl = document.getElementById(`${subject}-total`);
                const percEl = document.getElementById(`${subject}-perc`);
                const gradeEl = document.getElementById(`${subject}-grade`);

                if (allBlank) {
                    totalEl.textContent = '— / 200';
                    percEl.textContent = '—';
                    gradeEl.textContent = '—';
                    return { subjectTotal: null, subjectPercentage: null };
                }
                
                if (!allValid) {
                    totalEl.textContent = '— / 200';
                    percEl.textContent = '—';
                    gradeEl.textContent = '—';
                    return { subjectTotal: null, subjectPercentage: null };
                }

                const percentage = (total / SUBJECT_TOTAL_MAX) * 100;
                totalEl.textContent = `${total} / 200`;
                percEl.textContent = `${percentage.toFixed(1)}%`;
                gradeEl.textContent = getGrade(percentage);

                return { subjectTotal: total, subjectPercentage: percentage };
            }

            /**
             * Calculates the overall total, percentage, and grade
             */
            function calculateOverall() {
                let grandTotal = 0;
                let allSubjectsBlank = true;

                for (const subject of SUBJECTS) {
                    const { subjectTotal } = calculateSubject(subject);
                    if (subjectTotal !== null) {
                        allSubjectsBlank = false;
                        grandTotal += subjectTotal;
                    }
                }

                // Get UI elements
                const overallTotalEl = document.getElementById('overall-total');
                const overallPercEl = document.getElementById('overall-perc');
                const overallGradeEl = document.getElementById('overall-grade');

                if (allSubjectsBlank) {
                    overallTotalEl.textContent = `— / ${GRAND_TOTAL_MAX}`;
                    overallPercEl.textContent = '—';
                    overallGradeEl.textContent = '—';
                } else {
                    const grandPercentage = (grandTotal / GRAND_TOTAL_MAX) * 100;
                    overallTotalEl.textContent = `${grandTotal} / ${GRAND_TOTAL_MAX}`;
                    overallPercEl.textContent = `${grandPercentage.toFixed(1)}%`;
                    overallGradeEl.textContent = getGrade(grandPercentage);
                }
            }
            
            // Debounced version for performance
            const debouncedCalculateOverall = debounce(calculateOverall, 50);

            // --- 6. Data Persistence (localStorage) ---

            /**
             * Saves all input values to localStorage
             */
            function saveData() {
                const data = {};
                allInputs.forEach(input => {
                    data[input.id] = input.value;
                });
                localStorage.setItem('marksheetData', JSON.stringify(data));
            }

            const debouncedSaveData = debounce(saveData, 350);

            /**
             * Loads data from localStorage and recalculates all fields
             */
            function loadData() {
                const data = JSON.parse(localStorage.getItem('marksheetData'));
                if (data) {
                    allInputs.forEach(input => {
                        if (data[input.id] !== undefined) {
                            input.value = data[input.id];
                        }
                    });
                }
                // Run calculations on load
                calculateOverall(); // This will call calculateSubject for all
            }

            /**
             * Clears all data from inputs and localStorage
             */
            function clearAllData() {
                localStorage.removeItem('marksheetData');
                allInputs.forEach(input => {
                    input.value = '';
                });
                // Recalculate to reset UI
                calculateOverall();
                hideModal();
            }

            // --- 7. Event Listeners ---

            // Calculate on input
            allInputs.forEach(input => {
                input.addEventListener('input', () => {
                    // Recalculate everything.
                    // calculateOverall() triggers calculateSubject() for all rows.
                    debouncedCalculateOverall();
                    // Save data
                    debouncedSaveData();
                });
            });

            // Button listeners
            exportBtn.addEventListener('click', () => {
                window.print();
            });

            clearBtn.addEventListener('click', showModal);

            // Modal button listeners
            modalCancelBtn.addEventListener('click', hideModal);
            modalBackdrop.addEventListener('click', hideModal);
            modalConfirmBtn.addEventListener('click', clearAllData);

            // --- 8. Initial Load ---
            loadData();

        });
    </script>
</body>
</html>


