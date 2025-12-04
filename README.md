<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ekolojik Ayak İzi Testi (Tam Kapsamlı)</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #10b981; /* Canlı Yeşil */
            --primary-dark: #059669;
            --bg-color: #f0fdf4;
            --card-bg: #ffffff;
            --text-main: #1f2937;
            --text-sub: #4b5563;
            --border-color: #d1fae5;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }

        .header {
            background: linear-gradient(135deg, #059669, #10b981);
            color: white;
            padding: 60px 20px;
            text-align: center;
            border-bottom-left-radius: 40px;
            border-bottom-right-radius: 40px;
            box-shadow: 0 10px 25px rgba(16, 185, 129, 0.2);
            margin-bottom: 50px;
        }

        .header h1 {
            margin: 0;
            font-size: 2.2rem;
            font-weight: 800;
            letter-spacing: -1px;
        }

        .header p {
            opacity: 0.95;
            margin-top: 10px;
            font-size: 1.1rem;
            font-weight: 500;
        }

        .container {
            max-width: 850px;
            margin: 0 auto 80px;
            padding: 0 20px;
        }

        /* Bölüm Kartları */
        .section-card {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 40px;
            margin-bottom: 30px;
            border: 1px solid var(--border-color);
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
            position: relative;
            overflow: hidden;
        }

        .section-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 6px;
            height: 100%;
            background: var(--primary);
        }

        .section-title {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary-dark);
            margin-bottom: 30px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        /* Sorular */
        .question-group {
            margin-bottom: 40px;
        }

        .question-text {
            display: block;
            font-weight: 700;
            font-size: 1.1rem;
            margin-bottom: 16px;
            color: #111;
        }

        .options-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 12px;
        }

        /* Tıklanabilir Butonlar */
        .option-item {
            position: relative;
            cursor: pointer;
            display: block;
        }

        .option-item input {
            position: absolute;
            opacity: 0;
            height: 0;
            width: 0;
        }

        .option-box {
            display: flex;
            align-items: center;
            padding: 16px 20px;
            background: #f9fafb;
            border: 2px solid #e5e7eb;
            border-radius: 12px;
            font-size: 1rem;
            color: var(--text-sub);
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            height: 100%;
            box-sizing: border-box;
            font-weight: 500;
        }

        /* Hover */
        .option-item:hover .option-box {
            border-color: var(--primary);
            background: #ecfdf5;
            color: var(--primary-dark);
        }

        /* Seçili Durum */
        .option-item input:checked + .option-box {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
            box-shadow: 0 4px 12px rgba(16, 185, 129, 0.3);
            transform: translateY(-2px);
        }

        .btn-calc {
            background: var(--text-main);
            color: white;
            width: 100%;
            padding: 24px;
            border: none;
            border-radius: 16px;
            font-size: 1.3rem;
            font-weight: 800;
            cursor: pointer;
            transition: transform 0.2s, background 0.3s;
            margin-top: 30px;
            box-shadow: 0 10px 25px rgba(31, 41, 55, 0.2);
        }

        .btn-calc:hover {
            background: black;
            transform: translateY(-3px);
        }

        /* Sonuç Modal */
        #result-modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(8px);
        }

        .result-content {
            background: white;
            padding: 50px;
            border-radius: 30px;
            text-align: center;
            max-width: 480px;
            width: 90%;
            position: relative;
            animation: popIn 0.4s ease-out;
        }

        @keyframes popIn {
            from { transform: scale(0.9); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }

        .score-number {
            font-size: 5rem;
            font-weight: 900;
            color: var(--primary);
            line-height: 1;
            margin: 20px 0 10px;
            text-shadow: 2px 2px 0px rgba(16, 185, 129, 0.2);
        }

        .close-btn {
            margin-top: 30px;
            padding: 12px 30px;
            background: #f3f4f6;
            border: none;
            border-radius: 50px;
            font-weight: 600;
            color: var(--text-main);
            cursor: pointer;
            transition: 0.2s;
        }
        .close-btn:hover { background: #e5e7eb; }

        @media (max-width: 600px) {
            .options-grid { grid-template-columns: 1fr; }
            .header h1 { font-size: 1.8rem; }
            .section-card { padding: 25px; }
        }
    </style>
</head>
<body>

<div class="header">
    <h1>Tam Kapsamlı Ekolojik Ayak İzi</h1>
    <p>Excel Verilerine Göre Hazırlanmış Nihai Test</p>
</div>

<div class="container">
    <form id="ecoForm">

        <div class="section-card">
            <div class="section-title">🍎 GIDA TÜKETİMİ</div>

            <div class="question-group">
                <span class="question-text">1. Günlük et tüketiminiz ne düzeyde?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="g1" value="600"><div class="option-box">Yüksek (Hemen her öğün)</div></label>
                    <label class="option-item"><input type="radio" name="g1" value="400"><div class="option-box">Normal (Günde 1 kez)</div></label>
                    <label class="option-item"><input type="radio" name="g1" value="300"><div class="option-box">Düşük (Günaşırı)</div></label>
                    <label class="option-item"><input type="radio" name="g1" value="200"><div class="option-box">Vejeteryanım</div></label>
                    <label class="option-item"><input type="radio" name="g1" value="150"><div class="option-box">Veganım</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">2. Yiyecekleriniz yerel üretim mi?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="g2" value="0"><div class="option-box">Çoğu yerel</div></label>
                    <label class="option-item"><input type="radio" name="g2" value="30"><div class="option-box">Bazıları</div></label>
                    <label class="option-item"><input type="radio" name="g2" value="60"><div class="option-box">Hiçbiri / Bilmiyorum</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">3. Organik atıkları kompost (gübre) yapıyor musunuz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="g3" value="-20"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="g3" value="60"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">4. İşlenmiş ve paketli gıda tüketiminiz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="g4" value="200"><div class="option-box">Tamamı paketli</div></label>
                    <label class="option-item"><input type="radio" name="g4" value="60"><div class="option-box">Bazıları</div></label>
                    <label class="option-item"><input type="radio" name="g4" value="0"><div class="option-box">Hiçbiri (Doğal)</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">5. Ne kadar yiyecek israf ediyorsunuz (çöpe gidiyor)?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="g5" value="0"><div class="option-box">Hiç atmıyorum</div></label>
                    <label class="option-item"><input type="radio" name="g5" value="25"><div class="option-box">Çok az (1/10)</div></label>
                    <label class="option-item"><input type="radio" name="g5" value="50"><div class="option-box">Bazen (1/4)</div></label>
                    <label class="option-item"><input type="radio" name="g5" value="100"><div class="option-box">Yarısından fazlasını</div></label>
                </div>
            </div>
        </div>

        <div class="section-card">
            <div class="section-title">🚲 ULAŞIM</div>

            <div class="question-group">
                <span class="question-text">6. İşe veya okula nasıl gidiyorsunuz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="u1" value="0"><div class="option-box">Yürüyerek / Bisiklet</div></label>
                    <label class="option-item"><input type="radio" name="u1" value="30"><div class="option-box">Toplu taşıma</div></label>
                    <label class="option-item"><input type="radio" name="u1" value="100"><div class="option-box">Servis / Ortak araç</div></label>
                    <label class="option-item"><input type="radio" name="u1" value="200"><div class="option-box">Özel araç (Tek başıma)</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">7. Günde ne kadar süreniz trafikte geçiyor?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="u2" value="0"><div class="option-box">Hiç</div></label>
                    <label class="option-item"><input type="radio" name="u2" value="40"><div class="option-box">Yarım saatten az</div></label>
                    <label class="option-item"><input type="radio" name="u2" value="100"><div class="option-box">Yarım - bir saat arası</div></label>
                    <label class="option-item"><input type="radio" name="u2" value="200"><div class="option-box">Bir saatten fazla</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">8. Ailenizde kaç adet araç var?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="u3" value="-20"><div class="option-box">Hiç yok</div></label>
                    <label class="option-item"><input type="radio" name="u3" value="100"><div class="option-box">1 araç</div></label>
                    <label class="option-item"><input type="radio" name="u3" value="200"><div class="option-box">2 araç</div></label>
                    <label class="option-item"><input type="radio" name="u3" value="400"><div class="option-box">2'den fazla</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">9. Aracınızın yakıt tüketimi nasıl?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="u4" value="50"><div class="option-box">Az (6 lt altı)</div></label>
                    <label class="option-item"><input type="radio" name="u4" value="100"><div class="option-box">Orta (6-9 lt)</div></label>
                    <label class="option-item"><input type="radio" name="u4" value="200"><div class="option-box">Çok (10 lt üstü)</div></label>
                    <label class="option-item"><input type="radio" name="u4" value="0"><div class="option-box">Aracım yok</div></label>
                </div>
            </div>
            
            <div class="question-group">
                <span class="question-text">10. Yılda kaç kez uçağa biniyorsunuz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="u5" value="0"><div class="option-box">Hiç binmem</div></label>
                    <label class="option-item"><input type="radio" name="u5" value="200"><div class="option-box">2-4 kez</div></label>
                    <label class="option-item"><input type="radio" name="u5" value="400"><div class="option-box">4'ten fazla</div></label>
                </div>
            </div>
        </div>

        <div class="section-card">
            <div class="section-title">⚡ SU VE ENERJİ (Tam Liste)</div>

            <div class="question-group">
                <span class="question-text">11. Duş süreniz ortalama ne kadardır?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s1" value="30"><div class="option-box">Kısa (1-2 dk)</div></label>
                    <label class="option-item"><input type="radio" name="s1" value="40"><div class="option-box">Orta (3-6 dk)</div></label>
                    <label class="option-item"><input type="radio" name="s1" value="50"><div class="option-box">Uzun (10+ dk)</div></label>
                    <label class="option-item"><input type="radio" name="s1" value="80"><div class="option-box">Küveti doldururum</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">12. Tuvalet sifon sisteminiz tasarruflu mu?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s2" value="30"><div class="option-box">Hayır, standart</div></label>
                    <label class="option-item"><input type="radio" name="s2" value="-30"><div class="option-box">Evet, tasarruflu</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">13. Diş fırçalarken suyu açık bırakır mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s3" value="40"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="s3" value="0"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">14. Bulaşık makinesini her gün çalıştırır mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s4" value="40"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="s4" value="20"><div class="option-box">Hayır (Dolunca)</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">15. Aracınızı haftada en az bir kez yıkatır mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s_car" value="60"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="s_car" value="0"><div class="option-box">Hayır (Daha seyrek)</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">16. Kullanmadığınız elektronik cihazları (PC, TV, ışık) kapatır mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s5" value="0"><div class="option-box">Evet, kapatırım</div></label>
                    <label class="option-item"><input type="radio" name="s5" value="50"><div class="option-box">Hayır, açık kalır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">17. Kışın evinizin sıcaklığı nasıldır?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s6" value="10"><div class="option-box">Serin (15°C altı)</div></label>
                    <label class="option-item"><input type="radio" name="s6" value="30"><div class="option-box">Ilık (15-18°C)</div></label>
                    <label class="option-item"><input type="radio" name="s6" value="50"><div class="option-box">Sıcak (19-22°C)</div></label>
                    <label class="option-item"><input type="radio" name="s6" value="150"><div class="option-box">Çok Sıcak (22°C üstü)</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">18. Çamaşırları nasıl kurutursunuz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s7" value="-50"><div class="option-box">Asarak</div></label>
                    <label class="option-item"><input type="radio" name="s7" value="20"><div class="option-box">Bazen makinede</div></label>
                    <label class="option-item"><input type="radio" name="s7" value="60"><div class="option-box">Hep makinede</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">19. Buzdolabınız yüksek enerji verimliliğine sahip mi (A+)?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s8" value="-50"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="s8" value="20"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">20. Evde tasarruflu ampul kullanıyor musunuz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s9" value="-50"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="s9" value="100"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">21. Yazın serinlemek için ne kullanırsınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="s10" value="100"><div class="option-box">Klima</div></label>
                    <label class="option-item"><input type="radio" name="s10" value="-10"><div class="option-box">Vantilatör</div></label>
                    <label class="option-item"><input type="radio" name="s10" value="-50"><div class="option-box">Hiçbir şey</div></label>
                </div>
            </div>
        </div>

        <div class="section-card">
            <div class="section-title">👕 GİYİM VE EŞYA</div>

            <div class="question-group">
                <span class="question-text">22. Kıyafetlerinizi her gün yıkar mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e1" value="100"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="e1" value="0"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">23. Kıyafetlerinizin çoğunu her sene yeniler misiniz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e2" value="200"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="e2" value="0"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">24. Eski giysileri başkasına verir veya satar mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e3" value="-50"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="e3" value="100"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">25. Dolabınızda hiç giymediğiniz kıyafet oranı nedir?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e4" value="25"><div class="option-box">%25'ten az</div></label>
                    <label class="option-item"><input type="radio" name="e4" value="50"><div class="option-box">%50 civarı</div></label>
                    <label class="option-item"><input type="radio" name="e4" value="75"><div class="option-box">%75 civarı</div></label>
                    <label class="option-item"><input type="radio" name="e4" value="100"><div class="option-box">%75'ten fazla</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">26. Yılda kaç çift ayakkabı alırsınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e5" value="0"><div class="option-box">0-1 çift</div></label>
                    <label class="option-item"><input type="radio" name="e5" value="20"><div class="option-box">2-3 çift</div></label>
                    <label class="option-item"><input type="radio" name="e5" value="60"><div class="option-box">4-6 çift</div></label>
                    <label class="option-item"><input type="radio" name="e5" value="90"><div class="option-box">7+ çift</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">27. Günlük çöp miktarınız ne kadar?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e6" value="-75"><div class="option-box">Sıfır atık</div></label>
                    <label class="option-item"><input type="radio" name="e6" value="20"><div class="option-box">Ayakkabı kutusu kadar</div></label>
                    <label class="option-item"><input type="radio" name="e6" value="60"><div class="option-box">Küçük çöp kovası</div></label>
                    <label class="option-item"><input type="radio" name="e6" value="200"><div class="option-box">Büyük çöp kovası</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">28. Geri dönüşüm (kağıt, cam, metal) yapıyor musunuz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e7" value="-100"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="e7" value="20"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">29. Eşyaları atmadan önce başka amaçla kullanır mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e8" value="-20"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="e8" value="20"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">30. Bozulan eşyaları onarır mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e9" value="-20"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="e9" value="20"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">31. Tek kullanımlık eşyalardan kaçınır mısınız?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e10" value="-50"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="e10" value="60"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">32. Şarj edilebilir pil kullanıyor musunuz?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e11" value="-30"><div class="option-box">Evet</div></label>
                    <label class="option-item"><input type="radio" name="e11" value="30"><div class="option-box">Hayır</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">33. Evdeki elektronik alet sayısı (TV, PC vb.) kaçtır?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="e12" value="25"><div class="option-box">0-5 adet</div></label>
                    <label class="option-item"><input type="radio" name="e12" value="75"><div class="option-box">6-10 adet</div></label>
                    <label class="option-item"><input type="radio" name="e12" value="100"><div class="option-box">11-15 adet</div></label>
                    <label class="option-item"><input type="radio" name="e12" value="200"><div class="option-box">15'ten fazla</div></label>
                </div>
            </div>
        </div>

        <div class="section-card">
            <div class="section-title">🏠 BARINMA</div>

            <div class="question-group">
                <span class="question-text">34. Yaşadığınız ev tipi nedir?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="b1" value="100"><div class="option-box">Şehir dışı müstakil</div></label>
                    <label class="option-item"><input type="radio" name="b1" value="50"><div class="option-box">Şehir içi müstakil</div></label>
                    <label class="option-item"><input type="radio" name="b1" value="30"><div class="option-box">Köy evi</div></label>
                    <label class="option-item"><input type="radio" name="b1" value="20"><div class="option-box">Apartman dairesi</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">35. Evde kişi başına düşen oda sayısı kaçtır?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="b2" value="-50"><div class="option-box">1 oda</div></label>
                    <label class="option-item"><input type="radio" name="b2" value="0"><div class="option-box">2 oda</div></label>
                    <label class="option-item"><input type="radio" name="b2" value="50"><div class="option-box">3 oda</div></label>
                    <label class="option-item"><input type="radio" name="b2" value="100"><div class="option-box">4+ oda</div></label>
                </div>
            </div>

            <div class="question-group">
                <span class="question-text">36. Boş duran bir yazlık eviniz var mı?</span>
                <div class="options-grid">
                    <label class="option-item"><input type="radio" name="b3" value="0"><div class="option-box">Yok / Ortak kullanıyoruz</div></label>
                    <label class="option-item"><input type="radio" name="b3" value="200"><div class="option-box">Var (Bize özel)</div></label>
                </div>
            </div>
        </div>

        <button type="button" class="btn-calc" onclick="calculateResult()">SONUCU HESAPLA</button>

    </form>
</div>

<div id="result-modal">
    <div class="result-content">
        <h2>Sonuç Raporu</h2>
        <p style="color:#666; font-size:1.1rem;">Eğer dünyadaki herkes sizin gibi yaşasaydı;</p>
        
        <div class="score-number" id="worldCount">0.0</div>
        <div style="font-size:1.4rem; font-weight:800; color:#1f2937; margin-bottom:20px;">ADET DÜNYA GEREKİRDİ 🌍</div>

        <div style="background:#f9fafb; padding:20px; border-radius:15px; border:1px solid #e5e7eb;">
            <div style="font-size:0.9rem; color:#6b7280;">Toplam Puanınız:</div>
            <div style="font-size:1.8rem; font-weight:700; color:#059669;" id="rawScore">0</div>
            <div style="font-size:0.8rem; color:#9ca3af; margin-top:5px;">(Hesaplama: Toplam Puan / 300)</div>
        </div>

        <button class="close-btn" onclick="closeModal()">Kapat ve Tekrar Dene</button>
    </div>
</div>

<script>
    function calculateResult() {
        const form = document.getElementById('ecoForm');
        // Tüm seçili şıkları al
        const inputs = form.querySelectorAll('input[type="radio"]:checked');
        
        // 36 sorunun tamamı cevaplanmalı
        if (inputs.length < 36) {
            alert(`Lütfen tüm soruları cevaplayınız. (${inputs.length}/36 cevaplandı)`);
            
            // Cevaplanmayan ilk soruyu bul ve oraya kaydır (Opsiyonel UX iyileştirmesi)
            const allGroups = form.querySelectorAll('.question-group');
            for (let group of allGroups) {
                if (!group.querySelector('input:checked')) {
                    group.scrollIntoView({behavior: "smooth", block: "center"});
                    break;
                }
            }
            return;
        }

        let totalScore = 0;
        inputs.forEach(input => {
            totalScore += parseInt(input.value);
        });

        // Dünya Sayısı Hesabı
        let worlds = (totalScore / 300).toFixed(2);
        if (worlds < 0) worlds = 0;

        // Sonuçları Yazdır
        document.getElementById('worldCount').innerText = worlds;
        document.getElementById('rawScore').innerText = totalScore;
        
        // Modalı Aç
        document.getElementById('result-modal').style.display = 'flex';
    }

    function closeModal() {
        document.getElementById('result-modal').style.display = 'none';
        window.scrollTo({top: 0, behavior: 'smooth'});
    }
</script>

</body>
</html>
