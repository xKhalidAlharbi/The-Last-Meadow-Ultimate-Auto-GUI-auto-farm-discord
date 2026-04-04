# the-last-meadow-automation-ultimate-script
automation for new discord game 
# 🌿 The Last Meadow - Ultimate Auto GUI

This is the **best and only script** you will ever need to automate the Discord mini-game "The Last Meadow".  
It is highly optimized, ultra-fast, and designed perfectly for both **Ranger** and **Priest** classes.

### ✨ What makes this the best?
- **Supports 30+ Languages:** Play in English, Arabic, French, Portuguese, Spanish, and many more!
- **Auto Battle (Ranger):** Automatically solves the memory card game with 100% accuracy.
- **Auto Defence (Priest):** Freezes the screen and auto-catches every single fireball effortlessly.
- **Auto Target (Center):** Locks the target circle perfectly in the middle and auto-clicks it.
- **Lightning Fast Crafting:** Reads and executes the crafting arrow sequences instantly (0 delay).
- **Insane Adventure Auto-Clicker:** Speed adjustable down to `10ms` for maximum grinding.
- **Smart UI:** Compact, draggable, minimizable, and bug-free.

---

### 🚀 How to Setup (Easy Guide)

If you are using an older version or a different script, please reset your Discord first to avoid bugs.

1. Open Discord and press `Ctrl + R` (to refresh and clear old scripts).
2. Press `Ctrl + Shift + I` (or `F12`) to open the **Developer Tools**.
3. Click on the **Console** tab at the top.
4. **Copy the code below**, paste it into the console, and press `Enter`.
5. Select your language from the popup and **Enjoy!**

if you want to stop it press  `Ctrl + R` (to refresh and clear old scripts).

---

### 📜 The Code

```javascript
// =============================================
// THE LAST MEADOW - GLOBAL ULTIMATE GUI
// =============================================
(function () {
if (window._renderInterval) clearInterval(window._renderInterval);
if (window._meadowCleanup) { try { window._meadowCleanup(); } catch (e) {} }
const oldGui = document.getElementById("meadowAutoGUI"); if (oldGui) oldGui.remove();
const oldLang = document.getElementById("meadowLangModal"); if (oldLang) oldLang.remove();

const CDN = "https://cdn.discordapp.com/assets/content/";
const ICONS = {
    adventure: CDN+"282df26638d817cd1c3a926aeb51e7b2e871ce100b27fb56280a373af69c2cab.svg",
    craft: CDN+"b7febb5be9c15a67c50fc5978c3ecd1d258d0c424a0dc3ce41b2c8ac65c9e339.svg",
    wrongGame: CDN+"2c3bebb28ddf2cd9ecb1ba820617b9c88a7d21f203efa707c33bd597b82e0281.svg",
    battle: CDN+"19393b516c6014a9b5564ee7d03b33323e52c893ef9f989c8f6aeda1bcfb9756.svg",
    settings: CDN+"f89c2c158bfa6ddea9304df708f207b8a69853ddda9ee13f2066b7085605a475.svg",
    logo: CDN+"c9463738992e8f18a383be2725a5fa11d5f06b8a0820f0325033c086dd9dd649.png"
};
const ROT_MAP = {"0":"ArrowUp","90":"ArrowRight","180":"ArrowDown","270":"ArrowLeft"};

// ── 30 LANGUAGES DICTIONARY ──
const LANG_DATA = {
    en: { name:"English", flag:"🇬🇧", t:{ adventure:"Adventure", craft:"Craft", wrongGame:"Wrong Game", battle:"Battle", autoDefence:"Auto Defence", autoTarget:"Auto Target", drag:"Drag to move", speeds:"Speed Settings", advLabel:"Adventure (ms)", craftLabel:"Craft (ms)", speedTip:"Lower = faster", craftIdle:"Waiting", craftEntering:"Opening", craftSolving:"Solving", craftExiting:"Going back", battleIdle:"Waiting", battleEntering:"Opening", battleActive:"Defending", battleDone:"Victory", battleExiting:"Going back", paused:"Paused", done:"Done", noResources:"No resources"} },
    fr: { name:"Français", flag:"🇫🇷", t:{ adventure:"Aventure", craft:"Artisanat", wrongGame:"Mauvais Jeu", battle:"Combat", autoDefence:"Auto Défense", autoTarget:"Auto Cible", drag:"Glisser pour deplacer", speeds:"Reglages", advLabel:"Aventure (ms)", craftLabel:"Artisanat (ms)", speedTip:"Plus bas = rapide", craftIdle:"En attente", craftEntering:"Ouverture", craftSolving:"Resolution", craftExiting:"Retour", battleIdle:"En attente", battleEntering:"Ouverture", battleActive:"Defense", battleDone:"Victoire", battleExiting:"Retour", paused:"Pause", done:"Termine", noResources:"Pas de ressources"} },
    ar: { name:"العربية", flag:"🇸🇦", t:{ adventure:"مغامرة", craft:"صناعة", wrongGame:"لعبة خاطئة", battle:"معركة", autoDefence:"دفاع تلقائي", autoTarget:"استهداف تلقائي", drag:"اسحب للتحريك", speeds:"إعدادات السرعة", advLabel:"المغامرة (ms)", craftLabel:"الصناعة (ms)", speedTip:"أقل = أسرع", craftIdle:"في الانتظار", craftEntering:"جاري الفتح", craftSolving:"جاري الحل", craftExiting:"رجوع", battleIdle:"في الانتظار", battleEntering:"جاري الفتح", battleActive:"دفاع", battleDone:"انتصار", battleExiting:"رجوع", paused:"متوقف", done:"تم", noResources:"لا يوجد موارد"} },
    br: { name:"Português (BR)", flag:"🇧🇷", t:{ adventure:"Aventura", craft:"Criação", wrongGame:"Jogo Errado", battle:"Batalha", autoDefence:"Auto Defesa", autoTarget:"Auto Alvo", drag:"Arraste", speeds:"Velocidade", advLabel:"Aventura (ms)", craftLabel:"Criação (ms)", speedTip:"Menor = mais rápido", craftIdle:"Aguardando", craftEntering:"Abrindo", craftSolving:"Resolvendo", craftExiting:"Voltando", battleIdle:"Aguardando", battleEntering:"Abrindo", battleActive:"Defendendo", battleDone:"Vitória", battleExiting:"Voltando", paused:"Pausado", done:"Pronto", noResources:"Sem recursos"} },
    pt: { name:"Português (PT)", flag:"🇵🇹", t:{ adventure:"Aventura", craft:"Artesanato", wrongGame:"Jogo Errado", battle:"Batalha", autoDefence:"Auto Defesa", autoTarget:"Auto Alvo", drag:"Arrastar", speeds:"Velocidade", advLabel:"Aventura (ms)", craftLabel:"Artesanato (ms)", speedTip:"Menor = rápido", craftIdle:"Espera", craftEntering:"A abrir", craftSolving:"A resolver", craftExiting:"A voltar", battleIdle:"Espera", battleEntering:"A abrir", battleActive:"A defender", battleDone:"Vitória", battleExiting:"A voltar", paused:"Pausa", done:"Feito", noResources:"Sem recursos"} },
    es: { name:"Español", flag:"🇪🇸", t:{ adventure:"Aventura", craft:"Fabricar", wrongGame:"Juego Equivocado", battle:"Batalla", autoDefence:"Auto Defensa", autoTarget:"Auto Objetivo", drag:"Arrastrar", speeds:"Velocidades", advLabel:"Aventura (ms)", craftLabel:"Fabricar (ms)", speedTip:"Menor = rápido", craftIdle:"Esperando", craftEntering:"Abriendo", craftSolving:"Resolviendo", craftExiting:"Volviendo", battleIdle:"Esperando", battleEntering:"Abriendo", battleActive:"Defendiendo", battleDone:"Victoria", battleExiting:"Volviendo", paused:"Pausa", done:"Hecho", noResources:"Sin recursos"} },
    de: { name:"Deutsch", flag:"🇩🇪", t:{ adventure:"Abenteuer", craft:"Handwerk", wrongGame:"Falsches Spiel", battle:"Kampf", autoDefence:"Auto-Abwehr", autoTarget:"Auto-Ziel", drag:"Ziehen", speeds:"Geschwindigkeit", advLabel:"Abenteuer (ms)", craftLabel:"Handwerk (ms)", speedTip:"Niedriger = schneller", craftIdle:"Warten", craftEntering:"Öffnen", craftSolving:"Lösen", craftExiting:"Zurück", battleIdle:"Warten", battleEntering:"Öffnen", battleActive:"Verteidigen", battleDone:"Sieg", battleExiting:"Zurück", paused:"Pause", done:"Fertig", noResources:"Keine Ressourcen"} },
    it: { name:"Italiano", flag:"🇮🇹", t:{ adventure:"Avventura", craft:"Creazione", wrongGame:"Gioco Sbagliato", battle:"Battaglia", autoDefence:"Auto Difesa", autoTarget:"Auto Bersaglio", drag:"Trascina", speeds:"Velocità", advLabel:"Avventura (ms)", craftLabel:"Creazione (ms)", speedTip:"Minore = veloce", craftIdle:"Attesa", craftEntering:"Apertura", craftSolving:"Risoluzione", craftExiting:"Ritorno", battleIdle:"Attesa", battleEntering:"Apertura", battleActive:"Difesa", battleDone:"Vittoria", battleExiting:"Ritorno", paused:"Pausa", done:"Fatto", noResources:"Senza risorse"} },
    ru: { name:"Русский", flag:"🇷🇺", t:{ adventure:"Приключение", craft:"Крафт", wrongGame:"Не та игра", battle:"Битва", autoDefence:"Авто-защита", autoTarget:"Авто-цель", drag:"Тянуть", speeds:"Скорость", advLabel:"Приключение (ms)", craftLabel:"Крафт (ms)", speedTip:"Ниже = быстрее", craftIdle:"Ожидание", craftEntering:"Открытие", craftSolving:"Решение", craftExiting:"Назад", battleIdle:"Ожидание", battleEntering:"Открытие", battleActive:"Защита", battleDone:"Победа", battleExiting:"Назад", paused:"Пауза", done:"Готово", noResources:"Нет ресурсов"} },
    tr: { name:"Türkçe", flag:"🇹🇷", t:{ adventure:"Macera", craft:"Zanaat", wrongGame:"Yanlış Oyun", battle:"Savaş", autoDefence:"Oto Savunma", autoTarget:"Oto Hedef", drag:"Sürükle", speeds:"Hızlar", advLabel:"Macera (ms)", craftLabel:"Zanaat (ms)", speedTip:"Düşük = hızlı", craftIdle:"Bekleniyor", craftEntering:"Açılıyor", craftSolving:"Çözülüyor", craftExiting:"Geri", battleIdle:"Bekleniyor", battleEntering:"Açılıyor", battleActive:"Savunma", battleDone:"Zafer", battleExiting:"Geri", paused:"Duraklatıldı", done:"Bitti", noResources:"Kaynak yok"} },
    ja: { name:"日本語", flag:"🇯🇵", t:{ adventure:"冒険", craft:"クラフト", wrongGame:"違うゲーム", battle:"バトル", autoDefence:"自動防衛", autoTarget:"自動ターゲット", drag:"ドラッグ", speeds:"速度設定", advLabel:"冒険 (ms)", craftLabel:"クラフト (ms)", speedTip:"低い = 早い", craftIdle:"待機中", craftEntering:"開く", craftSolving:"解決中", craftExiting:"戻る", battleIdle:"待機中", battleEntering:"開く", battleActive:"防衛中", battleDone:"勝利", battleExiting:"戻る", paused:"一時停止", done:"完了", noResources:"リソースなし"} },
    zh: { name:"中文", flag:"🇨🇳", t:{ adventure:"冒险", craft:"制作", wrongGame:"错误游戏", battle:"战斗", autoDefence:"自动防御", autoTarget:"自动瞄准", drag:"拖动", speeds:"速度设置", advLabel:"冒险 (ms)", craftLabel:"制作 (ms)", speedTip:"更低=更快", craftIdle:"等待", craftEntering:"打开", craftSolving:"解决", craftExiting:"返回", battleIdle:"等待", battleEntering:"打开", battleActive:"防御中", battleDone:"胜利", battleExiting:"返回", paused:"暂停", done:"完成", noResources:"没有资源"} },
    ko: { name:"한국어", flag:"🇰🇷", t:{ adventure:"모험", craft:"제작", wrongGame:"잘못된 게임", battle:"전투", autoDefence:"자동 방어", autoTarget:"자동 타겟", drag:"드래그", speeds:"속도 설정", advLabel:"모험 (ms)", craftLabel:"제작 (ms)", speedTip:"낮음=빠름", craftIdle:"대기 중", craftEntering:"열기", craftSolving:"해결 중", craftExiting:"뒤로", battleIdle:"대기 중", battleEntering:"열기", battleActive:"방어 중", battleDone:"승리", battleExiting:"뒤로", paused:"일시정지", done:"완료", noResources:"자원 없음"} },
    hi: { name:"हिन्दी", flag:"🇮🇳", t:{ adventure:"साहसिक काम", craft:"शिल्प", wrongGame:"गलत खेल", battle:"लड़ाई", autoDefence:"ऑटो रक्षा", autoTarget:"ऑटो लक्ष्य", drag:"खींचें", speeds:"गति", advLabel:"साहसिक (ms)", craftLabel:"शिल्प (ms)", speedTip:"कम = तेज़", craftIdle:"प्रतीक्षा", craftEntering:"खोल रहा है", craftSolving:"हल कर रहा है", craftExiting:"वापस", battleIdle:"प्रतीक्षा", battleEntering:"खोल रहा है", battleActive:"रक्षा", battleDone:"जीत", battleExiting:"वापस", paused:"रुका हुआ", done:"हो गया", noResources:"कोई संसाधन नहीं"} },
    pl: { name:"Polski", flag:"🇵🇱", t:{ adventure:"Przygoda", craft:"Rzemiosło", wrongGame:"Zła Gra", battle:"Bitwa", autoDefence:"Auto Obrona", autoTarget:"Auto Cel", drag:"Przeciągnij", speeds:"Szybkość", advLabel:"Przygoda (ms)", craftLabel:"Rzemiosło (ms)", speedTip:"Niżej = szybciej", craftIdle:"Czekanie", craftEntering:"Otwieranie", craftSolving:"Rozwiązywanie", craftExiting:"Wstecz", battleIdle:"Czekanie", battleEntering:"Otwieranie", battleActive:"Obrona", battleDone:"Zwycięstwo", battleExiting:"Wstecz", paused:"Pauza", done:"Gotowe", noResources:"Brak zasobów"} },
    nl: { name:"Nederlands", flag:"🇳🇱", t:{ adventure:"Avontuur", craft:"Ambacht", wrongGame:"Verkeerd Spel", battle:"Gevecht", autoDefence:"Auto Verdediging", autoTarget:"Auto Doelwit", drag:"Slepen", speeds:"Snelheid", advLabel:"Avontuur (ms)", craftLabel:"Ambacht (ms)", speedTip:"Lager = sneller", craftIdle:"Wachten", craftEntering:"Openen", craftSolving:"Oplossen", craftExiting:"Terug", battleIdle:"Wachten", battleEntering:"Openen", battleActive:"Verdedigen", battleDone:"Overwinning", battleExiting:"Terug", paused:"Pauze", done:"Klaar", noResources:"Geen bronnen"} },
    sv: { name:"Svenska", flag:"🇸🇪", t:{ adventure:"Äventyr", craft:"Hantverk", wrongGame:"Fel Spel", battle:"Strid", autoDefence:"Auto Försvar", autoTarget:"Auto Mål", drag:"Dra", speeds:"Hastighet", advLabel:"Äventyr (ms)", craftLabel:"Hantverk (ms)", speedTip:"Lägre = snabbare", craftIdle:"Väntar", craftEntering:"Öppnar", craftSolving:"Löser", craftExiting:"Tillbaka", battleIdle:"Väntar", battleEntering:"Öppnar", battleActive:"Försvarar", battleDone:"Seger", battleExiting:"Tillbaka", paused:"Pausad", done:"Klar", noResources:"Inga resurser"} },
    id: { name:"Bahasa Indonesia", flag:"🇮🇩", t:{ adventure:"Petualangan", craft:"Kerajinan", wrongGame:"Game Salah", battle:"Pertarungan", autoDefence:"Auto Bertahan", autoTarget:"Auto Target", drag:"Geser", speeds:"Kecepatan", advLabel:"Petualangan (ms)", craftLabel:"Kerajinan (ms)", speedTip:"Rendah = cepat", craftIdle:"Menunggu", craftEntering:"Membuka", craftSolving:"Menyelesaikan", craftExiting:"Kembali", battleIdle:"Menunggu", battleEntering:"Membuka", battleActive:"Bertahan", battleDone:"Menang", battleExiting:"Kembali", paused:"Jeda", done:"Selesai", noResources:"Tidak ada SDA"} },
    vi: { name:"Tiếng Việt", flag:"🇻🇳", t:{ adventure:"Phiêu lưu", craft:"Chế tạo", wrongGame:"Sai trò chơi", battle:"Chiến đấu", autoDefence:"Tự phòng thủ", autoTarget:"Tự nhắm", drag:"Kéo", speeds:"Tốc độ", advLabel:"Phiêu lưu (ms)", craftLabel:"Chế tạo (ms)", speedTip:"Thấp = Nhanh", craftIdle:"Đang chờ", craftEntering:"Đang mở", craftSolving:"Đang giải", craftExiting:"Trở lại", battleIdle:"Đang chờ", battleEntering:"Đang mở", battleActive:"Phòng thủ", battleDone:"Chiến thắng", battleExiting:"Trở lại", paused:"Tạm dừng", done:"Xong", noResources:"Hết tài nguyên"} },
    th: { name:"ไทย", flag:"🇹🇭", t:{ adventure:"ผจญภัย", craft:"คราฟต์", wrongGame:"เกมผิด", battle:"ต่อสู้", autoDefence:"ป้องกันอัตโนมัติ", autoTarget:"เป้าหมายอัตโนมัติ", drag:"ลาก", speeds:"ความเร็ว", advLabel:"ผจญภัย (ms)", craftLabel:"คราฟต์ (ms)", speedTip:"ต่ำ = เร็ว", craftIdle:"รอ", craftEntering:"กำลังเปิด", craftSolving:"กำลังแก้", craftExiting:"กลับ", battleIdle:"รอ", battleEntering:"กำลังเปิด", battleActive:"ป้องกัน", battleDone:"ชนะ", battleExiting:"กลับ", paused:"หยุด", done:"เสร็จ", noResources:"ไม่มีทรัพยากร"} },
    el: { name:"Ελληνικά", flag:"🇬🇷", t:{ adventure:"Περιπέτεια", craft:"Κατασκευή", wrongGame:"Λάθος Παιχνίδι", battle:"Μάχη", autoDefence:"Auto Άμυνα", autoTarget:"Auto Στόχος", drag:"Σύρετε", speeds:"Ταχύτητα", advLabel:"Περιπέτεια (ms)", craftLabel:"Κατασκευή (ms)", speedTip:"Χαμηλότερα = πιο γρήγορα", craftIdle:"Αναμονή", craftEntering:"Άνοιγμα", craftSolving:"Επίλυση", craftExiting:"Πίσω", battleIdle:"Αναμονή", battleEntering:"Άνοιγμα", battleActive:"Άμυνα", battleDone:"Νίκη", battleExiting:"Πίσω", paused:"Παύση", done:"Έγινε", noResources:"Χωρίς πόρους"} },
    cs: { name:"Čeština", flag:"🇨🇿", t:{ adventure:"Dobrodružství", craft:"Řemeslo", wrongGame:"Špatná Hra", battle:"Bitva", autoDefence:"Auto Obrana", autoTarget:"Auto Cíl", drag:"Táhni", speeds:"Rychlost", advLabel:"Dobro (ms)", craftLabel:"Řemeslo (ms)", speedTip:"Méně = Rychleji", craftIdle:"Čekání", craftEntering:"Otevírání", craftSolving:"Řešení", craftExiting:"Zpět", battleIdle:"Čekání", battleEntering:"Otevírání", battleActive:"Obrana", battleDone:"Výhra", battleExiting:"Zpět", paused:"Pauza", done:"Hotovo", noResources:"Bez zdrojů"} },
    ro: { name:"Română", flag:"🇷🇴", t:{ adventure:"Aventură", craft:"Artizanat", wrongGame:"Joc Greșit", battle:"Bătălie", autoDefence:"Auto Apărare", autoTarget:"Auto Țintă", drag:"Trage", speeds:"Viteză", advLabel:"Aventură (ms)", craftLabel:"Artizanat (ms)", speedTip:"Mic = rapid", craftIdle:"Așteptare", craftEntering:"Deschidere", craftSolving:"Rezolvare", craftExiting:"Înapoi", battleIdle:"Așteptare", battleEntering:"Deschidere", battleActive:"Apărare", battleDone:"Victorie", battleExiting:"Înapoi", paused:"Pauză", done:"Gata", noResources:"Fără resurse"} },
    hu: { name:"Magyar", flag:"🇭🇺", t:{ adventure:"Kaland", craft:"Barkács", wrongGame:"Rossz Játék", battle:"Csata", autoDefence:"Auto Védelem", autoTarget:"Auto Cél", drag:"Húzás", speeds:"Sebesség", advLabel:"Kaland (ms)", craftLabel:"Barkács (ms)", speedTip:"Kisebb = Gyorsabb", craftIdle:"Várakozás", craftEntering:"Megnyitás", craftSolving:"Megoldás", craftExiting:"Vissza", battleIdle:"Várakozás", battleEntering:"Megnyitás", battleActive:"Védekezés", battleDone:"Győzelem", battleExiting:"Vissza", paused:"Szünet", done:"Kész", noResources:"Nincs nyersanyag"} },
    da: { name:"Dansk", flag:"🇩🇰", t:{ adventure:"Eventyr", craft:"Håndværk", wrongGame:"Forkert Spil", battle:"Kamp", autoDefence:"Auto Forsvar", autoTarget:"Auto Mål", drag:"Træk", speeds:"Hastighed", advLabel:"Eventyr (ms)", craftLabel:"Håndværk (ms)", speedTip:"Lavere = hurtigere", craftIdle:"Venter", craftEntering:"Åbner", craftSolving:"Løser", craftExiting:"Tilbage", battleIdle:"Venter", battleEntering:"Åbner", battleActive:"Forsvarer", battleDone:"Sejr", battleExiting:"Tilbage", paused:"Pause", done:"Færdig", noResources:"Ingen ressourcer"} },
    fi: { name:"Suomi", flag:"🇫🇮", t:{ adventure:"Seikkailu", craft:"Käsityö", wrongGame:"Väärä Peli", battle:"Taistelu", autoDefence:"Auto Puolustus", autoTarget:"Auto Kohde", drag:"Vedä", speeds:"Nopeus", advLabel:"Seikkailu (ms)", craftLabel:"Käsityö (ms)", speedTip:"Pienempi = nopeampi", craftIdle:"Odottaa", craftEntering:"Avaa", craftSolving:"Ratkaisee", craftExiting:"Takaisin", battleIdle:"Odottaa", battleEntering:"Avaa", battleActive:"Puolustaa", battleDone:"Voitto", battleExiting:"Takaisin", paused:"Tauko", done:"Valmis", noResources:"Ei resursseja"} },
    no: { name:"Norsk", flag:"🇳🇴", t:{ adventure:"Eventyr", craft:"Håndverk", wrongGame:"Feil Spill", battle:"Kamp", autoDefence:"Auto Forsvar", autoTarget:"Auto Mål", drag:"Dra", speeds:"Hastighet", advLabel:"Eventyr (ms)", craftLabel:"Håndverk (ms)", speedTip:"Lavere = raskere", craftIdle:"Venter", craftEntering:"Åpner", craftSolving:"Løser", craftExiting:"Tilbake", battleIdle:"Venter", battleEntering:"Åpner", battleActive:"Forsvarer", battleDone:"Seier", battleExiting:"Tilbake", paused:"Pause", done:"Ferdig", noResources:"Ingen ressurser"} },
    he: { name:"עברית", flag:"🇮🇱", t:{ adventure:"הרפתקה", craft:"יצירה", wrongGame:"משחק שגוי", battle:"קרב", autoDefence:"הגנה אוטומטית", autoTarget:"מטרה אוטומטית", drag:"גרור", speeds:"מהירות", advLabel:"הרפתקה (ms)", craftLabel:"יצירה (ms)", speedTip:"נמוך = מהיר", craftIdle:"ממתין", craftEntering:"פותח", craftSolving:"פותר", craftExiting:"חוזר", battleIdle:"ממתין", battleEntering:"פותח", battleActive:"מגן", battleDone:"ניצחון", battleExiting:"חוזר", paused:"מושהה", done:"בוצע", noResources:"אין משאבים"} },
    ms: { name:"Bahasa Melayu", flag:"🇲🇾", t:{ adventure:"Pengembaraan", craft:"Kraf", wrongGame:"Permainan Salah", battle:"Pertempuran", autoDefence:"Pertahanan Auto", autoTarget:"Sasaran Auto", drag:"Seret", speeds:"Kelajuan", advLabel:"Pengembaraan", craftLabel:"Kraf", speedTip:"Rendah = Cepat", craftIdle:"Menunggu", craftEntering:"Membuka", craftSolving:"Menyelesaikan", craftExiting:"Kembali", battleIdle:"Menunggu", battleEntering:"Membuka", battleActive:"Bertahan", battleDone:"Kemenangan", battleExiting:"Kembali", paused:"Jeda", done:"Selesai", noResources:"Tiada sumber"} },
    bn: { name:"বাংলা", flag:"🇧🇩", t:{ adventure:"অ্যাডভেঞ্চার", craft:"ক্রাফট", wrongGame:"ভুল খেলা", battle:"যুদ্ধ", autoDefence:"অটো ডিফেন্স", autoTarget:"অটো টার্গেট", drag:"টানুন", speeds:"গতি", advLabel:"অ্যাডভেঞ্চার (ms)", craftLabel:"ক্রাফট (ms)", speedTip:"কম = দ্রুত", craftIdle:"অপেক্ষায়", craftEntering:"খুলছে", craftSolving:"সমাধান", craftExiting:"ফিরে", battleIdle:"অপেক্ষায়", battleEntering:"খুলছে", battleActive:"প্রতিরক্ষা", battleDone:"বিজয়", battleExiting:"ফিরে", paused:"স্থগিত", done:"সম্পন্ন", noResources:"সম্পদ নেই"} }
};

let advInterval = null, clkInterval = null, clkCount = 0;
let advOn = false, crOn = false, btOn = false, autoDfOn = false, autoTgOn = false, clkRunning = false, dragging = false;
let lang = "en", advDelay = 50, crDelay = 520, activeNav = null, isMinimized = false;

const CS = { IDLE:0, ENTERING:1, SOLVING:2, EXITING:3, WAITING:4 };
let crState = CS.IDLE, crTimer = null, crBusy = false, crTotalWait = 0, crWaitStart = 0;
const BS = { IDLE:0, ENTERING:1, ACTIVE:2, DONE:3, EXITING:4, WAITING:5 };
let btState = BS.IDLE, btTimer = null, btRAF = null;
let btBusy = false, btTotalWait = 0, btWaitStart = 0;
let btGameDoc = null, btGameWin = null;
let crIconEl, crTextEl, btIconEl, btTextEl, autoDfIconEl, autoDfTextEl, autoTgIconEl, autoTgTextEl;

let originalWidth = null, mouseLockerInterval = null, tgInterval = null;

function hd(b) { return b + (Math.random() * 2 - 1) * b * 0.15; }
function sleep(ms) { return new Promise(r => setTimeout(r, ms)); }
function hsleep(ms) { return sleep(hd(ms)); }
function tx(k) { return LANG_DATA[lang].t[k] || k; }
function fmtTime(s) { return `${String(Math.floor(s/60)).padStart(2,"0")}:${String(s%60).padStart(2,"0")}`; }
function setText(el, v) { if (el && el.textContent !== v) el.textContent = v; }
function setCSS(el, p, v) { if (el && el.style[p] !== v) el.style[p] = v; }

function sendKey(key) {
    document.dispatchEvent(new KeyboardEvent("keydown", {key, code:key, bubbles:true, cancelable:true}));
    document.dispatchEvent(new KeyboardEvent("keyup", {key, code:key, bubbles:true, cancelable:true}));
}
function fastClick(el) {
    if (!el) return; el.click();
    const o = {bubbles:true, cancelable:true, view:window, button:0};
    el.dispatchEvent(new PointerEvent("pointerdown", o)); el.dispatchEvent(new MouseEvent("mousedown", o));
    el.dispatchEvent(new PointerEvent("pointerup", o)); el.dispatchEvent(new MouseEvent("mouseup", o));
}
function reactClick(el) {
    if (!el) return false;
    const c = el.querySelector('[role="button"]') || el.querySelector('.clickable__5c90e') || el.closest('[role="button"]') || el.closest('.clickable__5c90e') || el;
    const r = c.getBoundingClientRect(); if (r.width === 0 || r.height === 0) return false;
    const x = r.left + r.width/2 + (Math.random()*4-2); const y = r.top + r.height/2 + (Math.random()*4-2);
    const o = {bubbles:true, cancelable:true, view:window, clientX:x, clientY:y, button:0};
    c.dispatchEvent(new PointerEvent("pointerdown", {...o, pointerId:1})); c.dispatchEvent(new MouseEvent("mousedown", o));
    if (c.focus) c.focus();
    c.dispatchEvent(new PointerEvent("pointerup", {...o, pointerId:1})); c.dispatchEvent(new MouseEvent("mouseup", o));
    c.dispatchEvent(new MouseEvent("click", o)); return true;
}
function dualClick(el) { if (!el) return false; reactClick(el); setTimeout(() => fastClick(el), 150); return true; }
function getGameContainer() { return document.querySelector(".container__73695"); }
function getAdvButton() { const gc = getGameContainer(); if (!gc) return null; return gc.querySelector('.activityButtonText__8af73[data-text-variant="heading-xxl/normal"]') || Array.from(gc.querySelectorAll(".activityButton__8af73")).find(el => el.textContent?.includes("Adventure")); }
function findBtn(name) { const gc = getGameContainer(); if (!gc) return null; for (const b of gc.querySelectorAll(".activityButton__8af73")) if (b.textContent?.includes(name)) return b; return null; }
function getResourcePopup() { const p = document.querySelector(".container__139d4"); if (!p) return null; const t = p.textContent || ""; return (t.includes("out of resources") || t.includes("try again")) ? p : null; }
function dismissPopup() { const p = getResourcePopup(); if (!p) return false; const b = p.querySelector('.button__65fca[role="button"]'); if (b) { dualClick(b); return true; } return false; }
function isSuccessScreen() { const gc = getGameContainer(); if (!gc) { for (const el of document.querySelectorAll('[data-text-variant]')) if (el.textContent.includes("Success")) return true; } else if (gc.textContent.includes("Success")) return true; return !isMainScreen() && !!findContinueBtn(); }
function findContinueBtn() { for (const b of document.querySelectorAll('.button__65fca[role="button"]')) { const v = b.querySelector('.visibleText__65fca'); if (v && v.textContent.trim() === "Continue") return b; } return null; }
function findBackBtn() { return document.querySelector('.back__51dc1[role="button"]') || document.querySelector('[aria-label="Back"][role="button"]') || (document.querySelector('img[alt="Back"]')?.closest('[role="button"]')) || null; }
async function goBackToMain(max) { for (let i = 0; i < max; i++) { if (isMainScreen()) return true; const c = findContinueBtn(); if (c) { dualClick(c); await sleep(600); if (isMainScreen()) return true; } const b = findBackBtn(); if (b) { dualClick(b); await sleep(600); if (isMainScreen()) return true; } if (!c && !b) await sleep(400); } return isMainScreen(); }
function isMainScreen() { return !!findBtn("Adventure"); }
function readCountdownFor(name) { const btn = findBtn(name); if (!btn) return null; const cd = btn.querySelector(".countdownText__8af73"); if (!cd) return null; const m = cd.textContent?.trim().match(/(\d+):(\d+)/); return m ? parseInt(m[1]) * 60 + parseInt(m[2]) : null; }
function readCraftCountdown() { return readCountdownFor("Craft"); } function readBattleCountdown() { return readCountdownFor("Battle"); }
function getCraftArrows() { const s = document.querySelector(".sequences__34527"); if (!s) return null; const imgs = s.querySelectorAll(".character__34527 img"); return imgs.length > 0 ? [...imgs] : null; }
function readCraftSequence() { const s = document.querySelector(".sequences__34527"); if (!s) return null; const chars = s.querySelectorAll(".character__34527"); if (!chars.length) return null; const arrows = []; let hasError = false; for (const ch of chars) { const img = ch.querySelector("img"); if (!img) continue; const cls = img.className || ""; const ok = cls.includes("arrowSuccess"); const err = cls.includes("arrowError") || cls.includes("arrowFail"); if (err) hasError = true; const rot = (img.style.transform || "").match(/rotateZ\((\d+)deg\)/); arrows.push({ key: ROT_MAP[rot ? rot[1] : "0"] || "ArrowUp", done: ok, error: err }); } return { arrows, hasError }; }
function findGameDocument() { const g = document.querySelector('[class*="game__"]'); if (g && g.getBoundingClientRect().width > 0) return { doc: document, win: window }; return { doc: document, win: window }; }
function getBattleGame() { return (btGameDoc || document).querySelector('[class*="game__"]') || document.querySelector('[class*="game__"]'); }
function getCardGrid() { const game = getBattleGame(); if (!game) return null; const grid = game.querySelector('[class*="grid__"]'); if (!grid) return null; const items = [...grid.querySelectorAll('[class*="gridItem"]')]; return items.length >= 9 ? items : null; }
function isBattleActive() { return !!getCardGrid(); }
function getCardSymbol(card) { const svg = card.querySelector('svg'); if (svg) return svg.getAttribute('viewBox') || svg.getAttribute('width') + 'x' + svg.getAttribute('height'); const front = card.querySelector('[class*="gridAssetFront"]'); if (front) { const img = front.querySelector('img'); if (img && img.src) return img.src; return front.innerHTML.length + ':' + front.children.length; } return null; }
function isCardMatched(card) { if (/matched|success|complete|solved/.test(card.outerHTML.toLowerCase())) return true; const check = (el) => { try { const s = getComputedStyle(el); for (const p of ['borderColor','borderTopColor','backgroundColor','outlineColor','color']) { const c = s[p]; if (!c) continue; const m = c.match(/rgba?\(\s*(\d+),\s*(\d+),\s*(\d+)/); if (m && +m[2] > 80 && +m[2] > +m[1]*1.3 && +m[2] > +m[3]*1.3) return true; } } catch(e) {} return false; }; if (check(card)) return true; for (const ch of card.children) if (check(ch)) return true; try { if (getComputedStyle(card).pointerEvents === 'none') return true; } catch(e) {} return false; }
function readBattleScore() { const h = document.querySelector('[class*="leftHeader"]'); if (!h) return null; const el = h.querySelector('[data-text-variant="heading-xxl/normal"]'); if (!el) return null; const m = el.textContent?.match(/(\d+)\s*\/\s*(\d+)/); return m ? { cur: +m[1], max: +m[2] } : null; }
function canNav(w) { return activeNav === null || activeNav === w; } function lockNav(w) { activeNav = w; } function unlockNav(w) { if (activeNav === w) activeNav = null; }

function autoAdv() { const b = getAdvButton(); if (b) fastClick(b); }
function startAdv() { stopAdv(); advInterval = setInterval(autoAdv, advDelay); }
function stopAdv() { clearInterval(advInterval); advInterval = null; }

async function craftTick() {
    if (!crOn || dragging || crBusy) return; crBusy = true;
    try {
        if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("craft"); crState = CS.WAITING; crBusy = false; return; }
        if (isSuccessScreen()) { await goBackToMain(3); unlockNav("craft"); const cd = readCraftCountdown(); crTotalWait = (cd !== null && cd > 0) ? cd : 0; crWaitStart = Date.now(); crState = CS.WAITING; crBusy = false; return; }
        switch (crState) {
            case CS.IDLE: { if (getCraftArrows()) { lockNav("craft"); crState = CS.SOLVING; break; } const cd = readCraftCountdown(); if (cd !== null && cd > 0) { crTotalWait = cd; crWaitStart = Date.now(); crState = CS.WAITING; break; } if (!canNav("craft") || !isMainScreen()) break; const b = findBtn("Craft"); if (b) { lockNav("craft"); dualClick(b); crState = CS.ENTERING; } break; }
            case CS.ENTERING: { let w = 0; while (w < 4000) { if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("craft"); crState = CS.WAITING; return; } if (getCraftArrows()) { crState = CS.SOLVING; break; } if (w > 800 && isMainScreen()) { const b = findBtn("Craft"); if (b) dualClick(b); } await sleep(200); w += 200; } if (crState === CS.ENTERING) { unlockNav("craft"); crState = CS.IDLE; } break; }
            case CS.SOLVING: { 
                const d = readCraftSequence(); 
                if (!d || !d.arrows) { crState = CS.EXITING; break; } 
                const rem = d.arrows.filter(a => !a.done); 
                if (rem.length === 0) { crState = CS.EXITING; break; } 
                for (const arrow of rem) { 
                    if (!crOn) break; 
                    sendKey(arrow.key); 
                    await sleep(15); 
                } 
                await sleep(300); 
                if (!getCraftArrows()) crState = CS.EXITING; 
                break; 
            }
            case CS.EXITING: { await sleep(300); await goBackToMain(3); unlockNav("craft"); const cd = readCraftCountdown(); crTotalWait = (cd !== null && cd > 0) ? cd : 0; crWaitStart = Date.now(); crState = CS.WAITING; break; }
            case CS.WAITING: { const cd = readCraftCountdown(); if (cd === null || cd <= 0) { await sleep(2000); crState = CS.IDLE; } else if (crTotalWait === 0) { crTotalWait = cd; crWaitStart = Date.now(); } break; }
        }
    } finally { crBusy = false; }
}
function startCraft() { stopCraft(); crState = CS.IDLE; const lp = () => { craftTick(); crTimer = setTimeout(lp, hd(crDelay)); }; crTimer = setTimeout(lp, hd(crDelay)); }
function stopCraft() { clearTimeout(crTimer); crTimer = null; unlockNav("craft"); crState = CS.IDLE; crBusy = false; }

async function battleCardSolve() {
    const cards = getCardGrid(); if (!cards || cards.length < 9) return false;
    let memory = {}; let matched = new Set();
    for (let round = 0; round < 30 && btOn; round++) {
        const freshCards = getCardGrid(); const cc = (freshCards && freshCards.length >= 9) ? freshCards : cards; cc.forEach((c, i) => { if (isCardMatched(c)) matched.add(i); });
        const sc = readBattleScore(); if ((sc && sc.cur >= sc.max) || matched.size >= cc.length) return true;
        const unmatched = []; for (let i = 0; i < cc.length; i++) if (!matched.has(i)) unmatched.push(i); if (unmatched.length === 0) return true;
        const groups = {}; for (const [idx, sym] of Object.entries(memory)) { const i = parseInt(idx); if (matched.has(i)) continue; if (!groups[sym]) groups[sym] = []; groups[sym].push(i); }
        let triplet = null; for (const indices of Object.values(groups)) { if (indices.length >= 3) { triplet = indices.slice(0, 3); break; } }
        if (triplet) { for (const idx of triplet) { if (!btOn) return false; reactClick(cc[idx]); await sleep(500); } await sleep(1500); const vc = getCardGrid() || cc; triplet.forEach(idx => { if (idx < vc.length && isCardMatched(vc[idx])) { matched.add(idx); delete memory[idx]; } }); if (!triplet.some(idx => matched.has(idx))) { triplet.forEach(idx => delete memory[idx]); await sleep(1000); } continue; }
        const unknown = unmatched.filter(i => !memory[i]);
        if (unknown.length > 0) { const batch = unknown.slice(0, 3); for (const idx of batch) { if (!btOn) return false; reactClick(cc[idx]); await sleep(800); const sym = getCardSymbol(cc[idx]); if (sym) memory[idx] = sym; } await sleep(1500); const lc = getCardGrid() || cc; batch.forEach(idx => { if (idx < lc.length && isCardMatched(lc[idx])) { matched.add(idx); delete memory[idx]; } }); continue; }
        const partialGroups = {}; for (const [idx, sym] of Object.entries(memory)) { const i = parseInt(idx); if (matched.has(i)) continue; if (!partialGroups[sym]) partialGroups[sym] = []; partialGroups[sym].push(i); } let bestGroup = null, bestSize = 0; for (const [sym, indices] of Object.entries(partialGroups)) { if (indices.length > bestSize) { bestSize = indices.length; bestGroup = indices; } }
        if (bestGroup && bestGroup.length >= 3) { for (const idx of bestGroup.slice(0, 3)) { reactClick(cc[idx]); await sleep(500); } await sleep(1500); const vc = getCardGrid() || cc; bestGroup.forEach(idx => { if (idx < vc.length && isCardMatched(vc[idx])) { matched.add(idx); delete memory[idx]; } }); } else { memory = {}; await sleep(1000); }
    } const fs = readBattleScore(); return (fs && fs.cur >= fs.max) || matched.size >= 9;
}
async function battleTick() {
    if (!btOn || dragging || btBusy) return; btBusy = true;
    try {
        if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("battle"); btState = BS.WAITING; btBusy = false; return; }
        if (isSuccessScreen()) { await goBackToMain(3); unlockNav("battle"); const cd = readBattleCountdown(); btTotalWait = (cd !== null && cd > 0) ? cd : 0; btWaitStart = Date.now(); btState = BS.WAITING; btBusy = false; return; }
        switch (btState) {
            case BS.IDLE: { if (isBattleActive()) { const r = findGameDocument(); btGameDoc = r.doc; btGameWin = r.win; lockNav("battle"); btState = BS.ACTIVE; break; } const cd = readBattleCountdown(); if (cd !== null && cd > 0) { btTotalWait = cd; btWaitStart = Date.now(); btState = BS.WAITING; break; } if (!canNav("battle") || !isMainScreen()) break; const b = findBtn("Battle"); if (b) { lockNav("battle"); dualClick(b); btState = BS.ENTERING; } break; }
            case BS.ENTERING: { let w = 0; while (w < 6000) { if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("battle"); btState = BS.WAITING; return; } if (isBattleActive()) { const r = findGameDocument(); btGameDoc = r.doc; btGameWin = r.win; btState = BS.ACTIVE; break; } if (w > 800 && isMainScreen()) { const b = findBtn("Battle"); if (b) dualClick(b); } await sleep(200); w += 200; } if (btState === BS.ENTERING) { unlockNav("battle"); btState = BS.IDLE; } break; }
            case BS.ACTIVE: { try { await battleCardSolve(); } catch (e) {} btState = BS.DONE; break; }
            case BS.DONE: { await sleep(1500); btState = BS.EXITING; break; }
            case BS.EXITING: { await sleep(300); await goBackToMain(3); unlockNav("battle"); const cd = readBattleCountdown(); btTotalWait = (cd !== null && cd > 0) ? cd : 0; btWaitStart = Date.now(); btState = BS.WAITING; break; }
            case BS.WAITING: { const cd = readBattleCountdown(); if (cd === null || cd <= 0) { await sleep(2000); btState = BS.IDLE; } else if (btTotalWait === 0) { btTotalWait = cd; btWaitStart = Date.now(); } break; }
        }
    } finally { btBusy = false; }
}
function startBattle() { stopBattle(); btState = BS.IDLE; const lp = () => { battleTick(); btTimer = setTimeout(lp, hd(400)); }; btTimer = setTimeout(lp, hd(400)); }
function stopBattle() { clearTimeout(btTimer); btTimer = null; unlockNav("battle"); btState = BS.IDLE; btBusy = false; btGameDoc = null; btGameWin = null; }

function startAutoDf() {
    if (!originalWidth) originalWidth = window.innerWidth;
    Object.defineProperty(window, 'innerWidth', { get: function() { return 190; }, configurable: true }); window.dispatchEvent(new Event('resize'));
    if (mouseLockerInterval) clearInterval(mouseLockerInterval);
    mouseLockerInterval = setInterval(() => {
        const game = document.querySelector('[class*="game_"]'); if (!game) return;
        const fakeMouseOptions = { clientX: 85, clientY: window.innerHeight - 100, bubbles: true, cancelable: true, view: window };
        const mouseEvent = new MouseEvent('mousemove', fakeMouseOptions); const pointerEvent = new PointerEvent('pointermove', { ...fakeMouseOptions, pointerId: 1 });
        game.dispatchEvent(mouseEvent); game.dispatchEvent(pointerEvent); document.dispatchEvent(mouseEvent); document.dispatchEvent(pointerEvent);
    }, 16);
}
function stopAutoDf() {
    if (originalWidth) { Object.defineProperty(window, 'innerWidth', { get: function() { return originalWidth; }, configurable: true }); window.dispatchEvent(new Event('resize')); }
    if (mouseLockerInterval) { clearInterval(mouseLockerInterval); mouseLockerInterval = null; }
}

function startAutoTarget() {
    if (!document.getElementById('cheatStyleTarget')) {
        let cheatStyle = document.createElement('style'); cheatStyle.id = 'cheatStyleTarget';
        cheatStyle.innerHTML = `div[class*="targetContainer_"] { left: 50% !important; top: 50% !important; transform: translate(-50%, -50%) scale(1.5) !important; transition: none !important; z-index: 9999 !important; }`;
        document.head.appendChild(cheatStyle);
    }
    if (tgInterval) clearInterval(tgInterval);
    tgInterval = setInterval(() => { const target = document.querySelector('div[class*="targetContainer_"]'); if (target) fastClick(target); }, 50); 
}
function stopAutoTarget() {
    let s = document.getElementById('cheatStyleTarget'); if (s) s.remove();
    if (tgInterval) clearInterval(tgInterval); tgInterval = null;
}

function do500Clicks() {
    if (clkRunning) return; clkRunning = true; clkCount = 0;
    const cn = document.querySelector(".container__6952e") || document.body;
    const r = cn.getBoundingClientRect(), cx = r.left + r.width/2, cy = r.top + r.height/2 - 50;
    clkInterval = setInterval(() => {
        if (clkCount >= 500) {
            clearInterval(clkInterval); clkRunning = false; const b = document.getElementById("wgBtn");
            if (b) { setText(b.querySelector(".btnText"), tx("done")); b.style.background = "#00c78b"; b.style.color = "#1a1a1a"; b.style.transition = "opacity .6s"; setTimeout(() => b.style.opacity = "0", 2000); setTimeout(() => b.remove(), 2700); } return;
        } clkCount++; const b = document.getElementById("wgBtn");
        if (b) { const p = clkCount / 5; b.style.background = `linear-gradient(90deg,#00c78b ${p}%,#f5c400 ${p}%)`; setText(b.querySelector(".btnText"), `${tx("wrongGame")} (${Math.round(p)}%)`); }
        const tg = document.elementFromPoint(cx, cy); if (tg) tg.dispatchEvent(new MouseEvent("click", { clientX: cx + (Math.random()*90-45), clientY: cy + (Math.random()*90-45), bubbles: true }));
    }, 34);
}

function renderCraft() {
    const btn = document.getElementById("craftBtn"); if (!btn || !crIconEl || !crTextEl) return;
    if (!crOn) { setText(crTextEl, tx("craft")); setCSS(crIconEl,"filter","invert(1)"); setCSS(btn,"background","#1a1a1a"); setCSS(btn,"color","white"); return; }
    if (getResourcePopup()) { setText(crTextEl, tx("noResources")); setCSS(crIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return; }
    if (crState === CS.WAITING) { const cd = readCraftCountdown(); if (cd !== null && crTotalWait > 0) { const p = Math.min(100, (Date.now()-crWaitStart)/1000/crTotalWait*100); setText(crTextEl, fmtTime(cd)); setCSS(crIconEl,"filter","invert(1)"); setCSS(btn,"background",`linear-gradient(90deg,#00c78b ${p}%,#1a1a1a ${p}%)`); setCSS(btn,"color","white"); return; } setText(crTextEl, tx("craftIdle")); setCSS(crIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return; }
    const labels = {[CS.IDLE]:"craftIdle",[CS.ENTERING]:"craftEntering",[CS.SOLVING]:"craftSolving",[CS.EXITING]:"craftExiting"};
    if (crState === CS.IDLE && activeNav && activeNav !== "craft") setText(crTextEl, tx("paused")); else setText(crTextEl, tx(labels[crState] || "craft"));
    setCSS(crIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a");
}
function renderBattle() {
    const btn = document.getElementById("battleBtn"); if (!btn || !btIconEl || !btTextEl) return;
    if (!btOn) { setText(btTextEl, tx("battle")); setCSS(btIconEl,"filter","invert(1)"); setCSS(btn,"background","#1a1a1a"); setCSS(btn,"color","white"); return; }
    if (getResourcePopup()) { setText(btTextEl, tx("noResources")); setCSS(btIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return; }
    if (btState === BS.WAITING) { const cd = readBattleCountdown(); if (cd !== null && btTotalWait > 0) { const p = Math.min(100, (Date.now()-btWaitStart)/1000/btTotalWait*100); setText(btTextEl, fmtTime(cd)); setCSS(btIconEl,"filter","invert(1)"); setCSS(btn,"background",`linear-gradient(90deg,#00c78b ${p}%,#1a1a1a ${p}%)`); setCSS(btn,"color","white"); return; } setText(btTextEl, tx("battleIdle")); setCSS(btIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return; }
    if (btState === BS.ACTIVE) { const sc = readBattleScore(); if (sc) { const p = sc.cur/sc.max*100; setText(btTextEl, `${tx("battleActive")} ${sc.cur}/${sc.max}`); setCSS(btIconEl,"filter","invert(1)"); setCSS(btn,"background",`linear-gradient(90deg,#00c78b ${p}%,#1a1a1a ${p}%)`); setCSS(btn,"color","white"); return; } setText(btTextEl, tx("battleActive")); setCSS(btIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return; }
    const labels = {[BS.IDLE]:"battleIdle",[BS.ENTERING]:"battleEntering",[BS.DONE]:"battleDone",[BS.EXITING]:"battleExiting"};
    if (btState === BS.IDLE && activeNav && activeNav !== "battle") setText(btTextEl, tx("paused")); else setText(btTextEl, tx(labels[btState] || "battle"));
    setCSS(btIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a");
}
function renderAutoDf() { const btn = document.getElementById("autoDfBtn"); if (!btn || !autoDfIconEl || !autoDfTextEl) return; setText(autoDfTextEl, tx("autoDefence")); if (autoDfOn) { setCSS(autoDfIconEl, "filter", "none"); setCSS(btn, "background", "#00c78b"); setCSS(btn, "color", "#1a1a1a"); } else { setCSS(autoDfIconEl, "filter", "invert(1)"); setCSS(btn, "background", "#1a1a1a"); setCSS(btn, "color", "white"); } }
function renderAutoTg() { const btn = document.getElementById("autoTgBtn"); if (!btn || !autoTgIconEl || !autoTgTextEl) return; setText(autoTgTextEl, tx("autoTarget")); if (autoTgOn) { setCSS(autoTgIconEl, "filter", "none"); setCSS(btn, "background", "#00c78b"); setCSS(btn, "color", "#1a1a1a"); } else { setCSS(autoTgIconEl, "filter", "invert(1)"); setCSS(btn, "background", "#1a1a1a"); setCSS(btn, "color", "white"); } }

function updateLang() {
    const gui = document.getElementById("meadowAutoGUI");
    if (gui) { gui.dir = (lang === "ar" || lang === "he") ? "rtl" : "ltr"; }
    const flagSpan = document.getElementById("flagSpan"); if (flagSpan) flagSpan.innerText = LANG_DATA[lang].flag;
    const a = document.querySelector("#advBtn .btnText"); if (a) setText(a, tx("adventure"));
    const adf = document.querySelector("#autoDfBtn .btnText"); if (adf) setText(adf, tx("autoDefence"));
    const atg = document.querySelector("#autoTgBtn .btnText"); if (atg) setText(atg, tx("autoTarget"));
    const w = document.querySelector("#wgBtn .btnText"); if (w && !clkRunning) setText(w, tx("wrongGame"));
    setText(document.getElementById("dragHint"), tx("drag")); setText(document.getElementById("speedsTitle"), tx("speeds"));
    const al = document.getElementById("advLabel"); if (al) al.childNodes[0].textContent = tx("advLabel") + " : ";
    const cl = document.getElementById("craftLabel"); if (cl) cl.childNodes[0].textContent = tx("craftLabel") + " : ";
    setText(document.getElementById("speedTip"), tx("speedTip"));
}

function makeBtn(id, iconSrc, container) {
    const btn = document.createElement("button"); btn.id = id;
    btn.style.cssText = "width:100%;padding:10px;margin-bottom:6px;border:none;border-radius:6px;font-weight:bold;display:flex;align-items:center;gap:8px;justify-content:center;cursor:pointer;font-size:13px;min-height:40px;background:#1a1a1a;color:white;transition:all 0.2s;";
    const img = document.createElement("img"); img.src = iconSrc; img.draggable = false; img.style.cssText = "height:20px;width:20px;vertical-align:middle;filter:invert(1)";
    const span = document.createElement("span"); span.className = "btnText";
    btn.appendChild(img); btn.appendChild(span); container.appendChild(btn);
    return { btn, img, span };
}

function showLanguageModal(isFirstTime) {
    const oldMain = document.getElementById("meadowAutoGUI"); if (oldMain) oldMain.style.display = "none";
    const oldModal = document.getElementById("meadowLangModal"); if (oldModal) oldModal.remove();

    const modal = document.createElement("div"); modal.id = "meadowLangModal";
    modal.style.cssText = "position:fixed;top:50%;left:50%;transform:translate(-50%,-50%);z-index:9999999;width:340px;max-height:85vh;background:#f8f1e3;border:5px solid #1a1a1a;border-radius:12px;box-shadow:8px 8px 0 #1a1a1a;font-family:system-ui,sans-serif;color:#1a1a1a;padding:20px;display:flex;flex-direction:column;";
    
    let html = `<h2 style="text-align:center;margin:0 0 15px 0;font-size:20px;">🌍 Select Language</h2>`;
    html += `<div style="overflow-y:auto;display:grid;grid-template-columns:1fr 1fr;gap:8px;padding-right:5px;scrollbar-width:thin;">`;
    
    for (const key in LANG_DATA) {
        html += `<button class="lang-sel-btn" data-lang="${key}" style="padding:10px;border:2px solid #1a1a1a;border-radius:8px;background:white;cursor:pointer;font-weight:bold;display:flex;align-items:center;gap:8px;font-size:13px;transition:0.2s;">
            <span style="font-size:18px">${LANG_DATA[key].flag}</span> ${LANG_DATA[key].name}
        </button>`;
    }
    html += `</div>`;
    modal.innerHTML = html;
    document.body.appendChild(modal);

    modal.querySelectorAll('.lang-sel-btn').forEach(btn => {
        btn.addEventListener('click', () => {
            lang = btn.getAttribute('data-lang');
            modal.remove();
            if (isFirstTime) { createMainGUI(); } 
            else { const m = document.getElementById("meadowAutoGUI"); if(m) m.style.display = "block"; updateLang(); }
        });
        btn.addEventListener('mouseover', () => btn.style.background = "#00c78b");
        btn.addEventListener('mouseout', () => btn.style.background = "white");
    });
}

function createMainGUI() {
    const gui = document.createElement("div"); gui.id = "meadowAutoGUI";
    gui.style.cssText = "position:fixed;top:100px;left:40px;z-index:999999;width:240px;background:#f8f1e3;border:4px solid #1a1a1a;border-radius:10px;box-shadow:6px 6px 0 #1a1a1a;font-family:system-ui,sans-serif;color:#1a1a1a;padding:10px;user-select:none";
    gui.innerHTML = `
    <div id="dragHeader" style="background:#00c78b;color:white;padding:8px;margin:-10px -10px 10px -10px;border-radius:5px 5px 0 0;cursor:grab;display:flex;align-items:center;justify-content:space-between;min-height:30px">
        <div id="langFlagBtn" title="Change Language" style="cursor:pointer;background:rgba(0,0,0,0.2);padding:3px 8px;border-radius:5px;font-size:14px;display:flex;align-items:center;gap:4px;transition:0.2s;">
            🌐 <span id="flagSpan">${LANG_DATA[lang].flag}</span>
        </div>
        <img src="${ICONS.logo}" style="height:28px;pointer-events:none" draggable="false">
        <div style="display:flex;align-items:center;gap:10px;margin:0 5px;">
            <img id="settingsBtn" title="Settings" src="${ICONS.settings}" style="height:16px;width:16px;cursor:pointer;filter:invert(1);" draggable="false">
            <div id="minToggleBtn" title="Minimize" style="cursor:pointer;color:white;font-weight:bold;font-size:20px;line-height:1;margin-bottom:2px;">−</div>
        </div>
    </div>
    <div id="guiContent">
        <div id="dragHint" style="text-align:center;font-size:11px;opacity:.75;margin-bottom:10px"></div>
        <div id="btnBox" style="max-height:350px;overflow-y:auto;padding:0 2px;"></div>
        <div id="settingsPanel" style="display:none;margin-top:8px;padding:10px;background:#e8e0d3;border:2px solid #1a1a1a;border-radius:6px">
            <div id="speedsTitle" style="font-weight:bold;margin-bottom:8px;text-align:center;font-size:13px;"></div>
            <div style="margin-bottom:12px"><label id="advLabel" style="font-size:12px">Aventure (ms) : <span id="valAdv">${advDelay}</span></label><input type="range" id="sliderAdv" min="10" max="900" value="${advDelay}" style="width:100%"></div>
            <div><label id="craftLabel" style="font-size:12px">Artisanat (ms) : <span id="valCraft">${crDelay}</span></label><input type="range" id="sliderCraft" min="300" max="800" value="${crDelay}" style="width:100%"></div>
            <div id="speedTip" style="text-align:center;margin-top:10px;font-size:10px;opacity:.7"></div>
        </div>
    </div>`;
    document.body.appendChild(gui);

    const box = document.getElementById("btnBox");
    const adv = makeBtn("advBtn", ICONS.adventure, box); adv.btn.style.minHeight = "auto";
    const craft = makeBtn("craftBtn", ICONS.craft, box); crIconEl = craft.img; crTextEl = craft.span;
    const battle = makeBtn("battleBtn", ICONS.battle, box); btIconEl = battle.img; btTextEl = battle.span;
    const autoDf = makeBtn("autoDfBtn", ICONS.battle, box); autoDfIconEl = autoDf.img; autoDfTextEl = autoDf.span;
    const autoTg = makeBtn("autoTgBtn", ICONS.craft, box); autoTgIconEl = autoTg.img; autoTgTextEl = autoTg.span;
    const wg = makeBtn("wgBtn", ICONS.wrongGame, box); wg.btn.style.minHeight = "auto"; wg.btn.style.background = "#f5c400"; wg.btn.style.color = "#1a1a1a"; wg.img.style.filter = "none";

    const header = document.getElementById("dragHeader"); let dx, dy, sx, sy;
    header.onmousedown = e => {
        if (e.target.closest("#langFlagBtn") || e.target.id === "settingsBtn" || e.target.id === "minToggleBtn") return;
        e.preventDefault(); dragging = true; header.style.cursor = "grabbing"; sx = e.clientX; sy = e.clientY;
        document.onmousemove = ev => { if (!ev.isTrusted) return; dx = sx - ev.clientX; dy = sy - ev.clientY; sx = ev.clientX; sy = ev.clientY; gui.style.top = gui.offsetTop - dy + "px"; gui.style.left = gui.offsetLeft - dx + "px"; };
        document.onmouseup = (ev) => { if (ev && !ev.isTrusted) return; document.onmousemove = document.onmouseup = null; dragging = false; header.style.cursor = "grab"; };
    };

    document.getElementById("langFlagBtn").addEventListener("click", () => showLanguageModal(false));
    document.getElementById("langFlagBtn").addEventListener("mouseover", function() { this.style.background="rgba(0,0,0,0.4)"; });
    document.getElementById("langFlagBtn").addEventListener("mouseout", function() { this.style.background="rgba(0,0,0,0.2)"; });
    
    document.getElementById("minToggleBtn").addEventListener("click", (e) => {
        isMinimized = !isMinimized;
        const content = document.getElementById("guiContent");
        if (isMinimized) { content.style.display = "none"; e.target.innerText = "+"; gui.style.paddingBottom = "0"; } 
        else { content.style.display = "block"; e.target.innerText = "−"; gui.style.paddingBottom = "10px"; }
    });

    adv.btn.addEventListener("click", () => { advOn = !advOn; setCSS(adv.img,"filter",advOn?"none":"invert(1)"); setCSS(adv.btn,"background",advOn?"#00c78b":"#1a1a1a"); setCSS(adv.btn,"color",advOn?"#1a1a1a":"white"); advOn ? startAdv() : stopAdv(); });
    craft.btn.addEventListener("click", () => { crOn = !crOn; crOn ? startCraft() : stopCraft(); });
    battle.btn.addEventListener("click", () => { btOn = !btOn; btOn ? startBattle() : stopBattle(); });
    autoDf.btn.addEventListener("click", () => { autoDfOn = !autoDfOn; autoDfOn ? startAutoDf() : stopAutoDf(); });
    autoTg.btn.addEventListener("click", () => { autoTgOn = !autoTgOn; autoTgOn ? startAutoTarget() : stopAutoTarget(); });
    wg.btn.addEventListener("click", do500Clicks);
    document.getElementById("settingsBtn").addEventListener("click", () => { const p = document.getElementById("settingsPanel"); p.style.display = p.style.display === "none" ? "block" : "none"; });
    document.getElementById("sliderAdv").addEventListener("input", e => { advDelay = parseInt(e.target.value); setText(document.getElementById("valAdv"), String(advDelay)); if (advOn) startAdv(); });
    document.getElementById("sliderCraft").addEventListener("input", e => { crDelay = parseInt(e.target.value); setText(document.getElementById("valCraft"), String(crDelay)); if (crOn) startCraft(); });

    updateLang();
    window._renderInterval = setInterval(() => { renderCraft(); renderBattle(); renderAutoDf(); renderAutoTg(); }, 200);
}

showLanguageModal(true);

window._meadowCleanup = () => { 
    stopAdv(); stopCraft(); stopBattle(); stopAutoDf(); stopAutoTarget();
    clearInterval(clkInterval); if (window._renderInterval) clearInterval(window._renderInterval);
    crOn = advOn = btOn = autoDfOn = autoTgOn = false; 
    const g = document.getElementById("meadowAutoGUI"); if (g) g.remove(); 
    const l = document.getElementById("meadowLangModal"); if (l) l.remove();
};
window.stopMeadowScript = window._meadowCleanup;
})();
