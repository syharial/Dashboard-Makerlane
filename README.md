# Dashboard-Makerlane
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard Kampanye Makerlane & Wireframe</title>
    <style>
        :root {
            --bg-color: #020502;
            --card-bg: #121a12;
            --accent-green: #80E893;
            --text-main: #FFFFFF;
            --text-muted: #A0A0A0;
            --border-color: #223322;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Inter', sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-main); display: flex; height: 100vh; overflow: hidden; }
        
        /* Sidebar Kalender */
        .sidebar { width: 420px; background-color: var(--card-bg); border-right: 1px solid var(--border-color); display: flex; flex-direction: column; height: 100vh; }
        .sidebar-header { padding: 20px; border-bottom: 1px solid var(--border-color); }
        .sidebar-header h1 { font-size: 18px; color: var(--accent-green); margin-bottom: 4px; }
        .sidebar-header p { font-size: 12px; color: var(--text-muted); }
        
        .schedule-list { overflow-y: auto; padding: 15px; flex-grow: 1; }
        .week-section { margin-bottom: 20px; }
        .week-title { font-size: 13px; font-weight: bold; color: var(--accent-green); text-transform: uppercase; margin-bottom: 8px; letter-spacing: 0.5px; }
        
        .schedule-item { 
            background: rgba(255,255,255,0.03); border: 1px solid var(--border-color); padding: 10px 12px; border-radius: 6px; margin-bottom: 8px; cursor: pointer; transition: all 0.2s ease;
        }
        .schedule-item:hover { background: rgba(128, 232, 147, 0.08); border-color: var(--accent-green); }
        .schedule-item.active { background: rgba(128, 232, 147, 0.15); border-color: var(--accent-green); }
        
        .item-meta { display: flex; justify-content: space-between; font-size: 11px; color: var(--text-muted); margin-bottom: 4px; }
        .item-title { font-size: 13px; font-weight: 600; color: var(--text-main); }
        .badge { background: var(--accent-green); color: #000; font-size: 9px; font-weight: bold; padding: 2px 6px; border-radius: 4px; text-transform: uppercase; }
        .badge-carousel { background: #3b82f6; color: #fff; }

        /* Area Pratinjau Wireframe */
        .preview-area { flex-grow: 1; display: flex; flex-direction: column; height: 100vh; background: #080c08; padding: 30px; overflow-y: auto; align-items: center; justify-content: center; }
        .preview-header { width: 100%; max-width: 600px; margin-bottom: 15px; display: flex; justify-content: space-between; align-items: center; }
        .preview-header h2 { font-size: 16px; font-weight: bold; }
        .preview-header span { font-size: 12px; color: var(--text-muted); }

        /* Kanvas Simulasi HP (9:16 atau 4:5) */
        .canvas-container { 
            width: 340px; height: 540px; background: #000; border: 2px solid var(--border-color); border-radius: 16px; 
            position: relative; overflow: hidden; display: flex; flex-direction: column; justify-content: space-between; padding: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }
        
        /* Carousel Container (Multi-slide) */
        .carousel-wrapper { display: flex; gap: 15px; width: 100%; max-width: 700px; overflow-x: auto; padding-bottom: 10px; }
        .carousel-wrapper .canvas-container { flex: 0 0 320px; height: 480px; }

        /* Elemen Wireframe */
        .wf-logo { width: 28px; height: 28px; background: url('Gemini_Generated_Image_ksknmfksknmfkskn.jpg') no-repeat center/contain; }
        .wf-content { margin-top: auto; margin-bottom: auto; }
        .wf-line-1 { font-size: 20px; font-weight: bold; color: #fff; text-transform: uppercase; line-height: 1.2; }
        .wf-line-2 { font-size: 22px; font-weight: bold; color: var(--accent-green); text-transform: uppercase; line-height: 1.2; margin: 4px 0; }
        .wf-desc { font-size: 11px; color: var(--text-muted); margin-top: 8px; line-height: 1.4; }
        .wf-footer { font-size: 10px; color: var(--text-muted); text-align: center; border-top: 1px solid rgba(255,255,255,0.1); padding-top: 8px; }
    </style>
</head>
<body>

    <div class="sidebar">
        <div class="sidebar-header">
            <h1>Makerlane Campaign</h1>
            <p>26 Oktober - 20 November 2026</p>
        </div>
        <div class="schedule-list" id="scheduleList">
            <!-- Diisi otomatis via JS -->
        </div>
    </div>

    <div class="preview-area" id="previewArea">
        <div class="preview-header">
            <h2 id="previewTitle">Pilih Jadwal Konten</h2>
            <span id="previewInfo">Klik item di samping untuk melihat wireframe</span>
        </div>
        <div id="canvasView" style="display: flex; justify-content: center; align-items: center; width: 100%;">
            <p style="color: var(--text-muted); font-size: 13px;">Belum ada konten yang dipilih.</p>
        </div>
    </div>

    <script>
        const campaignData = [
            { week: "Minggu 0: Persiapan", date: "24-25 Okt", title: "Finalisasi Master Template", type: "Internal", channel: "Internal", l1: "PERSIAPAN", l2: "FINALISASI ASET", desc: "Siapkan 4 master template dan izin streamer." },
            { week: "Minggu 1: Kenalan", date: "Senin, 26 Okt", title: "#1 Teaser Campaign", type: "Template B", channel: "IG Feed", l1: "DUKUNG STREAMER", l2: "DUKUNG KARYA", desc: "Create Your Way. Grow Every Day. Perkenalan awal Makerlane." },
            { week: "Minggu 1: Kenalan", date: "Rabu, 28 Okt", title: "#2 Ajakan Gabung (Kreator)", type: "Template A", channel: "IG Feed", l1: "KARYAMU LAYAK", l2: "DIBAYAR PENUH", desc: "Alur proyek jelas, tanpa drama. Daftar hari ini." },
            { week: "Minggu 1: Kenalan", date: "Jumat, 30 Okt", title: "#3 Value Utama (Klien)", type: "Template A", channel: "IG Feed", l1: "BIKIN KONTEN", l2: "BEBAS RIBET", desc: "Top up tanpa potongan biaya. Temukan clipper andal." },
            { week: "Minggu 2: Edukasi", date: "Senin, 2 Nov", title: "#4 Kesalahan Clipper", type: "Carousel", channel: "IG Feed", slides: [
                { l1: "3 KESALAHAN", l2: "CLIPPER PEMULA", desc: "Cover: Swipe untuk tahu apa saja kesalahannya." },
                { l1: "KESALAHAN 1", l2: "TANPA INVOICE", desc: "Slide 2: Kerja tanpa kesepakatan tertulis yang jelas." },
                { l1: "SOLUSI AMAN", l2: "PAKAI MAKERLANE", desc: "Slide 3: Alur transaksi transparan dan terlindungi." }
            ]},
            { week: "Minggu 2: Edukasi", date: "Rabu, 4 Nov", title: "#5 Cara Pilih Kreator", type: "Carousel", channel: "IG Feed", slides: [
                { l1: "PILIH KREATOR", l2: "SESUAI BRAND", desc: "Cover: Tips memilih clipper yang pas untuk UMKM." },
                { l1: "CEK PORTOFOLIO", l2: "DAN REVIEW", desc: "Slide 2: Lihat riwayat kerja nyata sebelum mulai." }
            ]},
            { week: "Minggu 2: Edukasi", date: "Jumat, 6 Nov", title: "#6 Sorotan Streamer #1", type: "Template D", channel: "IG Feed", l1: "TEMPAT TERBAIK", l2: "UNTUK KREATOR", desc: "Sorotan streamer asli dan dukungan gratis Makerlane." },
            { week: "Minggu 3: Cara Kerja", date: "Senin, 9 Nov", title: "#7 Campaign 4 Langkah (Klien)", type: "Carousel", channel: "IG Feed", slides: [
                { l1: "4 LANGKAH MUDAH", l2: "UNTUK KLIEN", desc: "Cover: Cara mulai delegasi tugas konten." },
                { l1: "MULAI PROYEK", l2: "DENGAN AMAN", desc: "Slide 2: Top up saldo tanpa potongan tersembunyi." }
            ]},
            { week: "Minggu 3: Cara Kerja", date: "Rabu, 11 Nov", title: "#8 Kerja 3 Langkah (Kreator)", type: "Carousel", channel: "IG Feed", slides: [
                { l1: "3 LANGKAH KREATIF", l2: "UNTUK KREATOR", desc: "Cover: Ubah skill editing jadi cuan." },
                { l1: "TERIMA TUGAS", l2: "& CAIRKAN DANA", desc: "Slide 2: Proses screening dan verifikasi cepat." }
            ]},
            { week: "Minggu 3: Cara Kerja", date: "Jumat, 13 Nov", title: "#9 Sorotan Streamer #2", type: "Template D", channel: "IG Feed", l1: "KARYA ANAK BANGSA", l2: "LAYAK DIDUKUNG", desc: "Wajah campaign dan jangkauan ke komunitas." },
            { week: "Minggu 4: Bukti & Ajakan", date: "Senin, 16 Nov", title: "#10 Hasil Nyata (Kreator)", type: "Template A", channel: "IG Feed", l1: "BUKTI NYATA", l2: "KREATOR SUKSES", desc: "Angka asli dari proyek dan testimoni kreator." },
            { week: "Minggu 4: Bukti & Ajakan", date: "Rabu, 18 Nov", title: "#11 Top Up Tanpa Potongan", type: "Template B", channel: "IG Feed", l1: "TOP UP SALDO", l2: "100% UTUH", desc: "Jelaskan biaya secara transparan di awal." },
            { week: "Minggu 4: Bukti & Ajakan", date: "Jumat, 20 Nov", title: "#12 Recap Sebulan + CTA", type: "Carousel", channel: "IG Feed", slides: [
                { l1: "RECAP 1 BULAN", l2: "MAKERLANE", desc: "Cover: Perjalanan seru bersama streamer & kreator." },
                { l1: "MARI BERGABUNG", l2: "SEKARANG JUGA", desc: "Slide 2: Klik link bio dan mulai buat karyamu." }
            ]}
        ];

        const listContainer = document.getElementById('scheduleList');
        const previewTitle = document.getElementById('previewTitle');
        const previewInfo = document.getElementById('previewInfo');
        const canvasView = document.getElementById('canvasView');

        let currentWeek = "";
        let htmlContent = "";

        campaignData.forEach((item, index) => {
            if (item.week !== currentWeek) {
                currentWeek = item.week;
                htmlContent += `<div class="week-section"><div class="week-title">${currentWeek}</div>`;
            }

            const isCarousel = item.type === "Carousel";
            htmlContent += `
                <div class="schedule-item" onclick="selectItem(${index})">
                    <div class="item-meta">
                        <span>${item.date}</span>
                        <span class="badge ${isCarousel ? 'badge-carousel' : ''}">${item.type}</span>
                    </div>
                    <div class="item-title">${item.title}</div>
                </div>
            `;

            if (index === campaignData.length - 1 || campaignData[index + 1].week !== currentWeek) {
                htmlContent += `</div>`;
            }
        });

        listContainer.innerHTML = htmlContent;

        function selectItem(index) {
            document.querySelectorAll('.schedule-item').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.schedule-item')[index].classList.add('active');

            const data = campaignData[index];
            previewTitle.innerText = `${data.title} (${data.date})`;
            previewInfo.innerText = `Channel: ${data.channel} | Tipe: ${data.type}`;

            if (data.type === "Carousel" && data.slides) {
                let slidesHtml = '<div class="carousel-wrapper">';
                data.slides.forEach((slide, sIdx) => {
                    slidesHtml += `
                        <div class="canvas-container">
                            <div style="display: flex; justify-content: space-between; align-items: center;">
                                <div class="wf-logo"></div>
                                <span style="font-size: 10px; color: var(--text-muted);">Slide ${sIdx + 1}/${data.slides.length}</span>
                            </div>
                            <div class="wf-content">
                                <div class="wf-line-1">${slide.l1}</div>
                                <div class="wf-line-2">${slide.l2}</div>
                                <div class="wf-desc">${slide.desc}</div>
                            </div>
                            <div class="wf-footer">BATAS AMAN 80PX</div>
                        </div>
                    `;
                });
                slidesHtml += '</div>';
                canvasView.innerHTML = slidesHtml;
            } else {
                canvasView.innerHTML = `
                    <div class="canvas-container">
                        <div style="display: flex; justify-content: space-between; align-items: center;">
                            <div class="wf-logo"></div>
                            <span style="font-size: 10px; color: var(--text-muted);">4:5 Feed/Story</span>
                        </div>
                        <div class="wf-content">
                            <div class="wf-line-1">${data.l1}</div>
                            <div class="wf-line-2">${data.l2}</div>
                            <div class="wf-desc">${data.desc}</div>
                        </div>
                        <div class="wf-footer">MAKERLANE GUIDELINE • SATU HOOK HIJAU</div>
                    </div>
                `;
            }
        }

        // Otomatis pilih item pertama saat load
        selectItem(1);
    </script>
</body>
</html>
