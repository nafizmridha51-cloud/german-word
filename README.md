<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>জার্মান শব্দ অভিধান | AI Smart Learning</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body { 
            font-family: 'Noto Sans Bengali', sans-serif; 
            background: #f8fafc; 
        }
        .loader {
            border: 3px solid #f3f3f3;
            border-top: 3px solid #0ea5e9;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
            display: inline-block;
            vertical-align: middle;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        /* Article Color Coding */
        .art-der { color: #2563eb; font-weight: bold; }
        .art-die { color: #dc2626; font-weight: bold; }
        .art-das { color: #16a34a; font-weight: bold; }

        .voice-btn:active { transform: scale(0.85); }
    </style>
</head>
<body class="min-h-screen p-4 md:p-8">
    <div class="max-w-3xl mx-auto">
        <header class="text-center mb-10">
            <h1 class="text-3xl md:text-4xl font-bold text-slate-800 mb-2">জার্মান শব্দ অভিধান</h1>
            <p class="text-slate-600">✨ AI চালিত স্মার্ট লার্নিং সিস্টেম</p>
        </header>

        <!-- Search Section -->
        <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 mb-8">
            <div class="flex flex-col sm:flex-row gap-4">
                <input type="text" id="word" placeholder="যেমন: Museum, Katze, Laufen..." 
                    class="flex-1 px-4 py-3 rounded-xl border border-slate-200 focus:ring-2 focus:ring-sky-500 focus:outline-none text-lg">
                <button onclick="searchWord()" id="search-btn"
                    class="bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 px-8 rounded-xl transition-all active:scale-95 disabled:opacity-50">
                    খুঁজুন
                </button>
            </div>
        </div>

        <!-- Loading State -->
        <div id="loading" class="hidden text-center p-10">
            <div class="loader mr-2"></div>
            <span class="text-slate-600 font-medium" id="loading-text">AI বিশ্লেষণ করছে...</span>
        </div>

        <!-- Result Section -->
        <div id="result" class="hidden space-y-6">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
                <!-- Word Header: Speaker next to word, Larger Image -->
                <div class="p-8 bg-slate-50 border-b border-slate-100 flex flex-col sm:flex-row items-center justify-between gap-8">
                    <div class="flex-1 text-center sm:text-left">
                        <h3 class="text-xs uppercase tracking-widest text-slate-400 font-bold mb-2">জার্মান শব্দ</h3>
                        <div class="flex items-center justify-center sm:justify-start gap-4">
                            <div class="flex items-baseline gap-2">
                                <span id="res-article-main" class="text-2xl sm:text-3xl italic"></span>
                                <span id="res-word" class="text-4xl sm:text-5xl font-bold text-slate-800 tracking-tight"></span>
                            </div>
                            <!-- Speaker Icon Inline with Word -->
                            <button onclick="playVoice()" id="voice-btn" class="voice-btn p-2 text-sky-600 hover:text-sky-700 transition-all focus:outline-none" title="উচ্চারণ শুনুন">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.536 8.464a5 5 0 010 7.072m2.828-9.9a9 9 0 010 12.728M5.586 15H4a1 1 0 01-1-1v-4a1 1 0 011-1h1.586l4.707-4.707C10.923 3.663 12 4.109 12 5v14c0 .891-1.077 1.337-1.707.707L5.586 15z" />
                                </svg>
                            </button>
                        </div>
                        <p id="res-plural" class="text-lg text-slate-500 mt-2 font-medium"></p>
                    </div>

                    <!-- Significantly Larger Image container -->
                    <div id="image-container" class="w-48 h-48 sm:w-64 sm:h-64 bg-slate-100 rounded-3xl flex items-center justify-center overflow-hidden shadow-lg border border-slate-200 flex-shrink-0 transition-all duration-500">
                        <span class="text-slate-300 text-xs text-center px-4 italic">ছবি এখানে লোড হবে</span>
                    </div>
                </div>
                
                <div class="p-8">
                    <div class="space-y-8">
                        <!-- Meaning Row -->
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                            <div class="p-4 rounded-xl bg-slate-50/50">
                                <h3 class="text-xs uppercase tracking-widest text-slate-400 font-bold mb-2">বাংলা অর্থ</h3>
                                <p id="res-meaning" class="text-2xl text-sky-700 font-semibold"></p>
                            </div>
                            <div class="p-4 rounded-xl bg-slate-50/50">
                                <h3 class="text-xs uppercase tracking-widest text-slate-400 font-bold mb-2">English Meaning</h3>
                                <p id="res-meaning-en" class="text-xl text-slate-700 font-semibold"></p>
                            </div>
                        </div>
                        
                        <!-- Extra Info Row -->
                        <div class="grid grid-cols-2 gap-6">
                            <div>
                                <h3 class="text-xs uppercase tracking-widest text-slate-400 font-bold mb-1">উচ্চারণ (IPA)</h3>
                                <p id="res-ipa" class="text-lg text-slate-700 italic font-serif"></p>
                            </div>
                            <div>
                                <h3 class="text-xs uppercase tracking-widest text-slate-400 font-bold mb-1">ধরণ</h3>
                                <p id="res-type" class="text-lg text-slate-700 capitalize"></p>
                            </div>
                        </div>

                        <!-- Examples and Tips -->
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div class="p-6 bg-sky-50 rounded-2xl border border-sky-100 shadow-sm">
                                <h3 class="text-xs uppercase tracking-widest text-sky-600 font-bold mb-3">✨ উদাহরণ বাক্য</h3>
                                <p id="res-sentence-de" class="text-lg text-slate-800 font-medium mb-2 leading-relaxed"></p>
                                <p id="res-sentence-bn" class="text-slate-500 text-base italic"></p>
                            </div>

                            <div class="p-6 bg-amber-50 rounded-2xl border border-amber-100 shadow-sm">
                                <h3 class="text-xs uppercase tracking-widest text-amber-600 font-bold mb-2">✨ লার্নিং টিপ</h3>
                                <p id="res-tip" class="text-slate-700 text-base leading-relaxed"></p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div id="error-box" class="hidden mt-6 p-4 bg-red-50 border border-red-100 rounded-xl text-red-600 text-center">
        </div>
    </div>

    <script>
        const apiKey = ""; 
        let currentWordForVoice = "";

        async function fetchWithRetry(url, options, maxRetries = 5) {
            let delay = 1000;
            for (let i = 0; i < maxRetries; i++) {
                try {
                    const response = await fetch(url, options);
                    if (response.ok) return await response.json();
                } catch (err) {}
                if (i < maxRetries - 1) {
                    await new Promise(resolve => setTimeout(resolve, delay));
                    delay *= 2;
                }
            }
            throw new Error("Connection failed.");
        }

        function encodeWAV(samples, sampleRate) {
            const buffer = new ArrayBuffer(44 + samples.length * 2);
            const view = new DataView(buffer);
            const writeString = (offset, string) => {
                for (let i = 0; i < string.length; i++) view.setUint8(offset + i, string.charCodeAt(i));
            };
            writeString(0, 'RIFF');
            view.setUint32(4, 32 + samples.length * 2, true);
            writeString(8, 'WAVE');
            writeString(12, 'fmt ');
            view.setUint32(16, 16, true);
            view.setUint16(20, 1, true); 
            view.setUint16(22, 1, true); 
            view.setUint32(24, sampleRate, true);
            view.setUint32(28, sampleRate * 2, true);
            view.setUint16(32, 2, true);
            view.setUint16(34, 16, true);
            writeString(36, 'data');
            view.setUint32(40, samples.length * 2, true);
            let offset = 44;
            for (let i = 0; i < samples.length; i++, offset += 2) view.setInt16(offset, samples[i], true);
            return new Blob([buffer], { type: 'audio/wav' });
        }

        async function playVoice() {
            if (!currentWordForVoice) return;
            const btn = document.getElementById('voice-btn');
            btn.disabled = true;
            btn.classList.add('opacity-40');

            try {
                const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=${apiKey}`;
                const payload = {
                    contents: [{ parts: [{ text: `Say clearly in German: ${currentWordForVoice}` }] }],
                    generationConfig: {
                        responseModalities: ["AUDIO"],
                        speechConfig: { voiceConfig: { prebuiltVoiceConfig: { voiceName: "Kore" } } }
                    },
                    model: "gemini-2.5-flash-preview-tts"
                };

                const data = await fetchWithRetry(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const audioPart = data.candidates?.[0]?.content?.parts?.find(p => p.inlineData)?.inlineData;
                if (!audioPart || !audioPart.data) throw new Error("No audio");

                const audioDataB64 = audioPart.data;
                const mimeType = audioPart.mimeType;
                const sampleRate = parseInt(mimeType.match(/rate=(\d+)/)?.[1] || "24000");

                const binaryString = atob(audioDataB64);
                const bytes = new Int16Array(binaryString.length / 2);
                for (let i = 0; i < bytes.length; i++) bytes[i] = (binaryString.charCodeAt(i * 2 + 1) << 8) | binaryString.charCodeAt(i * 2);

                const wavBlob = encodeWAV(bytes, sampleRate);
                const audio = new Audio(URL.createObjectURL(wavBlob));
                audio.play();
            } catch (err) {
                console.error(err);
            } finally {
                btn.disabled = false;
                btn.classList.remove('opacity-40');
            }
        }

        async function searchWord() {
            const wordInput = document.getElementById('word');
            const inputVal = wordInput.value.trim();
            const btn = document.getElementById('search-btn');
            const loading = document.getElementById('loading');
            const result = document.getElementById('result');
            const errorBox = document.getElementById('error-box');

            if (!inputVal) return;

            errorBox.classList.add('hidden');
            result.classList.add('hidden');
            loading.classList.remove('hidden');
            btn.disabled = true;

            try {
                const geminiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
                const prompt = `Analyze the German word "${inputVal}". 
                    Provide the following in JSON format:
                    - pure_word: German word
                    - article: der/die/das or ""
                    - meaning_bn: Bengali translation
                    - meaning_en: English translation
                    - type: noun/verb/adj etc
                    - plural: plural form with article (if noun)
                    - ipa: IPA pronunciation
                    - example_de: a short German sentence using this word
                    - example_bn: Bengali translation of that sentence
                    - tip: a short learning tip or mnemonic in Bengali
                    - image_prompt: descriptive English prompt for AI image generation representing this word literally.`;

                const geminiData = await fetchWithRetry(geminiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: prompt }] }],
                        generationConfig: { responseMimeType: "application/json" }
                    })
                });

                const info = JSON.parse(geminiData.candidates?.[0]?.content?.parts?.[0]?.text || "{}");
                currentWordForVoice = (info.article ? info.article + " " : "") + info.pure_word;

                document.getElementById('res-word').innerText = info.pure_word;
                const artEl = document.getElementById('res-article-main');
                artEl.innerText = info.article;
                artEl.className = "text-2xl sm:text-3xl italic " + (info.article.toLowerCase() === 'der' ? 'art-der' : info.article.toLowerCase() === 'die' ? 'art-die' : info.article.toLowerCase() === 'das' ? 'art-das' : '');

                document.getElementById('res-plural').innerText = info.plural ? `Plural: ${info.plural}` : "";
                document.getElementById('res-meaning').innerText = info.meaning_bn;
                document.getElementById('res-meaning-en').innerText = info.meaning_en;
                document.getElementById('res-ipa').innerText = info.ipa;
                document.getElementById('res-type').innerText = info.type;
                document.getElementById('res-sentence-de').innerText = info.example_de;
                document.getElementById('res-sentence-bn').innerText = info.example_bn;
                document.getElementById('res-tip').innerText = info.tip;

                const imagenUrl = `https://generativelanguage.googleapis.com/v1beta/models/imagen-4.0-generate-001:predict?key=${apiKey}`;
                const imagenData = await fetchWithRetry(imagenUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        instances: { prompt: info.image_prompt },
                        parameters: { sampleCount: 1 }
                    })
                });

                const b64 = imagenData.predictions?.[0]?.bytesBase64Encoded;
                if (b64) {
                    document.getElementById('image-container').innerHTML = `<img src="data:image/png;base64,${b64}" class="w-full h-full object-cover" alt="${info.pure_word}">`;
                }

                loading.classList.add('hidden');
                result.classList.remove('hidden');

            } catch (err) {
                console.error(err);
                errorBox.innerText = "Dukkito, somossa hoyeche. Abar chesta korun.";
                errorBox.classList.remove('hidden');
                loading.classList.add('hidden');
            } finally {
                btn.disabled = false;
            }
        }

        document.getElementById('word').addEventListener('keypress', (e) => { if (e.key === 'Enter') searchWord(); });
    </script>
</body>
</html>
