<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beri Kebebasan — Ruang Refleksi Interaktif</title>
    <style>
        :root {
            --primary-gradient: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
            --bg-gradient: linear-gradient(180deg, #e0f2fe 0%, #f0fdf4 50%, #fffdf5 100%);
            --text-main: #0f172a;
            --text-muted: #475569;
            --card-bg: rgba(255, 255, 255, 0.75);
            --card-border: rgba(255, 255, 255, 0.6);
            --shadow-sm: 0 10px 30px rgba(15, 23, 42, 0.04);
            --shadow-md: 0 20px 40px rgba(15, 23, 42, 0.08);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background: var(--bg-gradient);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            color: var(--text-main);
            text-align: center;
            padding: 24px;
            position: relative;
        }

        /* Latar Belakang Awan Halus */
        .cloud-bg {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 1;
            pointer-events: none;
        }

        .cloud {
            position: absolute;
            background: rgba(255, 255, 255, 0.4);
            border-radius: 100px;
            filter: blur(20px);
            animation: floatClouds 60s linear infinite;
        }

        .cloud-1 { width: 400px; height: 120px; top: 15%; left: -10%; animation-delay: 0s; }
        .cloud-2 { width: 300px; height: 100px; top: 45%; left: -20%; animation-delay: -20s; }
        .cloud-3 { width: 500px; height: 150px; top: 70%; left: -15%; animation-delay: -40s; }

        @keyframes floatClouds {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(calc(100vw + 500px)); }
        }

        /* Kontainer Utama */
        .container {
            max-width: 480px;
            width: 100%;
            background: var(--card-bg);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            padding: 48px 32px;
            border-radius: 32px;
            box-shadow: var(--shadow-md);
            border: 1px solid var(--card-border);
            z-index: 10;
            transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
        }

        .container:hover {
            transform: translateY(-4px);
            box-shadow: 0 30px 60px rgba(15, 23, 42, 0.12);
        }

        /* Tipografi */
        h1 {
            font-size: 2.75rem;
            font-weight: 800;
            margin-bottom: 16px;
            letter-spacing: -0.03em;
            background: linear-gradient(135deg, #1d4ed8 0%, #6d28d9 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        p {
            font-size: 1.125rem;
            color: var(--text-muted);
            margin-bottom: 36px;
            line-height: 1.6;
            font-weight: 400;
        }

        /* Tombol Utama */
        .btn-release {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            padding: 18px 36px;
            font-size: 1.15rem;
            font-weight: 600;
            color: #ffffff;
            background: var(--primary-gradient);
            border: none;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 8px 25px rgba(37, 99, 235, 0.25);
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            outline: none;
            user-select: none;
        }

        .btn-release:hover {
            transform: scale(1.04) translateY(-2px);
            box-shadow: 0 12px 30px rgba(37, 99, 235, 0.35);
        }

        .btn-release:active {
            transform: scale(0.97) translateY(0);
            box-shadow: 0 4px 15px rgba(37, 99, 235, 0.2);
        }

        /* Elemen Burung Merpati yang Terbang */
        .dove {
            position: absolute;
            font-size: 2.5rem;
            user-select: none;
            pointer-events: none;
            z-index: 5;
            will-change: transform, opacity;
            animation: flyUpwards 4.5s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards;
        }

        @keyframes flyUpwards {
            0% {
                transform: translateY(105vh) translateX(0) scale(0.3) rotate(0deg);
                opacity: 0;
            }
            15% {
                opacity: 1;
                transform: translateY(85vh) translateX(calc(var(--sway-1) * 0.2)) scale(0.8) rotate(var(--rot));
            }
            70% {
                opacity: 0.9;
            }
            100% {
                transform: translateY(-15vh) translateX(var(--sway-2)) scale(1.2) rotate(calc(var(--rot) * 1.5));
                opacity: 0;
            }
        }

        /* Kutipan di Bagian Bawah */
        .footer-quote {
            position: absolute;
            bottom: 24px;
            font-size: 0.9rem;
            color: var(--text-muted);
            max-width: 85%;
            line-height: 1.5;
            z-index: 10;
            pointer-events: none;
            font-style: italic;
            opacity: 0.8;
            transition: opacity 0.3s ease;
        }

        body:hover .footer-quote {
            opacity: 1;
        }

        /* Responsif untuk Layar Kecil */
        @media (max-width: 480px) {
            h1 { font-size: 2.25rem; }
            p { font-size: 1rem; margin-bottom: 28px; }
            .btn-release { padding: 16px 32px; font-size: 1.05rem; }
            .container { padding: 36px 24px; }
        }
    </style>
</head>
<body>

    <div class="cloud-bg">
        <div class="cloud cloud-1"></div>
        <div class="cloud cloud-2"></div>
        <div class="cloud cloud-3"></div>
    </div>

    <div class="container">
        <h1>Kebebasan</h1>
        <p>Tekan tombol di bawah untuk melepaskan merpati perdamaian dan memberikan makna pada kebebasan.</p>
        <button class="btn-release" id="releaseBtn">
            Beri Kebebasan <span>🕊️</span>
        </button>
    </div>

    <div class="footer-quote" id="quoteText">
        "Kebebasan sejati bukan sekadar membuang belenggu, melainkan hidup dengan menghormati dan memperjuangkan kebebasan orang lain." — Nelson Mandela
    </div>

    <script>
        const button = document.getElementById('releaseBtn');
        const quoteText = document.getElementById('quoteText');

        // Daftar kutipan reflektif tentang kebebasan
        const quotes = [
            '"Kebebasan sejati bukan sekadar membuang belenggu, melainkan hidup dengan menghormati dan memperjuangkan kebebasan orang lain." — Nelson Mandela',
            '"Kebebasan tidak pernah diberikan secara sukarela oleh penindas; itu harus dituntut oleh yang tertindas." — Martin Luther King Jr.',
            '"Hanya mereka yang membebaskan diri dari ketakutan yang benar-benar merdeka." — Refleksi Kebebasan',
            '"Kebebasan adalah hak untuk memilih apa yang ingin kita lakukan, dan tanggung jawab atas konsekuensi pilihan tersebut." — Jean-Paul Sartre',
            '"Burung yang lahir di sangkar mengira terbang adalah sebuah penyakit." — Alejandro Jodorowsky'
        ];

        button.addEventListener('click', () => {
            // Jumlah merpati yang dirilis setiap klik
            const doveCount = 6;
            
            for (let i = 0; i < doveCount; i++) {
                setTimeout(() => {
                    createDove();
                }, i * 250); // Efek jeda berurutan agar lebih alami
            }

            // Mengubah kutipan secara acak saat tombol ditekan
            const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
            quoteText.style.opacity = 0;
            setTimeout(() => {
                quoteText.innerText = randomQuote;
                quoteText.style.opacity = 1;
            }, 300);
        });

        function createDove() {
            const dove = document.createElement('div');
            dove.classList.add('dove');
            dove.innerText = '🕊️';

            // Menentukan posisi horizontal awal secara acak di sepanjang lebar layar
            const startX = Math.random() * window.innerWidth;
            dove.style.left = `${startX}px`;
            
            // Variasi arah terbang agar terlihat acak dan dinamis (Swaying effect)
            const sway1 = `${(Math.random() * 200 - 100)}px`;
            const sway2 = `${(Math.random() * 400 - 200)}px`;
            const rotation = `${(Math.random() * 40 - 20)}deg`;
            
            dove.style.setProperty('--sway-1', sway1);
            dove.style.setProperty('--sway-2', sway2);
            dove.style.setProperty('--rot', rotation);

            // Variasi durasi terbang (antara 3.5 sampai 6 detik)
            const duration = 3.5 + Math.random() * 2.5;
            dove.style.animationDuration = `${duration}s`;

            // Variasi ukuran merpati (skala font)
            const size = 1.8 + Math.random() * 1.5;
            dove.style.fontSize = `${size}rem`;

            document.body.appendChild(dove);

            // Menghapus elemen setelah animasi selesai agar memori tetap bersih
            setTimeout(() => {
                dove.remove();
            }, duration * 1000);
        }
    </script>
</body>
</html>
