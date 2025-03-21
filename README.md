<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Turnover Rate & Cost Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        .calculator {
            max-width: 400px;
            margin: auto;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 10px;
            box-shadow: 2px 2px 12px rgba(0, 0, 0, 0.1);
        }
        input {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            padding: 10px 20px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        .result {
            font-size: 20px;
            margin-top: 20px;
        }
        .message {
            font-size: 18px;
            margin-top: 20px;
            padding: 15px;
            border-radius: 10px;
        }
        .good { background-color: #d4edda; color: #155724; }
        .mild { background-color: #fff3cd; color: #856404; }
        .high { background-color: #f8d7da; color: #721c24; }
        .schedule-btn {
            margin-top: 15px;
            display: inline-block;
            padding: 10px 15px;
            background-color: #28a745;
            color: #fff;
            text-decoration: none;
            border-radius: 5px;
        }
        .schedule-btn:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <h2>Turnover Rate & Cost Calculator</h2>
        <label for="employeesLeft">Employees Who Left:</label>
        <input type="number" id="employeesLeft" placeholder="Enter number of employees who left">
        
        <label for="averageEmployees">Average Number of Employees:</label>
        <input type="number" id="averageEmployees" placeholder="Enter average number of employees">
        
        <label for="hourlyWage">Average Hourly Wage ($):</label>
        <input type="number" id="hourlyWage" placeholder="Enter hourly wage">
        
        <button onclick="calculateTurnover()">Calculate</button>
        
        <div class="result" id="turnoverResult"></div>
        <div class="result" id="turnoverCost"></div>
        <div id="followUpMessage"></div>
    </div>

    <script>
        function calculateTurnover() {
            let employeesLeft = parseFloat(document.getElementById("employeesLeft").value);
            let averageEmployees = parseFloat(document.getElementById("averageEmployees").value);
            let hourlyWage = parseFloat(document.getElementById("hourlyWage").value);
            let messageDiv = document.getElementById("followUpMessage");

            if (!employeesLeft || !averageEmployees || averageEmployees === 0 || !hourlyWage || hourlyWage === 0) {
                document.getElementById("turnoverResult").innerHTML = "Please enter valid numbers.";
                document.getElementById("turnoverCost").innerHTML = "";
                messageDiv.innerHTML = "";
                return;
            }

            let turnoverRate = (employeesLeft / averageEmployees) * 100;
            let annualSalary = hourlyWage * 40 * 52;
            let turnoverCost = annualSalary * employeesLeft;

            document.getElementById("turnoverResult").innerHTML = `Turnover Rate: ${turnoverRate.toFixed(2)}%`;
            document.getElementById("turnoverCost").innerHTML = `Total Turnover Cost: $${turnoverCost.toLocaleString()}`;

            // Clear previous message
            messageDiv.innerHTML = "";

            // Show follow-up message based on turnover rate
            let message = "";
            let styleClass = "";

            if (turnoverRate < 10) {
                message = "Your turnover rate is low – great work! But even small inefficiencies can cost thousands. Let’s identify hidden savings and boost retention even further.";
                styleClass = "good";
            } else if (turnoverRate >= 10 && turnoverRate <= 20) {
                message = "Your turnover rate is moderate. This could be a sign of underlying issues worth exploring. Let’s talk about it.";
                styleClass = "mild";
            } else {
                message = "High alert! Your turnover rate is high and may be costing your business significantly. Let’s uncover the root cause and fix it.";
                styleClass = "high";
            }

            messageDiv.innerHTML = `<div class="message ${styleClass}">${message}<br><a href="https://calendly.com/thelozadaglobalgennetwork/30min"schedule-btn">Schedule a Free Analysis Call</a></div>`;
        }
    </script>
</body>
</html>
