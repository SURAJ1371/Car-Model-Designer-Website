# Car-Model-Designer-Website
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enhanced Live Car Model Designer</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #89fffd, #ef32d9);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            color: #fff;
        }

        .container {
            background: rgba(0, 0, 0, 0.5);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 0 25px rgba(0, 0, 0, 0.4);
            text-align: center;
            width: 90%;
            max-width: 600px;
        }

        h1 {
            font-size: 2em;
            margin-bottom: 20px;
            color: #ffdd57;
        }

        .car {
            position: relative;
            width: 300px;
            height: 150px;
            margin-bottom: 20px;
            transition: transform 0.5s ease-in-out;
        }

        .car-body {
            background-color: red;
            width: 100%;
            height: 80px;
            border-radius: 30px;
            position: absolute;
            top: 30px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.4);
            transition: background-color 0.3s ease;
        }

        .car-roof {
            background-color: red;
            width: 120px;
            height: 50px;
            border-radius: 10px 10px 0 0;
            position: absolute;
            top: 0;
            left: 90px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
            transition: background-color 0.3s ease, visibility 0.3s ease;
        }

        .car-wheels {
            position: absolute;
            bottom: 0;
            width: 100%;
            display: flex;
            justify-content: space-between;
            padding: 0 10px;
        }

        .wheel {
            background-color: black;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.7);
            transition: background-color 0.3s ease;
        }

        .controls {
            display: flex;
            justify-content: space-around;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        .control-group {
            margin: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        label {
            margin-bottom: 5px;
            display: block;
            font-weight: bold;
            color: #ffdd57;
        }

        input[type="color"],
        input[type="range"],
        select {
            padding: 8px;
            border-radius: 5px;
            border: 2px solid #ffdd57;
            background: rgba(0, 0, 0, 0.2);
            color: #fff;
            text-align: center;
            transition: all 0.3s ease;
            width: 150px;
            margin-top: 5px;
        }

        input[type="range"] {
            width: 160px;
        }

        input[type="color"]:hover,
        select:hover,
        input[type="range"]:hover {
            border-color: #fff;
            cursor: pointer;
        }

        .car-position-control {
            display: flex;
            justify-content: space-between;
            width: 200px;
            margin-top: 10px;
        }

        .car-position-control button {
            padding: 10px;
            border: none;
            border-radius: 50%;
            background: rgba(255, 221, 87, 0.8);
            color: #000;
            font-size: 18px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
            cursor: pointer;
            transition: transform 0.2s ease;
        }

        .car-position-control button:hover {
            transform: scale(1.1);
        }

        .car-position-control button:active {
            transform: scale(0.9);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Enhanced Live Car Model Designer</h1>
        <div class="car" id="car">
            <div class="car-body" id="car-body"></div>
            <div class="car-roof" id="car-roof"></div>
            <div class="car-wheels">
                <div class="wheel" id="wheel-left"></div>
                <div class="wheel" id="wheel-right"></div>
            </div>
        </div>
        <div class="controls">
            <div class="control-group">
                <label for="body-color">Car Body Color:</label>
                <input type="color" id="body-color" value="#ff0000">
            </div>
            <div class="control-group">
                <label for="wheel-color">Wheel Color:</label>
                <input type="color" id="wheel-color" value="#000000">
            </div>
            <div class="control-group">
                <label for="roof-toggle">Toggle Roof:</label>
                <select id="roof-toggle">
                    <option value="visible">With Roof</option>
                    <option value="hidden">Without Roof</option>
                </select>
            </div>
            <div class="control-group">
                <label for="car-size">Car Size:</label>
                <input type="range" id="car-size" min="50" max="150" value="100">
            </div>
            <div class="control-group car-position-control">
                <button id="move-left">&larr;</button>
                <button id="move-right">&rarr;</button>
            </div>
        </div>
    </div>

    <script>
        const carBody = document.getElementById('car-body');
        const carRoof = document.getElementById('car-roof');
        const wheelLeft = document.getElementById('wheel-left');
        const wheelRight = document.getElementById('wheel-right');
        const car = document.getElementById('car');

        // Change car body color
        document.getElementById('body-color').addEventListener('input', function() {
            carBody.style.backgroundColor = this.value;
            carRoof.style.backgroundColor = this.value;
        });

        // Change wheel color
        document.getElementById('wheel-color').addEventListener('input', function() {
            wheelLeft.style.backgroundColor = this.value;
            wheelRight.style.backgroundColor = this.value;
        });

        // Toggle roof visibility
        document.getElementById('roof-toggle').addEventListener('change', function() {
            carRoof.style.visibility = this.value;
        });

        // Resize car
        document.getElementById('car-size').addEventListener('input', function() {
            const scale = this.value / 100;
            car.style.transform = `scale(${scale})`;
        });

        // Move car position
        document.getElementById('move-left').addEventListener('click', function() {
            const currentPosition = parseInt(window.getComputedStyle(car).left) || 0;
            car.style.left = (currentPosition - 20) + 'px';
        });

        document.getElementById('move-right').addEventListener('click', function() {
            const currentPosition = parseInt(window.getComputedStyle(car).left) || 0;
            car.style.left = (currentPosition + 20) + 'px';
        });
    </script>
</body>
</html>
