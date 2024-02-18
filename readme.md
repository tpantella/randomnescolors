<html> 
<head>
    <title>Random NES Colors</title> 
    A site made to generate four colors within the 56 colors that the Nintendo Entertainment System can produce, for visual inspiration.
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            background-image: none;
            background-color: #ffffff;
            overflow: hidden;
        }
        #color-stripes {
            position: fixed;
            top: 0;
            left: 0;
            height: 100vh;
            width: 100vw;
            z-index: -1;
            background: linear-gradient(to right, #000000, #000000 25%, #fcfcfc 25%, #fcfcfc 50%, #f8f8f8 50%, #f8f8f8 75%, #bcbcbc 75%, #bcbcbc);
        }
        h1 {
            text-align: center;
            margin-top: 20px;
        }
        #color-grid {
            text-align: center;
            margin-bottom: 20px;
        }
        .color-square {
            width: 100px;
            height: 100px;
            margin: 10px;
            display: inline-block;
            position: relative;
            border-radius: 5px;
            overflow: hidden;
        }
        .history-row {
            margin-top: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .history-square {
            width: 50px;
            height: 50px;
            margin-right: 10px;
            display: inline-block;
            position: relative;
            border-radius: 5px;
            overflow: hidden;
        }
        .history-square span {
            position: absolute;
            bottom: 2px;
            left: 2px;
            color: white;
            font-size: 12px;
        }
        #current-colors {
            background-color: white;
            padding: 10px;
            border-radius: 10px;
            margin-bottom: 20px;
            display: inline-block;
            text-align: center;
        }
        #current-colors div {
            display: inline-block;
            width: 30px;
            height: 30px;
            margin: 5px;
            border-radius: 5px;
            overflow: hidden;
        }
        button {
            margin: 0 auto;
            display: block;
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            background-color: #ffffff;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div id="color-stripes"></div>
    <h1>Random NES Colors</h1>
    <div id="color-grid"></div>
    <button onclick="refreshColors()">Refresh Colors</button>
    <div id="history"></div>

    <script>
        const colorList = [
            "#000000",
            "#fcfcfc",
            "#f8f8f8",
            "#bcbcbc",
            "#7c7c7c",
            "#a4e4fc",
            "#3cbcfc",
            "#0078f8",
            "#0000fc",
            "#b8b8f8",
            "#6888fc",
            "#0058f8",
            "#0000bc",
            "#d8b8f8",
            "#9878f8",
            "#6844fc",
            "#4428bc",
            "#f8b8f8",
            "#f878f8",
            "#d800cc",
            "#940084",
            "#f8a4c0",
            "#f85898",
            "#e40058",
            "#a80020",
            "#f0d0b0",
            "#f87858",
            "#f83800",
            "#a81000",
            "#fce0a8",
            "#fca044",
            "#e45c10",
            "#881400",
            "#f8d878",
            "#f8b800",
            "#ac7c00",
            "#503000",
            "#d8f878",
            "#b8f818",
            "#00b800",
            "#007800",
            "#b8f8b8",
            "#58d854",
            "#00a800",
            "#006800",
            "#b8f8d8",
            "#58f898",
            "#00a844",
            "#005800",
            "#00fcfc",
            "#00e8d8",
            "#008888",
            "#004058",
            "#f8d8f8",
            "#787878"
        ];

        let history = [];

        function getRandomColors(colorList, numColors) {
            const randomColors = [];
            while (randomColors.length < numColors) {
                const randomColor = colorList[Math.floor(Math.random() * colorList.length)];
                if (!randomColors.includes(randomColor)) {
                    randomColors.push(randomColor);
                }
            }
            return randomColors;
        }

        function displayColors(colors) {
            const colorGrid = document.getElementById("color-grid");
            colorGrid.innerHTML = "";
            colors.forEach((color, index) => {
                const colorSquare = document.createElement("div");
                colorSquare.classList.add("color-square");
                colorSquare.style.backgroundColor = color;
                colorGrid.appendChild(colorSquare);
            });

            // Add white rounded rectangle around topmost four squares
            if (colors.length >= 4) {
                const topFourSquares = document.querySelectorAll(".color-square:nth-child(-n+4)");
                topFourSquares.forEach(square => {
                    square.style.border = "2px solid white";
                    square.style.borderRadius = "5px";
                    square.style.padding = "2px";
                });
            }
        }

        function displayHistory() {
            const historyDiv = document.getElementById("history");
            historyDiv.innerHTML = "<h3 style='text-align:center;'>Previous Combinations:</h3>";
            history.forEach(combination => {
                const row = document.createElement("div");
                row.classList.add("history-row");
                combination.forEach((color, index) => {
                    const square = document.createElement("div");
                    square.classList.add("history-square");
                    square.style.backgroundColor = color;
                    row.appendChild(square);

                    // Add space between hex codes
                    if (index < combination.length - 1) {
                        const space = document.createElement("span");
                        space.textContent = "   ";
                        row.appendChild(space);
                    }
                });
                historyDiv.appendChild(row);
            });
        }

        function refreshColors() {
            const randomColors = getRandomColors(colorList, 4);
            displayColors(randomColors);
            history.push(randomColors);
            displayHistory();
            updateBackgroundStripes(randomColors);
        }

        function updateBackgroundStripes(colors) {
            const colorStripes = document.getElementById("color-stripes");
            colorStripes.style.background = `linear-gradient(to right, ${colors[0]}, ${colors[0]} 25%, ${colors[1]} 25%, ${colors[1]} 50%, ${colors[2]} 50%, ${colors[2]} 75%, ${colors[3]} 75%, ${colors[3]})`;
        }

        refreshColors(); // Display initial colors
    </script>
</body>
</html>

