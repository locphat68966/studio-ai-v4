<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>STUDIO AI V2 - KENSEI ENGINE</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #0b0f19; color: #e2e8f0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        .kensei-panel { background: linear-gradient(145deg, #111827, #1f2937); border: 1px solid #374151; box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.5); }
        .btn-glow { transition: all 0.3s ease; background: linear-gradient(90deg, #3b82f6, #8b5cf6); }
        .btn-glow:hover { box-shadow: 0 0 15px #8b5cf6; transform: translateY(-1px); }
    </style>
</head>
<body class="flex flex-col items-center justify-start min-h-screen p-4 space-y-6 relative">

    <div class="absolute top-4 right-4 z-50">
        <button onclick="toggleSettings()" class="bg-gray-800 hover:bg-gray-700 text-gray-200 px-3 py-2 rounded-xl border border-gray-600 text-sm font-medium flex items-center gap-2 transition shadow-lg">
            ⚙️ Cài đặt
        </button>
        <div id="settings-menu" class="hidden absolute right-0 mt-2 w-72 sm:w-80 bg-gray-900 border border-gray-700 rounded-xl p-2 shadow-2xl space-y-1 font-mono">
            <div class="border-b border-gray-800/60 pb-1">
                <div onclick="toggleFolder('admin-folder')" class="flex items-center justify-between p-2.5 hover:bg-gray-800 rounded-lg cursor-pointer transition group">
                    <div class="flex items-center gap-2 text-sm font-semibold text-red-400">📁 <span>Admin Control</span></div>
                    <span id="admin-folder-arrow" class="inline-block text-xs text-gray-500">▶</span>
                </div>
                <div id="admin-folder" class="hidden p-3 bg-gray-950/80 rounded-lg mt-1 mx-1 border border-gray-800 space-y-2">
                    <label for="api-link" class="block text-[11px] font-semibold text-gray-400">ĐƯỜNG LINK API (LOCAL TUNNEL):</label>
                    <input type="url" id="api-link" placeholder="https://xxxx.loca.lt" class="w-full bg-gray-900 border border-gray-700 rounded-lg px-2.5 py-2 text-xs focus:outline-none focus:border-red-500 transition text-gray-100 font-mono">
                </div>
            </div>
            <div>
                <div onclick="toggleFolder('account-folder')" class="flex items-center justify-between p-2.5 hover:bg-gray-800 rounded-lg cursor-pointer transition group">
                    <div class="flex items-center gap-3 text-sm font-semibold text-blue-400">
                        <div class="w-7 h-7 rounded-full bg-gradient-to-tr from-blue-500 to-purple-600 flex items-center justify-center text-white text-xs font-bold shadow-inner">PL</div>
                        <span>Your Account</span>
                    </div>
                    <span id="account-folder-arrow" class="inline-block text-xs text-gray-500">▶</span>
                </div>
                <div id="account-folder" class="hidden p-3 bg-gray-950/80 rounded-lg mt-1 mx-1 border border-gray-800 space-y-1 text-xs">
                    <p class="text-gray-400">Chủ sở hữu: <span class="text-gray-200 font-medium">Phạm Hồ Gia Lộc Phát</span></p>
                    <p class="text-gray-400">Vai trò: <span class="text-purple-400">Chủ sở hữu hệ thống</span></p>
                    <p class="text-gray-400">Trạng thái: <span id="auth-status-panel" class="text-yellow-500 italic">Chưa xác thực</span></p>
                </div>
            </div>
        </div>
    </div>

    <div class="w-full max-w-2xl kensei-panel rounded-2xl p-6 space-y-6 mt-12">
        <h1 class="text-3xl font-extrabold text-center tracking-wider text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-purple-500">STUDIO AI V2 - KENSEI ENGINE</h1>
        <hr class="border-gray-700">
        <div class="space-y-3">
            <label class="block text-sm font-semibold text-purple-400 tracking-wide">👤 XÁC THỰC TÀI KHOẢN:</label>
            <div class="grid grid-cols-3 gap-3">
                <button onclick="handleAuth('google')" class="bg-gray-800 hover:bg-gray-700 border border-gray-600 py-2.5 rounded-lg text-sm font-medium transition">Google</button>
                <button onclick="handleAuth('apple')" class="bg-gray-800 hover:bg-gray-700 border border-gray-600 py-2.5 rounded-lg text-sm font-medium transition">Apple</button>
                <button onclick="handleAuth('email')" class="bg-gray-800 hover:bg-gray-700 border border-gray-600 py-2.5 rounded-lg text-sm font-medium transition">✉️ Email</button>
            </div>
        </div>
        <div class="space-y-2">
            <label for="image-style" class="block text-sm font-semibold text-blue-400 tracking-wide">🎨 PHONG CÁCH HỘI HỌA (STYLE):</label>
            <select id="image-style" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-purple-500 text-gray-100 cursor-pointer">
                <option value="PHOTOREALISTIC">Photorealistic (Ảnh tả thực, độ chi tiết cao 8k)</option>
                <option value="ANIME_SHINKAI">Anime Makoto Shinkai (Hoạt hình Nhật Bản duy mỹ)</option>
                <option value="CYBERPUNK">Cyberpunk 2077 (Tương lai, đèn neon kịch tính)</option>
                <option value="CINEMATIC">Cinematic Movie (Góc máy điện ảnh, ánh sáng nghệ thuật)</option>
                <option value="COMIC_RETRO">Western Comic Book (Truyện tranh Âu Mỹ cổ điển)</option>
                <option value="OIL_PAINTING">Classic Oil Painting (Tranh sơn dầu phục hưng)</option>
                <option value="DIGITAL_ART">Digital Concept Art (Nghệ thuật số, kỳ ảo)</option>
            </select>
        </div>
        <div class="space-y-2">
            <label for="prompt" class="block text-sm font-semibold text-blue-400 tracking-wide">📝 Ý TƯỞNG SÁNG TẠO (PROMPT):</label>
            <textarea id="prompt" rows="3" placeholder="Nhập mô tả ý tưởng chi tiết tại đây..." class="w-full bg-gray-900 border border-gray-700 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-blue-500 text-gray-100 resize-none"></textarea>
        </div>
        <button onclick="generateImage()" class="w-full btn-glow text-white font-bold py-3.5 rounded-xl tracking-wider uppercase text-sm">⚡ Khởi tạo tài sản hình ảnh</button>
        <div class="border-2 border-dashed border-gray-700 rounded-2xl min-h-[250px] flex items-center justify-center relative overflow-hidden bg-gray-950">
            <div id="loading" class="hidden flex flex-col items-center space-y-2 z-10">
                <div class="w-8 h-8 border-4 border-purple-500 border-t-transparent rounded-full animate-spin"></div>
                <p class="text-xs text-purple-400 font-mono">ENGI_RUNNING...</p>
            </div>
            <img id="result-image" src="" alt="Kết quả render" class="hidden max-w-full max-h-[400px] object-contain rounded-xl z-0">
            <span id="placeholder-text" class="text-sm text-gray-500 font-mono">Hệ thống đang đợi lệnh thực thi...</span>
        </div>
    </div>

    <div class="w-full max-w-2xl bg-gray-900/50 border border-gray-800 rounded-2xl p-4 space-y-3">
        <div class="flex items-center justify-between">
            <span class="text-xs font-mono text-gray-400">📂 TRÌNH XUẤT MÃ NGUỒN (WEB FRAMEWORK)</span>
            <button onclick="downloadCodeFile()" class="bg-purple-900/40 hover:bg-purple-900/80 text-purple-300 border border-purple-700/50 px-3 py-1.5 rounded-lg text-xs font-semibold transition">📥 Tải tệp mã nguồn (.html)</button>
        </div>
        <textarea id="code-display" readonly class="w-full h-40 bg-black text-green-400 font-mono text-xs p-3 rounded-xl border border-gray-800 focus:outline-none resize-y select-all" placeholder="Đang nạp cấu trúc mã nguồn..."></textarea>
    </div>

    <script>
        function toggleSettings() { document.getElementById('settings-menu').classList.toggle('hidden'); }
        function toggleFolder(folderId) {
            const folder = document.getElementById(folderId);
            const arrow = document.getElementById(`${folderId}-arrow`);
            const isHidden = folder.classList.toggle('hidden');
            arrow.innerText = isHidden ? "▶" : "▼";
        }
        window.addEventListener('DOMContentLoaded', () => { syncCodeToTextArea(); });
        function syncCodeToTextArea() { document.getElementById('code-display').value = "<!DOCTYPE html>\n" + document.documentElement.outerHTML; }
        function downloadCodeFile() {
            const currentCode = document.documentElement.outerHTML;
            const blob = new Blob(["<!DOCTYPE html>\n" + currentCode], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a'); a.href = url; a.download = 'index.html'; document.body.appendChild(a); a.click(); document.body.removeChild(a); URL.revokeObjectURL(url);
        }
        async function handleAuth(provider) {
            const apiLink = document.getElementById('api-link').value.trim();
            const statusPanel = document.getElementById('auth-status-panel');
            if(!apiLink) { alert("Hệ thống yêu cầu: Bung mục 'Admin Control' trong Cài đặt và nhập link API!"); return; }
            statusPanel.innerText = `Đang nạp ${provider}...`;
            try {
                const response = await fetch(`${apiLink}/auth/login`, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({ provider }) });
                const data = await response.json();
                statusPanel.innerText = `Đã đồng bộ: ${data.method || provider}`;
                statusPanel.className = "text-green-400 font-bold font-mono";
            } catch (error) {
                statusPanel.innerText = "Lỗi kết nối API."; statusPanel.className = "text-red-400 font-bold";
            }
        }
        async function generateImage() {
            const apiLink = document.getElementById('api-link').value.trim();
            const prompt = document.getElementById('prompt').value.trim();
            const style = document.getElementById('image-style').value;
            const imgEl = document.getElementById('result-image');
            const loadingEl = document.getElementById('loading');
            const placeholderEl = document.getElementById('placeholder-text');
            if (!apiLink || !prompt) { alert("Yêu cầu kiểm tra: Thiếu nội dung Prompt hoặc chưa dán link API!"); return; }
            placeholderEl.classList.add('hidden'); imgEl.classList.add('hidden'); loadingEl.classList.remove('hidden');
            try {
                const response = await fetch(`${apiLink}/generate?prompt=${encodeURIComponent(prompt)}&style=${style}`);
                if (!response.ok) throw new Error();
                const blob = await response.blob();
                imgEl.src = URL.createObjectURL(blob); imgEl.classList.remove('hidden');
            } catch (error) {
                alert("Thực thi thất bại. Hãy kiểm tra Backend Colab."); placeholderEl.classList.remove('hidden');
            } finally { loadingEl.classList.add('hidden'); }
        }
    </script>
</body>
</html>
