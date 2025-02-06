<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Propuesta de San Valentín</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #ffe6e6;
            font-family: Arial, sans-serif;
            overflow: hidden;
        }

        .container {
            text-align: center;
            padding: 2rem;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            position: relative;
            z-index: 1;
        }

        .bears {
            font-size: 3rem;
            margin-bottom: 1rem;
            white-space: pre;
        }

        .message {
            font-size: 1.5rem;
            margin-bottom: 2rem;
            color: #ff4d6d;
        }

        .buttons {
            display: flex;
            justify-content: center;
            gap: 1rem;
        }

        .btn {
            padding: 1rem 2rem;
            font-size: 1.2rem;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .btn:hover {
            transform: scale(1.1);
        }

        .btn-yes {
            background-color: #ff4d6d;
            color: white;
        }

        .btn-no {
            background-color: #ffffff;
            color: #ff4d6d;
            border: 2px solid #ff4d6d;
            position: relative;
        }

        .success-screen {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: #ff87ab;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 2rem;
            z-index: 2;
        }

        .heart {
            position: absolute;
            font-size: 2rem;
            color: #ff4d6d;
            pointer-events: none;
            animation: float 3s infinite;
        }

        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
            100% { transform: translateY(0) rotate(360deg); }
        }

        .messages {
            position: fixed;
            top: 10px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 1.2rem;
            color: #ff4d6d;
            text-align: center;
            z-index: 3;
        }
    </style>
</head>
<body>
    <div class="messages"></div>
    
    <div class="container">
        <div class="bears">ʕ •ᴥ•ʔ ♥ ʕ•ᴥ• ʔ</div>
        <div class="message">¿Quieres ser la niña que sea mi cita el 14 de febrero?</div>
        <div class="buttons">
            <button class="btn btn-yes" onclick="acceptProposal()">¡Sí!</button>
            <button class="btn btn-no" onclick="moveButton(this)">No</button>
        </div>
    </div>

    <div class="success-screen">
        <h1>¡Te amo preciosa! 💜🐻</h1>
        <p>¡Sabía que dirías que sí!, TQM a ti y a Paquito 💜🐻</p>
    </div>

    <script>
        let noCount = 0;
        const maxMessages = [
            "¡No seas tímida preciosa! 😊",
            "¡Yo op q el otro botón es mejor! 😉",
            "¿Estás segura? 🤔",
            "¡Inténtalo de nuevo! 💝",
            "¡Xfiiiiis, ti?! 💜🐻",
            "¡Casi le das al Sí! 😘",
            "¡No te resistas al amor! 💖",
            "¡El otro botón brilla más! ✨",
            "¡Yo se que quieres decir que siiiii! 🌹",
            "¡El destino nos une! 💫"
        ];

        function showMessage() {
            const messagesDiv = document.querySelector('.messages');
            const message = maxMessages[Math.floor(Math.random() * maxMessages.length)];
            const messageElement = document.createElement('div');
            messageElement.textContent = message;
            messageElement.style.opacity = '1';
            messagesDiv.appendChild(messageElement);
            
            setTimeout(() => {
                messageElement.style.opacity = '0';
                setTimeout(() => messagesDiv.removeChild(messageElement), 500);
            }, 2000);
        }

        function moveButton(button) {
            noCount++;
            showMessage();
            
            // Reduce el tamaño del botón gradualmente
            const currentWidth = button.offsetWidth;
            const currentHeight = button.offsetHeight;
            button.style.width = `${currentWidth * 0.9}px`;
            button.style.height = `${currentHeight * 0.9}px`;

            // Mueve el botón a una posición aleatoria
            const maxX = window.innerWidth - button.offsetWidth;
            const maxY = window.innerHeight - button.offsetHeight;
            const randomX = Math.random() * maxX;
            const randomY = Math.random() * maxY;
            
            button.style.position = 'fixed';
            button.style.left = randomX + 'px';
            button.style.top = randomY + 'px';

            // Añade un corazón flotante en la posición original
            addFloatingHeart(randomX, randomY);
        }

        function addFloatingHeart(x, y) {
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.textContent = '♥';
            heart.style.left = x + 'px';
            heart.style.top = y + 'px';
            document.body.appendChild(heart);

            setTimeout(() => {
                document.body.removeChild(heart);
            }, 3000);
        }

        function acceptProposal() {
            const container = document.querySelector('.container');
            const successScreen = document.querySelector('.success-screen');
            
            container.style.display = 'none';
            successScreen.style.display = 'flex';
            
            // Añade corazones flotantes aleatorios
            for (let i = 0; i < 50; i++) {
                setTimeout(() => {
                    const x = Math.random() * window.innerWidth;
                    const y = Math.random() * window.innerHeight;
                    addFloatingHeart(x, y);
                }, i * 100);
            }
        }

        // Añade corazones flotantes aleatorios al inicio
        for (let i = 0; i < 10; i++) {
            const x = Math.random() * window.innerWidth;
            const y = Math.random() * window.innerHeight;
            addFloatingHeart(x, y);
        }
    </script>
</body>
</html>
