<!DOCTYPE html>
<html>
<head>
    <title>Power, Energy, and Total Charge Calculator</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">
    <style>
        .data-box {
            border: 2px solid black;
            padding: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="mt-5" justify-content="center" align-items="center" display= "flex">Power, Energy, and Total Charge Calculator</h1>
        
        <form method="post" action="" class="mt-4">
            <div class="form-group">
                <label for="voltage">Voltage (V):</label>
                <input type="number" step="0.01" class="form-control" id="voltage" name="voltage" required>
            </div>
            <div class="form-group">
                <label for="current">Current (A):</label>
                <input type="number" step="0.01" class="form-control" id="current" name="current" required>
            </div>
            <div class="form-group">
                <label for="currentrate">Current Rate (per kWh):</label>
                <input type="number" step="0.01" class="form-control" id="currentrate" name="currentrate" required>
            </div>
            <button type="submit" class="btn btn-primary" justify-content="center" align-items="center" display= "flex">Calculate</button><br><br>
        </form>
        
        <?php
        if ($_SERVER["REQUEST_METHOD"] == "POST") {
            $voltage = $_POST["voltage"];
            $current = $_POST["current"];
            $currentrate = $_POST["currentrate"];
            
            // Calculate power (P = I * V)
            $power = $voltage * $current; // Assuming voltage is constant at 1V
            
            // Calculate charge (Q = E / rate)
            $rate = $currentrate/100;
            ?>

            <div class="data-box">
                <?php
                    echo "<p>Power: " . $power . " kw</p>";
                    echo "<p>Rate: " . $rate . " Wh</p>";
                ?>
            </div>

            <?php
            $hour = 1;

            // Calculate energy (E = P * t * 1000)
            $energy = $power * $hour * 1000;
            
            // Calculate total charge (Q = E * (currentrate/100))
            $total = $energy * ($currentrate/100);

            echo "<table class='table mt-4'>";
            echo "<thead>";
            echo "<tr>";
            echo "<th>#</th>";
            echo "<th>Hour</th>";
            echo "<th>Energy (Watt-hours)</th>";
            echo "<th>Total (kWh)</th>";
            echo "</tr>";
            echo "</thead>";
            echo "<tbody>";
            
            for ($hour = 1; $hour <= 24; $hour++) {
                
                // Calculate power (P = V * A)
                $power = $voltage * $current; // Assuming voltage is constant at 1V
            
                // Calculate energy (E = P * t * 1000)
                $energy = $power * $hour * 1000;
                        
                // Calculate total charge (Q = E * (currentrate/100))
                $total = $energy * ($currentrate/100);

                echo "<tr>";
                echo "<td>{$hour}</td>";
                echo "<td>{$hour}</td>";
                echo "<td>{$energy}</td>";
                echo "<td>{$total}</td>";
                echo "</tr>";

            }
            
            echo "</tbody>";
            echo "</table>";
        }
        ?>
    </div>
</body>
</html>
