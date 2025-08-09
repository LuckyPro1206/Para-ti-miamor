# Para-ti-miamor
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Imagen a Números RGB</title>
</head>
<body>
    <h1>Convertir imagen a números (RGB)</h1>
    <input type="file" id="fileInput" accept="image/*">
    <pre id="output"></pre>

    <canvas id="canvas" style="display:none;"></canvas>

    <script>
        const fileInput = document.getElementById('fileInput');
        const output = document.getElementById('output');
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

        fileInput.addEventListener('change', function(event) {
            const file = event.target.files[0];
            if (!file) return;

            const img = new Image();
            img.onload = function() {
                canvas.width = img.width;
                canvas.height = img.height;
                ctx.drawImage(img, 0, 0);
                const imageData = ctx.getImageData(0, 0, img.width, img.height).data;

                let numbers = [];
                for (let i = 0; i < imageData.length; i += 4) {
                    let r = imageData[i];
                    let g = imageData[i + 1];
                    let b = imageData[i + 2];
                    numbers.push(${r},${g},${b});
                }
                output.textContent = numbers.join(" ");
            };
            img.src = URL.createObjectURL(file);
        });
    </script>
</body>
</html>
