function showSection(id) {
    document.querySelectorAll('section').forEach(s => s.classList.remove('active'));
    document.getElementById(id).classList.add('active');
}

function speakText(text) {
    speechSynthesis.speak(new SpeechSynthesisUtterance(text));
}

let score = 0, qNum = 1;
const correct = { q1: 'B', q2: 'B', q3: 'B' };

function answer(q, ans) {
    if (ans === correct[q]) score++;
    document.getElementById(q).classList.add('hidden');
    qNum++;
    if (qNum <= 3) document.getElementById('q' + qNum).classList.remove('hidden');
}

function submitQuiz() {
    document.getElementById('score').innerText = Score: ${score}/3;
    firebase.firestore().collection('results').add({ score, time: Date.now() });
}

function checkPwd() {
    const pwd = document.getElementById('pwd').value;
    const strong = pwd.length >= 8 && /[A-Z]/.test(pwd) && /[0-9]/.test(pwd);
    document.getElementById('pwd-result').innerText = strong ? 'Strong' : 'Weak';
}

async function checkUrl() {
    const url = document.getElementById('url').value;
    try {
        const res = await fetch(https://checkurl.phishtank.com/checkurl/?url=${encodeURIComponent(url)}&format=json);
        const data = await res.json();
        document.getElementById('url-result').innerText = data.results.in_database ? 'Phishing!' : 'Safe';
    } catch { document.getElementById('url-result').innerText = 'Error'; }
}

function googleTranslateElementInit() {
    new google.translate.TranslateElement({pageLanguage: 'en'}, 'google_translate_element');
}
