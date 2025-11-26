<!-- INFEXCARE - Prototipe Website Edukasi Pencegahan Infeksi
     File: INFEXCARE-prototype.html
     Deskripsi singkat di atas: single-file prototype (HTML/CSS/JS) untuk presentasi tugas.

     Fitur yang disertakan:
     - Landing / Hero
     - 3 topik materi: Kebersihan Tangan, APD, Etika Batuk
     - Poster SVG siap unduh (Hand Hygiene, Etika Batuk)
     - Quiz singkat 5 pertanyaan dengan scoring & pembahasan
     - Navigasi sederhana, responsif, style minimalis (biru/putih)

     Cara pakai: buka file ini di browser (double-click). Untuk presentasi, bisa tunjukkan prototype langsung.
-->

<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>INFEXCARE — Edukasi Pencegahan Infeksi</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --primary:#008CBA; /* biru */
      --accent:#8BBC8A;  /* hijau lembut */
      --bg:#ffffff;
      --text:#0b2b3a;
      --radius:12px;
    }
    *{box-sizing:border-box}
    body{font-family:'Poppins',system-ui,Segoe UI,Roboto,Arial; margin:0; color:var(--text); background:linear-gradient(180deg,#f7fbfd 0%, #ffffff 100%);}
    header{background:var(--primary); color:white; padding:28px 20px; border-bottom-left-radius:20px; border-bottom-right-radius:20px}
    .container{max-width:1000px;margin:18px auto;padding:0 16px}
    .hero{display:flex;gap:20px;align-items:center;flex-wrap:wrap}
    .hero h1{margin:0;font-size:1.6rem}
    .hero p{margin:6px 0 12px;color:rgba(255,255,255,0.92)}
    .cta-group{display:flex;gap:10px;flex-wrap:wrap}
    .btn{background:white;color:var(--primary);padding:10px 14px;border-radius:10px;border:none;font-weight:600;cursor:pointer}
    nav{margin-top:12px;display:flex;gap:12px;flex-wrap:wrap}
    nav a{color:white;text-decoration:none;padding:8px 10px;border-radius:8px;background:rgba(255,255,255,0.08)}

    main{padding:18px 0}
    .grid{display:grid;grid-template-columns:1fr 320px;gap:18px}
    @media (max-width:880px){.grid{grid-template-columns:1fr}}

    .card{background:var(--bg);border-radius:var(--radius);box-shadow:0 6px 18px rgba(10,20,30,0.06);padding:16px}
    h2{margin:0 0 10px 0}
    .topic-list{display:flex;gap:10px;flex-wrap:wrap}
    .topic{flex:1;min-width:160px;padding:12px;border-radius:10px;background:linear-gradient(180deg,rgba(0,140,186,0.06),rgba(139,188,138,0.03));cursor:pointer}

    .poster{display:flex;flex-direction:column;gap:12px}
    .poster button{padding:10px;border-radius:8px;border:1px solid rgba(0,0,0,0.06);cursor:pointer;background:white}

    footer{margin-top:24px;padding:18px;text-align:center;color:rgba(10,20,30,0.6)}

    /* Quiz */
    .quiz-q{margin-bottom:12px}
    .choices{display:flex;flex-direction:column;gap:8px}
    .choice{padding:10px;border-radius:8px;border:1px solid rgba(0,0,0,0.06);cursor:pointer}
    .choice.selected{background:rgba(0,140,186,0.08);border-color:var(--primary)}
    .score{font-weight:700;margin-top:10px}

    /* small helper */
    .muted{color:rgba(0,0,0,0.55);font-size:0.95rem}
    .inline-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
    @media (max-width:520px){.inline-grid{grid-template-columns:1fr}}

  </style>
</head>
<body>
  <header>
    <div class="container">
      <div class="hero">
        <div style="flex:1">
          <h1>INFEXCARE</h1>
          <p>Cegah Infeksi dengan Langkah Sederhana — panduan praktis untuk masyarakat, caregiver, dan mahasiswa kesehatan.</p>
          <div class="cta-group">
            <button class="btn" onclick="scrollToSection('kebersihan')">Kebersihan Tangan</button>
            <button class="btn" onclick="scrollToSection('apd')">APD</button>
            <button class="btn" onclick="scrollToSection('batuk')">Etika Batuk</button>
          </div>
        </div>
        <div style="width:220px;text-align:right">
          <!-- simple SVG mascot -->
          <svg width="160" height="140" viewBox="0 0 160 140" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect x="0" y="0" width="160" height="140" rx="12" fill="white"/>
            <g transform="translate(18,12)">
              <circle cx="52" cy="40" r="28" fill="#8BBC8A" opacity="0.12"/>
              <g transform="translate(20,20)">
                <circle cx="12" cy="8" r="20" fill="#008CBA"/>
                <rect x="-12" y="40" width="48" height="10" rx="6" fill="#008CBA" opacity="0.2"/>
              </g>
            </g>
          </svg>
        </div>
      </div>
      <nav style="margin-top:12px">
        <a href="#home" onclick="event.preventDefault();scrollToTop()">Home</a>
        <a href="#materi" onclick="event.preventDefault();scrollToSection('materi')">Materi</a>
        <a href="#quiz" onclick="event.preventDefault();scrollToSection('quiz')">Quiz</a>
        <a href="#poster" onclick="event.preventDefault();scrollToSection('poster')">Poster</a>
      </nav>
    </div>
  </header>

  <main class="container">
    <section id="materi">
      <div class="grid">
        <div>
          <div class="card">
            <h2>Materi Inti (Ringkas)</h2>
            <p class="muted">Pilih salah satu topik untuk melihat ringkasan cepat dan panduan praktis.</p>
            <div class="topic-list" style="margin-top:12px">
              <div class="topic" onclick="showTopic('kebersihan')">Kebersihan Tangan</div>
              <div class="topic" onclick="showTopic('apd')">Penggunaan APD</div>
              <div class="topic" onclick="showTopic('batuk')">Etika Batuk</div>
            </div>

            <div id="topic-content" style="margin-top:16px"></div>
          </div>

          <div class="card" style="margin-top:14px">
            <h2 id="quiz">Quiz Singkat</h2>
            <p class="muted">Tes pemahamanmu (5 soal). Skor dan pembahasan muncul setelah selesai.</p>
            <div id="quiz-area"></div>
          </div>
        </div>

        <aside>
          <div class="card poster">
            <h3>Poster & Download</h3>
            <p class="muted">Unduh poster ringkas untuk disebarkan.</p>
            <button onclick="downloadPoster('hand')">Unduh Poster: Hand Hygiene</button>
            <button onclick="downloadPoster('cough')">Unduh Poster: Etika Batuk</button>
            <hr style="margin:12px 0">
            <h4>Ringkasan Cepat</h4>
            <ul>
              <li><strong>Cuci tangan:</strong> 7 langkah, 20 detik</li>
              <li><strong>APD:</strong> Pakai & lepas sesuai urutan</li>
              <li><strong>Batuk:</strong> Tutup dengan siku atau tisu</li>
            </ul>
          </div>

          <div class="card" style="margin-top:12px">
            <h4>Tanggal Pembelajaran</h4>
            <p class="muted">Gunakan prototipe ini untuk tugas, presentasi, atau edukasi singkat.</p>
          </div>
        </aside>
      </div>
    </section>

    <section id="poster" style="margin-top:18px">
      <div class="card">
        <h2>Preview Poster</h2>
        <div class="inline-grid" style="margin-top:12px">
          <div class="card" style="min-height:180px;display:flex;align-items:center;justify-content:center;">
            <div id="poster-preview-hand"></div>
          </div>
          <div class="card" style="min-height:180px;display:flex;align-items:center;justify-content:center;">
            <div id="poster-preview-cough"></div>
          </div>
        </div>
      </div>
    </section>

    <footer style="margin-top:18px">
      <p>INFEXCARE • Prototype edukasi pencegahan infeksi — dibuat untuk tugas & demonstrasi.</p>
    </footer>
  </main>

  <script>
    // --- Konten ringkas untuk setiap topik ---
    const topics = {
      kebersihan: `
        <h3>Kebersihan Tangan</h3>
        <p><strong>Kenapa penting?</strong> Banyak patogen berpindah lewat tangan. Cuci tangan menurunkan risiko infeksi.</p>
        <h4>Cara cuci tangan (7 langkah singkat):</h4>
        <ol>
          <li>Basahi tangan, sabun.</li>
          <li>Gosok telapak ke telapak.</li>
          <li>Gosok punggung tangan.</li>
          <li>Gosok sela jari & ibu jari.</li>
          <li>Gosok ujung jari dan kuku.</li>
          <li>Bilas & keringkan dengan tisu bersih.</li>
          <li>Matikan keran dengan tisu.</li>
        </ol>
        <p class="muted">Kapan cuci tangan? WHO: 5 Moments — sebelum menyentuh pasien, sebelum prosedur aseptik, setelah paparan cairan tubuh, setelah menyentuh pasien, serta setelah kontak dengan lingkungan pasien.</p>
      `,
      apd: `
        <h3>Penggunaan APD</h3>
        <p><strong>Apa saja?</strong> Masker, sarung tangan, gown, pelindung mata.</p>
        <h4>Aturan singkat:</h4>
        <ul>
          <li>Pilih APD sesuai risiko (mis. masker bedah untuk batuk; N95 untuk aerosol).</li>
          <li>Ikuti urutan <em>donning</em> dan <em>doffing</em> untuk mengurangi kontaminasi.</li>
          <li>Buang APD sekali pakai ke tempat khusus.</li>
        </ul>
      `,
      batuk: `
        <h3>Etika Batuk & Kebersihan Respirasi</h3>
        <p>Tutupi mulut dengan tisu atau siku bagian dalam ketika batuk/bersin. Gunakan masker bila sedang sakit.</p>
        <h4>Cara membuang tisu:</h4>
        <ol>
          <li>Masukkan tisu ke kantong sampah tertutup.</li>
          <li>Cuci tangan setelah membuang tisu.</li>
        </ol>
      `
    }

    function showTopic(id){
      document.getElementById('topic-content').innerHTML = topics[id];
      scrollToSection('materi');
    }

    function scrollToSection(id){
      const el = document.getElementById(id);
      if(el) el.scrollIntoView({behavior:'smooth',block:'start'});
    }
    function scrollToTop(){window.scrollTo({top:0,behavior:'smooth'})}

    // --- Quiz ---
    const quizData = [
      {q:'Berapa lama minimal waktu saat mencuci tangan dengan sabun?', choices:['10 detik','20 detik','30 detik','5 detik'], a:1, explain:'Waktu minimal 20 detik agar sabun efektif membersihkan.'},
      {q:'Urutan yang benar saat melepas APD adalah?', choices:['Masker -> Sarung tangan -> Gown','Gown -> Sarung tangan -> Masker','Sarung tangan -> Masker -> Gown','Masker -> Gown -> Sarung tangan'], a:1, explain:'Lepas gown dahulu, lalu sarung tangan, terakhir masker (bergantung situasi). Tujuannya mengurangi kontak permukaan terkontaminasi.'},
      {q:'Batuk yang benar dilakukan dengan:', choices:['Tangan terbuka','Siku bagian dalam atau tisu','Mata tertutup','Bersin ke arah orang lain'], a:1, explain:'Tutup dengan siku bagian dalam atau tisu untuk mencegah droplet menyebar.'},
      {q:'Kapan harus menggunakan handrub alkohol?', choices:['Tangan kotor terlihat','Setelah menggunakan toilet','Sebelum menyentuh pasien','Setelah mencuci piring'], a:2, explain:'Handrub digunakan sebelum menyentuh pasien jika tangan tidak terlihat kotor.'},
      {q:'Salah satu 5 Moments WHO adalah:', choices:['Sebelum memakai APD','Setelah menyentuh pasien','Sebelum tidur','Setelah makan'], a:1, explain:'Salah satu momen adalah setelah menyentuh pasien.'}
    ];

    function renderQuiz(){
      const area = document.getElementById('quiz-area');
      area.innerHTML = '';
      quizData.forEach((item, idx)=>{
        const qwrap = document.createElement('div'); qwrap.className='quiz-q card';
        qwrap.innerHTML = `<div style=\"font-weight:600\">Soal ${idx+1}</div><p style=\"margin:6px 0 8px 0\">${item.q}</p>`;
        const choices = document.createElement('div'); choices.className='choices';
        item.choices.forEach((ch,ci)=>{
          const btn = document.createElement('div'); btn.className='choice'; btn.textContent = ch;
          btn.onclick = ()=>{
            // mark
            qwrap.querySelectorAll('.choice').forEach(c=>c.classList.remove('selected'));
            btn.classList.add('selected');
            item.selected = ci;
          }
          choices.appendChild(btn);
        });
        qwrap.appendChild(choices);
        area.appendChild(qwrap);
      });
      const submit = document.createElement('button'); submit.className='btn'; submit.style.marginTop='8px'; submit.textContent='Submit Jawaban';
      submit.onclick = gradeQuiz;
      area.appendChild(submit);
    }

    function gradeQuiz(){
      let score=0; let missing=false;
      quizData.forEach((it,i)=>{ if(typeof it.selected === 'undefined') missing=true; if(it.selected===it.a) score++; });
      if(missing){ if(!confirm('Beberapa soal belum dijawab. Lanjutkan penilaian?')) return; }
      const area = document.getElementById('quiz-area');
      area.innerHTML='';
      area.innerHTML = `<div class="card"><h3>Hasil Quiz</h3><p class="score">Skor: ${score} / ${quizData.length}</p></div>`;
      quizData.forEach((it,idx)=>{
        const c = document.createElement('div'); c.className='card';
        c.innerHTML = `<strong>Soal ${idx+1}:</strong> ${it.q}<br><em>Jawabanmu:</em> ${typeof it.selected==='number'?it.choices[it.selected]:'(tidak dijawab)'}<br><em>Jawaban benar:</em> ${it.choices[it.a]}<p class=\"muted\">Pembahasan: ${it.explain}</p>`;
        area.appendChild(c);
      });
    }

    // --- Poster SVG generator & download ---
    function makeHandPosterSVG(){
      return `<?xml version='1.0' encoding='UTF-8'?>\n<svg xmlns='http://www.w3.org/2000/svg' width='800' height='1200' viewBox='0 0 800 1200'>\n  <rect width='100%' height='100%' fill='#ffffff'/>\n  <rect x='40' y='40' width='720' height='1120' rx='24' fill='#f2fbff' stroke='#dff3fb'/>\n  <text x='60' y='120' font-family='Poppins, sans-serif' font-size='42' fill='#008CBA' font-weight='700'>Cuci Tangan yang Benar</text>\n  <text x='60' y='170' font-family='Poppins, sans-serif' font-size='20' fill='#0b2b3a'>7 langkah — selama minimal 20 detik</text>\n  <g transform='translate(60,220)'>\n    <rect x='0' y='0' width='680' height='860' rx='16' fill='white' stroke='#e6f7fb'/>\n    <text x='30' y='60' font-family='Poppins, sans-serif' font-size='24' fill='#008CBA' font-weight='600'>Langkah</text>\n    <text x='30' y='110' font-family='Poppins, sans-serif' font-size='18' fill='#0b2b3a'>1. Basahi tangan & sabun.\n2. Gosok telapak tangan.\n3. Gosok punggung tangan.\n4. Sela jari.\n5. Ibu jari dan ujung jari.\n6. Bilas & keringkan.\n7. Matikan keran dengan tisu.</text>\n    <circle cx='560' cy='520' r='120' fill='#8BBC8A' opacity='0.12'/>\n    <text x='420' y='520' font-family='Poppins, sans-serif' font-size='18' fill='#0b2b3a'>20 detik</text>\n  </g>\n  <text x='60' y='1120' font-family='Poppins, sans-serif' font-size='16' fill='#6b6b6b'>INFEXCARE — Edukasi Pencegahan Infeksi</text>\n</svg>`;
    }
    function makeCoughPosterSVG(){
      return `<?xml version='1.0' encoding='UTF-8'?>\n<svg xmlns='http://www.w3.org/2000/svg' width='800' height='1200' viewBox='0 0 800 1200'>\n  <rect width='100%' height='100%' fill='#ffffff'/>\n  <rect x='40' y='40' width='720' height='1120' rx='24' fill='#f7fff7' stroke='#e9f8ee'/>\n  <text x='60' y='120' font-family='Poppins, sans-serif' font-size='42' fill='#008CBA' font-weight='700'>Etika Batuk</text>\n  <text x='60' y='170' font-family='Poppins, sans-serif' font-size='20' fill='#0b2b3a'>Tutup mulut dengan siku atau tisu — buang tisu pada tempatnya</text>\n  <g transform='translate(60,220)'>\n    <rect x='0' y='0' width='680' height='860' rx='16' fill='white' stroke='#eefbf0'/>\n    <text x='30' y='90' font-family='Poppins, sans-serif' font-size='20' fill='#0b2b3a'>1. Tutup mulut dengan siku bagian dalam atau tisu.\n2. Masukkan tisu ke tempat sampah tertutup.\n3. Cuci tangan setelah membuang tisu.</text>\n    <g transform='translate(420,220)'>\n      <rect x='0' y='0' width='220' height='220' rx='12' fill='#008CBA' opacity='0.12'/>\n      <text x='10' y='120' font-family='Poppins, sans-serif' font-size='28' fill='#008CBA'>Jaga</text>
    </g>
  </g>\n  <text x='60' y='1120' font-family='Poppins, sans-serif' font-size='16' fill='#6b6b6b'>INFEXCARE — Edukasi Pencegahan Infeksi</text>\n</svg>`;
    }

    function downloadSVG(filename, svgText){
      const blob = new Blob([svgText], {type: 'image/svg+xml;charset=utf-8'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href=url; a.download = filename; document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
    }

    function downloadPoster(which){
      if(which==='hand') downloadSVG('poster_hand_hygiene.svg', makeHandPosterSVG());
      else downloadSVG('poster_etika_batuk.svg', makeCoughPosterSVG());
    }

    // render previews
    document.getElementById('poster-preview-hand').innerHTML = makeHandPosterSVG();
    document.getElementById('poster-preview-cough').innerHTML = makeCoughPosterSVG();

    // init
    showTopic('kebersihan');
    renderQuiz();
  </script>
</body>
</html>
