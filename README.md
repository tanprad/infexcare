<!doctype html>
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
return `<?xml version='1.0' encoding='UTF-8'?>\n<svg xmlns='http://www.w3.org/2000/svg' width='800' height='1200' viewBox='0 0 800 1200'>\n <rect width='100%' height='100%' fill='#ffffff'/>\n <rect x='40' y='40' width='720' height='1120' rx='24' fill='#f2fbff' stroke='#dff3fb'/>\n <text x='60' y='120' font-family='Poppins, sans-serif' font-size='42' fill='#008CBA' font-weight='700'>Cuci Tangan yang Benar</text>\n <text x='60' y='170' font-family='Poppins, sans-serif' font-size='20' fill='#0b2b3a'>7 langkah — selama minimal 20 detik</text>\n <g transform='translate(60,220)'>\n <rect x='0' y='0' width='680' height='860' rx='16' fill='white' stroke='#e6f7fb'/>\n <text x='30' y='60' font-family='Poppins, sans-serif' font-size='24' fill='#008CBA' font-weight='600'>Langkah</text>\n <text x='30' y='110' font-family='Poppins, sans-serif' font-size='18' fill='#0b2b3a'>1. Basahi tangan & sabun.\n2. Gosok telapak tangan.\n3. Gosok punggung tangan.\n4. Sela jari.\n5. Ibu jari dan ujung jari.\n6. Bilas & keringkan.\n7. Matikan keran dengan tisu.</text>\n <circle cx='560' cy='520' r='120' fill='#8BBC8A' opacity='0.12'/>\n <text x='420' y='520' font-family='Poppins, sans-serif' font-size='18' fill='#0b2b3a'>20 detik</text>\n </g>\n <text x='60' y='1120' font-family='Poppins, sans-serif' font-size='16' fill='#6b6b6b'>INFEXCARE — Edukasi Pencegahan Infeksi</text>\n</svg>`;
}
function makeCoughPosterSVG(){
return `<?xml version='1.0' encoding='UTF-8'?>\n<svg xmlns='http://www.w3.org/2000/svg' width='800' height='1200' viewBox='0 0 800 1200'>\n <rect width='100%' height='100%' fill='#ffffff'/>\n <rect x='40' y='40' width='720' height='1120' rx='24' fill='#f7fff7' stroke='#e9f8ee'/>\n <text x='60' y='120' font-family='Poppins, sans-serif' font-size='42' fill='#008CBA' font-weight='700'>Etika Batuk</text>\n <text x='60' y='170' font-family='Poppins, sans-serif' font-size='20' fill='#0b2b3a'>Tutup mulut dengan siku atau tisu — buang tisu pada tempatnya</text>\n <g transform='translate(60,220)'>\n <rect x='0' y='0' width='680' height='860' rx='16' fill='white' stroke='#eefbf0'/>\n <text x='30' y='90' font-family='Poppins, sans-serif' font-size='20' fill='#0b2b3a'>1. Tutup mulut dengan siku bagian dalam atau tisu.\n2. Masukkan tisu ke tempat sampah tertutup.\n3. Cuci tangan setelah membuang tisu.</text>\n <g transform='translate(420,220)'>\n <rect x='0' y='0' width='220' height='220' rx='12' fill='#008CBA' opacity='0.12'/>\n <text x='10' y='120' font-family='Poppins, sans-serif' font-size='28' fill='#008CBA'>Jaga</text>
</g>
</g>\n <text x='60' y='1120' font-family='Poppins, sans-serif' font-size='16' fill='#6b6b6b'>INFEXCARE — Edukasi Pencegahan Infeksi</text>\n</svg>`;
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
