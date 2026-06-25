<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For You ❤️</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ffeef8 0%, #ffd3eb 100%);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            text-align: center;
        }

        .card {
            background: rgba(255, 255, 255, 0.9);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(224, 76, 145, 0.15);
            max-width: 500px;
            width: 90%;
            transition: all 0.5s ease;
        }

        .gif-container img {
            max-width: 200px;
            margin-bottom: 20px;
            border-radius: 10px;
        }

        h1 {
            color: #d11a5b;
            font-size: 2rem;
            margin-bottom: 10px;
        }

        p {
            color: #555;
            font-size: 1.1rem;
            margin-bottom: 30px;
            line-height: 1.5;
        }

        .btn-group {
            display: flex;
            justify-content: center;
            gap: 20px;
            position: relative;
            height: 50px;
        }

        button {
            padding: 12px 35px;
            font-size: 1.1rem;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.2s ease, background-color 0.2s ease;
        }

        #yesBtn {
            background-color: #e04c91;
            color: white;
            box-shadow: 0 5px 15px rgba(224, 76, 145, 0.4);
        }

        #yesBtn:hover {
            transform: scale(1.1);
            background-color: #cc3b7d;
        }

        #noBtn {
            background-color: #94a3b8;
            color: white;
            position: absolute;
            transition: left 0.15s ease, top 0.15s ease;
        }

        /* Success screen changes */
        .celebrate h1 {
            color: #22c55e;
        }
    </style>
</head>
<body>

    <div class="card" id="proposalCard">
        <div class="gif-container">
            <!-- Using a cute placeholder gif, you can change this URL later -->
            <img id="mainGif" src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExM3N0N3g3b3Y5dmpxcHhodW54NTh0Znd0M3VndXg2YWhvOG9pYThmZCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/9f2hmeIcG7W7G6EMp7/giphy.gif" alt="Cute bear">
        </div>
        <h1 id="questionTitle">Will you make me the happiest person and be mine forever? 💍</h1>
        <p id="subText">I promise to always share my snacks and love you unconditionally.</p>

        <div class="btn-group" id="btnGroup">
            <button id="yesBtn" onclick="celebrate()">Yes!</button>
            <button id="noBtn" onmouseover="moveNoButton()" onclick="moveNoButton()">No</button>
        </div>
    </div>

    <script>
        const noBtn = document.getElementById('noBtn');
        const yesBtn = document.getElementById('yesBtn');
        const card = document.getElementById('proposalCard');
        const title = document.getElementById('questionTitle');
        const subText = document.getElementById('subText');
        const gif = document.getElementById('mainGif');
        const btnGroup = document.getElementById('btnGroup');

        // Initial setup for No button absolute positioning constraints
        // This keeps it within the button group container initially
        noBtn.style.left = 'calc(50% + 10px)';

        function moveNoButton() {
            // Get screen dimensions to avoid throwing the button off-screen
            const padding = 50;
            const maxX = window.innerWidth - noBtn.offsetWidth - padding;
            const maxY = window.innerHeight - noBtn.offsetHeight - padding;

            // Generate completely random coordinates anywhere on the page
            const randomX = Math.max(padding, Math.floor(Math.random() * maxX));
            const randomY = Math.max(padding, Math.floor(Math.random() * maxY));

            // Switch to fixed positioning once it starts moving so it can escape the card container
            noBtn.style.position = 'fixed';
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
            
            // Subtle psychological trick: Every time she attempts to click 'No', the 'Yes' button gets slightly bigger
            const currentScale = parseFloat(yesBtn.style.transform.replace('scale(', '').replace(')', '')) || 1;
            if (currentScale < 2.5) {
                yesBtn.style.transform = `scale(${currentScale + 0.15})`;
            }
        }

        function celebrate() {
            // Remove the rogue "No" button entirely
            noBtn.remove();
            
            // Reset Yes button scale back to normal
            yesBtn.style.transform = 'scale(1)';
            yesBtn.remove(); // Remove button group clean look

            // Update content to celebrate
            card.classList.add('celebrate');
            title.innerHTML = "YAYY! I knew you'd say yes! ❤️🎉";
            subText.innerHTML = "Can't wait to spend the rest of my days with you. Get ready for a lifetime of adventures!";
            
            // Change to a happy celebration gif
            gif.src = "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMms0Y201ODZ6eWxsOHZib3ZndG5rZWZmbm42Y2xmdjd0cGZwbDBybCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/LYD5TeqYSuS8S3o1nB/giphy.gif";
            
            // Optional: You can trigger browser confetti here if you want to link an external script later!
        }
    </script>
</body>
</html>
