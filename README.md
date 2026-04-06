# 🌿 The Last Meadow - Ultimate Auto GUI (auto farm)

This is the **best and only script** you will ever need to automate the Discord mini-game "The Last Meadow".  
It is highly optimized, ultra-fast, and features a literal "DOM Hack" to solve memory games instantly.

### ✨ What makes this the best?
- **Supports 30+ Languages:** Play in your native language.
- **Auto Heal (NEW ⚡):** Smarter algorithm! Explores random cards efficiently to build memory and solves the 3-card game instantly.
- **Auto Battle:** Automatically enters and loops the Battle mode (Use alongside Target/Defence!).
- **Auto Defence:** Freezes the screen and auto-catches every fireball effortlessly.
- **Auto Target:** Locks the target perfectly in the middle and auto-clicks it precisely.
- **Lightning Fast Crafting:** Executes crafting sequences instantly (0 delay).
- **Insane Auto-Clicker:** Adjustable adventure speed down to `10ms`.
- **Smart UI:** Compact, draggable, minimizable, and bug-free (with fixed sliders!).

---

### 🚀 How to Setup

If you are using an older version, please refresh Discord first.

1. Open Discord and press `Ctrl + R` (to clear old scripts).
2. Press `Ctrl + Shift + I` (or `F12`) to open **Developer Tools**.
3. Click on the **Console** tab at the top.
4. **Copy the code below**, paste it into the console, and press `Enter`.
5. Select your language and **Enjoy!**

---

<img width="1919" height="943" alt="1" src="https://github.com/user-attachments/assets/8b05d45d-5155-4174-a114-e89241309fbe" />



<img width="1622" height="926" alt="2" src="https://github.com/user-attachments/assets/9ca790c9-6c19-4008-ad67-b4b533bfc5a4" />


<img width="269" height="588" alt="3" src="https://github.com/user-attachments/assets/c7703bfa-005b-4e27-81ea-76a34b646f8b" />


<img width="1920" height="1080" alt="4" src="https://github.com/user-attachments/assets/6ff21417-ed32-4588-aa55-83f4ec7bf7eb" />



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
    heal: CDN+"19393b516c6014a9b5564ee7d03b33323e52c893ef9f989c8f6aeda1bcfb9756.svg",
    settings: CDN+"f89c2c158bfa6ddea9304df708f207b8a69853ddda9ee13f2066b7085605a475.svg",
    logo: CDN+"c9463738992e8f18a383be2725a5fa11d5f06b8a0820f0325033c086dd9dd649.png"
};
const ROT_MAP = {"0":"ArrowUp","90":"ArrowRight","180":"ArrowDown","270":"ArrowLeft"};

const LANG_DATA = {
    en: { name:"English", flag:"🇬🇧", t:{ adventure:"Adventure", craft:"Craft", wrongGame:"Wrong Game", battle:"Battle", heal:"Auto Heal", autoDefence:"Auto Defence", autoTarget:"Auto Target", drag:"Drag to move", speeds:"Speed Settings", advLabel:"Adventure (ms)", craftLabel:"Craft (ms)", speedTip:"Lower = faster", craftIdle:"Waiting", craftEntering:"Opening", craftSolving:"Solving", craftExiting:"Going back", battleIdle:"Waiting", battleEntering:"Opening", battleActive:"In Game", battleExiting:"Going back", healIdle:"Waiting", healEntering:"Opening", healActive:"Healing", healDone:"Victory", healExiting:"Going back", paused:"Paused", done:"Done", noResources:"No resources"} },
    fr: { name:"Français", flag:"🇫🇷", t:{ adventure:"Aventure", craft:"Artisanat", wrongGame:"Mauvais Jeu", battle:"Bataille", heal:"Auto Soin", autoDefence:"Auto Défense", autoTarget:"Auto Cible", drag:"Glisser pour deplacer", speeds:"Reglages", advLabel:"Aventure (ms)", craftLabel:"Artisanat (ms)", speedTip:"Plus bas = rapide", craftIdle:"En attente", craftEntering:"Ouverture", craftSolving:"Resolution", craftExiting:"Retour", battleIdle:"En attente", battleEntering:"Ouverture", battleActive:"En jeu", battleExiting:"Retour", healIdle:"En attente", healEntering:"Ouverture", healActive:"Soins", healDone:"Victoire", healExiting:"Retour", paused:"Pause", done:"Termine", noResources:"Pas de ressources"} },
    ar: { name:"العربية", flag:"🇸🇦", t:{ adventure:"مغامرة", craft:"صناعة", wrongGame:"لعبة خاطئة", battle:"معركة", heal:"علاج تلقائي", autoDefence:"دفاع تلقائي", autoTarget:"استهداف تلقائي", drag:"اسحب للتحريك", speeds:"إعدادات السرعة", advLabel:"المغامرة (ms)", craftLabel:"الصناعة (ms)", speedTip:"أقل = أسرع", craftIdle:"في الانتظار", craftEntering:"جاري الفتح", craftSolving:"جاري الحل", craftExiting:"رجوع", battleIdle:"في الانتظار", battleEntering:"جاري الفتح", battleActive:"في اللعبة", battleExiting:"رجوع", healIdle:"في الانتظار", healEntering:"جاري الفتح", healActive:"علاج", healDone:"انتصار", healExiting:"رجوع", paused:"متوقف", done:"تم", noResources:"لا يوجد موارد"} },
    br: { name:"Português (BR)", flag:"🇧🇷", t:{ adventure:"Aventura", craft:"Criação", wrongGame:"Jogo Errado", battle:"Batalha", heal:"Auto Cura", autoDefence:"Auto Defesa", autoTarget:"Auto Alvo", drag:"Arraste", speeds:"Velocidade", advLabel:"Aventura (ms)", craftLabel:"Criação (ms)", speedTip:"Menor = mais rápido", craftIdle:"Aguardando", craftEntering:"Abrindo", craftSolving:"Resolvendo", craftExiting:"Voltando", battleIdle:"Aguardando", battleEntering:"Abrindo", battleActive:"Em jogo", battleExiting:"Voltando", healIdle:"Aguardando", healEntering:"Abrindo", healActive:"Curando", healDone:"Vitória", healExiting:"Voltando", paused:"Pausado", done:"Pronto", noResources:"Sem recursos"} },
    pt: { name:"Português (PT)", flag:"🇵🇹", t:{ adventure:"Aventura", craft:"Artesanato", wrongGame:"Jogo Errado", battle:"Batalha", heal:"Auto Cura", autoDefence:"Auto Defesa", autoTarget:"Auto Alvo", drag:"Arrastar", speeds:"Velocidade", advLabel:"Aventura (ms)", craftLabel:"Artesanato (ms)", speedTip:"Menor = rápido", craftIdle:"Espera", craftEntering:"A abrir", craftSolving:"A resolver", craftExiting:"A voltar", battleIdle:"Espera", battleEntering:"A abrir", battleActive:"Em jogo", battleExiting:"A voltar", healIdle:"Espera", healEntering:"A abrir", healActive:"A curar", healDone:"Vitória", healExiting:"A voltar", paused:"Pausa", done:"Feito", noResources:"Sem recursos"} },
    es: { name:"Español", flag:"🇪🇸", t:{ adventure:"Aventura", craft:"Fabricar", wrongGame:"Juego Equivocado", battle:"Batalla", heal:"Auto Curar", autoDefence:"Auto Defensa", autoTarget:"Auto Objetivo", drag:"Arrastrar", speeds:"Velocidades", advLabel:"Aventura (ms)", craftLabel:"Fabricar (ms)", speedTip:"Menor = rápido", craftIdle:"Esperando", craftEntering:"Abriendo", craftSolving:"Resolviendo", craftExiting:"Volviendo", battleIdle:"Esperando", battleEntering:"Abriendo", battleActive:"En juego", battleExiting:"Volviendo", healIdle:"Esperando", healEntering:"Abriendo", healActive:"Curando", healDone:"Victoria", healExiting:"Volviendo", paused:"Pausa", done:"Hecho", noResources:"Sin recursos"} },
    de: { name:"Deutsch", flag:"🇩🇪", t:{ adventure:"Abenteuer", craft:"Handwerk", wrongGame:"Falsches Spiel", battle:"Kampf", heal:"Auto Heilen", autoDefence:"Auto-Abwehr", autoTarget:"Auto-Ziel", drag:"Ziehen", speeds:"Geschwindigkeit", advLabel:"Abenteuer (ms)", craftLabel:"Handwerk (ms)", speedTip:"Niedriger = schneller", craftIdle:"Warten", craftEntering:"Öffnen", craftSolving:"Lösen", craftExiting:"Zurück", battleIdle:"Warten", battleEntering:"Öffnen", battleActive:"Im Spiel", battleExiting:"Zurück", healIdle:"Warten", healEntering:"Öffnen", healActive:"Heilen", healDone:"Sieg", healExiting:"Zurück", paused:"Pause", done:"Fertig", noResources:"Keine Ressourcen"} },
    it: { name:"Italiano", flag:"🇮🇹", t:{ adventure:"Avventura", craft:"Creazione", wrongGame:"Gioco Sbagliato", battle:"Battaglia", heal:"Auto Guarire", autoDefence:"Auto Difesa", autoTarget:"Auto Bersaglio", drag:"Trascina", speeds:"Velocità", advLabel:"Avventura (ms)", craftLabel:"Creazione (ms)", speedTip:"Minore = veloce", craftIdle:"Attesa", craftEntering:"Apertura", craftSolving:"Risoluzione", craftExiting:"Ritorno", battleIdle:"Attesa", battleEntering:"Apertura", battleActive:"In gioco", battleExiting:"Ritorno", healIdle:"Attesa", healEntering:"Apertura", healActive:"Guarigione", healDone:"Vittoria", healExiting:"Ritorno", paused:"Pausa", done:"Fatto", noResources:"Senza risorse"} },
    ru: { name:"Русский", flag:"🇷🇺", t:{ adventure:"Приключение", craft:"Крафт", wrongGame:"Не та игра", battle:"Битва", heal:"Авто-лечение", autoDefence:"Авто-защита", autoTarget:"Авто-цель", drag:"Тянуть", speeds:"Скорость", advLabel:"Приключение (ms)", craftLabel:"Крафт (ms)", speedTip:"Ниже = быстрее", craftIdle:"Ожидание", craftEntering:"Открытие", craftSolving:"Решение", craftExiting:"Назад", battleIdle:"Ожидание", battleEntering:"Открытие", battleActive:"В игре", battleExiting:"Назад", healIdle:"Ожидание", healEntering:"Открытие", healActive:"Лечение", healDone:"Победа", healExiting:"Назад", paused:"Пауза", done:"Готово", noResources:"Нет ресурсов"} },
    tr: { name:"Türkçe", flag:"🇹🇷", t:{ adventure:"Macera", craft:"Zanaat", wrongGame:"Yanlış Oyun", battle:"Savaş", heal:"Oto İyileştir", autoDefence:"Oto Savunma", autoTarget:"Oto Hedef", drag:"Sürükle", speeds:"Hızlar", advLabel:"Macera (ms)", craftLabel:"Zanaat (ms)", speedTip:"Düşük = hızlı", craftIdle:"Bekleniyor", craftEntering:"Açılıyor", craftSolving:"Çözülüyor", craftExiting:"Geri", battleIdle:"Bekleniyor", battleEntering:"Açılıyor", battleActive:"Oyunda", battleExiting:"Geri", healIdle:"Bekleniyor", healEntering:"Açılıyor", healActive:"İyileştirme", healDone:"Zafer", healExiting:"Geri", paused:"Duraklatıldı", done:"Bitti", noResources:"Kaynak yok"} },
    ja: { name:"日本語", flag:"🇯🇵", t:{ adventure:"冒険", craft:"クラフト", wrongGame:"違うゲーム", battle:"バトル", heal:"自動ヒール", autoDefence:"自動防衛", autoTarget:"自動ターゲット", drag:"ドラッグ", speeds:"速度設定", advLabel:"冒険 (ms)", craftLabel:"クラフト (ms)", speedTip:"低い = 早い", craftIdle:"待機中", craftEntering:"開く", craftSolving:"解決中", craftExiting:"戻る", battleIdle:"待機中", battleEntering:"開く", battleActive:"ゲーム中", battleExiting:"戻る", healIdle:"待機中", healEntering:"開く", healActive:"治療中", healDone:"勝利", healExiting:"戻る", paused:"一時停止", done:"完了", noResources:"リソースなし"} },
    zh: { name:"中文", flag:"🇨🇳", t:{ adventure:"冒险", craft:"制作", wrongGame:"错误游戏", battle:"战斗", heal:"自动治愈", autoDefence:"自动防御", autoTarget:"自动瞄准", drag:"拖动", speeds:"速度设置", advLabel:"冒险 (ms)", craftLabel:"制作 (ms)", speedTip:"更低=更快", craftIdle:"等待", craftEntering:"打开", craftSolving:"解决", craftExiting:"返回", battleIdle:"等待", battleEntering:"打开", battleActive:"游戏中", battleExiting:"返回", healIdle:"等待", healEntering:"打开", healActive:"治愈中", healDone:"胜利", healExiting:"返回", paused:"暂停", done:"完成", noResources:"没有资源"} },
    ko: { name:"한국어", flag:"🇰🇷", t:{ adventure:"모험", craft:"제작", wrongGame:"잘못된 게임", battle:"전투", heal:"자동 치유", autoDefence:"자동 방어", autoTarget:"자동 타겟", drag:"드래그", speeds:"속도 설정", advLabel:"모험 (ms)", craftLabel:"제작 (ms)", speedTip:"낮음=빠름", craftIdle:"대기 중", craftEntering:"열기", craftSolving:"해결 중", craftExiting:"뒤로", battleIdle:"대기 중", battleEntering:"열기", battleActive:"게임 중", battleExiting:"뒤로", healIdle:"대기 중", healEntering:"열기", healActive:"치유 중", healDone:"승리", healExiting:"뒤로", paused:"일시정지", done:"완료", noResources:"자원 없음"} },
    hi: { name:"हिन्दी", flag:"🇮🇳", t:{ adventure:"साहसिक काम", craft:"शिल्प", wrongGame:"गलत खेल", battle:"लड़ाई", heal:"ऑटो उपचार", autoDefence:"ऑटो रक्षा", autoTarget:"ऑटो लक्ष्य", drag:"खींचें", speeds:"गति", advLabel:"साहसिक (ms)", craftLabel:"शिल्प (ms)", speedTip:"कम = तेज़", craftIdle:"प्रतीक्षा", craftEntering:"खोल रहा है", craftSolving:"हल कर रहा है", craftExiting:"वापस", battleIdle:"प्रतीक्षा", battleEntering:"खोल रहा है", battleActive:"खेल में", battleExiting:"वापस", healIdle:"प्रतीक्षा", healEntering:"खोल रहा है", healActive:"उपचार", healDone:"जीत", healExiting:"वापस", paused:"रुका हुआ", done:"हो गया", noResources:"कोई संसाधन नहीं"} },
    pl: { name:"Polski", flag:"🇵🇱", t:{ adventure:"Przygoda", craft:"Rzemiosło", wrongGame:"Zła Gra", battle:"Bitwa", heal:"Auto Uzdrowienie", autoDefence:"Auto Obrona", autoTarget:"Auto Cel", drag:"Przeciągnij", speeds:"Szybkość", advLabel:"Przygoda (ms)", craftLabel:"Rzemiosło (ms)", speedTip:"Niżej = szybciej", craftIdle:"Czekanie", craftEntering:"Otwieranie", craftSolving:"Rozwiązywanie", craftExiting:"Wstecz", battleIdle:"Czekanie", battleEntering:"Otwieranie", battleActive:"W grze", battleExiting:"Wstecz", healIdle:"Czekanie", healEntering:"Otwieranie", healActive:"Uzdrawianie", healDone:"Zwycięstwo", healExiting:"Wstecz", paused:"Pauza", done:"Gotowe", noResources:"Brak zasobów"} },
    nl: { name:"Nederlands", flag:"🇳🇱", t:{ adventure:"Avontuur", craft:"Ambacht", wrongGame:"Verkeerd Spel", battle:"Gevecht", heal:"Auto Genezen", autoDefence:"Auto Verdediging", autoTarget:"Auto Doelwit", drag:"Slepen", speeds:"Snelheid", advLabel:"Avontuur (ms)", craftLabel:"Ambacht (ms)", speedTip:"Lager = sneller", craftIdle:"Wachten", craftEntering:"Openen", craftSolving:"Oplossen", craftExiting:"Terug", battleIdle:"Wachten", battleEntering:"Openen", battleActive:"In spel", battleExiting:"Terug", healIdle:"Wachten", healEntering:"Openen", healActive:"Genezen", healDone:"Overwinning", healExiting:"Terug", paused:"Pauze", done:"Klaar", noResources:"Geen bronnen"} },
    sv: { name:"Svenska", flag:"🇸🇪", t:{ adventure:"Äventyr", craft:"Hantverk", wrongGame:"Fel Spel", battle:"Strid", heal:"Auto Hela", autoDefence:"Auto Försvar", autoTarget:"Auto Mål", drag:"Dra", speeds:"Hastighet", advLabel:"Äventyr (ms)", craftLabel:"Hantverk (ms)", speedTip:"Lägre = snabbare", craftIdle:"Väntar", craftEntering:"Öppnar", craftSolving:"Löser", craftExiting:"Tillbaka", battleIdle:"Väntar", battleEntering:"Öppnar", battleActive:"I spel", battleExiting:"Tillbaka", healIdle:"Väntar", healEntering:"Öppnar", healActive:"Helar", healDone:"Seger", healExiting:"Tillbaka", paused:"Pausad", done:"Klar", noResources:"Inga resurser"} },
    id: { name:"Bahasa Indonesia", flag:"🇮🇩", t:{ adventure:"Petualangan", craft:"Kerajinan", wrongGame:"Game Salah", battle:"Pertarungan", heal:"Auto Sembuh", autoDefence:"Auto Bertahan", autoTarget:"Auto Target", drag:"Geser", speeds:"Kecepatan", advLabel:"Petualangan (ms)", craftLabel:"Kerajinan (ms)", speedTip:"Rendah = cepat", craftIdle:"Menunggu", craftEntering:"Membuka", craftSolving:"Menyelesaikan", craftExiting:"Kembali", battleIdle:"Menunggu", battleEntering:"Membuka", battleActive:"Dalam game", battleExiting:"Kembali", healIdle:"Menunggu", healEntering:"Membuka", healActive:"Menyembuhkan", healDone:"Menang", healExiting:"Kembali", paused:"Jeda", done:"Selesai", noResources:"Tidak ada SDA"} },
    vi: { name:"Tiếng Việt", flag:"🇻🇳", t:{ adventure:"Phiêu lưu", craft:"Chế tạo", wrongGame:"Sai trò chơi", battle:"Chiến đấu", heal:"Tự Chữa Lành", autoDefence:"Tự phòng thủ", autoTarget:"Tự nhắm", drag:"Kéo", speeds:"Tốc độ", advLabel:"Phiêu lưu (ms)", craftLabel:"Chế tạo (ms)", speedTip:"Thấp = Nhanh", craftIdle:"Đang chờ", craftEntering:"Đang mở", craftSolving:"Đang giải", craftExiting:"Trở lại", battleIdle:"Đang chờ", battleEntering:"Đang mở", battleActive:"Đang chơi", battleExiting:"Trở lại", healIdle:"Đang chờ", healEntering:"Đang mở", healActive:"Chữa lành", healDone:"Chiến thắng", healExiting:"Trở lại", paused:"Tạm dừng", done:"Xong", noResources:"Hết tài nguyên"} },
    th: { name:"ไทย", flag:"🇹🇭", t:{ adventure:"ผจญภัย", craft:"คราฟต์", wrongGame:"เกมผิด", battle:"ต่อสู้", heal:"รักษาอัตโนมัติ", autoDefence:"ป้องกันอัตโนมัติ", autoTarget:"เป้าหมายอัตโนมัติ", drag:"ลาก", speeds:"ความเร็ว", advLabel:"ผจญภัย (ms)", craftLabel:"คราฟต์ (ms)", speedTip:"ต่ำ = เร็ว", craftIdle:"รอ", craftEntering:"กำลังเปิด", craftSolving:"กำลังแก้", craftExiting:"กลับ", battleIdle:"รอ", battleEntering:"กำลังเปิด", battleActive:"ในเกม", battleExiting:"กลับ", healIdle:"รอ", healEntering:"กำลังเปิด", healActive:"รักษา", healDone:"ชนะ", healExiting:"กลับ", paused:"หยุด", done:"เสร็จ", noResources:"ไม่มีทรัพยากร"} },
    el: { name:"Ελληνικά", flag:"🇬🇷", t:{ adventure:"Περιπέτεια", craft:"Κατασκευή", wrongGame:"Λάθος Παιχνίδι", battle:"Μάχη", heal:"Αυτό Θεραπεία", autoDefence:"Auto Άμυνα", autoTarget:"Auto Στόχος", drag:"Σύρετε", speeds:"Ταχύτητα", advLabel:"Περιπέτεια (ms)", craftLabel:"Κατασκευή (ms)", speedTip:"Χαμηλότερα = πιο γρήγορα", craftIdle:"Αναμονή", craftEntering:"Άνοιγμα", craftSolving:"Επίλυση", craftExiting:"Πίσω", battleIdle:"Αναμονή", battleEntering:"Άνοιγμα", battleActive:"Στο παιχνίδι", battleExiting:"Πίσω", healIdle:"Αναμονή", healEntering:"Άνοιγμα", healActive:"Θεραπεία", healDone:"Νίκη", healExiting:"Πίσω", paused:"Παύση", done:"Έγινε", noResources:"Χωρίς πόρους"} },
    cs: { name:"Čeština", flag:"🇨🇿", t:{ adventure:"Dobrodružství", craft:"Řemeslo", wrongGame:"Špatná Hra", battle:"Bitva", heal:"Auto Léčení", autoDefence:"Auto Obrana", autoTarget:"Auto Cíl", drag:"Táhni", speeds:"Rychlost", advLabel:"Dobro (ms)", craftLabel:"Řemeslo (ms)", speedTip:"Méně = Rychleji", craftIdle:"Čekání", craftEntering:"Otevírání", craftSolving:"Řešení", craftExiting:"Zpět", battleIdle:"Čekání", battleEntering:"Otevírání", battleActive:"Ve hře", battleExiting:"Zpět", healIdle:"Čekání", healEntering:"Otevírání", healActive:"Léčení", healDone:"Výhra", healExiting:"Zpět", paused:"Pauza", done:"Hotovo", noResources:"Bez zdrojů"} },
    ro: { name:"Română", flag:"🇷🇴", t:{ adventure:"Aventură", craft:"Artizanat", wrongGame:"Joc Greșit", battle:"Bătălie", heal:"Auto Vindecare", autoDefence:"Auto Apărare", autoTarget:"Auto Țintă", drag:"Trage", speeds:"Viteză", advLabel:"Aventură (ms)", craftLabel:"Artizanat (ms)", speedTip:"Mic = rapid", craftIdle:"Așteptare", craftEntering:"Deschidere", craftSolving:"Rezolvare", craftExiting:"Înapoi", battleIdle:"Așteptare", battleEntering:"Deschidere", battleActive:"În joc", battleExiting:"Înapoi", healIdle:"Așteptare", healEntering:"Deschidere", healActive:"Vindecare", healDone:"Victorie", healExiting:"Înapoi", paused:"Pauză", done:"Gata", noResources:"Fără resurse"} },
    hu: { name:"Magyar", flag:"🇭🇺", t:{ adventure:"Kaland", craft:"Barkács", wrongGame:"Rossz Játék", battle:"Csata", heal:"Auto Gyógyítás", autoDefence:"Auto Védelem", autoTarget:"Auto Cél", drag:"Húzás", speeds:"Sebesség", advLabel:"Kaland (ms)", craftLabel:"Barkács (ms)", speedTip:"Kisebb = Gyorsabb", craftIdle:"Várakozás", craftEntering:"Megnyitás", craftSolving:"Megoldás", craftExiting:"Vissza", battleIdle:"Várakozás", battleEntering:"Megnyitás", battleActive:"Játékban", battleExiting:"Vissza", healIdle:"Várakozás", healEntering:"Megnyitás", healActive:"Gyógyítás", healDone:"Győzelem", healExiting:"Vissza", paused:"Szünet", done:"Kész", noResources:"Nincs nyersanyag"} },
    da: { name:"Dansk", flag:"🇩🇰", t:{ adventure:"Eventyr", craft:"Håndværk", wrongGame:"Forkert Spil", battle:"Kamp", heal:"Auto Helbred", autoDefence:"Auto Forsvar", autoTarget:"Auto Mål", drag:"Træk", speeds:"Hastighed", advLabel:"Eventyr (ms)", craftLabel:"Håndværk (ms)", speedTip:"Lavere = hurtigere", craftIdle:"Venter", craftEntering:"Åbner", craftSolving:"Løser", craftExiting:"Tilbage", battleIdle:"Venter", battleEntering:"Åbner", battleActive:"I spil", battleExiting:"Tilbage", healIdle:"Venter", healEntering:"Åbner", healActive:"Helbreder", healDone:"Sejr", healExiting:"Tilbage", paused:"Pause", done:"Færdig", noResources:"Ingen ressourcer"} },
    fi: { name:"Suomi", flag:"🇫🇮", t:{ adventure:"Seikkailu", craft:"Käsityö", wrongGame:"Väärä Peli", battle:"Taistelu", heal:"Auto Parantaa", autoDefence:"Auto Puolustus", autoTarget:"Auto Kohde", drag:"Vedä", speeds:"Nopeus", advLabel:"Seikkailu (ms)", craftLabel:"Käsityö (ms)", speedTip:"Pienempi = nopeampi", craftIdle:"Odottaa", craftEntering:"Avaa", craftSolving:"Ratkaisee", craftExiting:"Takaisin", battleIdle:"Odottaa", battleEntering:"Avaa", battleActive:"Pelissä", battleExiting:"Takaisin", healIdle:"Odottaa", healEntering:"Avaa", healActive:"Parantaa", healDone:"Voitto", healExiting:"Takaisin", paused:"Tauko", done:"Valmis", noResources:"Ei resursseja"} },
    no: { name:"Norsk", flag:"🇳🇴", t:{ adventure:"Eventyr", craft:"Håndverk", wrongGame:"Feil Spill", battle:"Kamp", heal:"Auto Helbred", autoDefence:"Auto Forsvar", autoTarget:"Auto Mål", drag:"Dra", speeds:"Hastighet", advLabel:"Eventyr (ms)", craftLabel:"Håndverk (ms)", speedTip:"Lavere = raskere", craftIdle:"Venter", craftEntering:"Åpner", craftSolving:"Løser", craftExiting:"Tilbake", battleIdle:"Venter", battleEntering:"Åpner", battleActive:"I spill", battleExiting:"Tilbake", healIdle:"Venter", healEntering:"Åpner", healActive:"Helbreder", healDone:"Seier", healExiting:"Tilbake", paused:"Pause", done:"Ferdig", noResources:"Ingen ressurser"} },
    he: { name:"עברית", flag:"🇮🇱", t:{ adventure:"הרפתקה", craft:"יצירה", wrongGame:"משחק שגוי", battle:"קרב", heal:"ריפוי אוטומטי", autoDefence:"הגנה אוטומטית", autoTarget:"מטרה אוטומטית", drag:"גרור", speeds:"מהירות", advLabel:"הרפתקה (ms)", craftLabel:"יצירה (ms)", speedTip:"נמוך = מהיר", craftIdle:"ממתין", craftEntering:"פותח", craftSolving:"פותר", craftExiting:"חוזר", battleIdle:"ממתין", battleEntering:"פותח", battleActive:"במשחק", battleExiting:"חוזר", healIdle:"ממתין", healEntering:"פותח", healActive:"מרפא", healDone:"ניצחון", healExiting:"חוזר", paused:"מושהה", done:"בוצע", noResources:"אין משאבים"} },
    ms: { name:"Bahasa Melayu", flag:"🇲🇾", t:{ adventure:"Pengembaraan", craft:"Kraf", wrongGame:"Permainan Salah", battle:"Pertempuran", heal:"Auto Sembuh", autoDefence:"Pertahanan Auto", autoTarget:"Sasaran Auto", drag:"Seret", speeds:"Kelajuan", advLabel:"Pengembaraan", craftLabel:"Kraf", speedTip:"Rendah = Cepat", craftIdle:"Menunggu", craftEntering:"Membuka", craftSolving:"Menyelesaikan", craftExiting:"Kembali", battleIdle:"Menunggu", battleEntering:"Membuka", battleActive:"Dalam permainan", battleExiting:"Kembali", healIdle:"Menunggu", healEntering:"Membuka", healActive:"Menyembuhkan", healDone:"Kemenangan", healExiting:"Kembali", paused:"Jeda", done:"Selesai", noResources:"Tiada sumber"} },
    bn: { name:"বাংলা", flag:"🇧🇩", t:{ adventure:"অ্যাডভেঞ্চার", craft:"ক্রাফট", wrongGame:"ভুল খেলা", battle:"যুদ্ধ", heal:"অটো সুস্থ", autoDefence:"অটো ডিফেন্স", autoTarget:"অটো টার্গেট", drag:"টানুন", speeds:"গতি", advLabel:"অ্যাডভেঞ্চার (ms)", craftLabel:"ক্রাফট (ms)", speedTip:"কম = দ্রুত", craftIdle:"অপেক্ষায়", craftEntering:"খুলছে", craftSolving:"সমাধান", craftExiting:"ফিরে", battleIdle:"অপেক্ষায়", battleEntering:"খুলছে", battleActive:"খেলায়", battleExiting:"ফিরে", healIdle:"অপেক্ষায়", healEntering:"খুলছে", healActive:"সুস্থ করা", healDone:"বিজয়", healExiting:"ফিরে", paused:"স্থগিত", done:"সম্পন্ন", noResources:"সম্পদ নেই"} }
};

// ── State Variables ──
let advInterval = null, clkInterval = null, clkCount = 0;
let advOn = false, crOn = false, btOn = false, hlOn = false, autoDfOn = false, autoTgOn = false, clkRunning = false, dragging = false;
let lang = "en", advDelay = 50, crDelay = 520, activeNav = null, isMinimized = false;

const CS = { IDLE:0, ENTERING:1, SOLVING:2, EXITING:3, WAITING:4 };
let crState = CS.IDLE, crTimer = null, crBusy = false, crTotalWait = 0, crWaitStart = 0;

const BTS = { IDLE:0, ENTERING:1, ACTIVE:2, EXITING:3, WAITING:4 };
let btState = BTS.IDLE, btTimer = null, btBusy = false, btTotalWait = 0, btWaitStart = 0;

const HS = { IDLE:0, ENTERING:1, ACTIVE:2, DONE:3, EXITING:4, WAITING:5 };
let hlState = HS.IDLE, hlTimer = null, hlBusy = false, hlTotalWait = 0, hlWaitStart = 0;

let crIconEl, crTextEl, btIconEl, btTextEl, hlIconEl, hlTextEl, autoDfIconEl, autoDfTextEl, autoTgIconEl, autoTgTextEl;
let originalWidth = null, mouseLockerInterval = null, tgInterval = null;

// ── Helpers ──
function hd(b) { return b + (Math.random() * 2 - 1) * b * 0.15; }
function sleep(ms) { return new Promise(r => setTimeout(r, ms)); }
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
    const c = el.querySelector('[role="button"]') || el.closest('[role="button"]') || el;
    const r = c.getBoundingClientRect(); if (r.width === 0 || r.height === 0) return false;
    const x = r.left + r.width/2 + (Math.random()*4-2);
    const y = r.top + r.height/2 + (Math.random()*4-2);
    const o = {bubbles:true, cancelable:true, view:window, clientX:x, clientY:y, button:0};
    c.dispatchEvent(new PointerEvent("pointerdown", {...o, pointerId:1}));
    c.dispatchEvent(new MouseEvent("mousedown", o));
    if (c.focus) c.focus();
    c.dispatchEvent(new PointerEvent("pointerup", {...o, pointerId:1}));
    c.dispatchEvent(new MouseEvent("mouseup", o));
    c.dispatchEvent(new MouseEvent("click", o));
    return true;
}
function dualClick(el) { if (!el) return false; reactClick(el); setTimeout(() => fastClick(el), 150); return true; }

function getGameContainer() { return document.querySelector(".container__73695"); }
function findBtn(name) { const gc = getGameContainer(); if (!gc) return null; for (const b of gc.querySelectorAll(".activityButton__8af73")) if (b.textContent?.includes(name)) return b; return null; }
function getAdvButton() { const gc = getGameContainer(); if (!gc) return null; return gc.querySelector('.activityButtonText__8af73[data-text-variant="heading-xxl/normal"]') || Array.from(gc.querySelectorAll(".activityButton__8af73")).find(el => el.textContent?.includes("Adventure")); }
function getResourcePopup() { const p = document.querySelector(".container__139d4"); if (!p) return null; const t = p.textContent || ""; return (t.includes("out of resources") || t.includes("try again")) ? p : null; }
function dismissPopup() { const p = getResourcePopup(); if (!p) return false; const b = p.querySelector('.button__65fca[role="button"]'); if (b) { dualClick(b); return true; } return false; }
function findContinueBtn() { for (const b of document.querySelectorAll('.button__65fca[role="button"]')) { const v = b.querySelector('.visibleText__65fca'); if (v && v.textContent.trim() === "Continue") return b; } return null; }
function findBackBtn() { return document.querySelector('.back__51dc1[role="button"]') || document.querySelector('[aria-label="Back"][role="button"]') || (document.querySelector('img[alt="Back"]')?.closest('[role="button"]')) || null; }
function isSuccessScreen() { const gc = getGameContainer(); if (!gc) { for (const el of document.querySelectorAll('[data-text-variant]')) if (el.textContent.includes("Success")) return true; } else if (gc.textContent.includes("Success")) return true; return !isMainScreen() && !!findContinueBtn(); }
function isGenericGameActive() { return !!document.querySelector('[class*="game__"]'); }
async function goBackToMain(max) { for (let i = 0; i < max; i++) { if (isMainScreen()) return true; const c = findContinueBtn(); if (c) { dualClick(c); await sleep(600); if (isMainScreen()) return true; } const b = findBackBtn(); if (b) { dualClick(b); await sleep(600); if (isMainScreen()) return true; } if (!c && !b) await sleep(400); } return isMainScreen(); }
function isMainScreen() { return !!findBtn("Adventure"); }
function readCountdownFor(name) { const btn = findBtn(name); if (!btn) return null; const cd = btn.querySelector(".countdownText__8af73"); if (!cd) return null; const m = cd.textContent?.trim().match(/(\d+):(\d+)/); return m ? parseInt(m[1]) * 60 + parseInt(m[2]) : null; }
function readCraftCountdown() { return readCountdownFor("Craft"); }
function readBattleCountdown() { return readCountdownFor("Battle"); }
function readHealCountdown() { return readCountdownFor("Heal"); }
function getCraftArrows() { const s = document.querySelector(".sequences__34527"); if (!s) return null; const imgs = s.querySelectorAll(".character__34527 img"); return imgs.length > 0 ? [...imgs] : null; }
function readCraftSequence() { const s = document.querySelector(".sequences__34527"); if (!s) return null; const chars = s.querySelectorAll(".character__34527"); if (!chars.length) return null; const arrows = []; for (const ch of chars) { const img = ch.querySelector("img"); if (!img) continue; const rot = (img.style.transform || "").match(/rotateZ\((\d+)deg\)/); const ok = (img.className||"").includes("arrowSuccess"); arrows.push({ key: ROT_MAP[rot ? rot[1] : "0"] || "ArrowUp", done: ok }); } return { arrows }; }
function canNav(w) { return activeNav === null || activeNav === w; }
function lockNav(w) { activeNav = w; }
function unlockNav(w) { if (activeNav === w) activeNav = null; }
function isBattleGameActive() {
    const grids = document.querySelectorAll('[class*="grid__"]');
    for (const grid of grids) {
        const items = [...grid.querySelectorAll('[class*="gridItem"]')];
        if (items.length >= 9) return true;
    }
    return false;
}

// ════════════════════════════════════════════
// ── BATTLE: Auto-Join Only ──
// ════════════════════════════════════════════
async function battleTick() {
    if (!btOn || dragging || btBusy) return;
    btBusy = true;
    try {
        if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("battle"); btState = BTS.WAITING; btBusy = false; return; }
        if (isSuccessScreen()) { await goBackToMain(3); unlockNav("battle"); const cd = readBattleCountdown(); btTotalWait = (cd !== null && cd > 0) ? cd : 0; btWaitStart = Date.now(); btState = BTS.WAITING; btBusy = false; return; }
        switch (btState) {
            case BTS.IDLE: {
                if (isBattleGameActive()) { lockNav("battle"); btState = BTS.ACTIVE; break; }
                const cd = readBattleCountdown();
                if (cd !== null && cd > 0) { btTotalWait = cd; btWaitStart = Date.now(); btState = BTS.WAITING; break; }
                if (!canNav("battle") || !isMainScreen()) break;
                const b = findBtn("Battle");
                if (b) { lockNav("battle"); dualClick(b); btState = BTS.ENTERING; }
                break;
            }
            case BTS.ENTERING: {
                let w = 0;
                while (w < 6000) {
                    if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("battle"); btState = BTS.WAITING; return; }
                    if (isBattleGameActive()) { btState = BTS.ACTIVE; break; }
                    if (w > 800 && isMainScreen()) { const b = findBtn("Battle"); if (b) dualClick(b); }
                    await sleep(200); w += 200;
                }
                if (btState === BTS.ENTERING) { unlockNav("battle"); btState = BTS.IDLE; }
                break;
            }
            case BTS.ACTIVE: {
                await sleep(1000);
                if (!isBattleGameActive() || isSuccessScreen()) { btState = BTS.EXITING; }
                break;
            }
            case BTS.EXITING: {
                await sleep(300);
                await goBackToMain(3);
                unlockNav("battle");
                const cd = readBattleCountdown();
                btTotalWait = (cd !== null && cd > 0) ? cd : 0;
                btWaitStart = Date.now();
                btState = BTS.WAITING;
                break;
            }
            case BTS.WAITING: {
                const cd = readBattleCountdown();
                if (cd === null || cd <= 0) { await sleep(2000); btState = BTS.IDLE; }
                else if (btTotalWait === 0) { btTotalWait = cd; btWaitStart = Date.now(); }
                break;
            }
        }
    } finally { btBusy = false; }
}
function startBattle() { stopBattle(); btState = BTS.IDLE; const lp = () => { battleTick(); btTimer = setTimeout(lp, hd(500)); }; btTimer = setTimeout(lp, hd(500)); }
function stopBattle() { clearTimeout(btTimer); btTimer = null; unlockNav("battle"); btState = BTS.IDLE; btBusy = false; }

// ════════════════════════════════════════════
// ── HEAL GAME ENGINE ──
// ════════════════════════════════════════════
function getHealGrid() {
    const grids = document.querySelectorAll('[class*="grid__"]');
    for (const grid of grids) {
        const items = [...grid.querySelectorAll('[class*="gridItem"]')];
        if (items.length >= 6) return items;
    }
    return null;
}
function isHealActive() { return !!getHealGrid(); }
function getCardKey(card) {
    const svg = card.querySelector('svg');
    if (svg) {
        const paths = svg.querySelectorAll('path');
        if (paths.length > 0) { const d = paths[0].getAttribute('d'); if (d && d.length > 10) return d.substring(0, 40); }
        const vb = svg.getAttribute('viewBox');
        if (vb) return vb + '_' + svg.innerHTML.length;
    }
    const img = card.querySelector('img');
    if (img && img.src) return img.src.split('/').pop().split('?')[0];
    for (const attr of card.attributes) { if (attr.name.includes('data') && attr.value) return attr.value; }
    return card.innerHTML.length + '_' + (card.textContent || '').trim().substring(0, 20);
}
function isCardMatched(card) {
    const html = card.outerHTML.toLowerCase();
    if (/matched|success|complete|solved|done/.test(html)) return true;
    const check = (el) => {
        try {
            const s = getComputedStyle(el);
            for (const p of ['borderColor','borderTopColor','backgroundColor','outlineColor']) {
                const c = s[p]; if (!c) continue;
                const m = c.match(/rgba?\(\s*(\d+),\s*(\d+),\s*(\d+)/);
                if (m && +m[2] > 80 && +m[2] > +m[1] * 1.3 && +m[2] > +m[3] * 1.3) return true;
            }
        } catch(e) {}
        return false;
    };
    if (check(card)) return true;
    for (const ch of card.children) if (check(ch)) return true;
    try { if (getComputedStyle(card).pointerEvents === 'none') return true; } catch(e) {}
    return false;
}
function readHealScore() {
    const headers = document.querySelectorAll('[data-text-variant="heading-xxl/normal"]');
    for (const h of headers) { const m = h.textContent?.match(/(\d+)\s*\/\s*(\d+)/); if (m) return { cur: +m[1], max: +m[2] }; }
    return null;
}
async function healCardSolve() {
    const cards = getHealGrid();
    if (!cards || cards.length < 6) return false;
    const totalCards = cards.length;
    let memory = {}, matched = new Set();
    for (let round = 0; round < 50 && hlOn; round++) {
        const freshCards = getHealGrid() || cards;
        freshCards.forEach((c, i) => { if (isCardMatched(c)) matched.add(i); });
        const sc = readHealScore();
        if (sc && sc.cur >= sc.max) return true;
        if (matched.size >= totalCards) return true;
        const unmatched = [];
        for (let i = 0; i < freshCards.length; i++) if (!matched.has(i)) unmatched.push(i);
        if (unmatched.length === 0) return true;
        const groups = {};
        for (const [idx, key] of Object.entries(memory)) {
            const i = parseInt(idx); if (matched.has(i)) continue;
            if (!groups[key]) groups[key] = []; groups[key].push(i);
        }
        let triplet = null;
        for (const [key, indices] of Object.entries(groups)) { if (indices.length >= 3) { triplet = indices.slice(0, 3); break; } }
        if (triplet) {
            for (const idx of triplet) { if (!hlOn) return false; reactClick(freshCards[idx]); await sleep(300); }
            await sleep(1200);
            const vc = getHealGrid() || freshCards; let anyMatched = false;
            triplet.forEach(idx => { if (idx < vc.length && isCardMatched(vc[idx])) { matched.add(idx); delete memory[idx]; anyMatched = true; } });
            if (!anyMatched) { triplet.forEach(idx => delete memory[idx]); await sleep(800); }
            continue;
        }
        const unknown = unmatched.filter(i => memory[i] === undefined);
        if (unknown.length >= 3) {
            const batch = unknown.slice(0, 3);
            for (const idx of batch) {
                if (!hlOn) return false;
                reactClick(freshCards[idx]); await sleep(200); await sleep(100);
                const vc = getHealGrid() || freshCards;
                if (idx < vc.length) { const key = getCardKey(vc[idx]); if (key) { memory[idx] = key; } }
            }
            await sleep(1200);
            const vc = getHealGrid() || freshCards;
            batch.forEach(idx => { if (idx < vc.length && isCardMatched(vc[idx])) { matched.add(idx); delete memory[idx]; } });
            continue;
        }
        let pairKey = null, pairIndices = null;
        for (const [key, indices] of Object.entries(groups)) { if (indices.length === 2) { pairKey = key; pairIndices = indices; break; } }
        if (pairKey && pairIndices && unknown.length > 0) {
            for (const idx of pairIndices) { reactClick(freshCards[idx]); await sleep(250); }
            const unknownIdx = unknown[0];
            reactClick(freshCards[unknownIdx]); await sleep(600);
            const vc = getHealGrid() || freshCards;
            if (unknownIdx < vc.length) { const key = getCardKey(vc[unknownIdx]); if (key) memory[unknownIdx] = key; }
            await sleep(1000);
            const vc2 = getHealGrid() || freshCards;
            [...pairIndices, unknownIdx].forEach(idx => { if (idx < vc2.length && isCardMatched(vc2[idx])) { matched.add(idx); delete memory[idx]; } });
            continue;
        }
        if (unknown.length > 0) {
            const batch = unknown.slice(0, 3);
            for (const idx of batch) {
                if (!hlOn) return false;
                reactClick(freshCards[idx]); await sleep(200); await sleep(100);
                const vc = getHealGrid() || freshCards;
                if (idx < vc.length) { const key = getCardKey(vc[idx]); if (key) { memory[idx] = key; } }
            }
            await sleep(1200);
            const vc = getHealGrid() || freshCards;
            batch.forEach(idx => { if (idx < vc.length && isCardMatched(vc[idx])) { matched.add(idx); delete memory[idx]; } });
            continue;
        }
        if (unknown.length === 0 && !triplet) { memory = {}; await sleep(500); }
    }
    const fs = readHealScore(); return fs && fs.cur >= fs.max;
}

async function healTick() {
    if (!hlOn || dragging || hlBusy) return; hlBusy = true;
    try {
        if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("heal"); hlState = HS.WAITING; hlBusy = false; return; }
        if (isSuccessScreen()) { await goBackToMain(3); unlockNav("heal"); const cd = readHealCountdown(); hlTotalWait = (cd !== null && cd > 0) ? cd : 0; hlWaitStart = Date.now(); hlState = HS.WAITING; hlBusy = false; return; }
        switch (hlState) {
            case HS.IDLE: { if (isHealActive()) { lockNav("heal"); hlState = HS.ACTIVE; break; } const cd = readHealCountdown(); if (cd !== null && cd > 0) { hlTotalWait = cd; hlWaitStart = Date.now(); hlState = HS.WAITING; break; } if (!canNav("heal") || !isMainScreen()) break; const b = findBtn("Heal"); if (b) { lockNav("heal"); dualClick(b); hlState = HS.ENTERING; } break; }
            case HS.ENTERING: { let w = 0; while (w < 6000) { if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("heal"); hlState = HS.WAITING; return; } if (isHealActive()) { hlState = HS.ACTIVE; break; } if (w > 800 && isMainScreen()) { const b = findBtn("Heal"); if (b) dualClick(b); } await sleep(200); w += 200; } if (hlState === HS.ENTERING) { unlockNav("heal"); hlState = HS.IDLE; } break; }
            case HS.ACTIVE: { try { await healCardSolve(); } catch(e) {} hlState = HS.DONE; break; }
            case HS.DONE: { await sleep(1500); hlState = HS.EXITING; break; }
            case HS.EXITING: { await sleep(300); await goBackToMain(3); unlockNav("heal"); const cd = readHealCountdown(); hlTotalWait = (cd !== null && cd > 0) ? cd : 0; hlWaitStart = Date.now(); hlState = HS.WAITING; break; }
            case HS.WAITING: { const cd = readHealCountdown(); if (cd === null || cd <= 0) { await sleep(2000); hlState = HS.IDLE; } else if (hlTotalWait === 0) { hlTotalWait = cd; hlWaitStart = Date.now(); } break; }
        }
    } finally { hlBusy = false; }
}
function startHeal() { stopHeal(); hlState = HS.IDLE; const lp = () => { healTick(); hlTimer = setTimeout(lp, hd(400)); }; hlTimer = setTimeout(lp, hd(400)); }
function stopHeal() { clearTimeout(hlTimer); hlTimer = null; unlockNav("heal"); hlState = HS.IDLE; hlBusy = false; }

// ════════════════════════════════════════════
// ── ADVENTURE ──
// ════════════════════════════════════════════
function autoAdv() { const b = getAdvButton(); if (b) fastClick(b); }
function startAdv() { stopAdv(); advInterval = setInterval(autoAdv, advDelay); }
function stopAdv() { clearInterval(advInterval); advInterval = null; }

// ════════════════════════════════════════════
// ── CRAFT ──
// ════════════════════════════════════════════
async function craftTick() {
    if (!crOn || dragging || crBusy) return; crBusy = true;
    try {
        if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("craft"); crState = CS.WAITING; crBusy = false; return; }
        if (isSuccessScreen()) { await goBackToMain(3); unlockNav("craft"); const cd = readCraftCountdown(); crTotalWait = (cd !== null && cd > 0) ? cd : 0; crWaitStart = Date.now(); crState = CS.WAITING; crBusy = false; return; }
        switch (crState) {
            case CS.IDLE: { if (getCraftArrows()) { lockNav("craft"); crState = CS.SOLVING; break; } const cd = readCraftCountdown(); if (cd !== null && cd > 0) { crTotalWait = cd; crWaitStart = Date.now(); crState = CS.WAITING; break; } if (!canNav("craft") || !isMainScreen()) break; const b = findBtn("Craft"); if (b) { lockNav("craft"); dualClick(b); crState = CS.ENTERING; } break; }
            case CS.ENTERING: { let w = 0; while (w < 4000) { if (getResourcePopup()) { dismissPopup(); await sleep(500); unlockNav("craft"); crState = CS.WAITING; return; } if (getCraftArrows()) { crState = CS.SOLVING; break; } if (w > 800 && isMainScreen()) { const b = findBtn("Craft"); if (b) dualClick(b); } await sleep(200); w += 200; } if (crState === CS.ENTERING) { unlockNav("craft"); crState = CS.IDLE; } break; }
            case CS.SOLVING: { const d = readCraftSequence(); if (!d || !d.arrows) { crState = CS.EXITING; break; } const rem = d.arrows.filter(a => !a.done); if (rem.length === 0) { crState = CS.EXITING; break; } for (const arrow of rem) { if (!crOn) break; sendKey(arrow.key); await sleep(15); } await sleep(300); if (!getCraftArrows()) crState = CS.EXITING; break; }
            case CS.EXITING: { await sleep(300); await goBackToMain(3); unlockNav("craft"); const cd = readCraftCountdown(); crTotalWait = (cd !== null && cd > 0) ? cd : 0; crWaitStart = Date.now(); crState = CS.WAITING; break; }
            case CS.WAITING: { const cd = readCraftCountdown(); if (cd === null || cd <= 0) { await sleep(2000); crState = CS.IDLE; } else if (crTotalWait === 0) { crTotalWait = cd; crWaitStart = Date.now(); } break; }
        }
    } finally { crBusy = false; }
}
function startCraft() { stopCraft(); crState = CS.IDLE; const lp = () => { craftTick(); crTimer = setTimeout(lp, hd(crDelay)); }; crTimer = setTimeout(lp, hd(crDelay)); }
function stopCraft() { clearTimeout(crTimer); crTimer = null; unlockNav("craft"); crState = CS.IDLE; crBusy = false; }

// ════════════════════════════════════════════
// ── AUTO DEFENCE ──
// ════════════════════════════════════════════
function startAutoDf() {
    if (!originalWidth) originalWidth = window.innerWidth;
    Object.defineProperty(window, 'innerWidth', { get: function() { return 190; }, configurable: true });
    window.dispatchEvent(new Event('resize'));
    if (mouseLockerInterval) clearInterval(mouseLockerInterval);
    mouseLockerInterval = setInterval(() => {
        const game = document.querySelector('[class*="game_"]'); if (!game) return;
        const fakeMouseOptions = { clientX: 85, clientY: window.innerHeight - 100, bubbles: true, cancelable: true, view: window };
        const mouseEvent = new MouseEvent('mousemove', fakeMouseOptions);
        const pointerEvent = new PointerEvent('pointermove', { ...fakeMouseOptions, pointerId: 1 });
        game.dispatchEvent(mouseEvent); game.dispatchEvent(pointerEvent);
        document.dispatchEvent(mouseEvent); document.dispatchEvent(pointerEvent);
    }, 16);
}
function stopAutoDf() {
    if (originalWidth) { Object.defineProperty(window, 'innerWidth', { get: function() { return originalWidth; }, configurable: true }); window.dispatchEvent(new Event('resize')); }
    if (mouseLockerInterval) { clearInterval(mouseLockerInterval); mouseLockerInterval = null; }
}

// ════════════════════════════════════════════
// ── AUTO TARGET - استراتيجية جديدة كليًا ──
// ════════════════════════════════════════════

// دالة لإيجاد الـ target container بكل الطرق الممكنة
function findTargetContainer() {
    // طريقة 1: البحث بـ class يحتوي على targetContainer
    let el = document.querySelector('[class*="targetContainer"]');
    if (el) return el;
    // طريقة 2: البحث عبر الـ game container
    const game = document.querySelector('[class*="game_"]') || document.querySelector('[class*="game__"]');
    if (game) {
        const children = game.querySelectorAll('div');
        for (const child of children) {
            if (child.className && child.className.includes && child.className.includes('target')) return child;
        }
    }
    // طريقة 3: البحث بالـ style (left, top, transform كخاصية)
    const allDivs = document.querySelectorAll('div[style*="transform: scale"]');
    for (const div of allDivs) {
        if (div.style.left && div.style.top && div.style.transform) {
            const parent = div.closest('[class*="game"]') || div.closest('[class*="container"]');
            if (parent) return div;
        }
    }
    return null;
}

// دالة للحصول على React Fiber من عنصر DOM
function getReactFiber(el) {
    if (!el) return null;
    const key = Object.keys(el).find(k =>
        k.startsWith('__reactFiber') ||
        k.startsWith('__reactInternalInstance') ||
        k.startsWith('_reactFiber')
    );
    return key ? el[key] : null;
}

// دالة للحصول على React Props من عنصر DOM
function getReactProps(el) {
    if (!el) return null;
    const key = Object.keys(el).find(k =>
        k.startsWith('__reactProps') ||
        k.startsWith('__reactEventHandlers')
    );
    return key ? el[key] : null;
}

// دالة للبحث عن onClick في شجرة React Fiber
function findReactHandler(el, eventName) {
    try {
        let fiber = getReactFiber(el);
        let depth = 0;
        while (fiber && depth < 20) {
            const props = fiber.memoizedProps || fiber.pendingProps;
            if (props) {
                if (props[eventName]) return { handler: props[eventName], fiber };
                if (props.onClick && eventName === 'onClick') return { handler: props.onClick, fiber };
                if (props.onPointerDown && eventName === 'onPointerDown') return { handler: props.onPointerDown, fiber };
                if (props.onMouseDown && eventName === 'onMouseDown') return { handler: props.onMouseDown, fiber };
            }
            fiber = fiber.return;
            depth++;
        }
    } catch(e) {}
    return null;
}

// إنشاء synthetic event لـ React
function createSyntheticEvent(el, eventType, cx, cy) {
    const nativeEvent = new MouseEvent(eventType, {
        bubbles: true, cancelable: true, view: window,
        clientX: cx, clientY: cy,
        screenX: cx, screenY: cy,
        button: 0, buttons: 1
    });
    return nativeEvent;
}

// الاستراتيجية الجديدة: تعديل الـ state مباشرة + CSS + أحداث متعددة
function startAutoTarget() {
    // 1. إضافة CSS لتثبيت الهدف في المنتصف
    let styleEl = document.getElementById('cheatStyleTarget');
    if (!styleEl) {
        styleEl = document.createElement('style');
        styleEl.id = 'cheatStyleTarget';
        styleEl.innerHTML = `
            [class*="targetContainer"] {
                left: 50% !important;
                top: 50% !important;
                transform: translate(-50%, -50%) scale(1) !important;
                transition: none !important;
                z-index: 9999 !important;
                pointer-events: all !important;
            }
            [class*="targetContainer"] * {
                pointer-events: all !important;
            }
        `;
        document.head.appendChild(styleEl);
    }

    if (tgInterval) clearInterval(tgInterval);

    tgInterval = setInterval(() => {
        const target = findTargetContainer();
        if (!target) return;

        // تحديث CSS يدوياً في كل دورة للتأكد
        target.style.setProperty('left', '50%', 'important');
        target.style.setProperty('top', '50%', 'important');
        target.style.setProperty('transform', 'translate(-50%, -50%) scale(1)', 'important');
        target.style.setProperty('transition', 'none', 'important');
        target.style.setProperty('pointer-events', 'all', 'important');

        const rect = target.getBoundingClientRect();
        const cx = rect.left + rect.width / 2;
        const cy = rect.top + rect.height / 2;

        // البحث عن كل العناصر تحت الهدف
        const elements = document.elementsFromPoint(cx, cy);

        // محاولة 1: تشغيل React handlers مباشرة
        for (const el of elements) {
            try {
                // محاولة onClick مباشرة
                const props = getReactProps(el);
                if (props) {
                    if (props.onClick) {
                        try {
                            const evt = createSyntheticEvent(el, 'click', cx, cy);
                            props.onClick(evt);
                        } catch(e) {}
                    }
                    if (props.onPointerDown) {
                        try {
                            const evt = new PointerEvent('pointerdown', {
                                bubbles: true, cancelable: true, view: window,
                                clientX: cx, clientY: cy, pointerId: 1,
                                pointerType: 'mouse', isPrimary: true, pressure: 0.5, buttons: 1
                            });
                            props.onPointerDown(evt);
                        } catch(e) {}
                    }
                    if (props.onMouseDown) {
                        try {
                            const evt = createSyntheticEvent(el, 'mousedown', cx, cy);
                            props.onMouseDown(evt);
                        } catch(e) {}
                    }
                }
            } catch(e) {}
        }

        // محاولة 2: إرسال أحداث DOM كاملة لكل العناصر
        const baseOpts = {
            bubbles: true, cancelable: true, composed: true, view: window,
            clientX: cx, clientY: cy,
            screenX: (window.screenX || 0) + cx,
            screenY: (window.screenY || 0) + cy,
            button: 0, buttons: 1
        };
        const pointerOpts = {
            ...baseOpts,
            pointerId: 1, pointerType: 'mouse',
            isPrimary: true, pressure: 0.5,
            width: 1, height: 1, tiltX: 0, tiltY: 0
        };

        // إرسال للـ target نفسه
        try { target.dispatchEvent(new PointerEvent('pointermove', { ...pointerOpts, pressure: 0 })); } catch(e) {}
        try { target.dispatchEvent(new MouseEvent('mousemove', baseOpts)); } catch(e) {}
        try { target.dispatchEvent(new PointerEvent('pointerdown', pointerOpts)); } catch(e) {}
        try { target.dispatchEvent(new MouseEvent('mousedown', baseOpts)); } catch(e) {}
        try { target.dispatchEvent(new PointerEvent('pointerup', { ...pointerOpts, pressure: 0 })); } catch(e) {}
        try { target.dispatchEvent(new MouseEvent('mouseup', baseOpts)); } catch(e) {}
        try { target.dispatchEvent(new MouseEvent('click', baseOpts)); } catch(e) {}

        // إرسال لكل العناصر تحت الهدف
        for (const el of elements) {
            if (el === document.body || el === document.documentElement || el === document || el === target) continue;
            try { el.dispatchEvent(new PointerEvent('pointerdown', pointerOpts)); } catch(e) {}
            try { el.dispatchEvent(new MouseEvent('mousedown', baseOpts)); } catch(e) {}
            try { el.dispatchEvent(new PointerEvent('pointerup', { ...pointerOpts, pressure: 0 })); } catch(e) {}
            try { el.dispatchEvent(new MouseEvent('mouseup', baseOpts)); } catch(e) {}
            try { el.dispatchEvent(new MouseEvent('click', baseOpts)); } catch(e) {}
        }

        // محاولة 3: البحث عن React handlers في شجرة الـ fiber وتنفيذها
        try {
            const result = findReactHandler(target, 'onClick');
            if (result && result.handler) {
                const fakeEvent = createSyntheticEvent(target, 'click', cx, cy);
                result.handler(fakeEvent);
            }
        } catch(e) {}

        // محاولة 4: استخدام __REACT_DEVTOOLS_GLOBAL_HOOK__ للوصول للـ store
        try {
            const hook = window.__REACT_DEVTOOLS_GLOBAL_HOOK__;
            if (hook && hook.getFiberRoots) {
                // هذا للتشخيص فقط
            }
        } catch(e) {}

    }, 50);
}

function stopAutoTarget() {
    const s = document.getElementById('cheatStyleTarget');
    if (s) s.remove();
    if (tgInterval) { clearInterval(tgInterval); tgInterval = null; }
    // إزالة الـ inline styles المضافة
    const target = findTargetContainer();
    if (target) {
        target.style.removeProperty('left');
        target.style.removeProperty('top');
        target.style.removeProperty('transform');
        target.style.removeProperty('transition');
        target.style.removeProperty('pointer-events');
    }
}

// ════════════════════════════════════════════
// ── WRONG GAME ──
// ════════════════════════════════════════════
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

// ════════════════════════════════════════════
// ── RENDER ──
// ════════════════════════════════════════════
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
    if (btState === BTS.WAITING) {
        const cd = readBattleCountdown();
        if (cd !== null && btTotalWait > 0) { const p = Math.min(100, (Date.now()-btWaitStart)/1000/btTotalWait*100); setText(btTextEl, fmtTime(cd)); setCSS(btIconEl,"filter","invert(1)"); setCSS(btn,"background",`linear-gradient(90deg,#00c78b ${p}%,#1a1a1a ${p}%)`); setCSS(btn,"color","white"); return; }
        setText(btTextEl, tx("battleIdle")); setCSS(btIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return;
    }
    const labels = {[BTS.IDLE]:"battleIdle",[BTS.ENTERING]:"battleEntering",[BTS.ACTIVE]:"battleActive",[BTS.EXITING]:"battleExiting"};
    if (btState === BTS.IDLE && activeNav && activeNav !== "battle") setText(btTextEl, tx("paused")); else setText(btTextEl, tx(labels[btState] || "battle"));
    setCSS(btIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a");
}

function renderHeal() {
    const btn = document.getElementById("healBtn"); if (!btn || !hlIconEl || !hlTextEl) return;
    if (!hlOn) { setText(hlTextEl, tx("heal")); setCSS(hlIconEl,"filter","invert(1)"); setCSS(btn,"background","#1a1a1a"); setCSS(btn,"color","white"); return; }
    if (getResourcePopup()) { setText(hlTextEl, tx("noResources")); setCSS(hlIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return; }
    if (hlState === HS.WAITING) { const cd = readHealCountdown(); if (cd !== null && hlTotalWait > 0) { const p = Math.min(100, (Date.now()-hlWaitStart)/1000/hlTotalWait*100); setText(hlTextEl, fmtTime(cd)); setCSS(hlIconEl,"filter","invert(1)"); setCSS(btn,"background",`linear-gradient(90deg,#00c78b ${p}%,#1a1a1a ${p}%)`); setCSS(btn,"color","white"); return; } setText(hlTextEl, tx("healIdle")); setCSS(hlIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return; }
    if (hlState === HS.ACTIVE) { const sc = readHealScore(); if (sc) { const p = sc.cur/sc.max*100; setText(hlTextEl, `${tx("healActive")} ${sc.cur}/${sc.max}`); setCSS(hlIconEl,"filter","invert(1)"); setCSS(btn,"background",`linear-gradient(90deg,#00c78b ${p}%,#1a1a1a ${p}%)`); setCSS(btn,"color","white"); return; } setText(hlTextEl, tx("healActive")); setCSS(hlIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); return; }
    const labels = {[HS.IDLE]:"healIdle",[HS.ENTERING]:"healEntering",[HS.DONE]:"healDone",[HS.EXITING]:"healExiting"};
    if (hlState === HS.IDLE && activeNav && activeNav !== "heal") setText(hlTextEl, tx("paused")); else setText(hlTextEl, tx(labels[hlState] || "heal"));
    setCSS(hlIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a");
}

function renderAutoDf() {
    const btn = document.getElementById("autoDfBtn"); if (!btn || !autoDfIconEl || !autoDfTextEl) return;
    setText(autoDfTextEl, tx("autoDefence"));
    if (autoDfOn) { setCSS(autoDfIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); }
    else { setCSS(autoDfIconEl,"filter","invert(1)"); setCSS(btn,"background","#1a1a1a"); setCSS(btn,"color","white"); }
}
function renderAutoTg() {
    const btn = document.getElementById("autoTgBtn"); if (!btn || !autoTgIconEl || !autoTgTextEl) return;
    setText(autoTgTextEl, tx("autoTarget"));
    if (autoTgOn) { setCSS(autoTgIconEl,"filter","none"); setCSS(btn,"background","#00c78b"); setCSS(btn,"color","#1a1a1a"); }
    else { setCSS(autoTgIconEl,"filter","invert(1)"); setCSS(btn,"background","#1a1a1a"); setCSS(btn,"color","white"); }
}

// ════════════════════════════════════════════
// ── LANGUAGE & GUI ──
// ════════════════════════════════════════════
function updateLang() {
    const gui = document.getElementById("meadowAutoGUI");
    if (gui) { gui.dir = (lang === "ar" || lang === "he") ? "rtl" : "ltr"; }
    const flagSpan = document.getElementById("flagSpan"); if (flagSpan) flagSpan.innerText = LANG_DATA[lang].flag;
    const a = document.querySelector("#advBtn .btnText"); if (a) setText(a, tx("adventure"));
    const hl = document.querySelector("#healBtn .btnText"); if (hl) setText(hl, tx("heal"));
    const adf = document.querySelector("#autoDfBtn .btnText"); if (adf) setText(adf, tx("autoDefence"));
    const atg = document.querySelector("#autoTgBtn .btnText"); if (atg) setText(atg, tx("autoTarget"));
    const w = document.querySelector("#wgBtn .btnText"); if (w && !clkRunning) setText(w, tx("wrongGame"));
    setText(document.getElementById("dragHint"), tx("drag"));
    setText(document.getElementById("speedsTitle"), tx("speeds"));
    setText(document.getElementById("speedTip"), tx("speedTip"));
    const al = document.getElementById("advSliderLabel"); if (al) setText(al, tx("advLabel") + " : ");
    const cl = document.getElementById("craftSliderLabel"); if (cl) setText(cl, tx("craftLabel") + " : ");
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
        html += `<button class="lang-sel-btn" data-lang="${key}" style="padding:10px;border:2px solid #1a1a1a;border-radius:8px;background:white;cursor:pointer;font-weight:bold;display:flex;align-items:center;gap:8px;font-size:13px;transition:0.2s;"><span style="font-size:18px">${LANG_DATA[key].flag}</span> ${LANG_DATA[key].name}</button>`;
    }
    html += `</div>`;
    modal.innerHTML = html;
    document.body.appendChild(modal);
    modal.querySelectorAll('.lang-sel-btn').forEach(btn => {
        btn.addEventListener('click', () => {
            lang = btn.getAttribute('data-lang'); modal.remove();
            if (isFirstTime) { createMainGUI(); } else { const m = document.getElementById("meadowAutoGUI"); if(m) m.style.display = "block"; updateLang(); }
        });
        btn.addEventListener('mouseover', () => btn.style.background = "#00c78b");
        btn.addEventListener('mouseout',  () => btn.style.background = "white");
    });
}

function createMainGUI() {
    const gui = document.createElement("div"); gui.id = "meadowAutoGUI";
    gui.style.cssText = "position:fixed;top:100px;left:40px;z-index:999999;width:240px;background:#f8f1e3;border:4px solid #1a1a1a;border-radius:10px;box-shadow:6px 6px 0 #1a1a1a;font-family:system-ui,sans-serif;color:#1a1a1a;padding:10px;user-select:none;";

    const header = document.createElement("div");
    header.id = "dragHeader";
    header.style.cssText = "background:#00c78b;color:white;padding:8px;margin:-10px -10px 10px -10px;border-radius:5px 5px 0 0;cursor:grab;display:flex;align-items:center;justify-content:space-between;min-height:30px;";
    header.innerHTML = `
        <div id="langFlagBtn" title="Change Language" style="cursor:pointer;background:rgba(0,0,0,0.2);padding:3px 8px;border-radius:5px;font-size:14px;display:flex;align-items:center;gap:4px;transition:0.2s;">🌐 <span id="flagSpan">${LANG_DATA[lang].flag}</span></div>
        <img src="${ICONS.logo}" style="height:28px;pointer-events:none" draggable="false">
        <div style="display:flex;align-items:center;gap:10px;margin:0 5px;">
            <img id="settingsBtn" title="Settings" src="${ICONS.settings}" style="height:16px;width:16px;cursor:pointer;filter:invert(1);" draggable="false">
            <div id="minToggleBtn" title="Minimize" style="cursor:pointer;color:white;font-weight:bold;font-size:20px;line-height:1;margin-bottom:2px;">−</div>
        </div>`;
    gui.appendChild(header);

    const content = document.createElement("div"); content.id = "guiContent";
    const dragHint = document.createElement("div"); dragHint.id = "dragHint"; dragHint.style.cssText = "text-align:center;font-size:11px;opacity:.75;margin-bottom:10px;";
    const btnBox = document.createElement("div"); btnBox.id = "btnBox"; btnBox.style.cssText = "max-height:400px;overflow-y:auto;padding:0 2px;";
    content.appendChild(dragHint); content.appendChild(btnBox);

    const settingsPanel = document.createElement("div"); settingsPanel.id = "settingsPanel";
    settingsPanel.style.cssText = "display:none;margin-top:8px;padding:12px;background:#e8e0d3;border:2px solid #1a1a1a;border-radius:6px;";

    const speedsTitle = document.createElement("div"); speedsTitle.id = "speedsTitle";
    speedsTitle.style.cssText = "font-weight:bold;margin-bottom:12px;text-align:center;font-size:13px;";
    settingsPanel.appendChild(speedsTitle);

    const advRow = document.createElement("div"); advRow.style.cssText = "margin-bottom:14px;";
    const advLabelEl = document.createElement("div"); advLabelEl.style.cssText = "font-size:12px;margin-bottom:5px;display:flex;justify-content:space-between;";
    const advLabelText = document.createElement("span"); advLabelText.id = "advSliderLabel"; advLabelText.textContent = tx("advLabel") + " : ";
    const advValSpan = document.createElement("span"); advValSpan.id = "advVal"; advValSpan.style.cssText = "font-weight:bold;color:#00c78b;"; advValSpan.textContent = String(advDelay);
    advLabelEl.appendChild(advLabelText); advLabelEl.appendChild(advValSpan);
    const advSlider = document.createElement("input"); advSlider.type = "range"; advSlider.id = "sliderAdv";
    advSlider.min = 10; advSlider.max = 900; advSlider.value = advDelay;
    advSlider.style.cssText = "width:100%;cursor:pointer;accent-color:#00c78b;height:6px;";
    advRow.appendChild(advLabelEl); advRow.appendChild(advSlider);
    settingsPanel.appendChild(advRow);

    const crRow = document.createElement("div"); crRow.style.cssText = "margin-bottom:6px;";
    const crLabelEl = document.createElement("div"); crLabelEl.style.cssText = "font-size:12px;margin-bottom:5px;display:flex;justify-content:space-between;";
    const crLabelText = document.createElement("span"); crLabelText.id = "craftSliderLabel"; crLabelText.textContent = tx("craftLabel") + " : ";
    const crValSpan = document.createElement("span"); crValSpan.id = "craftVal"; crValSpan.style.cssText = "font-weight:bold;color:#00c78b;"; crValSpan.textContent = String(crDelay);
    crLabelEl.appendChild(crLabelText); crLabelEl.appendChild(crValSpan);
    const crSlider = document.createElement("input"); crSlider.type = "range"; crSlider.id = "sliderCraft";
    crSlider.min = 300; crSlider.max = 800; crSlider.value = crDelay;
    crSlider.style.cssText = "width:100%;cursor:pointer;accent-color:#00c78b;height:6px;";
    crRow.appendChild(crLabelEl); crRow.appendChild(crSlider);
    settingsPanel.appendChild(crRow);

    const speedTip = document.createElement("div"); speedTip.id = "speedTip";
    speedTip.style.cssText = "text-align:center;margin-top:10px;font-size:10px;opacity:.7;";
    settingsPanel.appendChild(speedTip);
    content.appendChild(settingsPanel);
    gui.appendChild(content);
    document.body.appendChild(gui);

    advSlider.addEventListener("input", e => {
        advDelay = parseInt(e.target.value);
        setText(advValSpan, String(advDelay));
        if (advOn) startAdv();
    });
    crSlider.addEventListener("input", e => {
        crDelay = parseInt(e.target.value);
        setText(crValSpan, String(crDelay));
        if (crOn) startCraft();
    });

    const adv    = makeBtn("advBtn",    ICONS.adventure, btnBox); adv.btn.style.minHeight = "auto";
    const craft  = makeBtn("craftBtn",  ICONS.craft,     btnBox); crIconEl = craft.img; crTextEl = craft.span;
    const battle = makeBtn("battleBtn", ICONS.battle,    btnBox); btIconEl = battle.img; btTextEl = battle.span;
    const heal   = makeBtn("healBtn",   ICONS.heal,      btnBox); hlIconEl = heal.img;   hlTextEl = heal.span;
    heal.img.style.filter = "invert(1) sepia(1) saturate(5) hue-rotate(80deg)";
    const autoDf = makeBtn("autoDfBtn", ICONS.battle,    btnBox); autoDfIconEl = autoDf.img; autoDfTextEl = autoDf.span;
    const autoTg = makeBtn("autoTgBtn", ICONS.craft,     btnBox); autoTgIconEl = autoTg.img; autoTgTextEl = autoTg.span;
    const wg     = makeBtn("wgBtn",     ICONS.wrongGame, btnBox); wg.btn.style.minHeight = "auto"; wg.btn.style.background = "#f5c400"; wg.btn.style.color = "#1a1a1a"; wg.img.style.filter = "none";

    let isDragging = false, startX = 0, startY = 0, startLeft = 0, startTop = 0;

    header.addEventListener("mousedown", function(e) {
        const tag = e.target.tagName.toUpperCase();
        if (tag === "INPUT" || tag === "BUTTON" || tag === "SELECT") return;
        if (e.target.closest("#langFlagBtn")) return;
        if (e.target.id === "settingsBtn") return;
        if (e.target.id === "minToggleBtn") return;
        e.preventDefault();
        isDragging = true; dragging = true;
        header.style.cursor = "grabbing";
        startX = e.clientX; startY = e.clientY;
        startLeft = parseInt(gui.style.left) || gui.offsetLeft;
        startTop  = parseInt(gui.style.top)  || gui.offsetTop;
    });

    window.addEventListener("mousemove", function(e) {
        if (!isDragging || !e.isTrusted) return;
        gui.style.left = (startLeft + e.clientX - startX) + "px";
        gui.style.top  = (startTop  + e.clientY - startY) + "px";
    });

    window.addEventListener("mouseup", function(e) {
        if (!isDragging || !e.isTrusted) return;
        isDragging = false; dragging = false;
        header.style.cursor = "grab";
    });

    document.getElementById("langFlagBtn").addEventListener("click", () => showLanguageModal(false));
    document.getElementById("langFlagBtn").addEventListener("mouseover", function() { this.style.background="rgba(0,0,0,0.4)"; });
    document.getElementById("langFlagBtn").addEventListener("mouseout",  function() { this.style.background="rgba(0,0,0,0.2)"; });

    document.getElementById("minToggleBtn").addEventListener("click", function(e) {
        e.stopPropagation(); isMinimized = !isMinimized;
        if (isMinimized) { content.style.display = "none"; this.innerText = "+"; gui.style.paddingBottom = "0"; }
        else { content.style.display = "block"; this.innerText = "−"; gui.style.paddingBottom = "10px"; }
    });

    document.getElementById("settingsBtn").addEventListener("click", function(e) {
        e.stopPropagation();
        settingsPanel.style.display = settingsPanel.style.display === "none" ? "block" : "none";
    });

    adv.btn.addEventListener("click",   () => { advOn = !advOn; setCSS(adv.img,"filter",advOn?"none":"invert(1)"); setCSS(adv.btn,"background",advOn?"#00c78b":"#1a1a1a"); setCSS(adv.btn,"color",advOn?"#1a1a1a":"white"); advOn ? startAdv() : stopAdv(); });
    craft.btn.addEventListener("click", () => { crOn = !crOn;   crOn   ? startCraft()       : stopCraft(); });
    battle.btn.addEventListener("click",() => { btOn = !btOn;   btOn   ? startBattle()      : stopBattle(); });
    heal.btn.addEventListener("click",  () => { hlOn = !hlOn;   hlOn   ? startHeal()        : stopHeal(); });
    autoDf.btn.addEventListener("click",() => { autoDfOn = !autoDfOn; autoDfOn ? startAutoDf()    : stopAutoDf(); });
    autoTg.btn.addEventListener("click",() => { autoTgOn = !autoTgOn; autoTgOn ? startAutoTarget() : stopAutoTarget(); });
    wg.btn.addEventListener("click", do500Clicks);

    updateLang();
    window._renderInterval = setInterval(() => {
        renderCraft(); renderBattle(); renderHeal(); renderAutoDf(); renderAutoTg();
    }, 200);
}

showLanguageModal(true);

window._meadowCleanup = () => {
    stopAdv(); stopCraft(); stopBattle(); stopHeal(); stopAutoDf(); stopAutoTarget();
    clearInterval(clkInterval);
    if (window._renderInterval) clearInterval(window._renderInterval);
    crOn = advOn = btOn = hlOn = autoDfOn = autoTgOn = false;
    const g = document.getElementById("meadowAutoGUI"); if (g) g.remove();
    const l = document.getElementById("meadowLangModal"); if (l) l.remove();
};
window.stopMeadowScript = window._meadowCleanup;
})();
