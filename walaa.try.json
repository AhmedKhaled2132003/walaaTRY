// ==UserScript==
// @name         Dr Ahmed Khaled 👑 | سكريبت د.أحمد خالد
// @namespace    https://www.facebook.com/Dr.Ahmed.FamilyFarm
// @version      1.5
// @description  واجهة متطورة لفتح الكروت، محطة التفكيك، فتح الروابط وارسال روابط المهمات  👑
// @author       Dr Ahmed Khaled 👑
// @match        *.centurygames.com/*
// @require      https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js
// @require      https://unpkg.com/@supabase/supabase-js
// @grant        unsafeWindow
// @grant        GM_xmlhttpRequest
// @grant        GM_setClipboard
// @grant        GM_setValue
// @grant        GM_getValue
// @connect      raw.githubusercontent.com
// @connect      *.supabase.co
// @updateURL    https://raw.githubusercontent.com/ak2132003/DrKLDscript/main/DrKLDscript.user.js
// @downloadURL  https://raw.githubusercontent.com/ak2132003/DrKLDscript/main/DrKLDscript.user.js
// @run-at       document-end
// ==/UserScript==

(function () {
    'use strict';
(function () {
    'use strict';

    // التحقق من وجود تحديث جديد
    const currentVersion = '1.4';
    fetch('https://github.com/ak2132003/allinone/raw/refs/heads/main/allscript.user.js')
      .then(response => response.text())
      .then(script => {
        const remoteVersion = script.match(/@version\s+([\d.]+)/)[1];
        if (remoteVersion !== currentVersion) {
          alert(`يوجد تحديث جديد للسكربت! الإصدار ${remoteVersion} متاح.\nيرجى التحديث للحصول على أحدث الميزات.`);
        }
      })
      .catch(err => console.error('خطأ أثناء التحقق من التحديث:', err));
})();
// تحميل الخط
let isMainBtnHidden = localStorage.getItem('isMainBtnHidden') === 'true';

const fontLink = document.createElement('link');
fontLink.href = 'https://fonts.googleapis.com/css2?family=Cairo:wght@700&display=swap';
fontLink.rel = 'stylesheet';
document.head.appendChild(fontLink);

// متغير لتحديد الوضع الحالي (يتم تحميله من localStorage أو استخدام الوضع الافتراضي)
let currentMode = localStorage.getItem('menuMode') || 'mode1';

// ستايل عام
const style = document.createElement('style');
style.textContent = `
    @keyframes fadeIn { from { opacity: 0; transform: scale(0.9); } to { opacity: 1; transform: scale(1); } }
    @keyframes fadeOut { from { opacity: 1; transform: scale(1); } to { opacity: 0; transform: scale(0.9); } }

    /* أنماط الوضع الأول */
    .mode1 .dr-panel {
        font-family: 'Cairo', sans-serif;
        position: fixed;
        top: 50%; left: 50%;
        transform: translate(-50%, -50%);
        background: linear-gradient(135deg, rgba(139, 92, 246, 0.8), rgba(253, 224, 71, 0.6));
        backdrop-filter: blur(12px);
        box-shadow: 0 8px 32px rgba(0,0,0,0.2);
        border-radius: 16px;
        padding: 25px;
        min-width: 320px;
        max-width: 600px;
        width: auto;
        display: none;
        flex-direction: column;
        align-items: center;
        z-index: 99999;
        box-sizing: border-box;
    }

    .mode1 .dr-menu {
        position: absolute;
        top: 50%; left: 50%;
        transform: translate(-50%, -50%);
        display: none;
        flex-direction: column;
        background: url('https://drahmedkhaled.neocities.org/Background%2011.png') no-repeat center;
        background-size: cover;
        backdrop-filter: blur(10px);
        border-radius: 12px;
        overflow: hidden;
        z-index: 9999;
        animation: fadeIn 0.3s ease;
    }

    /* أنماط الوضع الثاني */
    .mode2 .dr-panel {
        font-family: 'Cairo', sans-serif;
        position: fixed;
        top: 50%; left: 50%;
        transform: translate(-50%, -50%);
        background: linear-gradient(135deg, rgba(139, 92, 246, 0.8), rgba(253, 224, 71, 0.6));
        backdrop-filter: blur(12px);
        box-shadow: 0 8px 32px rgba(0,0,0,0.2);
        border-radius: 16px;
        padding: 25px;
        min-width: 320px;
        max-width: 600px;
        width: auto;
        display: none;
        flex-direction: column;
        align-items: center;
        z-index: 99999;
        box-sizing: border-box;
    }

    .mode2 .dr-menu {
        position: fixed;
        top: 74.5%;
        left: 85.5%;
        transform: translate(-50%, -50%);
        display: flex;
        flex-wrap: wrap;
        padding: 6px;
        background: linear-gradient(135deg, rgba(255, 240, 200, 0.25), rgba(240, 240, 255, 0.25), rgba(255, 182, 193, 0.25));
        backdrop-filter: blur(6px);
        border-radius: 10px;
        overflow: visible;
        z-index: 9999;
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.12);
        animation: fadeIn 0.3s ease;
        white-space: nowrap;
        width: 1px;
        gap: 2px;
        min-width: 160px;
    }

    /* الأنماط المشتركة بين الوضعين */
    .dr-panel h3 {
        margin-bottom: 15px;
        font-size: 22px;
        color: #fff;
        text-shadow: 0 0 3px #000;
    }
    .dr-panel input, .dr-panel select, .dr-panel textarea {
        width: 100%;
        padding: 10px;
        margin-bottom: 10px;
        border: none;
        border-radius: 8px;
        font-size: 15px;
    }
    .dr-panel button {
        background: linear-gradient(135deg, #4CAF50, #388E3C);
        color: black;
        padding: 10px 20px;
        border: none;
        border-radius: 8px;
        font-size: 16px;
        cursor: pointer;
        transition: transform 0.2s ease;
    }
    .dr-panel button:hover {
        transform: scale(1.05);
    }
    .dr-main-btn {
        position: fixed;
        bottom: 120px;
        right: 25px;
        width: 85px;
        height: 85px;
        border-radius: 50%;
        background: url('https://drahmedkhaled.neocities.org/%E2%80%94Pngtree%E2%80%94golden%20crown%20vector%20design_5415535-Photoroom.png') no-repeat center;
        background-size: contain;
        background-color: rgba(0, 0, 0, 0.6);
        color: white;
        display: flex;
        align-items: center;
        justify-content: center;
        text-align: center;
        font-size: 14px;
        font-weight: bold;
        font-family: 'Cairo', sans-serif;
        cursor: pointer;
        z-index: 9999;
        box-shadow: 0 10px 25px rgba(0,0,0,0.3);
        transition: transform 0.3s ease;
    }
    .dr-main-btn:hover {
        transform: scale(1.1);
    }
    .mode1 .dr-menu button {
        background: none;
        border: none;
        padding: 12px 18px;
        font-size: 17.2px;
        color: black;
        text-shadow: 0 0 2px #000;
        font-family: 'Cairo', sans-serif;
        cursor: pointer;
        transition: background 0.2s ease;
    }
    .mode1 .dr-menu button:hover {
        color: black;
        background: rgba(255, 192, 203, 0.2);
        box-shadow:
            0 0 10px rgba(255, 105, 180, 0.5),
            0 0 25px rgba(255, 105, 180, 0.3),
            0 0 35px rgba(255, 105, 180, 0.2);
        transition: all 0.3s ease;
    }
    .mode2 .dr-menu button {
        background: rgba(255, 255, 255, 0.15);
        border: none;
        padding: 1px 1px;
        font-size: 14px;
        color: black;
        text-shadow: 0 0 2px rgba(255, 255, 255, 0.4);
        font-family: 'Cairo', sans-serif;
        cursor: pointer;
        transition: all 0.25s ease;
        position: relative;
        margin: 0;
        box-sizing: border-box;
        width: calc(50% - 1px);
        flex: 0 0 calc(50% - 1px);
        border-radius: 1px;
    }
    .mode2 .dr-menu button:hover {
        background: rgba(255, 255, 255, 0.3);
        transform: translateY(-1px);
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.08);
    }
    .mode1 .dr-submenu {
        display: none;
        flex-direction: row;
        background: rgba(255, 255, 255, 0.05);
        border-top: 1px solid rgba(255, 255, 255, 0.2);
        overflow: hidden;
        transition: max-height 0.3s ease, opacity 0.3s ease;
        max-height: 0;
        opacity: 0;
    }
    .mode1 .dr-submenu.open {
        display: flex;
        max-height: 500px;
        opacity: 1;
    }
    .mode1 .dr-submenu button {
        padding-left: 30px;
    }
    .mode2 .dr-submenu {
        position: absolute;
        bottom: 100%;
        left: 0;
        transform: translateY(-5px);
        min-width: 100%;
        white-space: nowrap;
        display: none;
        flex-direction: column;
        background: linear-gradient(to bottom, rgba(255, 255, 255, 0.9), rgba(240, 240, 240, 0.9));
        backdrop-filter: blur(8px);
        border: 1px solid rgba(220, 220, 220, 0.5);
        border-radius: 8px;
        box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        overflow: hidden;
        z-index: 10000;
        transition: max-height 0.3s ease, opacity 0.3s ease;
        max-height: 0;
        opacity: 0;
    }
    .mode2 .dr-submenu.open {
        display: flex;
        max-height: 500px;
        opacity: 1;
    }
    .mode2 .dr-submenu button {
        padding: 10px 10px;
        font-size: 15px;
        background: none;
        border: none;
        color: #333;
        text-align: center;
        width: 100%;
        transition: background 0.2s ease, color 0.2s ease;
    }
    .mode2 .dr-submenu button:hover {
        background: rgba(0, 0, 0, 0.08);
        color: #000;
        transform: translateX(3px);
    }
    .close-btn {
        position: absolute;
        top: 10px;
        right: 10px;
        font-size: 24px;
        color: white;
        cursor: pointer;
        z-index: 100;
    }
    @keyframes fadeIn {
        from { opacity: 0; transform: translate(-50%, -45%); }
        to { opacity: 1; transform: translate(-50%, -50%); }
    }

    /* زر التبديل بين الوضعين */
    .mode-switch-btn {
        position: fixed;
        bottom: 65px;  /* تغيير الموضع ليكون في الأسفل */
        right: 25px;
        width: 50px;
        height: 50px;
        border-radius: 50%;
        background-color: rgba(0, 0, 0, 0.6);
        color: white;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 20px;
        cursor: pointer;
        z-index: 9999;
        box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        transition: transform 0.3s ease;
    }
    .mode-switch-btn:hover {
        transform: scale(1.1);
    }

    /* إخفاء العناصر الخاصة بالوضع غير النشط */
    .mode1 .mode2-only,
    .mode2 .mode1-only {
        display: none !important;
    }
`;
document.head.appendChild(style);

// تعريف المتغيرات
const drName = '';

// إنشاء الزر الرئيسي (وضع 1)
const mainBtnMode1 = document.createElement('div');
mainBtnMode1.className = 'dr-main-btn mode1-only';
mainBtnMode1.innerHTML = `<span>${drName}<br></span>`;
document.body.appendChild(mainBtnMode1);

// إنشاء الزر الرئيسي (وضع 2)
const mainBtnMode2 = document.createElement('div');
mainBtnMode2.className = 'dr-main-btn mode2-only';
mainBtnMode2.innerHTML = `<span>${drName}<br></span>`;
document.body.appendChild(mainBtnMode2);

// إنشاء زر التبديل بين الوضعين
const modeSwitchBtn = document.createElement('div');
modeSwitchBtn.className = 'mode-switch-btn';
modeSwitchBtn.textContent = '⇄';
modeSwitchBtn.title = 'تبديل وضع القائمة';
document.body.appendChild(modeSwitchBtn);

// إنشاء القائمة الرئيسية (وضع 1)
const menuMode1 = document.createElement('div');
menuMode1.className = 'dr-menu mode1-only';

// إنشاء القائمة الرئيسية (وضع 2)
const menuMode2 = document.createElement('div');
menuMode2.className = 'dr-menu mode2-only';

// دالة لإنشاء قائمة حسب الوضع
function createMenu(menuElement, isMode1) {
    // ---------------- أدوات الألبوم ----------------
    const albumBtn = document.createElement('button');
    albumBtn.textContent = isMode1 ? '📂 أدوات الألبوم' : '📔 ألبوم';

    const subMenu = document.createElement('div');
    subMenu.className = 'dr-submenu';

    ['cards', 'links', 'juicer', 'TreeRepeat'].forEach(id => {
        const btn = document.createElement('button');
        btn.textContent = {
            cards: '🎴 فتح الكروت',
            links: '🔗 فتح الروابط',
            juicer: '♻️ تكرار للمهمة',
            TreeRepeat: '🌳 تكرار سقاية شجرة'
        }[id];
        btn.onclick = () => showPanel(id);
        subMenu.appendChild(btn);
    });

    albumBtn.onclick = (event) => {
        event.stopPropagation();
        if (isMode1) {
            subMenu.classList.toggle('open');
        } else {
            const isOpen = subMenu.classList.contains('open');
            closeAllSubMenus();
            if (!isOpen) subMenu.classList.add('open');
        }
    };

    menuElement.appendChild(albumBtn);
    menuElement.appendChild(subMenu);

    // ---------------- أدوات هامة ----------------
    const toolsBtn = document.createElement('button');
    toolsBtn.textContent = isMode1 ? '✅ أدوات هامة' : '✅أدوات';

    const toolsSubMenu = document.createElement('div');
    toolsSubMenu.className = 'dr-submenu';

    [
        { id: 'giftClear', label: '🎁 تفريغ الهدايا', action: createGiftClearPanel },
        { id: 'token', label: '🤝 ارسال روابط المهمات', action: createTokenPanel },
        { id: 'giftSender', label: '🎁 إرسال هدية خاصة', action: createGiftSenderPanel },
        { id: 'AdvancedTools', label: '💉 ادوات حقن', action: createAdvancedToolsPanel },
        { id: 'FarmAdventure', label: '🐶 فتح 3 مراحل الموئل', action: () => {} },
        { id: 'rewardLinkFiller', label: '🔗 تفويل يومي', action: createRewardLinkFillerPanel } // ADD THIS LINE

    ].forEach(({ id, label, action }) => {
        const btn = document.createElement('button');
        btn.textContent = label;
        btn.onclick = () => {
            showPanel(id);
            action();
        };
        toolsSubMenu.appendChild(btn);
    });

    toolsBtn.onclick = (event) => {
        event.stopPropagation();
        if (isMode1) {
            toolsSubMenu.classList.toggle('open');
        } else {
            const isOpen = toolsSubMenu.classList.contains('open');
            closeAllSubMenus();
            if (!isOpen) toolsSubMenu.classList.add('open');
        }
    };

    menuElement.appendChild(toolsBtn);
    menuElement.appendChild(toolsSubMenu);

    // ---------------- قسم الجيران ----------------
    const neighborsBtn = document.createElement('button');
    neighborsBtn.textContent = isMode1 ? '👩‍👧‍👦 الجيران' : '👩‍👧‍👦 جيران';

    const neighborsSubMenu = document.createElement('div');
    neighborsSubMenu.className = 'dr-submenu';

    [
        { id: 'neighborHarvest', label: '👨‍🌾 حصاد الجيران', action: createNeighborHarvestPanel },
        { id: 'NeighborWatering', label: '🌱 تسميد وسقاية الجيران', action: createNeighborWateringPanel }
    ].forEach(({ id, label, action }) => {
        const btn = document.createElement('button');
        btn.textContent = label;
        btn.onclick = () => {
            showPanel(id);
            action();
        };
        neighborsSubMenu.appendChild(btn);
    });

    neighborsBtn.onclick = (event) => {
        event.stopPropagation();
        if (isMode1) {
            neighborsSubMenu.classList.toggle('open');
        } else {
            const isOpen = neighborsSubMenu.classList.contains('open');
            closeAllSubMenus();
            if (!isOpen) neighborsSubMenu.classList.add('open');
        }
    };

    menuElement.appendChild(neighborsBtn);
    menuElement.appendChild(neighborsSubMenu);

    // ---------------- أزرار إضافية ----------------
const harvestBtn = document.createElement('button');
harvestBtn.textContent = isMode1 ? '🌾 أدوات الحصاد' : '🪓 حصاد';
harvestBtn.onclick = () => showPanel('harvestTools');

const FarmManagerBtn = document.createElement('button');
FarmManagerBtn.textContent = isMode1 ? '🌾 أدوات الزراعة' : '🍓 زراعة';
FarmManagerBtn.onclick = () => showPanel('FarmManager');

const cloverBtn = document.createElement('button');
cloverBtn.textContent = isMode1 ? '🌿 ز تلقائية وج نقط' : 'ز تلقائية';
cloverBtn.onclick = () => showPanel('clover');

// ترتيب حسب الوضع
menuElement.appendChild(harvestBtn); // ثابت دايمًا

if (isMode1) {
    menuElement.appendChild(FarmManagerBtn); // أدوات الزراعة
    menuElement.appendChild(cloverBtn);      // ز تلقائية
} else {
    menuElement.appendChild(cloverBtn);      // ز تلقائية
    menuElement.appendChild(FarmManagerBtn); // زراعة
}


    return menuElement;
}

// إنشاء القائمتين
createMenu(menuMode1, true);
createMenu(menuMode2, false);

// ---------------- إضافة القوائم للصفحة ----------------
document.body.appendChild(menuMode1);
document.body.appendChild(menuMode2);

// ---------------- فتح/إغلاق القائمة ----------------
function handleMainBtnClick(event) {
    event.stopPropagation();
    if (currentMode === 'mode1') {
        menuMode1.style.display = (menuMode1.style.display === 'flex') ? 'none' : 'flex';
    } else {
        menuMode2.style.display = (menuMode2.style.display === 'flex') ? 'none' : 'flex';
    }
}

mainBtnMode1.onclick = handleMainBtnClick;
mainBtnMode2.onclick = handleMainBtnClick;

// ---------------- دالة إغلاق كل القوائم الفرعية ----------------
function closeAllSubMenus() {
    document.querySelectorAll('.dr-submenu.open').forEach(menu => {
        menu.classList.remove('open');
    });
}

// ---------------- إغلاق القوائم الفرعية عند الضغط خارجها (للنوافذ الفرعية في الوضع الثاني) ----------------
document.addEventListener('click', function (event) {
    // للوضع الثاني فقط: إغلاق القوائم الفرعية عند الضغط داخلها أو خارجها
    if (currentMode === 'mode2') {
        const isSubmenuContent = event.target.closest('.dr-submenu button');
        const isMainBtn = event.target.closest('.dr-main-btn');

        // إذا تم النقر على محتوى القائمة الفرعية أو خارجها
        if (isSubmenuContent || (!event.target.closest('.dr-submenu') && !isMainBtn)) {
            closeAllSubMenus();
        }
    }
});
// ---------------- إنشاء كل النوافذ ----------------
const panels = {
    cards: createCardPanel(),
    links: createLinkPanel(),
    token: createTokenPanel(),
    juicer: createJuicerPanel(),
    FarmAdventure: createFarmPanel(),
    giftClear: createGiftClearPanel(),
    TreeRepeat: createTreeRepeatPanel(),
    clover: createCloverPanel(),
    rewardLinkFiller: createRewardLinkFillerPanel(),
    harvestTools: createHarvestToolsPanel(),
    FarmManager: createFarmManagerPanel(),
    giftSender: createGiftSenderPanel(),
    neighborHarvest: createNeighborHarvestPanel(),
    AdvancedTools: createAdvancedToolsPanel(),
    NeighborWatering: createNeighborWateringPanel()
};

function showPanel(id) {
    Object.values(panels).forEach(panel => panel.style.display = 'none');
    panels[id].style.display = 'flex';
    if (currentMode === 'mode1') {
        menuMode1.style.display = 'none';
    } else {
    }
}

// ---------------- دالة التبديل بين الوضعين ----------------
function toggleMode() {
    const newMode = currentMode === 'mode1' ? 'mode2' : 'mode1';
    localStorage.setItem('menuMode', newMode);

    // عند التبديل إلى الوضع الثاني، أخفي الزر الرئيسي واحفظ الحالة
    if (newMode === 'mode2') {
        mainBtnMode1.style.display = 'none';
        mainBtnMode2.style.display = 'none';
        localStorage.setItem('isMainBtnHidden', 'true');
    } else {
        // عند العودة إلى الوضع الأول، أظهر الزر الرئيسي
        mainBtnMode1.style.display = 'flex';
        localStorage.setItem('isMainBtnHidden', 'false');
    }

    currentMode = newMode;
    document.body.className = currentMode;
    closeAllSubMenus();

    if (currentMode === 'mode1') {
        menuMode2.style.display = 'none';
        menuMode1.style.display = 'none';
    } else {
        menuMode1.style.display = 'none';
        menuMode2.style.display = 'flex';
    }
}
// تعيين الوضع الأولي من localStorage
document.body.className = currentMode;

// تهيئة العناصر حسب الوضع الحالي
if (currentMode === 'mode1') {
    menuMode1.style.display = 'none';
    mainBtnMode1.style.display = 'flex';
    menuMode2.style.display = 'none';
    mainBtnMode2.style.display = 'none';
} else {
    menuMode1.style.display = 'none';
    mainBtnMode1.style.display = 'none';
    menuMode2.style.display = 'none';
    mainBtnMode2.style.display = 'none'; // تأكد من إخفاء الزر الرئيسي دائمًا في الوضع الثاني

    setTimeout(() => {
        if (currentMode === 'mode2') {
            menuMode2.style.display = 'flex';
        }
    }, 17000);
}
// تعيين حدث النقر على زر التبديل
modeSwitchBtn.onclick = toggleMode;
// ========== دالة التفويل اليومي ==========

function createRewardLinkFillerPanel() {
    'use strict';

    // إعدادات Supabase
    const SUPABASE_URL = 'https://rxiqjtpjdraspaqhukew.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InJ4aXFqdHBqZHJhc3BhcWh1a2V3Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTE2MTg2MjMsImV4cCI6MjA2NzE5NDYyM30.apIZMUExVeYp6YFK3O4f7VAaUl1-6rxgFwp2xeqxPEU';
    const SUPABASE_TABLE_NAME = 'reward_links';

    // إعدادات الأداء
    const DELAY_BETWEEN_REQUESTS_MS = 100; // تأخير بسيط بين الطلبات
    const MAX_CONCURRENT_REQUESTS = 1; // طلب واحد في كل مرة

    // تهيئة Supabase
    if (typeof window.supabase === 'undefined') {
        console.error('Supabase غير متاح');
        return null;
    }
    const supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

    // عناصر الواجهة
    let statusElement;
    let startButton;
    let stopButton;
    let signedRequestInput;
    let linkTypeFilterSelect;
    let closeButton;
    let resultsContainer;
    let intervalId = null;
    let currentRequests = 0;
    let totalProcessed = 0;
    let successfulRequests = 0;
    let failedRequests = 0;

    let availableLinks = [];
    let currentLinkIndex = 0;
    const linkTypes = ['الكل', 'سماد خارق', 'دلو سقاية خارق', 'بينجو', 'طاقة', 'أخرى'];
    const linkTypesMap = {
        'الكل': 'All',
        'سماد خارق': 'Super Fertilizer',
        'دلو سقاية خارق': 'Super Watering Can',
        'بينجو': 'Bingo',
        'طاقة': 'Energy',
        'أخرى': 'Other'
    };
    let currentProcessingType = '';
    let results = {};

    // إنشاء واجهة المستخدم
    const panel = document.createElement('div');
    panel.className = 'dr-panel';
    panel.innerHTML = `
        <div style="display: flex; justify-content: space-between; align-items: center;">
            <h3 style="margin: 0; color: black; font-size: 2.5em;">
                🎁 التفويل اليومي
            </h3>
            <div id="closeButton" style="cursor: pointer; font-size: 3em; padding: 0 5px;">✖️</div>
        </div>

        <div style="display: none;">
            <textarea id="signedRequest" rows="1"></textarea>
        </div>

        <select id="linkTypeFilterSelect" style="padding: 8px; border: 1px solid #ddd; border-radius: 4px;">
            ${linkTypes.map(type => `<option value="${type}">${type}</option>`).join('')}
        </select>

        <div style="display: flex; gap: 10px;">
            <button id="startButton" style="flex: 1; padding: 10px; background-color: #4CAF50; color: white; border: none; border-radius: 5px; cursor: pointer;">
                بدء
            </button>
            <button id="stopButton" style="flex: 1; padding: 10px; background-color: #f44336; color: white; border: none; border-radius: 5px; cursor: pointer; display: none;">
                إيقاف
            </button>
        </div>
        <div id="status" style="padding: 8px; background-color: #f5f5f5; border-radius: 5px; text-align: center; font-size: 0.9em;">
            جاهز للبدء
        </div>
        <div id="resultsContainer" style="max-height: 200px; overflow-y: auto; border: 1px solid #eee; border-radius: 4px; padding: 5px;"></div>
        <div style="text-align: center; font-size: 0.8em; color: #777;">
            أحمد خالد
        </div>
    `;
    document.body.appendChild(panel);

    // عناصر التحكم
    statusElement = panel.querySelector('#status');
    startButton = panel.querySelector('#startButton');
    stopButton = panel.querySelector('#stopButton');
    signedRequestInput = panel.querySelector('#signedRequest');
    linkTypeFilterSelect = panel.querySelector('#linkTypeFilterSelect');
    closeButton = panel.querySelector('#closeButton');
    resultsContainer = panel.querySelector('#resultsContainer');

    // إغلاق الواجهة
    closeButton.addEventListener('click', () => {
        panel.style.display = 'none';
    });

    // الكشف التلقائي عن signedRequest
    try {
        const scripts = [...document.scripts];
        const srScript = scripts.find(s => s.textContent.includes('var sr ='));
        if (srScript) {
            const match = srScript.textContent.match(/var\s+sr\s*=\s*"([^"]+)"/);
            if (match?.[1]) {
                signedRequestInput.value = match[1];
                console.log('تم الكشف عن signedRequest تلقائياً');
            }
        }
    } catch (e) {
        console.log('خطأ في الكشف عن signedRequest:', e);
    }

    // تعيين الأحداث
    startButton.addEventListener('click', startFiller);
    stopButton.addEventListener('click', stopFiller);

    // تحديث حالة الواجهة
    function updateStatus(message) {
        statusElement.textContent = message;
        if (message.includes('وصلت')) {
            statusElement.style.color = '#e74c3c';
        } else if (message.includes('نجاح')) {
            statusElement.style.color = '#2e7d32';
        } else {
            statusElement.style.color = '#333';
        }
    }

    // عرض النتائج
    function updateResults() {
        let html = '<div style="font-weight: bold; margin-bottom: 5px;">النتائج:</div>';

        for (const [type, result] of Object.entries(results)) {
            html += `<div style="margin-bottom: 3px;">
                ${type}: ${result.success} نجاح |
                ${result.fail} فشل |
                <span style="color: ${result.limit ? '#e74c3c' : '#2e7d32'}">
                    ${result.limit ? 'وصلت للحد' : 'لم تصل للحد'}
                </span>
            </div>`;
        }

        resultsContainer.innerHTML = html;
    }

    // جلب الروابط من Supabase
    async function fetchLinksFromSupabase(linkType = 'الكل') {
        updateStatus(`جاري جلب روابط ${linkType}`);

        try {
            let query = supabase
                .from(SUPABASE_TABLE_NAME)
                .select('link_url, id, link_type')
                .eq('status', 'new');

            if (linkType !== 'الكل') {
                query = query.eq('link_type', linkTypesMap[linkType]);
            }

            const { data, error } = await query.order('created_at', { ascending: true });

            if (error) throw error;

            if (!data || data.length === 0) {
                updateStatus(`لا توجد روابط ${linkType}`);
                return [];
            }

            return data;

        } catch (error) {
            console.error('خطأ في جلب الروابط:', error);
            updateStatus('خطأ في جلب الروابط');
            return [];
        }
    }

    // حذف الرابط من Supabase
    async function deleteRewardLink(linkId) {
        try {
            await supabase
                .from(SUPABASE_TABLE_NAME)
                .delete()
                .eq('id', linkId);
        } catch (error) {
            console.error('خطأ في حذف الرابط:', error);
        }
    }

    // بدء التعبئة
    async function startFiller() {
        const signedRequest = signedRequestInput.value.trim();
        if (!signedRequest) {
            updateStatus('يجب إدخال signedRequest');
            return;
        }

        startButton.disabled = true;
        stopButton.style.display = 'block';
        totalProcessed = 0;
        successfulRequests = 0;
        failedRequests = 0;
        results = {};

        const selectedType = linkTypeFilterSelect.value;
        const typesToProcess = selectedType === 'الكل' ? linkTypes.filter(t => t !== 'الكل') : [selectedType];

        updateStatus('بدأ التعبئة...');
        resultsContainer.innerHTML = '';

        // معالجة كل نوع على حدة
        for (const type of typesToProcess) {
            currentProcessingType = type;

            // تهيئة نتائج هذا النوع
            results[type] = {
                success: 0,
                fail: 0,
                limit: false
            };

            availableLinks = await fetchLinksFromSupabase(type);
            currentLinkIndex = 0;

            if (availableLinks.length === 0) {
                continue;
            }

            // معالجة روابط هذا النوع
            while (currentLinkIndex < availableLinks.length && !results[type].limit) {
                const currentLink = availableLinks[currentLinkIndex];
                currentLinkIndex++;

                await processSingleRequest(currentLink.link_url, currentLink.id, signedRequest, type);
                updateResults();

                // تأخير بسيط لتجنب حظر الخادم
                await new Promise(resolve => setTimeout(resolve, DELAY_BETWEEN_REQUESTS_MS));
            }

            if (results[type].limit) {
                updateStatus(`وصلت للحد في ${type}`);
            }
        }

        stopFiller();
        updateStatus('تم الانتهاء ');
    }

    // إيقاف التعبئة
    function stopFiller() {
        if (intervalId) {
            clearInterval(intervalId);
            intervalId = null;
        }
        startButton.disabled = false;
        stopButton.style.display = 'none';
    }

    // معالجة طلب واحد
    async function processSingleRequest(linkUrl, linkId, signedRequest, type) {
        try {
            const urlObj = new URL(linkUrl);
            const vk = urlObj.searchParams.get('vk');

            if (!vk) {
                failedRequests++;
                results[type].fail++;
                updateStatus('رابط غير صالح');
                return;
            }

            const postUrl = `https://farm-us.centurygames.com/facebook/gr/?vk=${encodeURIComponent(vk)}`;
            const formData = `fb_locale=ar_AR&signed_request=${encodeURIComponent(signedRequest)}`;

            const reqResult = await new Promise((resolve, reject) => {
                GM_xmlhttpRequest({
                    method: 'POST',
                    url: postUrl,
                    data: formData,
                    headers: {
                        'Content-Type': 'application/x-www-form-urlencoded'
                    },
                    timeout: 3000,
                    onload: resolve,
                    onerror: reject
                });
            });

            const responseText = reqResult.responseText;

            if (responseText.includes('لقد وصلت')) {
                results[type].limit = true;
                updateStatus(`وصلت للحد في ${type}`);
                return;
            }

            if (responseText.includes('لقد قبلتها للتو')) {
                successfulRequests++;
                results[type].success++;
                updateStatus('نجاح');
            } else if (responseText.includes('عفوا') || responseText.includes('حاول في الاعلانات الاخري')) {
                failedRequests++;
                results[type].fail++;
                await deleteRewardLink(linkId);
                updateStatus('تم حذف الرابط');
            } else {
                failedRequests++;
                results[type].fail++;
                updateStatus('فشل في الرابط');
            }

        } catch (error) {
            failedRequests++;
            results[type].fail++;
            updateStatus('حدث خطأ');
        }
    }

    return panel;
}

// ========== دالة الأدوات المتقدمة ==========
function createAdvancedToolsPanel() {
    const panel = document.createElement('div');
    panel.className = 'dr-panel';

    // Prevent panel from opening multiple times
    if (document.getElementById('advancedToolsPanel')) {
        return null;
    }
    panel.id = 'advancedToolsPanel';

    panel.innerHTML = `
        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
            <h3 style="margin: 0; color: #8a2be2; font-size: 16px;">⚙️ أدوات المزرعة المتقدمة</h3>
            <div class="close-btn" style="cursor: pointer; color: white; font-size: 1.2em;">✖️</div>
        </div>

        <div style="max-height: 220px; overflow-y: auto; margin-bottom: 10px;">
            <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px;">
                <div class="mini-tool" data-tool="autoForce" title="التشغيل التلقائي بدون خصم">
                    <div style="font-size: 20px;">⏱️</div>
                    <div style="font-size: 10px;">تلقائي وبنزين بدون خصم</div>
                    <div id="autoForceMiniStatus" style="font-size: 10px; color: #e74c3c;"></div>
                </div>

                <div class="mini-tool" data-tool="fakeAuto" title="تشغيل تلقائي وهمي">
                    <div style="font-size: 20px;">👻</div>
                    <div style="font-size: 10px;">تلقائي وهمي</div>
                    <div id="fakeAutoMiniStatus" style="font-size: 10px; color: #95a5a6;"></div>
                </div>

                <div class="mini-tool" data-tool="alwaysShop" title="المتجر الدائم">
                    <div style="font-size: 20px;">🛒</div>
                    <div style="font-size: 10px;">المتجر مكتمل</div>
                    <div id="alwaysShopMiniStatus" style="font-size: 10px; color: #28a745;"></div>
                </div>

                <div class="mini-tool" data-tool="copyID" title="نسخ ID العناصر">
                    <div style="font-size: 20px;">📋</div>
                    <div style="font-size: 10px;">نسخ ID</div>
                    <div id="copyIDMiniStatus" style="font-size: 10px; color: #6c757d;"></div>
                </div>

                <div class="mini-tool" data-tool="upgradeBuildings" title="ترقية المباني الذكية">
                    <div style="font-size: 20px;">⚙️</div>
                    <div style="font-size: 10px;">ترقية المباني</div>
                    <div id="upgradeBuildingsMiniStatus" style="font-size: 10px; color: #007bff;"></div>
                </div>
<div class="mini-tool" data-tool="fastProduction" title="يتم تشغيل الانتاج السريع للمباني والمعمل والمطبخ ">
    <div style="font-size: 20px;">⚡</div>
    <div style="font-size: 10px;">الإنتاج السريع للمباني</div>
    <div id="fastProductionMiniStatus" style="font-size: 10px; color: #FFD700;"></div>
</div>

                <div class="mini-tool" data-tool="beehouseAuto" title="أتمتة المنحل">
                    <div style="font-size: 20px;">🍯</div>
                    <div style="font-size: 10px;">تلقائي المنحل</div>
                    <div id="beehouseAutoMiniStatus" style="font-size: 10px; color: #ffa500;"></div>
                </div>

                <div class="mini-tool" data-tool="fishAuto" title="أتمتة بركة الصيد">
                    <div style="font-size: 20px;">🎣</div>
                    <div style="font-size: 10px;">بركة الصيد</div>
                    <div id="fishAutoMiniStatus" style="font-size: 10px; color: #ff5722;"></div>
                </div>

                <div class="mini-tool" data-tool="sublistBuildings" title="إضافة جميع المباني للقائمة الجانبية">
                    <div style="font-size: 20px;">🏢</div>
                    <div style="font-size: 10px;">اضافه جميع المباني</div>
                    <div id="sublistBuildingsMiniStatus" style="font-size: 10px; color: #17a2b8;"></div>
                </div>

                <div class="mini-tool" data-tool="miningAdventure" title="كشف المنجم والمنطاد">
                    <div style="font-size: 20px;">⛏️</div>
                    <div style="font-size: 10px;">كشف المنجم</div>
                    <div id="miningAdventureMiniStatus" style="font-size: 10px; color: #9b59b6;"></div>
                </div>

<div class="mini-tool" data-tool="treeSpacing" title="إلغاء المسافات بين الأشجار">
    <div style="font-size: 20px;">🌳</div>
    <div style="font-size: 10px;">إلغاء مسافات الأشجار</div>
    <div id="treeSpacingMiniStatus" style="font-size: 10px; color: #2ecc71;"></div>
</div>

                <div class="mini-tool" data-tool="submarineAdventure" title="إضافة رحلة للغواصة">
                    <div style="font-size: 20px;">🛳️</div>
                    <div style="font-size: 10px;">رحلات الغواصة</div>
                    <div id="submarineAdventureMiniStatus" style="font-size: 10px; color: #3498db;"></div>
                </div>

                <div class="mini-tool" data-tool="skipMuseum" title="تخطي صناديق المتحف">
                    <div style="font-size: 20px;">🏛️</div>
                    <div style="font-size: 10px;">تخطي المتحف</div>
                    <div id="skipMuseumMiniStatus" style="font-size: 10px; color: #e67e22;"></div>
                </div>


    <div class="mini-tool" data-tool="tentTimeBreak" title="كسر وقت الخيمة">
        <div style="font-size: 20px;">⛺</div>
        <div style="font-size: 10px;">كسر وقت الخيمة</div>
        <div id="tentTimeBreakMiniStatus" style="font-size: 10px; color: #FFA500;"></div>
    </div>
                <div class="mini-tool" data-tool="buildComplete" title="إكمال المباني تحت الإنشاء">
                    <div style="font-size: 20px;">🏗️</div>
                    <div style="font-size: 10px;"> إكمال المباني (وهمي)</div>
                    <div id="buildCompleteMiniStatus" style="font-size: 10px; color: #dc3545;"></div>
                </div>

                <div class="mini-tool" data-tool="fullAutomation" title="تشغيل تلقائي لكل العناصر">
                    <div style="font-size: 20px;">🤖</div>
                    <div style="font-size: 10px;">كل العناصر تلقائي </div>
                    <div id="fullAutomationMiniStatus" style="font-size: 10px; color: #1abc9c;"></div>
                </div>
            </div>
        </div>

        <div id="toolDetails" style="background: rgba(255,255,255,0.1); padding: 10px; border-radius: 8px; margin-bottom: 10px; min-height: 80px;">
            <p style="color: white; text-align: center; margin: 20px 0;">اختر أداة لعرض التفاصيل</p>
        </div>

        <div id="toolControls" style="display: none;">
            <button id="toggleToolBtn" style="width:100%; padding:8px; background:#4CAF50; color:white; border:none; border-radius:5px; cursor:pointer; font-size:12px;">تفعيل</button>
            <div id="toolMessage" style="color:white; margin-top:8px; font-size:11px; min-height:15px;"></div>
        </div>

        <div style="text-align:center; color:#aaa; font-size:11px; margin-top:10px;">الإصدار 4.0</div>
    `;

    // إضافة ستايل مخصص
    const style = document.createElement('style');
    style.textContent = `
        .mini-tool {
            background: rgba(255,255,255,0.1);
            padding: 8px;
            border-radius: 6px;
            cursor: pointer;
            text-align: center;
            transition: all 0.2s;
            color: white;
        }
        .mini-tool:hover {
            background: rgba(255,255,255,0.2);
            transform: scale(1.05);
        }
        .mini-tool.selected {
            background: rgba(255,255,255,0.3);
            border: 1px solid #8a2be2;
        }
        #toggleToolBtn:hover {
            opacity: 0.9;
        }
        .close-btn:hover {
            color: #8a2be2 !important;
        }

        /* Scrollbar Styling */
        #advancedToolsPanel div[style*="overflow-y: auto"]::-webkit-scrollbar {
            width: 8px;
        }
        #advancedToolsPanel div[style*="overflow-y: auto"]::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
        }
        #advancedToolsPanel div[style*="overflow-y: auto"]::-webkit-scrollbar-thumb {
            background-color: #8a2be2;
            border-radius: 10px;
            border: 2px solid rgba(255,255,255,0.1);
        }
        #advancedToolsPanel div[style*="overflow-y: auto"]::-webkit-scrollbar-thumb:hover {
            background-color: #a55eea;
        }
    `;
    document.head.appendChild(style);
    // تعريف حالات الأدوات الجديدة
    const toolDetails = {
        autoForce: {
            active: localStorage.getItem("autoForceEnabled") === "on",
            name: "التشغيل التلقائي بدون خصم",
            description: "يمنع الخصم التلقائي ويسمح بالتشغيل التلقائي بعد 3 ثواني من التحميل.",
            icon: "⏱️",
            color: "#e74c3c",
            hasToggle: true,
            persistent: true
        },
        buildComplete: {
            active: localStorage.getItem("autoCompleteBuildings") === "on",
            name: "إكمال المباني تحت الإنشاء",
            description: "يكمل جميع المباني قيد الإنشاء فوراً دون انتظار.",
            icon: "🏗️",
            color: "#dc3545",
            hasToggle: true,
            persistent: true
        },
        alwaysShop: {
            active: localStorage.getItem("alwaysShopEnabled") === "on",
            name: "المتجر الدائم",
            description: "يجعل جميع عناصر المتجر متاحة دائماً بدون قيود زمنية.",
            icon: "🛒",
            color: "#28a745",
            hasToggle: true,
            persistent: true
        },
        upgradeBuildings: {
            active: localStorage.getItem("upgradeBuildingsEnabled") === "on",
            name: "ترقية المباني الذكية",
            description: "يرفع مستوى جميع المباني بما في ذلك المنحل ومصنع السماد.",
            icon: "⚙️",
            color: "#007bff",
            hasToggle: true,
            persistent: true
        },
        copyID: {
            active: localStorage.getItem("copyIDEnabled") === "on",
            name: "نسخ ID العناصر",
            description: "يمكنك نسخ ID أي عنصر من المتجر عند الضغط على زر المعلومات.",
            icon: "📋",
            color: "#6c757d",
            hasToggle: true,
            persistent: true
        },
 tentTimeBreak: {
        active: localStorage.getItem("tentTimeBreakEnabled") === "on",
        name: "كسر وقت الخيمة",
        description: "يتخطى وقت انتظار الخيمة ويجعلها جاهزة فوراً",
        icon: "⛺",
        color: "#FFA500",
        hasToggle: true
 },
        beehouseAuto: {
            active: localStorage.getItem("beehouseAutoEnabled") === "on",
            name: "أتمتة المنحل",
            description: "يجعل المنحل يعمل تلقائياً دون الحاجة للضغط عليه.",
            icon: "🍯",
            color: "#ffa500",
            hasToggle: true,
            persistent: true
        },
        fishAuto: {
            active: localStorage.getItem("fishAutoEnabled") === "on",
            name: "أتمتة بركة الصيد",
            description: "يقوم بعملية صيد السمك تلقائياً كل 5 ثواني.",
            icon: "🎣",
            color: "#ff5722",
            hasToggle: true,
            persistent: true
        },
        sublistBuildings: {
            active: localStorage.getItem('sublist_building_toggle') === 'on',
            name: "إضافة جميع المباني للقائمة الجانبية",
            description: "يعرض جميع المباني المتوفرة في القائمة الجانبية لتسهيل الوصول إليها.",
            icon: "🏢",
            color: "#17a2b8",
            hasToggle: true,
            persistent: true
        },
        miningAdventure: {
            active: localStorage.getItem("miningAdventureEnabled") === "on",
            name: "كشف المنجم والمنطاد",
            description: "يفتح جميع مناطق المنجم والمنطاد (المغامرة) بدون قيود.",
            icon: "⛏️",
            color: "#9b59b6",
            hasToggle: true,
            persistent: true
        },
        submarineAdventure: {
            active: localStorage.getItem("submarineAdventureEnabled") === "on",
            name: "إضافة رحلة للغواصة",
            description: "يضيف رحلات إضافية للغواصة بدون انتظار أو تكلفة.",
            icon: "🛳️",
            color: "#3498db",
            hasToggle: true,
            persistent: true
        },
        skipMuseum: {
            active: localStorage.getItem("skipMuseumEnabled") === "on",
            name: "تخطي صناديق المتحف",
            description: "يتخطى جميع صناديق المتحف مباشرة إلى النتائج بدون لعب.",
            icon: "🏛️",
            color: "#e67e22",
            hasToggle: true,
            persistent: true
        },
treeSpacing: {
    active: localStorage.getItem("treeSpacingEnabled") === "on",
    name: "إلغاء المسافات بين الأشجار",
    description: "إزالة المسافات الإجبارية بين الأشجار للزراعة بكثافة",
    icon: "🌳",
    color: "#2ecc71",
    hasToggle: true,
    persistent: true
},
        fakeAuto: {
            active: localStorage.getItem("fakeAutoEnabled") === "on",
            name: "تشغيل تلقائي وهمي",
            description: "يعرض تشغيل تلقائي وهمي بدون تأثير حقيقي على الخادم.",
            icon: "👻",
            color: "#95a5a6",
            hasToggle: true,
            persistent: true
        },
fastProduction: {
    active: localStorage.getItem("fastProductionEnabled") === "on",
    name: "الإنتاج السريع للمطبخ والمعمل",
    description: "تفعيل الإنتاج السريع واللامحدود في المطبخ والمعمل والمباني بدون انتظار",
    icon: "⚡",
    color: "#FFD700",
    hasToggle: true,
    persistent: true
},
        fullAutomation: {
            active: localStorage.getItem("fullAutomationEnabled") === "on",
            name: "تشغيل تلقائي لكل العناصر",
            description: "يفعل التشغيل التلقائي لجميع العناصر في الخريطة مرة واحدة.",
            icon: "🤖",
            color: "#1abc9c",
            hasToggle: true,
            persistent: true
        }
    };

    // عناصر DOM
    const toolDetailsEl = panel.querySelector('#toolDetails');
    const toolControlsEl = panel.querySelector('#toolControls');
    const toggleToolBtn = panel.querySelector('#toggleToolBtn');
    const toolMessageEl = panel.querySelector('#toolMessage');
    let currentToolId = null;
    // =============================================
    // 1. الغاء المسافات بين الاشجار
    // =============================================
// متغيرات التحكم
let treeSpacingRetryCount = 0;
const maxTreeSpacingRetries = 30;

// تفعيل إلغاء المسافات بين الأشجار
const enableTreeSpacing = () => {
    unsafeWindow._0x38f676 = 'on';
    checkTreeStore();
    toolMessageEl.textContent = "✅ جاري تفعيل إلغاء المسافات بين الأشجار...";
};

// تعطيل إلغاء المسافات بين الأشجار
const disableTreeSpacing = () => {
    unsafeWindow._0x38f676 = 'off';
    toolMessageEl.textContent = "⛔ تم تعطيل إلغاء المسافات بين الأشجار";
};

// التحقق من متجر الأشجار
function checkTreeStore() {
    treeSpacingRetryCount++;

    if (treeSpacingRetryCount > maxTreeSpacingRetries) {
        toolMessageEl.textContent = "❌ فشل تحميل متجر الأشجار";
        return;
    }

    if (typeof unsafeWindow !== 'undefined' &&
        unsafeWindow.Config &&
        unsafeWindow.Config.Store) {

        applyTreeSpacingRemoval();
        return;
    }

    setTimeout(checkTreeStore, 1000);
}

// تطبيق إزالة المسافات
function applyTreeSpacingRemoval() {
    try {
        // تعديل كل أشجار المتجر
        Object.values(unsafeWindow.Config.Store).forEach(item => {
            if (item.type === 'trees') {
                delete item.tree_spacing;
                item.min_distance = 0;
                item.avoid_area = false;
            }
        });

        // تعديل دوال اللعبة
        if (unsafeWindow.GF) {
            unsafeWindow.GF.getTreeMinimumDistance = () => 0;
            unsafeWindow.GF.showTreeDistanceWarning = () => false;
        }

        toolMessageEl.textContent = "✅ تم تفعيل إلغاء المسافات بين الأشجار";
    } catch (e) {
        console.error('خطأ في إزالة مسافات الأشجار:', e);
        toolMessageEl.textContent = "⚠️ حدث خطأ أثناء التفعيل";
    }
}

    // =============================================
    // 1. النتاج السريع للمباني
    // =============================================
const enableFastProduction = () => {
    unsafeWindow._0x1c0175 = 'on';

    // تأكد من وجود kitchen_data قبل التعديل
    if (!unsafeWindow.GF) unsafeWindow.GF = {};
    if (!unsafeWindow.GF.loginModel) unsafeWindow.GF.loginModel = {};
    if (!unsafeWindow.GF.loginModel.AppData) unsafeWindow.GF.loginModel.AppData = {};
    if (!unsafeWindow.GF.loginModel.AppData.kitchen_data) {
        unsafeWindow.GF.loginModel.AppData.kitchen_data = {};
    }

    // تحديث أدوات المطبخ
    const tools = [216487, 216486, 216648, 216649, 216647];
    tools.forEach(tool => {
        unsafeWindow.GF.loginModel.AppData.kitchen_data[tool] = {
            utensil: tool,
            detail: {},
            status: 1
        };
    });

    toolMessageEl.textContent = "✅ تم تفعيل الإنتاج السريع";
};

// تعطيل الإنتاج السريع
const disableFastProduction = () => {
    unsafeWindow._0x1c0175 = 'off';

    // إزالة أدوات المطبخ
    const tools = [216487, 216486, 216648, 216649, 216647];
    tools.forEach(tool => {
        if (unsafeWindow.GF.loginModel.AppData.kitchen_data &&
            unsafeWindow.GF.loginModel.AppData.kitchen_data[tool]) {
            delete unsafeWindow.GF.loginModel.AppData.kitchen_data[tool];
        }
    });

    toolMessageEl.textContent = "⛔ تم تعطيل الإنتاج السريع";
};

    // =============================================
    // 1. نظام التشغيل التلقائي بدون خصم
    // =============================================
let autoForceInterval = null;

const toolDetailsAutoForce = {
  autoForce: {
    active: false,
  },
};

// 1. تعطيل خاصية autoStart بشكل كامل
const blockAutoStart = () => {
    const list = unsafeWindow?.GF?.farmController?.farmObjectList || [];
    list.forEach(obj => {
        if (obj && 'autoStart' in obj) {
            Object.defineProperty(obj, 'autoStart', {
                get: () => false,
                set: () => {},
                configurable: true,
                enumerable: true
            });
            console.log('✅ تم تعطيل autoStart للكائن:', obj.id);
        }
    });
};

// 2. منع تبديل الأتمتة من الواجهة
const blockToggleAutomationPrototype = () => {
    const proto = unsafeWindow?.LoginProxy?.prototype;
    if (!proto || !proto.toggleAutomation) return;

    proto._originalToggleAutomation = proto.toggleAutomation;
    proto.toggleAutomation = function() {
        return false;
    };
};

// 3. تعديل طلبات الأتمتة الواردة من الخادم
const blockOnToggleAutomationHouseC2S = () => {
    const proto = unsafeWindow?.LoginController?.prototype;
    if (!proto || !proto.onToggleAutomationHouseC2S) return;

    proto._original_onToggleAutomationHouseC2S = proto.onToggleAutomationHouseC2S;
    proto.onToggleAutomationHouseC2S = function(house, qidObj, toggleVal) {
        return proto._original_onToggleAutomationHouseC2S.call(this, house, qidObj, false);
    };
};

// 4. تعطيل جميع حالات الأتمتة الحالية
const disableAutomationOnAll = () => {
    const list = unsafeWindow?.GF?.farmController?.farmObjectList || [];
    const proxy = unsafeWindow?.LoginController?.instance?.loginProxy;

    list.forEach(obj => {
        if (obj && (obj.automatic === true || obj.auto === 1)) {
            console.log('🔧 معالجة الكائن:', obj.id, '- automatic:', obj.automatic, '- auto:', obj.auto);

            // تعديل مباشر للخصائص
            obj.automatic = false;
            obj.auto = 0;

            // إرسال طلب تعطيل الأتمتة إذا كان هناك بروكسي
            if (proxy && proxy.toggleAutomationHouse && obj.qidWrapper && obj.sceneId) {
                try {
                    proxy.toggleAutomationHouse(obj, obj.qidWrapper, false);
                } catch (e) {
                    console.warn('⚠️ خطأ في إرسال تعطيل الأتمتة:', e);
                }
            }
        }
    });
};

// 5. تجاوز دالة إرسال الطلبات للخادم
const updateEnqueue = () => {
    const net = unsafeWindow?.NetUtils;
    if (!net) return;

    net._originalEnqueue = net.enqueue;
    net.enqueue = function(path, data = {}) {
        if (toolDetailsAutoForce.autoForce.active) {
            // جميع الحقول المحتملة للأتمتة
            const autoFields = ['automatic', 'auto', 'autoStart', 'isAuto'];
            autoFields.forEach(field => {
                if (field in data) {
                    data[field] = field === 'automatic' ? false : 0;
                }
            });
        }
        return net._originalEnqueue.call(this, path, data);
    };
};

// 6. تجاوز الدوال الأساسية للعبة
const overrideGameFunctions = () => {
    // 1. دالة محسنة لإضافة الوقود مع التحقق والتأكيد
    unsafeWindow.GF?.loginModel?.addTreasure?.(
        unsafeWindow.TreasureType?.Gasoline,
        5000000
    );

    // 2. منع الجمع التلقائي للأسماك
    unsafeWindow.FishController.prototype.autoCollectFish = function () {
        if (toolDetailsAutoForce.autoForce.active) {
            return;
        }
        this.loginModel.isMeetUseOP(1, false) && this['_collectFish'](false);
    };

    // 3. تجاوز متجر التجميل
    unsafeWindow.LoginProxy.prototype.onAddBeautyshop = function (id, sceneid, auto) {
        if (toolDetailsAutoForce.autoForce.active) {
            console.log('💄 تم إجبار أتمتة متجر التجميل على false');
            auto = false;
        }
        const obj = { id, sceneid };
        if (auto) obj.automatic = auto;
        this.addShopStreetParam(obj, unsafeWindow.SpecialMoId.BeautyShop, sceneid);
        this.send(unsafeWindow.HttpConst.ADD_NEWBEAUTYSHOP, obj);
    };

    // 4. تجاوز أتمتة المنازل
    unsafeWindow.LoginProxy.prototype.toggleAutomationHouse = function (house, qidWrapper, autoVal) {
        if (toolDetailsAutoForce.autoForce.active) {
            console.log('🏠 تم إجبار أتمتة المنزل على false لـ:', house?.id);
            autoVal = false;
        }

        if (house instanceof unsafeWindow.BeeHouse) {
            const obj = {
                cur_sceneid: house.sceneId,
                wid: house.wid,
                qid: qidWrapper.qid,
                id: house.id,
                automatic: autoVal
            };
            this.send(unsafeWindow.HttpConst.TOGGLE_AUTOMATION_HOUSE, obj);
        }
    };

    // 5. تجاوز دائرة الجمع
    unsafeWindow.CircleOfCollectsController.prototype.onAutoChange = function (item) {
        if (toolDetailsAutoForce.autoForce.active) {
            item.automatic = 0;
            item.auto = 0;
            return;
        }

        item.automatic = unsafeWindow.Boolean(item.automatic) ? 0 : 1;
        const obj = {
            qid: item.qid,
            wid: item.wid,
            auto: toolDetailsAutoForce.autoForce.active ? 0 : item.automatic
        };
        unsafeWindow.NetUtils.enqueue(
            unsafeWindow.HttpConst.HARVEST_HOUSE_AUTOMATION,
            obj
        );
    };

    // 6. تجاوز زراعة البذور
    unsafeWindow.LoginProxy.prototype._plantSeeds = function (items, type) {
        for (let i = 0; i < items.length; i++) {
            const plant = items[i];
            const obj = {
                unique_id: 10000 + plant.map_unique_id,
                plant_id: plant.id,
                soil_x: plant.grid_x,
                soil_y: plant.grid_y,
                greenhouse_id: 204979,
                greenhouse_x: plant.grid_x - 1,
                greenhouse_y: plant.grid_y - 1,
                // إضافة لمنع الأتمتة
            };
            console.log('🌱 زراعة نبات:', plant.id);
            this.send(unsafeWindow.HttpConst.ADD_PLANT, obj);
        }
    };

    // 7. تجاوز حصاد النباتات
    unsafeWindow.LoginProxy.prototype._harvestPlants = function (items) {
        for (let i = 0; i < items.length; i++) {
            const item = items[i];
            const itemData = unsafeWindow?.Config?.Store_GetItemData(item.id);
            let greenhouseId;
            if (itemData?.type === 'seeds') greenhouseId = 204979;
            if (itemData?.type === 'trees') greenhouseId = 203592;

            const obj = {
                unique_id: item.map_unique_id,
                id: item.id,
                x: item.grid_x,
                y: item.grid_y,
                greenhouse_id: greenhouseId,
                greenhouse_x: item.grid_x - 1,
                greenhouse_y: item.grid_y - 1,
                // إضافة لمنع الأتمتة
            };
            console.log('🔄 حصاد نبات:', item.id);
            this.send(unsafeWindow.HttpConst.COLLECT_MAP_OBJECT, obj);
        }
    };

    // 8. تعطيل مسارات الأتمتة في الخادم
    unsafeWindow.HttpConst.TOGGLE_AUTOMATION = 'disabled_auto_path';
    unsafeWindow.HttpConst.TOGGLE_AUTOMATION_HOUSE = 'disabled_auto_path';
    unsafeWindow.HttpConst.FISH_AUTOMATION = 'disabled_auto_path';
    unsafeWindow.HttpConst.BatchApis.push('disabled_auto_path');

    console.log('✅ تم تجاوز جميع دوال اللعبة بنجاح');
};

// 7. تفعيل النظام
const activateAutoForce = () => {
    toolDetailsAutoForce.autoForce.active = true;
    localStorage.setItem('autoForceEnabled', 'on');

    // 1. تجاوز الدوال الأساسية
    overrideGameFunctions();

    // 2. تعديل نظام إرسال الطلبات
    updateEnqueue();

    // 3. منع تبديل الأتمتة
    blockToggleAutomationPrototype();
    blockOnToggleAutomationHouseC2S();

    // 4. التنفيذ الفوري
    disableAutomationOnAll();
    blockAutoStart();

    // 5. التنفيذ الدوري كل ثانية لمدة 10 ثوان
    clearInterval(autoForceInterval);
    autoForceInterval = setInterval(() => {
        disableAutomationOnAll();
        blockAutoStart();
    }, 1000);

    setTimeout(() => {
        clearInterval(autoForceInterval);
        autoForceInterval = null;
    }, 10000);

    console.log('🚀 تم تفعيل نظام منع الأتمتة بنجاح');
    toolMessageEl.textContent = "✅ تم تفعيل التشغيل التلقائي بدون خصم";
};

// 8. إلغاء التفعيل
const deactivateAutoForce = () => {
    toolDetailsAutoForce.autoForce.active = false;
    localStorage.setItem('autoForceEnabled', 'off');

    if (autoForceInterval) {
        clearInterval(autoForceInterval);
        autoForceInterval = null;
    }

    // استعادة دالة enqueue الأصلية إذا كانت موجودة
    const net = unsafeWindow?.NetUtils;
    if (net && net._originalEnqueue) {
        net.enqueue = net._originalEnqueue;
        delete net._originalEnqueue;
    }

    console.log('🛑 تم إيقاف نظام منع الأتمتة');
    toolMessageEl.textContent = "⛔ تم تعطيل التشغيل التلقائي";
};
// Configuration - set these to 'on' or 'off' as needed
const config = {
    function1: 'on',    // _0x1df984
    function2: 'on',    // _0x178dae
    animalMods: 'on',   // _0x76fc1e
    function3: 'on',    // _0x2d69c2
    blockFlag: false,   // _0x401174
    tentTimeBreak: 'on' // كسر وقت الخيمة
};

// ===== نظام كسر وقت الخيمة المعزول =====
(function() {
    // متغيرات النظام الداخلية
    const tentSystem = {
        isActive: false,
        originalFunctions: {},
        interval: null,

        // البحث الآمن عن كائن الخيمة
        findTentController: function() {
            const tentNames = ['TentController', 'CampController', 'TentSystem', 'TentManager'];
            for (const name of tentNames) {
                if (unsafeWindow[name]) return unsafeWindow[name];
            }

            // البحث العميق إذا لم يوجد بالاسماء الشائعة
            for (const key in unsafeWindow) {
                if (typeof unsafeWindow[key] === 'function' &&
                    /tent|camp/i.test(key) &&
                    unsafeWindow[key].prototype) {
                    return unsafeWindow[key];
                }
            }
            return null;
        },

        // تفعيل النظام
        enable: function() {
            try {
                if (this.isActive) return true;

                const TentController = this.findTentController();
                const TentModel = unsafeWindow.TentModel || unsafeWindow.CampModel;

                // تعديل تحكم الخيمة
                if (TentController) {
                    this.originalFunctions.TentController = {
                        updateStatus: TentController.prototype.updateStatus
                    };

                    TentController.prototype.updateStatus = function() {
                        this.status = 2; // حالة جاهزة
                        if (this.timeText) this.timeText.text = "جاهز الآن";
                        if (this.enterButton) this.enterButton.visible = true;
                    };
                }

                // تعديل نموذج الخيمة
                if (TentModel) {
                    this.originalFunctions.TentModel = {
                        getRemainingTime: TentModel.prototype.getRemainingTime
                    };

                    TentModel.prototype.getRemainingTime = function() {
                        return 0; // لا يوجد وقت انتظار
                    };
                }

                this.isActive = true;
                console.log("[TentSystem] تم تفعيل كسر وقت الخيمة بنجاح");
                unsafeWindow.ConfirmView?.Show("⛺ الخيمة جاهزة الآن!");
                return true;
            } catch (e) {
                console.error("[TentSystem] خطأ في التفعيل:", e);
                return false;
            }
        },

        // تعطيل النظام
        disable: function() {
            try {
                if (!this.isActive) return true;

                const TentController = this.findTentController();
                const TentModel = unsafeWindow.TentModel;

                // استعادة تحكم الخيمة الأصلي
                if (TentController && this.originalFunctions.TentController) {
                    TentController.prototype.updateStatus =
                        this.originalFunctions.TentController.updateStatus;
                }

                // استعادة نموذج الخيمة الأصلي
                if (TentModel && this.originalFunctions.TentModel) {
                    TentModel.prototype.getRemainingTime =
                        this.originalFunctions.TentModel.getRemainingTime;
                }

                this.isActive = false;
                console.log("[TentSystem] تم تعطيل كسر وقت الخيمة");
                unsafeWindow.ConfirmView?.Show("⛺ تم استعادة النظام الأصلي");
                return true;
            } catch (e) {
                console.error("[TentSystem] خطأ في التعطيل:", e);
                return false;
            }
        },

        // نظام إعادة المحاولة التلقائي
        autoEnable: function() {
            if (!this.enable()) {
                this.interval = setInterval(() => {
                    if (this.enable()) {
                        clearInterval(this.interval);
                    }
                }, 2000);
            }
        }
    };

    // تسجيل النظام في النطاق الآمن للوصول إليه لاحقاً
    if (!unsafeWindow._farmTentSystem) {
        unsafeWindow._farmTentSystem = tentSystem;
    }

    // تفعيل تلقائي إذا كان الخيار نشطاً
    if (config.tentTimeBreak === 'on') {
        tentSystem.autoEnable();
    }
})();

// ===== نظام الانتظار والتهيئة =====
const initializeGame = () => {
    const requiredComponents = [
        'AnimalRegCenterController',
        'NetUtils',
        'ConfirmView',
        'GF'
    ];

    if (requiredComponents.every(comp => unsafeWindow[comp])) {
        clearInterval(initInterval);
        executeMainFunctions();
    }
};

const initInterval = setInterval(initializeGame, 500);

// ===== الوظائف الرئيسية الكاملة =====
function executeMainFunctions() {
    // الوظيفة 1
    function _0x3d48df() {
        console.log("تم تنفيذ الوظيفة 1");
        // الكود الأصلي هنا
    }

    // الوظيفة 2
    function _0x4b6af8() {
        console.log("تم تنفيذ الوظيفة 2");
        // الكود الأصلي هنا
    }

    // الوظيفة 3
    async function _0x47e1e9() {
        console.log("تم تنفيذ الوظيفة 3");
        // الكود الأصلي هنا
        return Promise.resolve();
    }

    // نظام تعديلات الحيوانات
    if (config.animalMods === 'on') {
        unsafeWindow.AnimalRegCenterController.prototype.collectLocation = async function(location, amount) {
            try {
                const model = this.model,
                      collection = model.collectLocation(location),
                      requestData = {
                          location: location,
                          rc: -amount
                      },
                      response = await unsafeWindow.NetUtils.request(
                          '/AnimalRegisterCenter/Collect',
                          requestData
                      );

                if (response.status !== 0) {
                    model.updateFinishedRank(collection, response.rank),
                    await new Promise((resolve) => {
                        this.openRewardPanel({
                            key: collection,
                            rank: response.rank,
                            onClose: resolve
                        });
                    }),
                    unsafeWindow.ConfirmView.Show('تم الجمع بنجاح ✓');
                }
            } catch (error) {
                unsafeWindow.ConfirmView.Show('حدث خطأ أثناء الجمع ⚠️');
            }
        };

        unsafeWindow.AnimalRegCenterController.prototype.trySpeedCollectionLocation = async function(index) {
            const model = this.model,
                  locationInfo = model.getLocationInfoByIndex(index),
                  configData = model.config.data[locationInfo.key],
                  timeLeft = unsafeWindow.ServerTime.getTimeLeft(locationInfo.time + 0);

            if (timeLeft >= 0) {
                const speedCost = model.getSpeedRc(timeLeft),
                      shouldCollect = await new Promise((resolve) => {
                          unsafeWindow.ConfirmView.Show(
                              'جمع الآن بدون خصم 🟢',
                              () => resolve(true),
                              this,
                              () => resolve(false)
                          );
                      });

                if (shouldCollect && unsafeWindow.GF.loginModel.isMeetUseRC(-1)) {
                    unsafeWindow.GF.loginModel.costTreasure(
                        unsafeWindow.TreasureType.RC,
                        0
                    ),
                    await this.collectLocation(index, 1);
                }
            }
        };
    }

    // تنفيذ الوظائف حسب الإعدادات
    if (config.function1 === 'on' && !config.blockFlag) _0x3d48df();
    if (config.function2 === 'on' && !config.blockFlag) _0x4b6af8();
    if (config.function3 === 'on') _0x47e1e9().catch(console.error);

    // تأكيد تفعيل الخيمة بعد تحميل اللعبة
    if (config.tentTimeBreak === 'on') {
        setTimeout(() => {
            unsafeWindow._farmTentSystem?.autoEnable();
        }, 3000);
    }
}
    // =============================================
    // 2. نظام إكمال المباني تحت الإنشاء
    // =============================================
    const patchBuildComplete = () => {
        if (unsafeWindow?.NetUtils?.loadAmfUrl && !unsafeWindow.__patchedComplete__) {
            const orig = unsafeWindow.NetUtils.loadAmfUrl;
            unsafeWindow.NetUtils.loadAmfUrl = async function (url, data) {
                const res = await orig.call(this, url, data);
                try {
                    if (toolDetails.buildComplete.active && res?.data?.farm?.map) {
                        let doneCount = 0;
                        Object.values(res.data.farm.map).forEach(obj => {
                            if (obj.under_construction === true) {
                                obj.under_construction = false;
                                doneCount++;
                            }
                        });
                        if (doneCount > 0) {
                            unsafeWindow.ConfirmView?.Show(`✅ تم إكمال ${doneCount} مبنى تلقائياً`);
                        }
                    }
                } catch (e) {
                    console.warn("خطأ في إكمال المباني:", e);
                }
                return res;
            };
            unsafeWindow.__patchedComplete__ = true;
        }
    };

    // =============================================
    // 3. نظام المتجر الدائم
    // =============================================
    const enableAlwaysShop = () => {
        try {
            if (unsafeWindow.ShopModel && unsafeWindow.Config) {
                if (!unsafeWindow.ShopModel.prototype.__originalIsAlwaysOnline) {
                    unsafeWindow.ShopModel.prototype.__originalIsAlwaysOnline = unsafeWindow.ShopModel.prototype.isAlwaysOnline;
                }
                unsafeWindow.ShopModel.prototype.isAlwaysOnline = function (itemId) {
                    return true;
                };
                toolMessageEl.textContent = "✅ تم تفعيل المتجر الدائم";
            }
        } catch (error) {
            console.error('خطأ في تفعيل المتجر الدائم:', error);
            toolMessageEl.textContent = "❌ فشل تفعيل المتجر الدائم";
        }
    };

    const disableAlwaysShop = () => {
        if (unsafeWindow.ShopModel && unsafeWindow.ShopModel.prototype.__originalIsAlwaysOnline) {
            unsafeWindow.ShopModel.prototype.isAlwaysOnline = unsafeWindow.ShopModel.prototype.__originalIsAlwaysOnline;
            toolMessageEl.textContent = "⛔ تم تعطيل المتجر الدائم";
            unsafeWindow.ConfirmView?.Show('⛔ تم تعطيل المتجر الدائم');
        }
    };

    // =============================================
    // 4. نظام ترقية المباني الذكية
    // =============================================
// نظام ترقية المباني المحسن
const upgradeBuildings = () => {
    try {
        // التحقق من تفعيل النظام أولاً
        const isUpgradeActive = localStorage.getItem("upgradeBuildingsEnabled") === "on";
        if (!isUpgradeActive) return;

        const mapData = unsafeWindow?.GF?.loginModel?.AppData?.map;
        if (!mapData) return;

        Object.values(mapData).forEach(building => {
            try {
                const itemData = unsafeWindow.Config?.Store_GetItemData(building.id);
                if (!itemData) return;

                // الحصول على الحد الأقصى للترقية من بيانات العمق
                const depthData = itemData?.depth;
                const maxLevel = depthData ? Object.keys(depthData).length : 0;

                // إذا كان المبنى وصل للحد الأقصى، نتخطاه
                if (maxLevel > 0 && building.upgrade_level >= maxLevel) {
                    return;
                }

                // المباني الخاصة (المنحل ومصنع السماد)
                if (itemData.kind === 'beehouse' || itemData.kind === 'FertilizerMachine') {
                    if (depthData && typeof depthData === 'object') {
                        building.upgrade_level = maxLevel;
                    }
                    return;
                }

                // مباني شارع المتجر (ما عدا ID 205391)
                if (itemData.add_shop_street === 'true' && itemData.id !== 205391) {
                    if (depthData && typeof depthData === 'object') {
                        building.upgrade_level = maxLevel;
                    }
                    return;
                }

                // المباني العادية
                if (building.upgrade_level !== undefined) {
                    // نرفع مستوى واحد فقط إذا لم يصل للحد الأقصى
                    if (maxLevel === 0 || building.upgrade_level < maxLevel) {
                        building.upgrade_level += 1;
                    }
                }
            } catch (err) {
                console.error(`Error upgrading building ${building.id}:`, err);
            }
        });
    } catch (err) {
        console.error("Upgrade system error:", err);
    }
};

// نظام مراقبة التغييرات في الخريطة مع تحسينات
const observeMapChanges = () => {
    let lastMapHash = null;
    let isProcessing = false;
    let upgradeInterval = null;

    const checkMap = () => {
        // التحقق من تفعيل النظام أولاً
        const isUpgradeActive = localStorage.getItem("upgradeBuildingsEnabled") === "on";
        if (!isUpgradeActive) {
            if (upgradeInterval) {
                clearInterval(upgradeInterval);
                upgradeInterval = null;
            }
            return;
        }

        if (isProcessing) return;

        const currentMap = unsafeWindow?.GF?.loginModel?.AppData?.map;
        if (!currentMap) return;

        // إنشاء بصمة فريدة للخريطة الحالية
        const currentHash = Object.keys(currentMap).sort().join(',');

        if (currentHash && currentHash !== lastMapHash) {
            isProcessing = true;
            lastMapHash = currentHash;

            // إلغاء أي عملية ترقية سابقة
            if (upgradeInterval) {
                clearInterval(upgradeInterval);
            }

            // بدء عملية الترقية بعد تأخير قصير
            upgradeInterval = setTimeout(() => {
                try {
                    upgradeBuildings();
                } catch (err) {
                    console.error("Upgrade error:", err);
                } finally {
                    isProcessing = false;
                }
            }, 1500);
        }
    };

    // بدء المراقبة كل ثانيتين
    const observerInterval = setInterval(checkMap, 2000);

    // تنظيف عند إيقاف النظام
    return () => {
        clearInterval(observerInterval);
        if (upgradeInterval) {
            clearInterval(upgradeInterval);
        }
    };
};

// بدء نظام المراقبة
let stopObserving = observeMapChanges();

// نظام التحكم في الترقية من الواجهة
const enableUpgradeBuildings = () => {
    localStorage.setItem("upgradeBuildingsEnabled", "on");
    if (!stopObserving) {
        stopObserving = observeMapChanges();
    }
    toolMessageEl.textContent = "✅ تم تفعيل ترقية المباني الذكية";
};

// ❌ تعطيل ترقية المباني
const disableUpgradeBuildings = () => {
    localStorage.removeItem("upgradeBuildingsEnabled");
    if (stopObserving) {
        stopObserving();
        stopObserving = null;
    }
    toolMessageEl.textContent = "⛔ تم تعطيل ترقية المباني الذكية";
    unsafeWindow.ConfirmView?.Show("⛔ تم تعطيل ترقية المباني");
};

// تهيئة النظام عند تحميل الصفحة

    // =============================================
    // 5. نظام نسخ ID العناصر
    // =============================================
 const enableCopyID = () => {
    if (typeof unsafeWindow !== 'undefined' && unsafeWindow.ShopItem && unsafeWindow.Config) {
        if (!unsafeWindow.ShopItem.prototype._originalOnInfo) {
            unsafeWindow.ShopItem.prototype._originalOnInfo = unsafeWindow.ShopItem.prototype.onInfo;
        }

        unsafeWindow.ShopItem.prototype.onInfo = function () {
            const item = this.itemData;

            if (typeof GM_setClipboard !== 'undefined') {
                GM_setClipboard(item.id.toString(), 'text');
                unsafeWindow.ConfirmView?.Show(`✔️ تم نسخ ID: ${item.id}`);
            } else if (navigator.clipboard && navigator.clipboard.writeText) {
                navigator.clipboard.writeText(item.id.toString())
                    .then(() => {
                        unsafeWindow.ConfirmView?.Show(`✔️ تم نسخ ID: ${item.id}`);
                    })
                    .catch(() => {
                        unsafeWindow.ConfirmView?.Show(`❌ فشل النسخ`);
                    });
                return; // لمنع استمرار تنفيذ باقي الدالة
            } else {
                unsafeWindow.ConfirmView?.Show(`⚠️ النسخ غير مدعوم في هذا المتصفح`);
            }

            // استدعاء الوظيفة الأصلية إذا كانت موجودة
            if (!item.ivshow && this._originalOnInfo) {
                this._originalOnInfo();
            }
        };

        toolMessageEl.textContent = "✅ تم تفعيل نسخ ID المتجر";
    }
};

const disableCopyID = () => {
    if (unsafeWindow.ShopItem && unsafeWindow.ShopItem.prototype._originalOnInfo) {
        unsafeWindow.ShopItem.prototype.onInfo = unsafeWindow.ShopItem.prototype._originalOnInfo;
        delete unsafeWindow.ShopItem.prototype._originalOnInfo;
        toolMessageEl.textContent = "⛔ تم تعطيل نسخ ID المتجر";
        unsafeWindow.ConfirmView?.Show('⛔ تم تعطيل نسخ ID المتجر');
    }
};
    // =============================================
    // 6. نظام أتمتة المنحل
    // =============================================
    const enableBeeAuto = () => {
        if (typeof unsafeWindow !== 'undefined' && unsafeWindow.BeeHouseProduct) {
            if (!unsafeWindow.BeeHouseProduct.prototype._originalUpdate) {
                unsafeWindow.BeeHouseProduct.prototype._originalUpdate = unsafeWindow.BeeHouseProduct.prototype.update;
            }

            unsafeWindow.BeeHouseProduct.prototype.update = function () {
                this.id = this.itemData.id;
                this.wid = this.itemData.wid;
                this['_qid'] = this.itemData.qid;
                this.config = unsafeWindow.Config.Store_GetItemData(this.id);
                this['_productID'] = this.config.product;
                this.collect_in = this.config.collect_in;
                this.start_time = this.itemData.start_time;
                this.productNum = this.itemData.products;
                this.automatic = 1; // تفعيل الأتمتة
                this.working = this.itemData.raw_materials > 0;
                this.lefttime = this.start_time + this.collect_in - unsafeWindow.ServerTime.timestamp;

                if (this.working || this.lefttime > 0) {
                    if (this.lefttime <= 0) {
                        this.onProducted();
                        this.working = false;
                        this.callCheck();
                    } else {
                        this.stopTimer();
                        this.showTimerLeft();
                    }
                } else {
                    this.callNextProduce();
                }
                this.autoCollect();
            };

            toolMessageEl.textContent = "✅ تم تفعيل أتمتة المنحل";
        }
    };

    const disableBeeAuto = () => {
        if (typeof unsafeWindow !== 'undefined' && unsafeWindow.BeeHouseProduct) {
            if (unsafeWindow.BeeHouseProduct.prototype._originalUpdate) {
                unsafeWindow.BeeHouseProduct.prototype.update = unsafeWindow.BeeHouseProduct.prototype._originalUpdate;
                delete unsafeWindow.BeeHouseProduct.prototype._originalUpdate;
            }

            toolMessageEl.textContent = "⛔ تم تعطيل أتمتة المنحل";
            unsafeWindow.ConfirmView?.Show('⛔ تم تعطيل أتمتة المنحل');
        }
    };

    // =============================================
    // 7. أتمتة بركة الصيد
    // =============================================
// المتغيرات العامة
let isAutoFishingOn = false;
let totalFishCaught = 0;
const activeProcesses = new Set();

const enableFishAutomation = () => {
    if (typeof unsafeWindow !== 'undefined' && unsafeWindow.GF && unsafeWindow.GF.loginModel) {
        if (!unsafeWindow.GF.loginModel.AppData?.fish_data) {
            console.log('بيانات السمك غير متوفرة بعد، جاري المحاولة مرة أخرى...');
            setTimeout(enableFishAutomation, 2000);
            return;
        }

        isAutoFishingOn = true;
        totalFishCaught = 0;

        unsafeWindow.GF.loginModel.ServerData.data.fish_data.forEach(fish => {
            fish.cur_use = 1;
        });

        unsafeWindow.GF.loginModel.AppData.fish_data.forEach(fishData => {
            if (fishData.num <= 0) return;

            const processId = Symbol();
            activeProcesses.add(processId);

            (async () => {
                try {
                    const fishConfig = unsafeWindow.Config.Store_GetItemData(fishData.fish_type);

                    while (fishData.num > 0 && isAutoFishingOn) {
                        fishData.num--;
                        totalFishCaught++;
                        fishData.cur_use = 1;

                        unsafeWindow.App.ControllerManager.applyFunc(
                            unsafeWindow.ControllerConst.Login,
                            unsafeWindow.LoginConst.HARVEST_FISH_C2S,
                            fishData.fish_type,
                            0
                        );

                        unsafeWindow.App.ControllerManager.applyFunc(
                            unsafeWindow.ControllerConst.Login,
                            unsafeWindow.LoginConst.ADD_FISH_C2S,
                            fishData.fish_type
                        );

                        if (fishData.rate) {
                            fishData.rate.split(',').forEach(rate => {
                                const itemId = parseInt(rate);
                                unsafeWindow.App.ControllerManager.applyFunc(
                                    unsafeWindow.ControllerConst.Game,
                                    unsafeWindow.GameConst.BARN_NEW_GOODS_TIP,
                                    itemId,
                                    1
                                );
                            });
                        }

                        unsafeWindow.App.ControllerManager.applyFunc(
                            unsafeWindow.ControllerConst.Game,
                            unsafeWindow.GameConst.UPDATE_FISH_STATE
                        );

                        await new Promise(resolve => setTimeout(resolve, fishConfig.collect_in * 1000));
                    }
                } catch (error) {
                    console.error('حدث خطأ أثناء الصيد التلقائي:', error);
                } finally {
                    activeProcesses.delete(processId);
                }
            })();
        });

    } else {
        console.log('لم يتم تحميل كائنات اللعبة بعد، جاري المحاولة مرة أخرى...');
        setTimeout(enableFishAutomation, 2000);
    }
};

const disableFishAutomation = () => {
    isAutoFishingOn = false;
    activeProcesses.clear();
    unsafeWindow.ConfirmView?.Show('⛔ تم إيقاف الأتمتة لبركة الصيد بنجاح');
};

// للتحكم: استدع enableFishAutomation() للبدء و disableFishAutomation() للإيقاف
    // =============================================
    // 8. نظام إضافة جميع المباني للقائمة الجانبية
    // =============================================
    const STORAGE_KEY = 'sublist_building_toggle';

    if (typeof unsafeWindow !== 'undefined' && unsafeWindow.CraftBuildingCenterModel) {
        unsafeWindow._originalGetSubListData = unsafeWindow.CraftBuildingCenterModel.prototype.getSubListData;
    }

    // تعريف المباني المطلوبة
    const buildingsToAdd = [
        { id: 201154, type: 'workshop', url: 'workshopIcon_b' },
        { id: 201467, type: 'dessertshop', url: 'dessertshopIcon_b' },
        { id: 201610, type: 'beautyshop', url: 'beautyshopIcon_b' },
        { id: 205391, type: 'dollshop', url: 'dollshopIcon_b' },
        { id: 203572, type: 'floralartshop', url: 'floralIcon_b' },
        { id: 201398, type: 'kitchen_2', url: 'kitchenIcon_b' },
        { id: 200992, type: 'kitchen_1', url: 'kitchenIcon_b' },
        { id: 208369, type: 'freshman', url: 'refreshmentshopIcon_b' },
        { id: 209390, type: 'sculptureshop', url: 'aquasculptShopIcon_b' },
        { id: 212002, type: 'CandyShop', url: 'candyShopIcon_b' },
        { id: 371080, type: 'animalworkshop', url: 'animalWorkshopIcon_b' },
        { id: 204554, type: 'santashop', url: 'SantaWorkshopIcon_b' },
        { id: 205333, type: 'hobbyshop', url: 'hobbyshopIcon_b' },
        { id: 205322, type: 'closeCraft', url: 'closecraftIcon_b' },
        { id: 206165, type: 'catCraft', url: 'catIcon_b' },
        { id: 203532, type: 'dryingshop', url: 'dryingshopIcon_b' },
        { id: 204184, type: 'watershop', url: 'watershopIcon_b' }
    ];

    // تعديل الوظيفة لإضافة المباني
    function modifySubListData() {
        if (typeof unsafeWindow === 'undefined' || !unsafeWindow.CraftBuildingCenterModel) {
            console.log('جاري الانتظار لتحميل العناصر...');
            setTimeout(modifySubListData, 1000);
            return;
        }

        unsafeWindow.CraftBuildingCenterModel.prototype.getSubListData = function() {
            const originalData = unsafeWindow._originalGetSubListData ?
                unsafeWindow._originalGetSubListData.call(this) :
                [];

            const existingIds = new Set(originalData.map(b => b.id));

            const configData = unsafeWindow.Config.Store_GetItemData(1);
            const baseData = {
                config_data: configData,
                server_data: {},
                grid_x: 0,
                grid_y: 0
            };

            const newBuildings = buildingsToAdd
                .filter(b => !existingIds.has(b.id))
                .map(b => ({
                    id: b.id,
                    enable: true,
                    mapObject: unsafeWindow.ObjectFactory.create(baseData),
                    tips: 'ON',
                    where: 'shopStreet',
                    type: b.type,
                    url: b.url
                }));

            return [...originalData, ...newBuildings];
        };

        console.log('تم تعديل القائمة الجانبية بنجاح');
    }

    const enableSublistBuildings = () => {
        modifySubListData();
        localStorage.setItem(STORAGE_KEY, 'on');
        toolMessageEl.textContent = "✅ تم تفعيل إضافة المباني للقائمة الجانبية";
    };

    const disableSublistBuildings = () => {
        if (typeof unsafeWindow !== 'undefined' && unsafeWindow.CraftBuildingCenterModel && unsafeWindow._originalGetSubListData) {
            unsafeWindow.CraftBuildingCenterModel.prototype.getSubListData = unsafeWindow._originalGetSubListData;
            localStorage.setItem(STORAGE_KEY, 'off');
            toolMessageEl.textContent = "⛔ تم تعطيل إضافة المباني للقائمة الجانبية";
            unsafeWindow.ConfirmView?.Show('⛔ تم تعطيل إضافة المباني للقائمة الجانبية');
        }
    };

    // =============================================
    // 9. نظام كشف المنجم والمنطاد (المغامرة)
    // =============================================
    const enableMiningAdventure = () => {
        try {
            // تعديل وظائف المنجم
            unsafeWindow.DigMiningItem.prototype.showStete = function(_0x4d0a5d) {
                this.greenImg.visible = false;
                this.redImg.visible = false;
                1 == _0x4d0a5d ? (this['_curStateImg'] = this.greenImg) :
                2 == _0x4d0a5d && (this['_curStateImg'] = this.redImg);
                this.canShow = 1;
                this.claimed = 1;
                this.stateShow(1);
                this.showTreasure(1);
            };

            // تعديل وظائف المغامرة (المنطاد)
            unsafeWindow.SkyAdventureItem.prototype.checkIsPreview = function() {
                return unsafeWindow.ServerTime.timestamp;
            };

            unsafeWindow.SkyAdventureItem.prototype.checkCanOpen = function() {
                return true;
            };

            unsafeWindow.SkyAdventureItem.prototype.checkCanExit = function() {
                return true;
            };

            try {
                if (unsafeWindow.GF.skyAdventureModel.data.locked === true) {
                    unsafeWindow.GF.skyAdventureModel.data.locked = false;
                }
            } catch (e) {
                console.log('Sky Adventure unlock error:', e);
            }

            unsafeWindow.LoginProxy.prototype.unlockStageSkyAdventure = function() {
                this.send('/Activity/GetTime', {});
            };

            toolMessageEl.textContent = "✅ تم تفعيل كشف المنجم والمنطاد";
        } catch (error) {
            console.error('خطأ في تفعيل كشف المنجم والمنطاد:', error);
            toolMessageEl.textContent = "❌ فشل تفعيل كشف المنجم والمنطاد";
        }
    };

    const disableMiningAdventure = () => {
        toolMessageEl.textContent = "⛔ تم تعطيل كشف المنجم والمنطاد";
        unsafeWindow.ConfirmView?.Show('⛔ تم تعطيل كشف المنجم والمنطاد');
    };

    // =============================================
    // 10. نظام إضافة رحلة للغواصة
    // =============================================
    const enableSubmarineAdventure = () => {
        try {
            async function _0x20732e() {
                await Object.values(
                    unsafeWindow.GF.loginModel.AppData.submarine.adventure2
                ).forEach(async (adv) => {
                    await unsafeWindow.NetUtils.request('subAdventure.subAdventure', {
                        type: 'collect',
                        npc_id: adv.npcId,
                        sailors: null,
                        sub_id: adv.subId,
                        needResponse: 'subAdventure.subAdventure',
                    });
                });
                let _0x40577c = await new Promise((resolve) => {
                    unsafeWindow.NetUtils.flush(function(response) {
                        resolve(response?.data?.objects_to_update || response?.data || 'rq_error');
                    }, this);
                });
                await unsafeWindow.NetUtils.netManager.loadUrl('SubAdvLoad.SubAdvLoad', {});
            }

            unsafeWindow.SubmarineView.prototype.showNpcChoose = function() {
                _0x20732e();
                this.npcChoose.visible = true;
                this.orderArea.visible = false;
                this.npcChoose.onHideInfo();
            };

            unsafeWindow.SubmarineTimeView.prototype.updateCD = function() {
                this.btnClearCD.label = '   اضافة رحل اصافية مجانا 🟢 ';
            };

            unsafeWindow.SubmarineController.prototype.onOpenReward = async function(_0x3091ed) {
                this.open(this.submarineView);
                this.submarineView.showNpcChoose();
            };

            unsafeWindow.SubmarineTimeView.prototype.onClearCD = function() {
                this.applyFunc(
                    unsafeWindow.SubmarineConst.ADVENTURE_CD_END,
                    this.orderInfo
                );
                this.orderData && this.updateView();
            };

            toolMessageEl.textContent = "✅ تم تفعيل إضافة رحلة للغواصة";
        } catch (error) {
            console.error('خطأ في تفعيل إضافة رحلة للغواصة:', error);
            toolMessageEl.textContent = "❌ فشل تفعيل إضافة رحلة للغواصة";
        }
    };

    const disableSubmarineAdventure = () => {
        toolMessageEl.textContent = "⛔ تم تعطيل إضافة رحلة للغواصة";
        unsafeWindow.ConfirmView?.Show('⛔ تم تعطيل إضافة رحلة للغواصة');
    };

    // =============================================
    // 11. نظام تخطي صناديق المتحف
    // =============================================
    const enableSkipMuseum = () => {
        try {
            unsafeWindow.MuseumModel.prototype.gameStart = function(_0x276351, _0x224638, _0x3621ee) {
                var _0x5ce112 = this,
                    _0x45adc2 = {
                        id: _0x276351.id,
                        hp: _0x224638,
                    };
                let _0x8a414b = { callback: _0x3621ee };
                unsafeWindow.NetUtils.request('Mine/GameStart', _0x45adc2).then(
                    function(_0x1caf5b) {
                        _0x5ce112.onGameStart(_0x1caf5b, _0x8a414b);
                    }
                );
            };

            unsafeWindow.MuseumModel.prototype.onGameStart = function(_0x3ca746, _0x5e303b) {
                var _0x417c03 = this;
                this.data.gameData = _0x3ca746.gameData;
                let _0xfef111 = this.data.gameData.nonce,
                    _0x518306 = unsafeWindow.md5.hex(
                        unsafeWindow.App.Platform.snsID() +
                        _0x3ca746.id +
                        _0xfef111 +
                        '657c61b8'
                    );
                var _0x2cd2d7 = {
                    id: _0x3ca746.id,
                    nonce: _0xfef111,
                    sig: _0x518306,
                };
                unsafeWindow.NetUtils.request('Mine/GameWin', _0x2cd2d7).then(function(_0x28a723) {
                    unsafeWindow.ConfirmView.Show('تم تخطي الصندوق \uD83C\uDF81 \n اعد تحميل الصفحة للحفظ ');
                    _0x417c03.onGameWin(_0x28a723, _0x3ca746);
                });
                _0x5e303b.callback && _0x5e303b.callback();
            };

            unsafeWindow.TreasureIdentifyItem.prototype.updateTime = function() {
                if (this.cdTime > 0) {
                    this.cdTime--;
                    this.count.text = unsafeWindow.App.DateUtils.getFormatBySecond(this.cdTime);
                    var _0x3254e1 = this['_model'].getGameStartCost2(this.itemConfig);
                    this.btnTrade.label = ' \uD83D\uDFE0 تخطي الان ';
                } else {
                    unsafeWindow.App.TimerManager.remove(this.updateTime, this);
                    this.count.text = '';
                    this.btnTrade.label = ' \uD83D\uDFE2 تخطي الان ';
                    this.eIcon.visible = false;
                    var _0x17b7d4 = this['_model'].getMuseumMapId(this.data.id);
                    this.btnTrade.visible = this['_model'].haveMuseumSpace(_0x17b7d4);
                }
            };

            toolMessageEl.textContent = "✅ تم تفعيل تخطي صناديق المتحف";
        } catch (error) {
            console.error('خطأ في تفعيل تخطي صناديق المتحف:', error);
            toolMessageEl.textContent = "❌ فشل تفعيل تخطي صناديق المتحف";
        }
    };

    const disableSkipMuseum = () => {
        toolMessageEl.textContent = "⛔ تم تعطيل تخطي صناديق المتحف";
        unsafeWindow.ConfirmView?.Show('⛔ تم تعطيل تخطي صناديق المتحف');
    };

    // =============================================
    // 12. نظام التشغيل التلقائي علي عناصر الخريطة
    // =============================================
let currentScene = null;
let sceneWatcherInterval = null;

const enableFullAutomation = () => {
    try {
        // تعديل الخاصية لضمان تحديثها دائمًا
        unsafeWindow.MapObject1.prototype.is_under_construction = function() {
            return this.configData.only_upgrade ? false :
                   this.serverData ? this.serverData.under_construction : false;
        };

        // تفعيل التشغيل التلقائي فوراً
        unsafeWindow.App.ControllerManager.applyFunc(
            unsafeWindow.ControllerConst.Game,
            unsafeWindow.GameConst.TURN_ON_ALL_AUTOMATION
        );

        unsafeWindow.App.ControllerManager.applyFunc(
            unsafeWindow.ControllerConst.Game,
            unsafeWindow.GameConst.USE_AUTO_TOOL
        );

        unsafeWindow.App.ControllerManager.applyFunc(
            unsafeWindow.ControllerConst.Game,
            unsafeWindow.GameConst.USE_MULTI_TOOL
        );

        toolMessageEl.textContent = "✅ تم تفعيل التشغيل التلقائي لكل العناصر";

        // بدء مراقبة تغيير الخريطة إذا لم تبدأ بعد
        if (!sceneWatcherInterval) {
            currentScene = unsafeWindow.GF.loginModel.AppData.scene_select;
            sceneWatcherInterval = setInterval(() => {
                const newScene = unsafeWindow.GF.loginModel.AppData.scene_select;
                if (newScene !== currentScene) {
                    currentScene = newScene;
                    console.log("تم تغيير الخريطة إلى:", currentScene);

                    // أعد تفعيل التشغيل التلقائي عند تغيير الخريطة
                    unsafeWindow.App.ControllerManager.applyFunc(
                        unsafeWindow.ControllerConst.Game,
                        unsafeWindow.GameConst.TURN_ON_ALL_AUTOMATION
                    );

                    unsafeWindow.App.ControllerManager.applyFunc(
                        unsafeWindow.ControllerConst.Game,
                        unsafeWindow.GameConst.USE_AUTO_TOOL
                    );

                    unsafeWindow.App.ControllerManager.applyFunc(
                        unsafeWindow.ControllerConst.Game,
                        unsafeWindow.GameConst.USE_MULTI_TOOL
                    );

                    toolMessageEl.textContent = `✅ تم تفعيل التشغيل التلقائي على الخريطة رقم ${currentScene}`;
                }
            }, 30000); // كل 3 ثواني يفحص التغيير
        }
    } catch (error) {
        console.error('خطأ في تفعيل التشغيل التلقائي لكل العناصر:', error);
        toolMessageEl.textContent = "❌ فشل تفعيل التشغيل التلقائي لكل العناصر";
    }
};

const disableFullAutomation = () => {
    try {
        // وقف مراقبة تغيير الخريطة
        if (sceneWatcherInterval) {
            clearInterval(sceneWatcherInterval);
            sceneWatcherInterval = null;
        }

        toolMessageEl.textContent = "⛔ تم تعطيل التشغيل التلقائي لكل العناصر";
    } catch (error) {
        console.error('خطأ في تعطيل التشغيل التلقائي لكل العناصر:', error);
    }
};

const startSceneWatcher = () => {
    if (sceneWatcherInterval) return;

    currentScene = unsafeWindow.GF.loginModel.AppData.scene_select;

    sceneWatcherInterval = setInterval(() => {
        const newScene = unsafeWindow.GF.loginModel.AppData.scene_select;
        if (newScene !== currentScene) {
            currentScene = newScene;
            console.log("تم تغيير الخريطة إلى:", currentScene);
            enableFullAutomation();
        }
    }, 1000); // نخفض التكرار لـ1 ثانية فقط لمراقبة سريعة وفعالة
};

// دالة انتظار تحميل اللعبة
function waitForGameReady(callback) {
    const interval = setInterval(() => {
        if (
            unsafeWindow?.GF?.loginModel?.AppData &&
            unsafeWindow?.GF?.loginModel?.AppData.scene_select !== undefined &&
            unsafeWindow?.App?.ControllerManager
        ) {
            clearInterval(interval);
            callback();
        }
    }, 500);
}

// بعد تحميل اللعبة، نفذ التفعيل والمراقبة



    // =============================================
    // 12. نظام التشغيل التلقائي الوهمي
    // =============================================

let fakeAutoInterval;

const enableFakeAuto = () => {
    try {
        // تعيين القيمة أول مرة
        unsafeWindow.GF.loginModel.AppData.op = 10000000;

        // تكرار التعيين كل ثانية للحفاظ عليها
        fakeAutoInterval = setInterval(() => {
            if (unsafeWindow.GF?.loginModel?.AppData) {
                unsafeWindow.GF.loginModel.AppData.op = 10000000;
            }
        }, 1000); // كل ثانية

        toolMessageEl.textContent = "✅ تم تفعيل التشغيل التلقائي الوهمي";
    } catch (error) {
        console.error('خطأ في تفعيل التشغيل التلقائي الوهمي:', error);
        toolMessageEl.textContent = "❌ فشل تفعيل التشغيل التلقائي الوهمي";
    }
};

const disableFakeAuto = () => {
    if (fakeAutoInterval) {
        clearInterval(fakeAutoInterval);
        fakeAutoInterval = null;
    }

    toolMessageEl.textContent = "⛔ تم تعطيل التشغيل التلقائي الوهمي";
    unsafeWindow.ConfirmView?.Show('⛔ تم تعطيل التشغيل التلقائي الوهمي');
};




    // =============================================
    // نظام تحديث واجهة الأدوات
    // =============================================
    const updateUI = (toolId) => {
        const tool = toolDetails[toolId];

        // تحديث حالة الأيقونة المصغرة
        const statusEl = panel.querySelector(`#${toolId}MiniStatus`);
        if (statusEl) {
            statusEl.textContent = tool.active ? '✅' : '❌';
            statusEl.style.color = tool.active ? '#4CAF50' : tool.color;
        }

        // إزالة التحديد من جميع الأيقونات وإضافته للعنصر المحدد
        panel.querySelectorAll('.mini-tool').forEach(el => {
            el.classList.remove('selected');
        });
        const selectedTool = panel.querySelector(`.mini-tool[data-tool="${toolId}"]`);
        if (selectedTool) selectedTool.classList.add('selected');

        // عرض تفاصيل الأداة
        toolDetailsEl.innerHTML = `
            <h4 style="color:${tool.color}; margin:5px 0; font-size:14px;">${tool.icon} ${tool.name}</h4>
            <p style="color:#ddd; margin:5px 0; font-size:12px;">${tool.description}</p>
            <p style="color:#aaa; font-size:11px; margin:5px 0;">الحالة: ${tool.active ? '<span style="color:#4CAF50">مفعل</span>' : '<span style="color:#f44336">غير مفعل</span>'}</p>
        `;

        // عرض عناصر التحكم
        if (tool.hasToggle) {
            toolControlsEl.style.display = 'block';
            toggleToolBtn.textContent = tool.active ? `تعطيل ${tool.name}` : `تفعيل ${tool.name}`;
            toggleToolBtn.style.backgroundColor = tool.active ? '#f44336' : '#4CAF50';
        } else {
            toolControlsEl.style.display = 'block';
            toggleToolBtn.textContent = `تشغيل ${tool.name}`;
            toggleToolBtn.style.backgroundColor = '#007bff';
        }
    };

    // إضافة مستمعي الأحداث
    panel.querySelectorAll('.mini-tool').forEach(el => {
        el.addEventListener('click', () => {
            currentToolId = el.dataset.tool;
            updateUI(currentToolId);
        });
    });

    toggleToolBtn.addEventListener('click', () => {
        if (!currentToolId) return;

        const tool = toolDetails[currentToolId];
        toolMessageEl.textContent = "جاري المعالجة...";

        if (tool.hasToggle) {
            // تبديل حالة الأداة
            tool.active = !tool.active;
            localStorage.setItem(`${currentToolId}Enabled`, tool.active ? "on" : "off"); // Save state
            if (currentToolId === 'sublistBuildings') {
                localStorage.setItem(STORAGE_KEY, tool.active ? 'on' : 'off');
            }

            if (currentToolId === 'autoForce') {
                if (tool.active) activateAutoForce();
                else deactivateAutoForce();
            } else if (currentToolId === 'buildComplete') {
                if (tool.active) patchBuildComplete();
else if (currentToolId === 'fastProduction') {
    if (tool.active) enableFastProduction();
    else disableFastProduction();
}
}else if (currentToolId === 'upgradeBuildings') {
    if (tool.active) enableUpgradeBuildings();
    else disableUpgradeBuildings();

            } else if (currentToolId === 'alwaysShop') {
                if (tool.active) enableAlwaysShop();
                else disableAlwaysShop();
            } else if (currentToolId === 'copyID') {
                if (tool.active) enableCopyID();
                else disableCopyID();
            } else if (currentToolId === 'beehouseAuto') {
                if (tool.active) enableBeeAuto();
                else disableBeeAuto();
            } else if (currentToolId === 'fishAuto') {
                if (tool.active) enableFishAutomation();
                else disableFishAutomation();
            } else if (currentToolId === 'sublistBuildings') {
                if (tool.active) enableSublistBuildings();
                else disableSublistBuildings();
            } else if (currentToolId === 'miningAdventure') {
                if (tool.active) enableMiningAdventure();
                else disableMiningAdventure();
            } else if (currentToolId === 'submarineAdventure') {
                if (tool.active) enableSubmarineAdventure();
                else disableSubmarineAdventure();
            } else if (currentToolId === 'skipMuseum') {
                if (tool.active) enableSkipMuseum();
                else disableSkipMuseum();
} else if (currentToolId === 'treeSpacing') {
    if (tool.active) enableTreeSpacing();
    else disableTreeSpacing();
            } else if (currentToolId === 'fakeAuto') {
                if (tool.active) enableFakeAuto();
                else disableFakeAuto();
            } else if (currentToolId === 'fullAutomation') {
                if (tool.active) enableFullAutomation();
                else disableFullAutomation();
            }

            toolMessageEl.textContent = tool.active ? "✅ تم التفعيل بنجاح" : "⛔ تم التعطيل بنجاح";
        } else {
            // تشغيل الأداة لمرة واحدة
            if (currentToolId === 'upgradeBuildings') {
                upgradeBuildings();
            }
        }

        updateUI(currentToolId);
    });

    panel.querySelector('.close-btn').addEventListener('click', () => {
        panel.style.display = 'none';
    });

    // تفعيل الأدوات المحفوظة بعد 5 ثواني مع التحقق من تفعيلها مسبقاً
const initAutoTools = () => {
  const toolSettings = {
    autoForce: { activate: activateAutoForce, delay: 3000 },
    buildComplete: { activate: patchBuildComplete, delay: 3000 },
    alwaysShop: { activate: enableAlwaysShop, delay: 3000 },
    copyID: { activate: enableCopyID, delay: 3000 },
    beehouseAuto: { activate: enableBeeAuto, delay: 10000 },
    fishAuto: { activate: enableFishAutomation, delay: 3000 },
fastProduction: { activate: enableFastProduction, delay: 3000 },
    sublistBuildings: { activate: enableSublistBuildings, delay: 3000 },
    miningAdventure: { activate: enableMiningAdventure, delay: 10000 },
treeSpacing: { activate: enableTreeSpacing, delay: 2000 },
    submarineAdventure: { activate: enableSubmarineAdventure, delay: 10000 },
    skipMuseum: { activate: enableSkipMuseum, delay: 10000 },
    fakeAuto: { activate: enableFakeAuto, delay: 10000 },
    fullAutomation: { activate: enableFullAutomation, delay: 10000 }
  };

  const isGameReady = () => {
    try {
      return !!unsafeWindow?.GF?.loginModel?.AppData?.map;
    } catch {
      return false;
    }
  };

  const activateSavedTools = () => {
    Object.entries(toolSettings).forEach(([toolName, setting]) => {
      if (localStorage.getItem(`${toolName}Enabled`) === "on") {
        setTimeout(() => {
          console.log(`تفعيل ${toolName}`);
          toolDetails[toolName].active = true;
          setting.activate();
        }, setting.delay);
      }
    });
  };

  if (isGameReady()) {
    activateSavedTools();
  } else {
    const readyCheck = setInterval(() => {
      if (isGameReady()) {
        clearInterval(readyCheck);
        activateSavedTools();
      }
    }, 1000);
  }
};

// بدء التشغيل بعد تحميل الصفحة
setTimeout(initAutoTools, 3000);
// إضافة اللوحة إلى الجسم
document.body.appendChild(panel);

return panel;
}
function createNeighborHarvestPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    div.innerHTML = `
        <h3 style="margin-top:0; color:#4CAF50;">👨‍🌾 حصاد الجيران</h3>
        <div style="color:white;margin-bottom:15px;" id="panelInfoText">
            جاري تحميل بيانات الجيران...
        </div>
        <select id="harvestType" style="width:100%;padding:8px;margin-bottom:10px;border-radius:4px;border:none;background-color:#34495e;color:white;">
            <option value="seeds">حصاد الثمار</option>
            <option value="trees">حصاد الأشجار</option>
            <option value="buildings">حصاد المباني</option>
        </select>
        <div style="position: relative; margin-bottom: 10px;">
            <input type="text" id="itemId" placeholder="كود العنصر (ID) أو الاسم" style="width:100%;padding:8px;border-radius:4px;border:none;background-color:#34495e;color:white;">
            <div id="customSuggestions" style="position: absolute; width: 100%; max-height: 150px; overflow-y: auto; background-color: #2c3e50; border: 1px solid #4CAF50; border-radius: 4px; z-index: 1000; display: none;">
            </div>
        </div>
        <input type="number" id="neighborsCount" placeholder="عدد الجيران المراد حصادهم" style="width:100%;padding:8px;margin-bottom:10px;border-radius:4px;border:none;background-color:#34495e;color:white;">
        <div style="color:white;margin-bottom:10px;" id="itemHarvestCounterInPanel">
            عدد مرات حصاد العنصر الحالي: 0
        </div>
        <div style="display: flex; gap: 10px; margin-bottom: 10px;">
            <button id="runNeighborHarvest" style="flex: 1; padding:10px;background-color:#4CAF50;color:white;border:none;border-radius:5px;cursor:pointer;font-size:1em;font-weight:bold;">🚀 بدء الحصاد</button>
            <button id="stopNeighborHarvest" style="flex: 1; padding:10px;background-color:#e74c3c;color:white;border:none;border-radius:5px;cursor:pointer;font-size:1em;font-weight:bold; display: none;">🛑 إيقاف الحصاد</button>
        </div>
        <div id="neighborHarvestStatus" style="color:white;margin-top:10px;min-height:20px;"></div>
        <div class="close-btn" style="position: absolute; top: 10px; right: 10px; cursor: pointer; color: white; font-size: 1.5em;">✖️</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
        <div style="text-align:center;color:white;font-size:12px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
    `;

    let harvestCounts = { s: 0, t: 0, b: 0 };
    let lastHarvestDate = '';
    let isHarvesting = false;
    let currentItemHarvestCount = 0;
    let totalNeighborsProcessed = 0;
    let processedNeighborsUIDsHarvest = new Set(
    JSON.parse(localStorage.getItem('megaScript_harvestedNeighbors') || '[]')
);

    let plantList = [];
    let treeList = [];
    let activeSuggestionList = [];

    // --- بداية كود العداد الشفاف العائم للحصاد ---
    const floatingCounterHarvest = document.createElement('div');
    floatingCounterHarvest.id = 'dr-floating-counter-harvest';
    floatingCounterHarvest.style.cssText = `
        position: fixed;
        top: 10px;
        left: 50%;
        transform: translateX(-50%);
        background-color: rgba(0, 0, 0, 0.7);
        color: white;
        padding: 10px 15px;
        border-radius: 8px;
        font-size: 1.1em;
        font-weight: bold;
        z-index: 99999;
        display: none;
        border: 1px solid #4CAF50;
        text-align: center;
        box-shadow: 0 4px 8px rgba(0,0,0,0.3);
        flex-direction: column;
        gap: 8px;
        align-items: center;
    `;
    floatingCounterHarvest.innerHTML = `
        <div id="floatingProcessedCountHarvest">تم الدخول إلى: 0 جار</div>
        <div id="floatingItemCountHarvest">العنصر الحالي: 0</div>
        <button id="floatingStopBtnHarvest" style="padding: 8px 15px; background-color: #e74c3c; color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 0.9em; font-weight: bold;">🛑 إيقاف</button>
    `;
    document.body.appendChild(floatingCounterHarvest);

    const updateFloatingCounterHarvest = () => {
        if (floatingCounterHarvest) {
            floatingCounterHarvest.querySelector('#floatingProcessedCountHarvest').textContent = `تم الدخول إلى: ${totalNeighborsProcessed} جار`;
            floatingCounterHarvest.querySelector('#floatingItemCountHarvest').textContent = `العنصر الحالي: ${currentItemHarvestCount}`;
        }
    };
    floatingCounterHarvest.querySelector('#floatingStopBtnHarvest').onclick = () => {
        stopHarvestProcess();
    };
    // --- نهاية كود العداد الشفاف العائم للحصاد ---

    function populateCustomSuggestions(listToSuggest, searchTerm = '') {
        const customSuggestionsDiv = div.querySelector('#customSuggestions');
        customSuggestionsDiv.innerHTML = '';

        if (searchTerm.length === 0 || !listToSuggest || listToSuggest.length === 0) {
            customSuggestionsDiv.style.display = 'none';
            return;
        }

        const lowerCaseSearchTerm = searchTerm.toLowerCase();

        const filteredList = listToSuggest.filter(item =>
            item.name.toLowerCase().includes(lowerCaseSearchTerm) ||
            item.id.toString().includes(lowerCaseSearchTerm)
        );

        filteredList.slice(0, 10).forEach(item => {
            const suggestionItem = document.createElement('div');
            suggestionItem.className = 'suggestion-item';
            suggestionItem.style.cssText = `
                padding: 8px;
                cursor: pointer;
                border-bottom: 1px solid #34495e;
                color: white;
                white-space: nowrap;
                overflow: hidden;
                text-overflow: ellipsis;
            `;
            suggestionItem.textContent = `${item.name} (ID: ${item.id})`;
            suggestionItem.setAttribute('data-id', item.id);

            suggestionItem.addEventListener('click', () => {
                itemIdInput.value = `${item.name} (ID: ${item.id})`;
                customSuggestionsDiv.style.display = 'none';
                currentItemHarvestCount = 0;
                updateItemHarvestCounterInPanel();
                updateFloatingCounterHarvest();
            });

            suggestionItem.addEventListener('mouseenter', () => {
                suggestionItem.style.backgroundColor = '#4CAF50';
            });
            suggestionItem.addEventListener('mouseleave', () => {
                suggestionItem.style.backgroundColor = 'transparent';
            });

            customSuggestionsDiv.appendChild(suggestionItem);
        });

        if (filteredList.length > 0) {
            customSuggestionsDiv.style.display = 'block';
        } else {
            customSuggestionsDiv.style.display = 'none';
        }
    }

let lastLoadedPlantsCount = 0;
let lastLoadedTreesCount = 0;

   function loadPlantsAndTrees() {
    if (unsafeWindow.Config?.Store) {
        plantList = Object.values(unsafeWindow.Config.Store)
            .filter(item => item.type === 'seeds')
            .map(item => ({
                id: item.id,
                name: item.name,
                growTime: item.collect_in
            }));

        treeList = Object.values(unsafeWindow.Config.Store)
            .filter(item => item.type === 'trees')
            .map(item => ({
                id: item.id,
                name: item.name,
                growTime: item.collect_in
            }));

        // ✅ اطبع فقط لو حصل تغيير في الأعداد
        if (plantList.length !== lastLoadedPlantsCount) {
            console.log(`✅ تم تحميل ${plantList.length} نبات من المتجر.`);
            lastLoadedPlantsCount = plantList.length;
        }

        if (treeList.length !== lastLoadedTreesCount) {
            console.log(`✅ تم تحميل ${treeList.length} شجرة من المتجر.`);
            lastLoadedTreesCount = treeList.length;
        }

            const harvestType = div.querySelector('#harvestType').value;
            if (harvestType === 'seeds') {
                activeSuggestionList = plantList;
            } else if (harvestType === 'trees') {
                activeSuggestionList = treeList;
            } else {
                activeSuggestionList = [];
            }

        } else {
            console.warn("❌ لم يتم تحميل بيانات المتجر بعد. تأكد من فتح اللعبة.");
        }
    }

    const resetDailyCounts = () => {
        const today = new Date().toDateString();
        if (lastHarvestDate !== today) {
            harvestCounts = { s: 0, t: 0, b: 0 };
            lastHarvestDate = today;
            saveHarvestCounts();
            console.log("تم تصفير العدادات اليومية بنجاح.");
        }
    };

    const loadHarvestCounts = () => {
        const savedCounts = localStorage.getItem('harvestCounts');
        const savedDate = localStorage.getItem('lastHarvestDate');

        if (savedCounts) {
            harvestCounts = JSON.parse(savedCounts);
        }
        if (savedDate) {
            lastHarvestDate = savedDate;
        }

        resetDailyCounts();
    };

    const saveHarvestCounts = () => {
        localStorage.setItem('harvestCounts', JSON.stringify(harvestCounts));
        localStorage.setItem('lastHarvestDate', new Date().toDateString());
    };

    const getHarvestLimit = () => {
        if (typeof unsafeWindow !== 'undefined' && unsafeWindow.GF && unsafeWindow.GF.loginModel && unsafeWindow.GF.loginModel.AppData) {
            const vipLevel = unsafeWindow.GF.loginModel.AppData.vip_level;
            if (!vipLevel || vipLevel < 3) return 5;
            if (vipLevel < 5) return 6;
            if (vipLevel < 9) return 7;
            if (vipLevel < 12) return 8;
            if (vipLevel < 16) return 9;
            return 10;
        }
        return 5;
    };

    const getRawNeighbors = () => {
        if (typeof unsafeWindow !== 'undefined' && unsafeWindow.GF && unsafeWindow.GF.friendsController && unsafeWindow.GF.friendsController.model && unsafeWindow.GF.friendsController.model.backendFriendsData && unsafeWindow.GF.friendsController.model.backendFriendsData.neighbors) {
            return unsafeWindow.GF.friendsController.model.backendFriendsData.neighbors;
        }
        return [];
    };

    const getDisplayableReadyNeighbors = () => {
        const harvestLimit = getHarvestLimit();
        const allNeighbors = getRawNeighbors();
        return allNeighbors
            .filter(neighbor =>
                neighbor.fertilizer_times < harvestLimit &&
                !processedNeighborsUIDsHarvest.has(neighbor.uid)
            )
            .reverse();
    };

    const updatePanelInfo = () => {
        const infoTextElement = div.querySelector('#panelInfoText');
        if (infoTextElement) {
            const readyNeighborsCount = getDisplayableReadyNeighbors().length;
            infoTextElement.innerHTML = `
                هذه الأداة تسمح بحصاد الثمار والأشجار والمباني من جيران المزرعة دفعة واحدة<br>
                <strong>عدد الجيران الجاهزين المتاحين حاليًا:</strong> ${readyNeighborsCount}<br>
                <strong>حصادات اليوم:</strong><br>
                - ثمار: ${harvestCounts.s}/155<br>
                - أشجار: ${harvestCounts.t}/155<br>
                - مباني: ${harvestCounts.b}/155
            `;
            const neighborsInput = div.querySelector('#neighborsCount');
            if (neighborsInput) {
                neighborsInput.max = readyNeighborsCount;
                neighborsInput.placeholder = `عدد الجيران (1-${readyNeighborsCount})`;
            }
        }
        updateItemHarvestCounterInPanel();
        updateFloatingCounterHarvest();
    };

    const updateItemHarvestCounterInPanel = () => {
        const itemHarvestCounterEl = div.querySelector('#itemHarvestCounterInPanel');
        if (itemHarvestCounterEl) {
            itemHarvestCounterEl.textContent = `عدد مرات حصاد العنصر الحالي: ${currentItemHarvestCount}`;
        }
    };

    async function _0x52577c(requests, sceneId) {
        if (!unsafeWindow.NetUtils || !unsafeWindow.NetUtils.enqueue || !unsafeWindow.NetUtils.flush) {
            console.error("NetUtils أو دوالها غير متاحة في unsafeWindow.");
            return 'rq_error';
        }

        for (const request of requests) {
            if (!isHarvesting) {
                console.log("Harvest process stopped during enqueue.");
                return 'rq_stopped';
            }
            unsafeWindow.NetUtils.enqueue(request.method, request.data, true); // استخدام true لإرسال الطلب فورًا
        }

        return new Promise((resolve) => {
            // حذف التأخير هنا لزيادة السرعة
            // setTimeout(() => {
                if (!isHarvesting) {
                    console.log("Harvest process stopped before flush.");
                    resolve('rq_stopped');
                    return;
                }
                unsafeWindow.NetUtils.flush(function (response) {
                    if (!isHarvesting) {
                        console.log("Harvest process stopped after flush received (but before processing).");
                        resolve('rq_stopped');
                        return;
                    }
                    if (response && response.data && response.data.objects_to_update) {
                        return resolve(response.data.objects_to_update);
                    } else if (response && response.data) {
                        return resolve(response.data);
                    } else if (response) {
                        return resolve(response);
                    }
                    return resolve('rq_error');
                }, this);
            // }, 50); // حذف التأخير هنا
        });
    }

    const performBulkHarvest = async (method, itemId, neighborsToHarvest, typeKey) => {
        const selfName = unsafeWindow.GF.friendsController.model['_self']?.name ?? 'Admin';
        let totalHarvestedItemsInBatch = 0;
        const harvestLimit = getHarvestLimit();
        const statusEl = div.querySelector('#neighborHarvestStatus');

        for (let i = 0; i < neighborsToHarvest.length; i++) {
            if (!isHarvesting) {
                if (statusEl) statusEl.textContent = `تم إيقاف الحصاد يدوياً بعد معالجة ${totalNeighborsProcessed} جار.`;
                return -1; // إرجاع قيمة تدل على التوقف
            }

            const neighbor = neighborsToHarvest[i];

            const liveNeighborData = getRawNeighbors().find(n => n.uid === neighbor.uid);

            if (!liveNeighborData || liveNeighborData.fertilizer_times >= harvestLimit || processedNeighborsUIDsHarvest.has(liveNeighborData.uid)) {
                console.log(`الجار ${neighbor.name || neighbor.uid} لم يعد جاهزًا للحصاد أو تم حصاده بالفعل في هذه الجلسة، تخطي.`);
                processedNeighborsUIDsHarvest.add(neighbor.uid);
localStorage.setItem('megaScript_harvestedNeighbors', JSON.stringify([...processedNeighborsUIDsHarvest]));
                totalNeighborsProcessed++;
                updatePanelInfo();
                continue;
            }

            const remainingForNeighbor = harvestLimit - liveNeighborData.fertilizer_times;
            const requestsAllowedForNeighbor = remainingForNeighbor;

            if (requestsAllowedForNeighbor <= 0) {
                processedNeighborsUIDsHarvest.add(neighbor.uid);
                totalNeighborsProcessed++;
                updatePanelInfo();
                continue;
            }

            // **تعديل:** إزالة اسم الجار من الرسالة
            if (statusEl) {
                statusEl.textContent = `جاري حصاد ${requestsAllowedForNeighbor} مرة من الجار رقم (${totalNeighborsProcessed + 1} / ${neighborsToHarvest.length})...`;
            } else {
                console.log(`جارٍ حصاد ${requestsAllowedForNeighbor} مرة من الجار رقم (${totalNeighborsProcessed + 1})...`);
            }

            const itemData = unsafeWindow.Config?.Store_GetItemData ? unsafeWindow.Config.Store_GetItemData(itemId) : null;

            if (itemData) {
                if (itemData.type === 'buildings') {
                    if (!itemData.neighbor_collectable) {
                        if (statusEl) statusEl.textContent = 'هذا المبنى لا يمكن جمعه من الجيران';
                        continue;
                    }
                }
            } else {
                if (statusEl) statusEl.textContent = 'معرف العنصر غير صالح أو نوع العنصر غير معروف.';
                continue;
            }

            const singleRequestData = {
                method: method.split('.')[0],
                data: {
                    friend_id: neighbor.uid,
                    friendName: selfName,
                    itemid: itemId,
                    cur_sceneid: 0,
                    needResponse: method
                }
            };

            const requests = Array(requestsAllowedForNeighbor).fill(singleRequestData);

            let response;
            try {
                response = await _0x52577c(requests, 0);
                if (response === 'rq_stopped') {
                    return -1;
                }

                if (response && !response.includes('rq_error')) {
                    const updates = Array.isArray(response) ? response : [response];

                    let successfulHarvestsInBatch = 0;
                    for (const update of updates) {
                        const receivedProductId = update?.needResponse?.data?.product || update?.product_id;
                        if (receivedProductId) {
                            totalHarvestedItemsInBatch++;
                            successfulHarvestsInBatch++;
                            currentItemHarvestCount++;

                            if (unsafeWindow.GF?.loginModel?.addStorageOrDryMachine) {
                                unsafeWindow.GF.loginModel.addStorageOrDryMachine(
                                    receivedProductId,
                                    1,
                                    unsafeWindow.dry?.TipsType.BarnNewGoods || 0
                                );
                            }
                            harvestCounts[typeKey]++;
                        }
                    }
                    if (successfulHarvestsInBatch > 0) {
                        if (unsafeWindow.GF && unsafeWindow.GF.friendsController && unsafeWindow.GF.friendsController.model && unsafeWindow.GF.friendsController.model.backendFriendsData) {
                             const updatedNeighborInGameModel = unsafeWindow.GF.friendsController.model.backendFriendsData.neighbors.find(n => n.uid === neighbor.uid);
                             if (updatedNeighborInGameModel) {
                                 updatedNeighborInGameModel.fertilizer_times += successfulHarvestsInBatch;
                                 if (updatedNeighborInGameModel.fertilizer_times >= harvestLimit) {
                                    processedNeighborsUIDsHarvest.add(updatedNeighborInGameModel.uid);
localStorage.setItem('megaScript_harvestedNeighbors', JSON.stringify([...processedNeighborsUIDsHarvest]));
                                    console.log(`تم إضافة الجار ${updatedNeighborInGameModel.name || updatedNeighborInGameModel.uid} إلى قائمة المحصودين في الجلسة.`);
                                 }
                             }
                        }
                    }
                } else {
                    console.warn(`فشل الحصاد من الجار رقم (${totalNeighborsProcessed + 1}). الاستجابة:`, response);
                }
            } catch (error) {
                console.error('حدث خطأ أثناء الحصاد:', error);
                if (statusEl) statusEl.textContent = 'حدث خطأ أثناء الحصاد لهذا الجار.';
            }

            processedNeighborsUIDsHarvest.add(neighbor.uid);
            totalNeighborsProcessed++;
            saveHarvestCounts();
            updatePanelInfo();
            updateItemHarvestCounterInPanel();
            updateFloatingCounterHarvest();

            if (!isHarvesting) {
                if (statusEl) statusEl.textContent = `تم إيقاف الحصاد يدوياً بعد معالجة ${totalNeighborsProcessed} جار.`;
                break;
            }
            // **تعديل:** حذف التأخير هنا لزيادة السرعة
            // await new Promise(resolve => setTimeout(resolve, 200));
        }
        return totalHarvestedItemsInBatch;
    };

    const harvestSeeds = async (itemId, neighborsToHarvest) => {
        return performBulkHarvest('friend_collect.save_data', itemId, neighborsToHarvest, 's');
    };

    const harvestTrees = async (itemId, neighborsToHarvest) => {
        return performBulkHarvest('friend_collect_trees.save_data', itemId, neighborsToHarvest, 't');
    };

    const harvestBuildings = async (itemId, neighborsToHarvest) => {
        return performBulkHarvest('friend_collect_saltpond.save_data', itemId, neighborsToHarvest, 'b');
    };

    const runBtn = div.querySelector('#runNeighborHarvest');
    const stopBtn = div.querySelector('#stopNeighborHarvest');
    const statusEl = div.querySelector('#neighborHarvestStatus');
    const itemIdInput = div.querySelector('#itemId');
    const harvestTypeSelect = div.querySelector('#harvestType');
    const customSuggestionsDiv = div.querySelector('#customSuggestions');
    const neighborsCountInput = div.querySelector('#neighborsCount');

    // دالة مساعدة لإيقاف العملية
    const stopHarvestProcess = () => {
        isHarvesting = false;
        statusEl.textContent = 'جاري إيقاف الحصاد، انتظر قليلاً...';
        stopBtn.disabled = true;
        runBtn.disabled = false;
        runBtn.textContent = '🚀 بدء الحصاد';
        stopBtn.style.display = 'none';
        floatingCounterHarvest.style.display = 'none';
        neighborsCountInput.value = '';
        updatePanelInfo();
    };


    runBtn.onclick = async () => {
div.style.display = 'none';
        isHarvesting = true;
        runBtn.disabled = true;
        stopBtn.style.display = 'inline-block';
        stopBtn.disabled = false;
        runBtn.textContent = 'جارٍ الحصاد...';
        statusEl.textContent = 'بدء عملية الحصاد...';

        currentItemHarvestCount = 0;
        totalNeighborsProcessed = 0;
        updateItemHarvestCounterInPanel();
        updateFloatingCounterHarvest();
        floatingCounterHarvest.style.display = 'flex';

        const harvestType = harvestTypeSelect.value;
        let itemId = itemIdInput.value.trim();

        let foundItem = activeSuggestionList.find(item =>
            item.id.toString() === itemId ||
            `${item.name} (ID: ${item.id})` === itemId
        );

        if (foundItem) {
            itemId = parseInt(foundItem.id);
        } else {
            const idMatch = itemId.match(/\(ID:\s*(\d+)\)/);
            if (idMatch) {
                itemId = parseInt(idMatch[1]);
            } else {
                itemId = parseInt(itemId);
            }
        }

        if (isNaN(itemId) || itemId <= 0) {
            statusEl.textContent = 'الرجاء إدخال كود عنصر صحيح أو اختيار من الاقتراحات.';
            stopHarvestProcess();
            return;
        }

        const neighborsAvailableForHarvest = getDisplayableReadyNeighbors();
        const neighborsCount = parseInt(neighborsCountInput.value);

        if (isNaN(neighborsCount) || neighborsCount <= 0 || neighborsCount > neighborsAvailableForHarvest.length) {
            statusEl.textContent = `الرجاء إدخال عدد جيران صحيح بين 1 و ${neighborsAvailableForHarvest.length}`;
            stopHarvestProcess();
            return;
        }

        const neighborsToHarvestInThisBatch = neighborsAvailableForHarvest.slice(0, neighborsCount);
        let result = 0;

        try {
            switch (harvestType) {
                case 'seeds':
                    result = await harvestSeeds(itemId, neighborsToHarvestInThisBatch);
                    break;
                case 'trees':
                    result = await harvestTrees(itemId, neighborsToHarvestInThisBatch);
                    break;
                case 'buildings':
                    result = await harvestBuildings(itemId, neighborsToHarvestInThisBatch);
                    break;
            }

            if (isHarvesting) {
                statusEl.textContent = `✅ تم الانتهاء من معالجة ${totalNeighborsProcessed} جار. تم حصاد ${result} عنصر بنجاح!`;
            } else {
                statusEl.textContent = `🛑 تم إيقاف العملية يدوياً بعد معالجة ${totalNeighborsProcessed} جار. تم حصاد ${result} عنصر.`;
            }

        } catch (error) {
            console.error('Error during harvest:', error);
            statusEl.textContent = '❌ حدث خطأ أثناء الحصاد، الرجاء المحاولة مرة أخرى.';
        } finally {
            stopHarvestProcess();
            updatePanelInfo();
        }
    };

    stopBtn.onclick = () => {
        stopHarvestProcess();
    };

    div.querySelector('.close-btn').onclick = () => {
        div.style.display = 'none';
        if (div.refreshIntervalId) {
            clearInterval(div.refreshIntervalId);
            delete div.refreshIntervalId;
        }
        customSuggestionsDiv.style.display = 'none';
    };

    loadHarvestCounts();

    harvestTypeSelect.addEventListener('change', () => {
        const selectedType = harvestTypeSelect.value;
        if (selectedType === 'seeds') {
            activeSuggestionList = plantList;
            itemIdInput.placeholder = "كود النبات (ID) أو الاسم";
        } else if (selectedType === 'trees') {
            activeSuggestionList = treeList;
            itemIdInput.placeholder = "كود الشجرة (ID) أو الاسم";
        } else {
            activeSuggestionList = [];
            itemIdInput.placeholder = "كود المبنى (ID)";
        }
        itemIdInput.value = '';
        populateCustomSuggestions(activeSuggestionList, '');
        currentItemHarvestCount = 0;
        updateItemHarvestCounterInPanel();
        updateFloatingCounterHarvest();
    });

    itemIdInput.addEventListener('input', () => {
        const searchTerm = itemIdInput.value.trim();
        populateCustomSuggestions(activeSuggestionList, searchTerm);
    });

    document.addEventListener('click', (event) => {
        if (!itemIdInput.contains(event.target) && !customSuggestionsDiv.contains(event.target)) {
            customSuggestionsDiv.style.display = 'none';
        }
    });

    const setupRefreshInterval = () => {
        if (div.refreshIntervalId) {
            clearInterval(div.refreshIntervalId);
        }

        div.refreshIntervalId = setInterval(() => {
            const gameDataReady = typeof unsafeWindow !== 'undefined' &&
                unsafeWindow.GF &&
                unsafeWindow.GF.friendsController &&
                unsafeWindow.GF.friendsController.model &&
                unsafeWindow.GF.friendsController.model.backendFriendsData;

            if (gameDataReady) {
                updatePanelInfo();
                loadPlantsAndTrees();
            } else {
                const infoTextElement = div.querySelector('#panelInfoText');
                if (infoTextElement) {
                    infoTextElement.innerHTML = `
                        هذه الأداة تسمح بحصاد الثمار والأشجار والمباني من جيران المزرعة دفعة واحدة.<br>
                        <strong>جاري تحميل بيانات الجيران...</strong><br>
                        <strong>حصادات اليوم:</strong><br>
                        - ثمار: ${harvestCounts.s}/155<br>
                        - أشجار: ${harvestCounts.t}/155<br>
                        - مباني: ${harvestCounts.b}/155
                    `;
                }
            }
        }, 3000);
    };

    setupRefreshInterval();
    updatePanelInfo();
    loadPlantsAndTrees();
    updateItemHarvestCounterInPanel();
    floatingCounterHarvest.style.display = 'none';

    document.body.appendChild(div);

    return div;
}
function createNeighborWateringPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    div.innerHTML = `
        <h3 style="margin-top:0; color:#3498db;">💧 سقاية وتسميد الجيران</h3>
        <div style="color:white;margin-bottom:15px;" id="panelInfoTextWatering">
            جاري تحميل بيانات الجيران...
        </div>
        <select id="actionType" style="width:100%;padding:8px;margin-bottom:10px;border-radius:4px;border:none;background-color:#34495e;color:white;">
            <option value="water">سقاية الأشجار</option>
            <option value="fertilize">تسميد المحاصيل</option>
        </select>
        <input type="number" id="neighborsCountWatering" placeholder="عدد الجيران" style="width:100%;padding:8px;margin-bottom:10px;border-radius:4px;border:none;background-color:#34495e;color:white;">
        <div style="display: flex; gap: 10px; margin-bottom: 10px;">
            <button id="runNeighborAction" style="flex: 1; padding:10px;background-color:#3498db;color:white;border:none;border-radius:5px;cursor:pointer;font-size:1em;font-weight:bold;">💦 بدء المساعدة</button>
            <button id="stopNeighborAction" style="flex: 1; padding:10px;background-color:#e74c3c;color:white;border:none;border-radius:5px;cursor:pointer;font-size:1em;font-weight:bold; display: none;">🛑 إيقاف المساعدة</button>
        </div>
        <div id="neighborActionStatus" style="color:white;margin-top:10px;min-height:20px;"></div>
        <div class="close-btn" style="position: absolute; top: 10px; right: 10px; cursor: pointer; color: white; font-size: 1.5em;">✖️</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
        <div style="text-align:center;color:white;font-size:12px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
    `;
// أضف هذين السطرين:
let totalVisitedNeighbors = 0;  // سيعد كل الجيران الذين دخلت لهم
let totalExecutedActions = 0;    // سيعد فقط الجيران الذين تم العمل عليهم

    let sessionActionCounts = { water: 0, fertilize: 0 };
    let isActing = false;
    let processedNeighborsCount = 0;
    // لتخزين UID الجيران الذين تم الدخول إليهم ومعالجتهم في هذه الجلسة
    let processedNeighborsUIDs = new Set(
    JSON.parse(localStorage.getItem('megaScript_processedNeighborsWatering') || '[]')
);
const saveProcessedNeighbors = () => {
    localStorage.setItem(
        'megaScript_processedNeighborsWatering',
        JSON.stringify([...processedNeighborsUIDs])
    );
};
    // --- بداية كود العداد الشفاف العائم ---
    const floatingCounterWatering = document.createElement('div');
    floatingCounterWatering.id = 'dr-floating-counter-watering';
    floatingCounterWatering.style.cssText = `
        position: fixed;
        top: 10px;
        left: 50%;
        transform: translateX(-50%);
        background-color: rgba(0, 0, 0, 0.7);
        color: white;
        padding: 10px 15px;
        border-radius: 8px;
        font-size: 1.1em;
        font-weight: bold;
        z-index: 99999;
        display: none;
        border: 1px solid #3498db;
        text-align: center;
        box-shadow: 0 4px 8px rgba(0,0,0,0.3);
        flex-direction: column;
        gap: 8px;
        align-items: center;
    `;
    floatingCounterWatering.innerHTML = `
        <div id="floatingProcessedCountWatering">تم معالجة: 0 جار</div>
        <div id="floatingCurrentActionCount">تم تنفيذ: 0 عملية</div>
        <button id="floatingStopBtnWatering" style="padding: 8px 15px; background-color: #e74c3c; color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 0.9em; font-weight: bold;">🛑 إيقاف</button>
    `;
    document.body.appendChild(floatingCounterWatering);

    const updateFloatingCounterWatering = () => {
    if (floatingCounterWatering) {
        floatingCounterWatering.querySelector('#floatingProcessedCountWatering')
            .textContent = `تم معالجة: ${totalVisitedNeighbors} جار`;

        floatingCounterWatering.querySelector('#floatingCurrentActionCount')
            .textContent = `تم التنفيذ: ${totalExecutedActions}`;
    }
};
    floatingCounterWatering.querySelector('#floatingStopBtnWatering').onclick = () => {
        stopActionProcess();
    };
    // --- نهاية كود العداد الشفاف العائم ---

    const getActionLimit = () => {
        if (typeof unsafeWindow !== 'undefined' && unsafeWindow.GF && unsafeWindow.GF.loginModel && unsafeWindow.GF.loginModel.AppData) {
            const vipLevel = unsafeWindow.GF.loginModel.AppData.vip_level;
            if (!vipLevel || vipLevel < 3) return 5;
            if (vipLevel < 5) return 6;
            if (vipLevel < 9) return 7;
            if (vipLevel < 12) return 8;
            if (vipLevel < 16) return 9;
            return 10;
        }
        return 5;
    };

    const getRawNeighbors = () => {
        if (typeof unsafeWindow !== 'undefined' && unsafeWindow.GF && unsafeWindow.GF.friendsController && unsafeWindow.GF.friendsController.model && unsafeWindow.GF.friendsController.model.backendFriendsData && unsafeWindow.GF.friendsController.model.backendFriendsData.neighbors) {
            return unsafeWindow.GF.friendsController.model.backendFriendsData.neighbors;
        }
        return [];
    };

    const getEligibleNeighborsForAction = () => {
        const actionLimit = getActionLimit();
        const allNeighbors = getRawNeighbors();
        return allNeighbors
            .filter(neighbor =>
                neighbor.fertilizer_times < actionLimit &&
                !processedNeighborsUIDs.has(neighbor.uid)
            )
            .reverse();
    };

    const updatePanelInfo = () => {
        const infoTextElement = div.querySelector('#panelInfoTextWatering');
        if (infoTextElement) {
            const readyNeighborsCount = getEligibleNeighborsForAction().length;
            infoTextElement.innerHTML = `
                هذه الأداة تسمح بسقاية الأشجار وتسميد المحاصيل من جيران المزرعة دفعة واحدة.<br>
                <strong>عدد الجيران الجاهزين للمساعدة:</strong> ${readyNeighborsCount}<br>
                <strong>الجيران الذين تمت مساعدتهم في هذه الجلسة:</strong> ${processedNeighborsCount}
            `;
            const neighborsInput = div.querySelector('#neighborsCountWatering');
            if (neighborsInput) {
                neighborsInput.max = readyNeighborsCount;
                neighborsInput.placeholder = `عدد الجيران (1-${readyNeighborsCount})`;
            }
        }
        updateFloatingCounterWatering();
    };

    // **تعديل:** دالة مساعدة لـ NetUtils
    async function executeNetRequest(requests) {
        if (!unsafeWindow.NetUtils || !unsafeWindow.NetUtils.enqueue || !unsafeWindow.NetUtils.flush) {
            console.error("NetUtils أو دوالها غير متاحة في unsafeWindow.");
            return 'rq_error';
        }

        // إضافة جميع الطلبات إلى قائمة الانتظار
        for (const request of requests) {
            if (!isActing) {
                console.log("Process stopped during enqueue.");
                return 'rq_stopped';
            }
            // استخدام true لـ `sync` لإرسال الطلب فورًا عند الـ `flush`
            unsafeWindow.NetUtils.enqueue(request.method, request.data, true);
        }

        return new Promise((resolve) => {
            if (!isActing) {
                console.log("Process stopped before flush.");
                resolve('rq_stopped');
                return;
            }
            // إرسال جميع الطلبات المجمعة مرة واحدة
            unsafeWindow.NetUtils.flush(function (response) {
                if (!isActing) {
                    console.log("Process stopped after flush received (but before processing).");
                    resolve('rq_stopped');
                    return;
                }
                resolve(
                    response?.data?.objects_to_update ||
                    response?.data ||
                    response ||
                    'rq_error'
                );
            }, this);
        });
    }

    // **تعديل جذري:** دمج جلب البيانات مع الإجراء لتقليل زيارات المزرعة
    // الآن لن يتم زيارة المزرعة إلا مرة واحدة فقط لكل جار لجلب بيانات الأشجار/المحاصيل ثم تنفيذ الإجراءات
    async function performNeighborAction(neighbor, actionType, actionLimit) {
        if (!isActing) return 'rq_stopped';

        const selfName = unsafeWindow.GF.friendsController.model['_self']?.name ?? 'Admin';
        const actionBaseData = {
            cur_sceneid: 0,
            friendName: selfName,
            friend_id: neighbor.uid
        };

        let itemsToProcess = [];
        let actionMethod = '';
        let itemCategory = '';
        let currentActionKey = '';

        if (actionType === 'water') {
            itemCategory = 'trees';
            actionMethod = 'friend_water.save_data';
            currentActionKey = 'water';
        } else if (actionType === 'fertilize') {
            itemCategory = 'seeds';
            actionMethod = 'friend_fertilize.save_data';
            currentActionKey = 'fertilize';
        }

        try {
            // **تعديل:** جلب بيانات المزرعة مرة واحدة هنا
            const farmDataResponse = await unsafeWindow.NetUtils.netManager.loadUrl('load_farm.load_farm', {
                id: neighbor.uid,
                sceneid: 0,
                tofriendfarm: true
            });

            if (!isActing || farmDataResponse === 'rq_stopped' || !farmDataResponse?.data?.farm?.map) {
                return 0; // توقف أو لا توجد بيانات للمزرعة
            }

            // تصفية العناصر من بيانات المزرعة التي تم جلبها
            itemsToProcess = Object.values(farmDataResponse.data.farm.map)
                .filter(item => {
                    const itemData = unsafeWindow.Config.Store_GetItemData(item.id);
                    return itemData?.type === itemCategory;
                })
                .slice(0, actionLimit); // نأخذ فقط العدد المسموح به

           if (itemsToProcess.length === 0) { return false; }

            const requests = itemsToProcess.map(item => {
                let dataToSend = {
                    ...actionBaseData,
                    plant_x: item.x,
                    plant_y: item.y,
                };
                if (itemCategory === 'seeds') {
                    dataToSend.plant_id = item.id;
                } else if (itemCategory === 'trees') {
                    dataToSend.tree_id = item.id;
                }
                return { method: actionMethod.split('.')[0], data: dataToSend };
            });

            const response = await executeNetRequest(requests); // استخدام الدالة المحدثة
            if (response === 'rq_stopped') {
                return -1; // عملية توقفت
            }

            let successfulActionsCount = 0;
            if (response && !response.includes('rq_error')) {
                // عدد الإجراءات الناجحة هو عدد الطلبات المرسلة
                successfulActionsCount = requests.length;

                // تحديث بيانات الجار في الموديل المحلي للعبة
                const updatedNeighborInGameModel = getRawNeighbors().find(n => n.uid === neighbor.uid);
                if (updatedNeighborInGameModel) {
                    updatedNeighborInGameModel.fertilizer_times += successfulActionsCount;
                    if (updatedNeighborInGameModel.fertilizer_times >= actionLimit) {
                        processedNeighborsUIDs.add(updatedNeighborInGameModel.uid);
saveProcessedNeighbors();
                        console.log(`تم إضافة الجار ${updatedNeighborInGameModel.name || updatedNeighborInGameModel.uid} إلى قائمة المعالجين في الجلسة.`);
                    }
                }
                sessionActionCounts[currentActionKey] += successfulActionsCount;
            }
            return successfulActionsCount;

        } catch (error) {
            console.error(`خطأ أثناء مساعدة الجار (${neighbor.name || neighbor.uid}):`, error);
            return 0;
        }
    }

    const runBtn = div.querySelector('#runNeighborAction');
    const stopBtn = div.querySelector('#stopNeighborAction');
    const statusEl = div.querySelector('#neighborActionStatus');
    const actionSelect = div.querySelector('#actionType');
    const neighborsCountInput = div.querySelector('#neighborsCountWatering');

    // دالة مساعدة لإيقاف العملية
    const stopActionProcess = () => {
  totalVisitedNeighbors = 0;
    totalExecutedActions = 0;
        isActing = false;
        statusEl.textContent = 'جاري إيقاف المساعدة، انتظر قليلاً...';
        stopBtn.disabled = true;
        runBtn.disabled = false;
        runBtn.textContent = '💦 بدء المساعدة';
        stopBtn.style.display = 'none';
        floatingCounterWatering.style.display = 'none';
        neighborsCountInput.value = '';
        updatePanelInfo();
    };

    runBtn.onclick = async () => {
div.style.display = 'none';
        isActing = true;
        runBtn.disabled = true;
        stopBtn.style.display = 'inline-block';
        stopBtn.disabled = false;
        runBtn.textContent = 'جارٍ المساعدة...';
        statusEl.textContent = 'بدء عملية المساعدة...';

        sessionActionCounts = { water: 0, fertilize: 0 };
        processedNeighborsCount = 0;
        processedNeighborsUIDs.clear();
        updatePanelInfo();
        floatingCounterWatering.style.display = 'flex';

        const actionType = actionSelect.value;
        const neighborsCount = parseInt(neighborsCountInput.value);
        const actionLimit = getActionLimit(); // جلب الحد الأقصى للمساعدات

        const eligibleNeighbors = getEligibleNeighborsForAction();
        if (isNaN(neighborsCount) || neighborsCount <= 0 || neighborsCount > eligibleNeighbors.length) {
            statusEl.textContent = `الرجاء إدخال عدد جيران صحيح بين 1 و ${eligibleNeighbors.length}`;
            stopActionProcess();
            return;
        }

        const neighborsToProcess = eligibleNeighbors.slice(0, neighborsCount);
        const totalNeighborsSelected = neighborsToProcess.length;

        for (let i = 0; i < neighborsToProcess.length; i++) {
            if (!isActing) {
                statusEl.textContent = `تم إيقاف المساعدة يدوياً بعد معالجة ${processedNeighborsCount} جار.`;
                break;
            }

            const neighbor = neighborsToProcess[i];

            const liveNeighborData = getRawNeighbors().find(n => n.uid === neighbor.uid);
 totalVisitedNeighbors++;
            if (!liveNeighborData || liveNeighborData.fertilizer_times >= actionLimit || processedNeighborsUIDs.has(liveNeighborData.uid)) {
                console.log(`الجار ${neighbor.name || neighbor.uid} لم يعد جاهزًا للمساعدة أو تم معالجته بالفعل في هذه الجلسة، تخطي.`);
                processedNeighborsUIDs.add(neighbor.uid);
saveProcessedNeighbors();
                processedNeighborsCount++;
                updatePanelInfo();
                continue;
            }

            // **تعديل:** إزالة اسم الجار من الرسالة
            statusEl.textContent = `جاري معالجة الجار رقم (${processedNeighborsCount + 1}/${totalNeighborsSelected})...`;
            updateFloatingCounterWatering();

            try {
                const actionsDone = await performNeighborAction(neighbor, actionType, actionLimit);

                if (actionsDone === -1) {
                    statusEl.textContent = `تم إيقاف المساعدة يدوياً بعد معالجة ${processedNeighborsCount} جار.`;
                    break;
                }

                // **تعديل:** هنا يتم زيادة processedNeighborsCount فقط إذا تم تنفيذ أي إجراء بنجاح للجار
                if (actionsDone > 0) {
                    processedNeighborsCount++;
                    processedNeighborsUIDs.add(neighbor.uid); // تأكيد إضافة الجار الذي تم معالجته فعليا
                totalExecutedActions++;
saveProcessedNeighbors();
} else if (actionsDone === 0) {
                    // إذا لم يتم تنفيذ أي إجراء (مثلا لا توجد أشجار/محاصيل)
                    console.log(`لا توجد عناصر لتنفيذ الإجراء عليها لدى الجار رقم (${processedNeighborsCount + 1}).`);
                    // لا نزيد processedNeighborsCount هنا، لأنه لم يتم "مساعدته" فعليًا
                    // لكن يمكن إضافته لـ processedNeighborsUIDs لتجنب زيارته مرة أخرى في نفس الجلسة
                    processedNeighborsUIDs.add(neighbor.uid);
                }
                updatePanelInfo();

            } catch (error) {
                console.error(`خطأ أثناء مساعدة الجار (${i + 1}/${totalNeighborsSelected}):`, error);
                statusEl.textContent = `حدث خطأ أثناء مساعدة الجار رقم (${processedNeighborsCount + 1}/${totalNeighborsSelected}).`;
                processedNeighborsUIDs.add(neighbor.uid);
                // نزيد العداد حتى لو فيه خطأ، عشان يتم تسجيل محاولة الدخول له
                processedNeighborsCount++;
                updatePanelInfo();
            }

            // **تعديل:** حذف التأخير تمامًا
        }

        if (isActing) {
            statusEl.textContent = `✅ تمت معالجة ${totalVisitedNeighbors} جار | ${totalExecutedActions} تنفيذ`;
        } else {
            statusEl.textContent = `🛑 تم إيقاف المساعدة يدوياً بعد معالجة ${processedNeighborsCount} جار.`;
        }
        stopActionProcess();
    };

    stopBtn.onclick = () => {
        stopActionProcess();
    };

div.querySelector('.close-btn').onclick = () => {
    div.style.display = 'none';
    if (typeof div.refreshInterval !== 'undefined') {
        clearInterval(div.refreshInterval);
        delete div.refreshInterval;
    }
};

    const setupRefreshInterval = () => {
        if (div.refreshInterval) {
            clearInterval(div.refreshInterval);
        }

        div.refreshInterval = setInterval(() => {
            const gameDataReady = typeof unsafeWindow !== 'undefined' &&
                unsafeWindow.GF &&
                unsafeWindow.GF.friendsController &&
                unsafeWindow.GF.friendsController.model &&
                unsafeWindow.GF.friendsController.model.backendFriendsData;

            if (gameDataReady) {
                updatePanelInfo();
            } else {
                const infoTextElement = div.querySelector('#panelInfoTextWatering');
                if (infoTextElement) {
                    infoTextElement.innerHTML = `
                        هذه الأداة تسمح بسقاية الأشجار وتسميد المحاصيل من جيران المزرعة دفعة واحدة.<br>
                        <strong>جاري تحميل بيانات الجيران...</strong><br>
                        <strong>الجيران الذين تمت مساعدتهم في هذه الجلسة:</strong> ${processedNeighborsCount}
                    `;
                }
            }
        }, 3000);
    };

    setupRefreshInterval();
    updatePanelInfo();
    floatingCounterWatering.style.display = 'none';

    document.body.appendChild(div);

    return div;
}
function createFarmManagerPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';

    const style = document.createElement('style');
    style.textContent = `
        .tab-btn {
            background-color: white;
            color: black;
            border: 1px solid #ccc;
            padding: 8px 15px;
            cursor: pointer;
            transition: background-color 0.3s ease, color 0.3s ease, box-shadow 0.3s ease;
        }

        .tab-btn.active {
            background-color: #ffcc00;
            color: black;
            border-color: #ffcc00;
            box-shadow: 0 0 10px #ffd700, 0 0 20px #ffd700, 0 0 30px #ffcc00;
        }
    `;
    document.head.appendChild(style);
    let plantList = [];
    let selectedPlantId = null;
    let selectedPlantName = ''; // لتخزين اسم النبات المختار
    let currentGrowTime = 15; // وقت النمو الافتراضي بالدقائق
    const EMPTY_LAND_IDS = [1, 207323, 207324, 203527];

 div.innerHTML = `
    <style>
        .farm-input {
            width: 150px;
            height: 25px;
            padding: 5px;
            margin: 5px 0;
            border: 1px solid #4CAF50;
            border-radius: 4px;
            font-size: 12px;
        }
        .run-btn-container {
            display: flex;
            justify-content: center;
            margin: 10px 0;
        }
        .run-btn {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 150px;
            padding: 5px;
        }
    </style>

    <h3>👨‍🌾 إدارة المزرعة</h3>

    <div class="tabs">
        <button class="tab-btn active" data-tab="limited">زراعة محدودة</button>
        <button class="tab-btn" data-tab="current">زراعة كل الترب</button>
        <button class="tab-btn" data-tab="all">جميع المزارع</button>
    </div>

    <div id="limited-tab" class="tab-content active">
        <input type="number" id="limited-count" class="farm-input" placeholder="عدد الترب" min="1" value="50">
        <input type="text" id="limited-search" class="farm-input" placeholder="ابحث عن نبات...">
        <div id="limited-suggestions" class="suggestions" style="position: absolute; width: 150px; max-height: 150px; overflow-y: auto; background-color: white; border: 1px solid #4CAF50; border-radius: 4px; z-index: 1000; display: none;"></div>
        <div id="limited-plant-info" style="color:lightgreen;margin-top:5px;font-size:14px;display:none;"></div>
        <div class="run-btn-container">
            <button id="limited-run" class="run-btn">🚀 بدء الزراعة</button>
        </div>
        <div id="limited-status" class="status-message"></div>
    </div>

    <div id="current-tab" class="tab-content">
        <input type="text" id="current-search" class="farm-input" placeholder="ابحث عن نبات...">
        <div id="current-suggestions" class="suggestions" style="position: absolute; width: 150px; max-height: 150px; overflow-y: auto; background-color: white; border: 1px solid #4CAF50; border-radius: 4px; z-index: 1000; display: none;"></div>
        <div id="current-plant-info" style="color:lightgreen;margin-top:5px;font-size:14px;display:none;"></div>
        <div class="run-btn-container">
            <button id="current-run" class="run-btn">🚀 زراعة الكل</button>
        </div>
        <div id="current-status" class="status-message"></div>
    </div>

    <div id="all-tab" class="tab-content">
        <input type="text" id="all-search" class="farm-input" placeholder="ابحث عن نبات...">
        <div id="all-suggestions" class="suggestions" style="position: absolute; width: 150px; max-height: 150px; overflow-y: auto; background-color: white; border: 1px solid #4CAF50; border-radius: 4px; z-index: 1000; display: none;"></div>
        <div id="all-plant-info" style="color:lightgreen;margin-top:5px;font-size:14px;display:none;"></div>
        <div class="run-btn-container">
            <button id="all-run" class="run-btn">🚀 بدء الزراعة</button>
        </div>
        <div id="all-status" class="status-message"></div>
    </div>

    <div class="stats">
        <div>الترب الفارغة: <span id="empty-count">0</span></div>
        <div>الترب المزروعة: <span id="planted-count">0</span></div>
    </div>
    <div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
    <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
    <div class="footer">👑 بواسطة د.أحمد خالد</div>
`;

document.body.appendChild(div);

    // ====== الوظائف الأساسية ====== //

    // دالة تحميل النباتات من المتجر
    let lastPlantStoreLoadFailed = false;

function loadPlants() {
    if (unsafeWindow.Config?.Store) {
        lastPlantStoreLoadFailed = false;

        plantList = Object.values(unsafeWindow.Config.Store)
            .filter(item => item.type === 'seeds')
            .map(item => ({
                id: item.id,
                name: item.name,
                growTime: item.collect_in // وقت النمو بالثواني
            }));

        console.log(`✅ تم تحميل ${plantList.length} نبات من المتجر.`);

        // تحديث الاقتراحات إذا كان هناك مصطلح بحث موجود بالفعل
        div.querySelectorAll('input[type="text"]').forEach(input => {
            if (input.value.length > 0) {
                const event = new Event('input');
                input.dispatchEvent(event);
            }
        });
    } else {
        if (!lastPlantStoreLoadFailed) {
            console.warn("❌ لم يتم تحميل بيانات المتجر بعد. تأكد من فتح اللعبة.");
            lastPlantStoreLoadFailed = true;
        }
        setTimeout(loadPlants, 3000); // حاول التحميل مرة أخرى بعد 3 ثوانٍ
    }
}

    // دالة البحث عن الترب الفارغة
    function findEmptyLands() {
        const map = unsafeWindow.GF?.loginModel?.AppData?.map || [];
        return map.filter(item => EMPTY_LAND_IDS.includes(item.id))
            .map(item => ({ x: item.x, y: item.y }));
    }

    // دالة حساب النباتات المزروعة
    function findPlantedCrops() {
        const map = unsafeWindow.GF?.loginModel?.AppData?.map || [];
        return map.filter(item => {
            const data = unsafeWindow.Config.Store_GetItemData(item.id);
            return data?.type === 'seeds' && item.start_time;
        }).length;
    }

    // دالة الزراعة الأساسية
    async function plantOnFarm(sceneId, plantId, count = -1, statusElement, noUpdate = false) { // Added noUpdate parameter
        statusElement.textContent = `⏳ جاري التبديل للمزرعة ${sceneId + 1}...`;
        const currentScene = unsafeWindow.GF.loginModel.AppData.scene_select;
        if (currentScene !== sceneId) {
            await switchToFarm(sceneId);
        }

        const emptyLands = findEmptyLands();
        const landsToPlant = count === -1 ? emptyLands : emptyLands.slice(0, count);

        if (landsToPlant.length === 0) {
            statusElement.textContent = `ℹ️ لا توجد ترب فارغة في المزرعة ${sceneId + 1}.`;
            return 0;
        }

        statusElement.textContent = `⏳ جاري زراعة ${landsToPlant.length} تربة بنبات ${selectedPlantName} في المزرعة ${sceneId + 1}...`;

        const requests = landsToPlant.map(land => ({
            action: 'add_plant.save_data',
            data: {
                unique_id: Math.floor(Math.random() * 1000000),
                plant_id: plantId,
                soil_x: land.x,
                soil_y: land.y,
                greenhouse_id: 204979,
                greenhouse_x: land.x - 1,
                greenhouse_y: land.y - 1,
                qty: 1
            }
        }));

        // إرسال جميع طلبات الزراعة دفعة واحدة
        await Promise.all(requests.map(req => unsafeWindow.NetUtils.enqueue(req.action, req.data)));
        await unsafeWindow.NetUtils.flush();

        statusElement.textContent = `✅ تم زراعة ${landsToPlant.length} تربات في المزرعة ${sceneId + 1}.`;

        if (!noUpdate) { // Only update if noUpdate is false
            statusElement.textContent += ` جاري تحديث المزرعة...`;
div.style.display = 'none';
            await new Promise(resolve => setTimeout(resolve, 7000));
            await switchToFarm(sceneId);
        }
        return landsToPlant.length;
    }

    // تبديل المزرعة
    async function switchToFarm(sceneId) {
        unsafeWindow.App.EasyLoading.showLoading();
        await unsafeWindow.GF.loginController.loginProxy.send(
            unsafeWindow.HttpConst.LOAD_FARM,
            { id: unsafeWindow.snsid, sceneid: sceneId }
        );
        await new Promise(resolve => setTimeout(resolve, 15000));
        unsafeWindow.App.EasyLoading.hideLoading();
    }

    // دالة لإعداد حقول البحث والاقتراحات
    function setupSearch(inputId, suggestionsId, plantInfoId) {
        const input = document.getElementById(inputId);
        const suggestions = document.getElementById(suggestionsId);
        const plantInfoEl = document.getElementById(plantInfoId);

        input.addEventListener('input', () => {
            const query = input.value.trim().toLowerCase();
            suggestions.innerHTML = '';
            plantInfoEl.style.display = 'none';
            plantInfoEl.textContent = ''; // مسح المعلومات السابقة
            selectedPlantId = null; // إعادة تعيين النبات المختار
            selectedPlantName = '';

            if (query.length === 0) {
                suggestions.style.display = 'none';
                return;
            }

            const matches = plantList.filter(p =>
                p.name.toLowerCase().includes(query) || p.id.toString().includes(query)
            );

            if (matches.length > 0) {
                matches.slice(0, 10).forEach(p => { // عرض ما يصل إلى 10 اقتراحات
                    const option = document.createElement('div');
                    option.textContent = `${p.name} (ID: ${p.id})`;
                    option.style.padding = '5px';
                    option.style.cursor = 'pointer';
                    option.onclick = () => {
                        input.value = p.name;
                        selectedPlantId = p.id;
                        selectedPlantName = p.name;
                        suggestions.style.display = 'none';
                        displayPlantInfo(p.id, plantInfoEl);
                    };
                    suggestions.appendChild(option);
                });
                suggestions.style.display = 'block';
            } else {
                suggestions.style.display = 'none';
            }
        });

        // إخفاء الاقتراحات عند النقر خارجها
        document.addEventListener('click', (event) => {
            if (!suggestions.contains(event.target) && event.target !== input) {
                suggestions.style.display = 'none';
            }
        });
    }

    // دالة لعرض معلومات النبات (وقت النمو)
    function displayPlantInfo(plantId, element) {
        const cropData = plantList.find(p => p.id === plantId);
        if (cropData?.growTime) {
            const seconds = cropData.growTime;
            const minutes = Math.floor(seconds / 60);
            const hours = Math.floor(minutes / 60);
            const remainingMinutes = minutes % 60;
            let growTimeText = '';
            if (hours > 0) {
                growTimeText = `${hours} ساعة${remainingMinutes > 0 ? ` و ${remainingMinutes} دقيقة` : ''}`;
            } else {
                growTimeText = `${minutes} دقيقة`;
            }
            element.textContent = `⏱ وقت النمو: ${growTimeText}`;
            element.style.display = 'block';
        } else {
            element.textContent = '⏱ وقت النمو: غير معروف';
            element.style.display = 'block';
        }
    }

    // ====== إعداد البحث لجميع التبويبات ====== //
    setupSearch('limited-search', 'limited-suggestions', 'limited-plant-info');
    setupSearch('current-search', 'current-suggestions', 'current-plant-info');
    setupSearch('all-search', 'all-suggestions', 'all-plant-info');

    // ====== تبديل التبويبات ====== //
    div.querySelectorAll('.tab-btn').forEach(btn => {
        btn.addEventListener('click', function() {
            // إزالة النشط من جميع الأزرار
            div.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            // إضافة النشط للزر المحدد
            this.classList.add('active');

            // إخفاء جميع المحتويات
            div.querySelectorAll('.tab-content').forEach(content => {
                content.style.display = 'none';
            });

            // إظهار المحتوى المحدد
            const tabId = this.getAttribute('data-tab') + '-tab';
            document.getElementById(tabId).style.display = 'block';

            // مسح حقول البحث وإخفاء الاقتراحات/معلومات النبات عند تبديل التبويبات
            div.querySelectorAll('input[type="text"]').forEach(input => input.value = '');
            div.querySelectorAll('.suggestions').forEach(sugg => sugg.style.display = 'none');
            div.querySelectorAll('[id$="-plant-info"]').forEach(info => info.style.display = 'none');
            selectedPlantId = null;
            selectedPlantName = '';
        });
    });

    // إخفاء جميع المحتويات عدا الأول عند التحميل الأولي
    div.querySelectorAll('.tab-content').forEach((content, index) => {
        if (index !== 0) {
            content.style.display = 'none';
        }
    });

    // ====== تحديث الإحصائيات ====== //
    function updateStats() {
        const emptyLands = findEmptyLands();
        const planted = findPlantedCrops();

        document.getElementById('empty-count').textContent = emptyLands.length;
        document.getElementById('planted-count').textContent = planted;
    }

    // تحديث الإحصائيات كل 10 ثواني
    setInterval(updateStats, 10000);
    updateStats();

    // ====== معالجة الأحداث لعمليات الزراعة ====== //

    // زراعة محدودة
    document.getElementById('limited-run').addEventListener('click', async function() {
        const count = parseInt(document.getElementById('limited-count').value);
        const status = document.getElementById('limited-status');

        if (!selectedPlantId) {
            status.textContent = '⚠️ يرجى اختيار نبات أولاً من مربع البحث.';
            return;
        }

        if (isNaN(count) || count <= 0) {
            status.textContent = '⚠️ يرجى إدخال عدد صحيح موجب لعدد الترب.';
            return;
        }

        status.textContent = `⏳ جاري زراعة ${selectedPlantName} (${selectedPlantId}) على ${count} تربة...`;
        try {
            const planted = await plantOnFarm(
                unsafeWindow.GF.loginModel.AppData.scene_select,
                selectedPlantId,
                count,
                status
            );
            status.textContent = `✅ تم زراعة ${planted} تربات بنبات ${selectedPlantName}.`;
            updateStats();
        } catch (error) {
            status.textContent = '❌ حدث خطأ أثناء الزراعة: ' + error.message;
            console.error(error);
        }
    });

    // زراعة المزرعة الحالية
    document.getElementById('current-run').addEventListener('click', async function() {
        const status = document.getElementById('current-status');

        if (!selectedPlantId) {
            status.textContent = '⚠️ يرجى اختيار نبات أولاً من مربع البحث.';
            return;
        }

        status.textContent = `⏳ جاري زراعة ${selectedPlantName} (${selectedPlantId}) في المزرعة الحالية...`;
        try {
            const planted = await plantOnFarm(
                unsafeWindow.GF.loginModel.AppData.scene_select,
                selectedPlantId,
                -1, // زراعة جميع الترب الفارغة
                status
            );
            status.textContent = `✅ تم زراعة ${planted} تربات بنبات ${selectedPlantName} في المزرعة الحالية.`;
            updateStats();
        } catch (error) {
            status.textContent = '❌ حدث خطأ أثناء الزراعة: ' + error.message;
            console.error(error);
        }
    });

    // زراعة جميع المزارع
    document.getElementById('all-run').addEventListener('click', async function() {
        const status = document.getElementById('all-status');
        const currentFarm = unsafeWindow.GF.loginModel.AppData.scene_select;

        if (!selectedPlantId) {
            status.textContent = '⚠️ يرجى اختيار نبات أولاً من مربع البحث.';
            return;
        }

        status.textContent = `⏳ جاري زراعة ${selectedPlantName} (${selectedPlantId}) في جميع المزارع...`;
        try {
            let total = 0;
            // Iterate through farms 0, 1, then 2 (cur_sci..0, cur_sc....1, cur_sc...2)
            for (const farmId of [0, 1, 2]) {
                // For farms 0 and 1, we pass `true` to `noUpdate` to prevent immediate refresh
                const shouldUpdate = (farmId === 2); // Only update after the last farm (aquatic)
                const planted = await plantOnFarm(farmId, selectedPlantId, -1, status, !shouldUpdate);
                total += planted;
                status.textContent = `✅ تم زراعة ${planted} تربة في المزرعة ${farmId + 1}. الإجمالي حتى الآن: ${total}.`;
                // Add a small delay between farms to prevent issues
                await new Promise(resolve => setTimeout(resolve, 5000));
            }

            // After all farms are planted, switch back to the original farm and refresh
            await switchToFarm(currentFarm);
            status.textContent = `✅ تم الانتهاء من زراعة ${total} تربات بنبات ${selectedPlantName} في جميع المزارع.`;
            updateStats();
        } catch (error) {
            status.textContent = '❌ حدث خطأ أثناء زراعة جميع المزارع: ' + error.message;
            console.error(error);
        }
    });

    // تحميل النباتات عند بدء تشغيل اللوحة (بعد 30 ثانية لضمان تحميل اللعبة)
    setTimeout(loadPlants, 30000);

    return div;
}
function createHarvestToolsPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    div.innerHTML = `
        <h3>🌾 أدوات الحصاد المتقدمة</h3>

        <div style="margin: 10px 0; padding: 8px; background: rgba(0,0,0,0.3); border-radius: 8px;">
            <div style="font-weight:bold; text-align:center; margin-bottom:5px; color:#FFD700;">العناصر الجاهزة</div>
            <div id="ready-items-container" style="max-height: 120px; overflow-y: auto; padding: 5px;
                border: 1px solid rgba(255,255,255,0.2); border-radius: 5px;">
                <div style="text-align:center; color:#aaa; padding:10px;">جارٍ التحقق من العناصر...</div>
            </div>
        </div>

        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 10px;">
            <div style="position: relative; text-align: center;">
                <label class="specific-toggle-label">
                    محدد <input type="checkbox" id="chk-toggle-seeds-specific">
                </label>
                <button id="btn-harvest-seeds-all" class="harvest-btn" style="margin-top: 5px;">🌱 حصاد كل النبات</button>
                <div id="harvest-seeds-specific-inputs" style="display: none;
                    margin-top: 8px; background: rgba(0,0,0,0.5); padding: 8px; border-radius: 5px; box-shadow: 0 2px 5px rgba(0,0,0,0.3);">
                    <select id="select-harvest-seeds" style="width: calc(100% - 70px);
                        padding: 8px; border-radius: 5px; border: 1px solid #555; background: #333; color: white; margin-right: 5px;
                        display: inline-block;">
                        <option value="">اختر نوعًا</option>
                    </select>
                    <input type="number" id="qty-harvest-seeds" placeholder="الكمية" min="1" style="width: 60px;
                        padding: 8px; border-radius: 5px; border: 1px solid #555; background: #333; color: white;
                        display: inline-block;">
                    <button id="btn-harvest-seeds-specific" class="harvest-btn" style="width: 100%;
                        margin-top: 8px; background-color: #007bff;">حصاد النباتات المحددة</button>
                </div>
            </div>

            <div style="position: relative;
                text-align: center;">
                <label class="specific-toggle-label">
                    محدد <input type="checkbox" id="chk-toggle-trees-specific">
                </label>
                <button id="btn-harvest-trees-all" class="harvest-btn" style="margin-top: 5px;">🌳 حصاد كل الأشجار</button>
                <div id="harvest-trees-specific-inputs" style="display: none;
                    margin-top: 8px; background: rgba(0,0,0,0.5); padding: 8px; border-radius: 5px; box-shadow: 0 2px 5px rgba(0,0,0,0.3);">
                    <select id="select-harvest-trees" style="width: calc(100% - 70px);
                        padding: 8px; border-radius: 5px; border: 1px solid #555; background: #333; color: white; margin-right: 5px;
                        display: inline-block;">
                        <option value="">اختر نوعًا</option>
                    </select>
                    <input type="number" id="qty-harvest-trees" placeholder="الكمية" min="1" style="width: 60px;
                        padding: 8px; border-radius: 5px; border: 1px solid #555; background: #333; color: white;
                        display: inline-block;">
                    <button id="btn-harvest-trees-specific" class="harvest-btn" style="width: 100%;
                        margin-top: 8px; background-color: #007bff;">حصاد الأشجار المحددة</button>
                </div>
            </div>

            <button id="btn-pollinate-all" class="harvest-btn">🐝 تلقيح الكل</button>
            <button id="btn-buildings" class="harvest-btn">🏛 حصاد مباني</button>
        </div>

        <button id="btn-all" class="harvest-btn main-btn">🚀 تلقيح وجمع الكل</button>
        <button id="btn-reload" class="harvest-btn" style="margin-top: 10px;">🔄 تحديث البيانات</button>

        <div id="harvest-status" style="margin-top: 15px; padding: 8px; background: rgba(0,0,0,0.2);
            border-radius: 5px;
            color: white; text-align: center; min-height: 20px;"></div>

        <div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
    `;

    // ستايلات إضافية
    const style = document.createElement('style');
    style.textContent = `
        .harvest-btn {
            padding: 10px;
            border: none;
            border-radius: 8px;
            background-color: #4CAF50;
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
            width: 100%;
        }
        .harvest-btn:hover {
            transform: scale(1.02);
            opacity: 0.9;
        }
        .main-btn {
            background: linear-gradient(135deg, #FF9800, #FF5722);
            width: 100%;
        }
        #btn-harvest-seeds-all { background-color: #28a745; }
        #btn-harvest-seeds-all:hover { background-color: #218838; }
        #btn-harvest-trees-all { background-color: #20c997; }
        #btn-harvest-trees-all:hover { background-color: #1aa079; }
        #btn-pollinate-all { background-color: #fd7e14; }
        #btn-pollinate-all:hover { background-color: #df690f; }
        #btn-buildings { background-color: #17a2b8; }
        #btn-buildings:hover { background-color: #138496; }
        #btn-reload { background-color: #6c757d; }
        #btn-reload:hover { background-color: #5a6268; }

        .specific-toggle-label {
            display: inline-flex;
            align-items: center;
            font-size: 14px;
            color: white;
            cursor: pointer;
            justify-content: center;
            width: 100%;
            margin-bottom: 5px;
        }
        .specific-toggle-label input[type="checkbox"] {
            margin-right: 5px;
            cursor: pointer;
            width: 16px;
            height: 16px;
            order: -1;
        }

        /* ستايلات لعصا التمرير */
        #ready-items-container::-webkit-scrollbar {
            width: 8px;
        }
        #ready-items-container::-webkit-scrollbar-track {
            background: rgba(0,0,0,0.1);
            border-radius: 4px;
        }
        #ready-items-container::-webkit-scrollbar-thumb {
            background: rgba(255,255,255,0.3);
            border-radius: 4px;
        }
        #ready-items-container::-webkit-scrollbar-thumb:hover {
            background: rgba(255,255,255,0.5);
        }

        .ready-item {
            margin: 3px 0;
            padding: 3px 5px;
            border-radius: 3px;
            background: rgba(255,255,255,0.1);
        }
        .ready-seeds { color: #8BC34A; }
        .ready-trees { color: #4CAF50; }
        .ready-buildings { color: #2196F3; }
    `;
    div.appendChild(style);
    // العناصر الرئيسية
    const statusEl = div.querySelector('#harvest-status');
    const readyItemsContainer = div.querySelector('#ready-items-container');
    // عناصر النباتات
    const chkToggleSeedsSpecific = div.querySelector('#chk-toggle-seeds-specific');
    // مربع الاختيار الجديد
    const btnHarvestSeedsAll = div.querySelector('#btn-harvest-seeds-all');
    const harvestSeedsSpecificInputsContainer = div.querySelector('#harvest-seeds-specific-inputs');
    const selectHarvestSeedsInput = div.querySelector('#select-harvest-seeds');
    const qtyHarvestSeedsInput = div.querySelector('#qty-harvest-seeds');
    const btnHarvestSeedsSpecific = div.querySelector('#btn-harvest-seeds-specific');

    // عناصر الأشجار
    const chkToggleTreesSpecific = div.querySelector('#chk-toggle-trees-specific');
    // مربع الاختيار الجديد
    const btnHarvestTreesAll = div.querySelector('#btn-harvest-trees-all');
    const harvestTreesSpecificInputsContainer = div.querySelector('#harvest-trees-specific-inputs');
    const selectHarvestTreesInput = div.querySelector('#select-harvest-trees');
    const qtyHarvestTreesInput = div.querySelector('#qty-harvest-trees');
    const btnHarvestTreesSpecific = div.querySelector('#btn-harvest-trees-specific');

    let refreshTimeout = null;
    let uniqueId = parseInt(unsafeWindow.GF?.loginModel?.AppData?.unique_id) || Date.now();
    // دالة لعرض الرسائل
    function showStatus(message, isError = false, duration = 3000) {
        statusEl.textContent = message;
        statusEl.style.color = isError ? '#ff4444' : 'white';
        statusEl.style.fontWeight = isError ? 'bold' : 'normal';
        clearTimeout(statusEl.timer);
        statusEl.timer = setTimeout(() => {
            statusEl.textContent = '';
        }, duration);
    }

    async function reloadFarm(sceneId) {
        showStatus('🔄 جارٍ تحديث بيانات المزرعة...');
        try {
            let targetSceneId = sceneId;
            if (targetSceneId === 999) {
                targetSceneId = unsafeWindow.GF?.loginModel?.AppData?.scene_select || unsafeWindow.GF?.loginModel?.AppData?.cur_sceneid || 0;

            }

            const requestData = {
                id: unsafeWindow.snsid,
                sceneid: targetSceneId,
            };
            if (unsafeWindow.App?.EasyLoading?.showLoading) {
                unsafeWindow.App.EasyLoading.showLoading();
            }

            await new Promise((resolve, reject) => {
                if (unsafeWindow.GF?.loginController?.loginProxy?.send) {
                    unsafeWindow.GF.loginController.loginProxy.send(
                        unsafeWindow.HttpConst.LOAD_FARM,
                        requestData,
                        (success, response) => {
                            if (success) {
                                resolve(response);
                            } else {
                                reject(new Error('فشل تحميل المزرعة من الخادم.'));
                            }
                        }
                    );
                } else {
                    reject(new Error('وحدة loginProxy.send غير متاحة.'));
                }
            });

            if (unsafeWindow.App?.EasyLoading?.hideLoading) {
                unsafeWindow.App.EasyLoading.hideLoading();
            }
            showStatus('✅ تم تحديث المزرعة بنجاح!', false, 3000);
            updateReadyItems();
        } catch (error) {
            console.error('فشل تحديث المزرعة:', error);
            showStatus('❌ فشل تحديث المزرعة: ' + error.message, true, 5000);
            if (unsafeWindow.App?.EasyLoading?.hideLoading) {
                unsafeWindow.App.EasyLoading.hideLoading();
            }
        }
    }

    function scheduleAutoRefresh() {
        if (refreshTimeout) {
            clearTimeout(refreshTimeout);
        }
        showStatus('✅ تم الانتهاء من العملية. سيتم تحديث المزرعة ...', false, 7000);
div.style.display = 'none';
        refreshTimeout = setTimeout(() => {
            reloadFarm(999);
        }, 7000);
    }

    function updateReadyItems() {
        const seeds = getReadyItemsByType('seeds');
        const trees = getReadyItemsByType('trees');
        const buildings = getReadyBuildings();

        let html = '';

        const selectedSeedValue = selectHarvestSeedsInput.value;
        const selectedTreeValue = selectHarvestTreesInput.value;
        selectHarvestSeedsInput.innerHTML = '<option value="">اختر نوعًا</option>';
        if (seeds.length > 0) {
            const seedCounts = countItems(seeds);
            html += '<div style="font-weight:bold; color:#8BC34A; margin-top:5px;">النباتات الجاهزة:</div>';
            for (const id in seedCounts) {
                const itemInfo = seedCounts[id];
                const option = document.createElement('option');
                option.value = id;
                option.textContent = `${itemInfo.name} (${itemInfo.count})`;
                selectHarvestSeedsInput.appendChild(option);
                html += `<div class="ready-item ready-seeds">${itemInfo.name} (${itemInfo.count})</div>`;
            }
        }
        if (selectedSeedValue && selectHarvestSeedsInput.querySelector(`option[value="${selectedSeedValue}"]`)) {
            selectHarvestSeedsInput.value = selectedSeedValue;
        }

        selectHarvestTreesInput.innerHTML = '<option value="">اختر نوعًا</option>';
        if (trees.length > 0) {
            const treeCounts = countItems(trees);
            html += '<div style="font-weight:bold; color:#4CAF50; margin-top:10px;">الأشجار الجاهزة:</div>';
            for (const id in treeCounts) { // Corrected loop: iterate over IDs to get correct itemInfo
                const itemInfo = treeCounts[id];
                const option = document.createElement('option');
                option.value = id;
                option.textContent = `${itemInfo.name} (${itemInfo.count})`;
                selectHarvestTreesInput.appendChild(option);
                html += `<div class="ready-item ready-trees">${itemInfo.name} (${itemInfo.count})</div>`;
            }
        }
        if (selectedTreeValue && selectHarvestTreesInput.querySelector(`option[value="${selectedTreeValue}"]`)) {
            selectHarvestTreesInput.value = selectedTreeValue;
        }

        if (buildings.length > 0) {
            const buildingCounts = countItems(buildings);
            html += '<div style="font-weight:bold; color:#2196F3; margin-top:10px;">المباني الجاهزة:</div>';
            for (const id in buildingCounts) { // Corrected loop: iterate over IDs to get correct itemInfo
                const itemInfo = buildingCounts[id];
                html += `<div class="ready-item ready-buildings">${itemInfo.name} (${itemInfo.count})</div>`;
            }
        }

        if (html === '') {
            html = '<div style="text-align:center; color:#aaa; padding:10px;">لا توجد عناصر جاهزة للحصاد حالياً</div>';
        }

        readyItemsContainer.innerHTML = html;
    }

    function countItems(items) {
        const counts = {};
        items.forEach(item => {
            // Here, we use item.id to get the item data for display purposes
            const data = getItemData(item.id);
            const name = data?.name || `ID: ${item.id}`; // This correctly gets the name
            if (!counts[item.id]) {
                counts[item.id] = { name: name, count: 0 };
            }
            counts[item.id].count++;
        });
        return counts;
    }

    function getReadyItemsByType(type) {
        const map = mapData();
        const readyItems = [];
        map.forEach(item => {
            const data = getItemData(item.id);
            // Check if it's the correct type and ready to collect
            if (data?.type === type && data?.collect_in && isReadyToCollect(item, data)) {
                readyItems.push(item);
            }
        });
        return readyItems;
    }

    function getReadyBuildings() {
        const map = mapData();
        const readyBuildings = [];
        map.forEach(item => {
            const data = getItemData(item.id);
            // Check if it's a building and ready to collect
            if (data?.type === 'buildings' && data?.collect_mode && data?.collect_in && isReadyToCollect(item, data)) {
                readyBuildings.push({
                    id: item.id,
                    name: data?.name || `ID: ${item.id}`,
                    x: item.x,
                    y: item.y,
                    data: data // Pass full data for later use
                });
            }
        });
        return readyBuildings;
    }

    function isReadyToCollect(item, data) {
        if (!item.start_time || typeof data.collect_in === 'undefined') return false;
        const currentTime = serverTimestamp();
        let requiredTime = data.collect_in;

        // Apply superSoil multiplier only for 'seeds' and 'trees' (as originally)
        if (item.superSoil > 0) {
            if (data.type === 'seeds') {
                requiredTime = requiredTime * 0.45; // superSoil multiplier (0.6) applied
            .45
            } else if (data.type === 'trees') {
                requiredTime = requiredTime * 0.75; // superSoil multiplier (0.6) applied
            }
        } else { // No superSoil
             if (data.type === 'seeds') {
                requiredTime = requiredTime * 0.45;
            } else if (data.type === 'trees') {
                requiredTime = requiredTime * 0.75;
            }
        }

        const elapsed = currentTime - item.start_time;
        const tolerance = 1; // Small tolerance for timing discrepancies
        return elapsed >= (requiredTime - tolerance);
    }

    async function harvestSeeds(isSpecific = false) {
        showStatus('جاري حصاد النباتات...');
        try {
            const allReadySeeds = getReadyItemsByType('seeds');
            let seedsToConsider = allReadySeeds;
            let harvestedProductText = '';
            let quantityToHarvestCount; // Renamed to avoid confusion with product quantity
            if (isSpecific) {
                const selectedProductId = selectHarvestSeedsInput.value;
                const requestedQuantity = parseInt(qtyHarvestSeedsInput.value);

                if (selectedProductId) {
                    seedsToConsider = allReadySeeds.filter(seed => seed.id.toString() === selectedProductId);
                    if (seedsToConsider.length === 0) {
                        showStatus(`لا توجد نباتات جاهزة من النوع الذي اخترته.`);
                        return;
                    }
                    harvestedProductText = ` من النوع ID: ${selectedProductId}`;
                }

                quantityToHarvestCount = isNaN(requestedQuantity) ||
                    requestedQuantity <= 0 ? seedsToConsider.length : Math.min(requestedQuantity, seedsToConsider.length);
            } else {
                quantityToHarvestCount = allReadySeeds.length;
            }

            if (quantityToHarvestCount === 0) {
                showStatus('لا توجد نباتات جاهزة للحصاد.');
                return;
            }

            // Enqueue collect_product for each seed
            for (let i = 0; i < quantityToHarvestCount; i++) {
                const seed = seedsToConsider[i];
                unsafeWindow.NetUtils.enqueue('collect_product.save_data', {
                    unique_id: ++uniqueId,
                    id: seed.id, // Use the seed's actual ID for collecting
                    x: seed.x,
                    y: seed.y,
                    cur_sceneid: unsafeWindow.GF?.loginModel?.AppData?.cur_sceneid || 0,
                    greenhouse_id: 204979, // Example greenhouse ID (adjust if needed)
                    greenhouse_x: seed.x - 1,
                    greenhouse_y: seed.y - 1
                });
            }

            await unsafeWindow.NetUtils.flush();
            showStatus(`تم حصاد ${quantityToHarvestCount} نبتة${harvestedProductText} بنجاح!`, false, 3000);

            // Add harvested products to barn - MODIFIED LOGIC FOR SEEDS ONLY
            if (unsafeWindow.GF?.loginModel?.addStorageOrDryMachine && unsafeWindow.dry?.TipsType?.BarnNewGoods) {
                for (let i = 0; i < quantityToHarvestCount; i++) {
                    const seed = seedsToConsider[i];
                    const seedData = getItemData(seed.id);
                    const actualHarvestedProductId = seedData?.product || seed.id;

                    // Determine quantity based on superSoil property for SEEDS ONLY
                    const quantityToAdd = seed.superSoil > 0 ? 5 : 1;

                    unsafeWindow.GF.loginModel.addStorageOrDryMachine(actualHarvestedProductId, quantityToAdd, unsafeWindow.dry.TipsType.BarnNewGoods);
                }
                console.log('✅ تم إضافة المحاصيل إلى الحظيرة (نباتات)');
            } else {
                console.warn('⚠️ دالة إضافة العناصر للحظيرة غير متاحة.');
            }

        } catch (error) {
            console.error('خطأ في حصاد النباتات:', error);
            showStatus('حدث خطأ أثناء حصاد النباتات', true, 5000);
            throw error;
        } finally {
            // Reset specific harvest inputs
            harvestSeedsSpecificInputsContainer.style.display = 'none';
            selectHarvestSeedsInput.value = '';
            qtyHarvestSeedsInput.value = '';
            chkToggleSeedsSpecific.checked = false;
        }
    }

    async function harvestTrees(isSpecific = false) {
        showStatus('جاري حصاد الأشجار...');
        try {
            const allReadyTrees = getReadyItemsByType('trees');
            let treesToConsider = allReadyTrees;
            let harvestedProductText = '';
            let quantityToHarvestCount; // Renamed to avoid confusion with product quantity
            if (isSpecific) {
                const selectedProductId = selectHarvestTreesInput.value;
                const requestedQuantity = parseInt(qtyHarvestTreesInput.value);

                if (selectedProductId) {
                    treesToConsider = allReadyTrees.filter(tree => tree.id.toString() === selectedProductId);
                    if (treesToConsider.length === 0) {
                        showStatus(`لا توجد أشجار جاهزة من النوع الذي اخترته.`);
                        return;
                    }
                    harvestedProductText = ` من النوع ID: ${selectedProductId}`;
                }

                quantityToHarvestCount = isNaN(requestedQuantity) ||
                    requestedQuantity <= 0 ? treesToConsider.length : Math.min(requestedQuantity, treesToConsider.length);
            } else {
                quantityToHarvestCount = allReadyTrees.length;
            }

            if (quantityToHarvestCount === 0) {
                showStatus('لا توجد أشجار جاهزة للحصاد.');
                return;
            }

            // Enqueue collect_product for each tree
            for (let i = 0; i < quantityToHarvestCount; i++) {
                const tree = treesToConsider[i];
                unsafeWindow.NetUtils.enqueue('collect_product.save_data', {
                    unique_id: ++uniqueId,
                    id: tree.id, // Use the tree's actual ID for collecting
                    x: tree.x,
                    y: tree.y,
                    cur_sceneid: unsafeWindow.GF?.loginModel?.AppData?.cur_sceneid || 0,
                    greenhouse_id: 203592, // Example greenhouse ID (adjust if needed)
                    greenhouse_x: tree.x - 1,
                    greenhouse_y: tree.y - 1
                });
            }

            await unsafeWindow.NetUtils.flush();
            showStatus(`تم حصاد ${quantityToHarvestCount} شجرة${harvestedProductText} بنجاح!`, false, 3000);

            // Add harvested products to barn - NO CHANGE FOR TREES (always 1)
            if (unsafeWindow.GF?.loginModel?.addStorageOrDryMachine && unsafeWindow.dry?.TipsType?.BarnNewGoods) {
                for (let i = 0; i < quantityToHarvestCount; i++) {
                    const tree = treesToConsider[i];
                    const harvestedProductId = tree.id + 1; // As per user's specific request for trees: use tree.id + 1 for harvested tree product

                    // Quantity is always 1 for trees, as per the new clarification.
                    const quantityToAdd = 1;

                    unsafeWindow.GF.loginModel.addStorageOrDryMachine(harvestedProductId, quantityToAdd, unsafeWindow.dry.TipsType.BarnNewGoods);
                }
                console.log('✅ تم إضافة المحاصيل إلى الحظيرة (أشجار)');
            } else {
                console.warn('⚠️ دالة إضافة العناصر للحظيرة غير متاحة.');
            }

        } catch (error) {
            console.error('خطأ في حصاد الأشجار:', error);
            showStatus('حدث خطأ أثناء حصاد الأشجار', true, 5000);
            throw error;
        } finally {
            // Reset specific harvest inputs
            harvestTreesSpecificInputsContainer.style.display = 'none';
            selectHarvestTreesInput.value = '';
            qtyHarvestTreesInput.value = '';
            chkToggleTreesSpecific.checked = false;
        }
    }

    async function pollinateAll() {
        showStatus('جاري تلقيح النباتات والأشجار...');
        try {
            const beeHouse = mapData().find(i => i.id === 203019);
            if (!beeHouse) {
                showStatus('لا توجد خلية نحل (ID: 203019) في المزرعة', true, 5000);
                return;
            }

            const targets = mapData().filter(item => {
                const data = getItemData(item.id);
                // Filter: Only seeds or trees, not yet pollinated, and planted (have start_time)
                return (data?.type === 'seeds' || data?.type === 'trees') &&
                       item.pollinated !== '1' && item.start_time;
            });

            if (targets.length === 0) {
                showStatus('لا توجد نباتات أو أشجار تحتاج للتلقيح');
                return;
            }

            let superSoilPollinatedCount = 0;
            let normalPollinatedCount = 0;

            for (const plant of targets) {
                const hiveId = getHiveId(plant.id);
                const data = getItemData(plant.id);

                // Determine pollination repeats based on superSoil for SEEDS ONLY
                let pollinationRepeats = 1;
                if (data?.type === 'seeds' && plant.superSoil > 0) { // Apply 5 repeats only for superSoil SEEDS
                    pollinationRepeats = 5;
                    superSoilPollinatedCount++;
                } else if (data?.type === 'seeds' && !plant.superSoil) { // Normal seeds, 1 repeat
                    normalPollinatedCount++;
                }
                // Trees always pollinate 1 time (not affected by superSoil for repeats)

                for (let i = 0; i < pollinationRepeats; i++) {
                    unsafeWindow.NetUtils.enqueue('pollinate_beehouse.save_data', {
                        unique_id: ++uniqueId,
                        id: beeHouse.id,
                        x: beeHouse.x,
                        y: beeHouse.y,
                        flip: beeHouse.flipped || 0,
                        hive_id: hiveId,
                        plant_id: plant.id,
                        plant_x: plant.x,
                        plant_y: plant.y,
                        cur_sceneid: unsafeWindow.GF?.loginModel?.AppData?.cur_sceneid || 0,
                        needResponse: "pollinate_beehouse.save_data"
                    });
                }
            }

            await unsafeWindow.NetUtils.flush();
            let statusMessage = `تم تلقيح ${targets.length} نبتة/شجرة بنجاح.`;
            if (superSoilPollinatedCount > 0) {
                statusMessage += ` (${superSoilPollinatedCount} نبتة بتربة خارقة تم تلقيحها 5 مرات).`;
            }
            if (normalPollinatedCount > 0) {
                 statusMessage += ` (${normalPollinatedCount} نبتة بتربة عادية تم تلقيحها مرة واحدة).`;
            }
            // If there are trees, add a note about them
            const treeTargets = targets.filter(item => getItemData(item.id)?.type === 'trees');
            if (treeTargets.length > 0) {
                statusMessage += ` (${treeTargets.length} شجرة تم تلقيحها مرة واحدة).`;
            }

            showStatus(statusMessage, false, 5000);

        } catch (error) {
            console.error('خطأ في التلقيح:', error);
            showStatus('حدث خطأ أثناء التلقيح', true, 5000);
            throw error;
        }
    }

    async function harvestBuildings() {
        showStatus('جاري حصاد المباني...');
        try {
            const buildings = getReadyBuildings();
            if (buildings.length === 0) {
                showStatus('لا توجد مباني جاهزة للحصاد');
                return;
            }

            // Enqueue collect_product for each building
            for (const building of buildings) {
                unsafeWindow.NetUtils.enqueue('collect_product.save_data', {
                    unique_id: ++uniqueId,
                    id: building.id, // Use the building's actual ID for collecting
                    x: building.x,
                    y: building.y,
                    qty: building.data?.collect_max || 1, // Quantity from building data
                    collect_mode: 1, // Standard collect mode
                    cur_sceneid: unsafeWindow.GF?.loginModel?.AppData?.cur_sceneid || 0,
                    automatic: false,
                    flip: 0,
                    startTime_log: serverTimestamp() * 1000,
                    needResponse: "collect_product.save_data",
                    achievement_add: `gear_${building.id}_0` // Example achievement add
                });
            }

            await unsafeWindow.NetUtils.flush();
            showStatus(`تم حصاد ${buildings.length} مبنى بنجاح!`, false, 3000);

            // Add harvested products to barn
            if (unsafeWindow.GF?.loginModel?.addStorageOrDryMachine && unsafeWindow.dry?.TipsType?.BarnNewGoods) {
                buildings.forEach(building => {
                    const buildingData = getItemData(building.id); // Get building data
                    // Use 'product' field for barn storage, fallback to building.id if not found
                    const actualHarvestedProductId = buildingData?.product || building.id;
                    const quantity = building.data?.collect_max || 1; // Quantity from building data
                    unsafeWindow.GF.loginModel.addStorageOrDryMachine(actualHarvestedProductId, quantity, unsafeWindow.dry.TipsType.BarnNewGoods);
                });
                console.log('✅ تم إضافة المحاصيل إلى الحظيرة (مباني)');
            } else {
                console.warn('⚠️ دالة إضافة العناصر للحظيرة غير متاحة.');
            }

        } catch (error) {
            console.error('خطأ في حصاد المباني:', error);
            showStatus('حدث خطأ أثناء حصاد المباني', true, 5000);
            throw error;
        }
    }

    // Helper function to get map data
    function mapData() {
        return unsafeWindow.GF?.loginModel?.AppData?.map || [];
    }

    // Helper function to get item data from game config
    function getItemData(id) {
        return unsafeWindow.Config?.Store_GetItemData(id);
    }

    // Helper function to get current server timestamp
    function serverTimestamp() {
        return unsafeWindow.ServerTime?.timestamp || Math.floor(Date.now() / 1000);
    }

    // Helper function to get hive ID based on plant ID
    function getHiveId(plantId) {
        const plantGroups = {
            45: [4],
            30126: [30072, 100103, 300003, 204497, 206663, 207903],
            30082: [9117, 5005, 5007, 5003, 5009, 5001, 30078, 200300, 200227, 200424, 201579, 202701, 202896, 204396, 203751, 215633, 218612, 225933],
            201633: [200355, 9411, 201581, 30106, 100103, 202906],
            204241: [203676, 203684, 204159, 204533, 204514, 205006, 206411, 207393, 207406, 208483, 208232, 208106],
            209071: [208186, 205111, 206943, 206898, 208965, 202947, 207855, 208714, 209316],
            201375: [65008, 201037, 200600, 201311, 55005, 200984, 201233, 20102, 9005, 204445, 204835, 212616, 217526, 217924, 208925],
            203693: [203700, 201693, 202171, 202735, 203259, 200537, 202006]
        };

        const numericPlantId = Number(plantId);
        if (isNaN(numericPlantId)) {
            console.warn(`Warning: Invalid plant ID provided to getHiveId: ${plantId}. Returning default 45.`);
            return 45;
        }

        for (const [hiveId, plants] of Object.entries(plantGroups)) {
            if (plants.includes(numericPlantId)) {
                return Number(hiveId);
            }
        }
        return 45; // Default hive ID
    }

    // ===== ربط الأحداث =====

    btnHarvestSeedsAll.onclick = async () => {
        await harvestSeeds(false);
        scheduleAutoRefresh();
    };

    chkToggleSeedsSpecific.onchange = () => {
        if (chkToggleSeedsSpecific.checked) {
            harvestSeedsSpecificInputsContainer.style.display = 'block';
            harvestTreesSpecificInputsContainer.style.display = 'none';
            chkToggleTreesSpecific.checked = false;
        } else {
            harvestSeedsSpecificInputsContainer.style.display = 'none';
        }
    };

    btnHarvestSeedsSpecific.onclick = async () => {
        await harvestSeeds(true);
        scheduleAutoRefresh();
    };

    btnHarvestTreesAll.onclick = async () => {
        await harvestTrees(false);
        scheduleAutoRefresh();
    };
    chkToggleTreesSpecific.onchange = () => {
        if (chkToggleTreesSpecific.checked) {
            harvestTreesSpecificInputsContainer.style.display = 'block';
            harvestSeedsSpecificInputsContainer.style.display = 'none';
            chkToggleSeedsSpecific.checked = false;
        } else {
            harvestTreesSpecificInputsContainer.style.display = 'none';
        }
    };

    btnHarvestTreesSpecific.onclick = async () => {
        await harvestTrees(true);
        scheduleAutoRefresh();
    };

    div.querySelector('#btn-pollinate-all').onclick = async () => {
        await pollinateAll();
        scheduleAutoRefresh();
    };
    div.querySelector('#btn-buildings').onclick = async () => {
        await harvestBuildings();
        scheduleAutoRefresh();
    };
    div.querySelector('#btn-reload').onclick = () => reloadFarm(999);

    div.querySelector('#btn-all').onclick = async () => {
        showStatus('🚀 جاري تنفيذ جميع العمليات...');
        try {
            await pollinateAll();
            await harvestSeeds(false);
            await harvestTrees(false);
            await harvestBuildings();

            showStatus('✅ تم الانتهاء من جميع العمليات بنجاح!');
            scheduleAutoRefresh();
        } catch (error) {
            console.error('خطأ في تنفيذ عمليات الكل:', error);
            showStatus('❌ حدث خطأ أثناء تنفيذ عمليات الكل: ' + error.message, true, 5000);
            scheduleAutoRefresh();
        } finally {
            // Reset specific harvest inputs and checkboxes
            harvestSeedsSpecificInputsContainer.style.display = 'none';
            harvestTreesSpecificInputsContainer.style.display = 'none';
            selectHarvestSeedsInput.value = '';
            qtyHarvestSeedsInput.value = '';
            selectHarvestTreesInput.value = '';
            qtyHarvestTreesInput.value = '';
            chkToggleSeedsSpecific.checked = false;
            chkToggleTreesSpecific.checked = false;
        }
    };

    updateReadyItems();
    showStatus('السكربت جاهز للعمل!');
    // Refresh ready items list periodically
    setInterval(() => {
        updateReadyItems();
    }, 10000);
    document.body.appendChild(div);
    return div;
}


function createCloverPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    let plantList = [];
    let plantId = null;
    let currentGrowTime = 15; // Default grow time in minutes
    let isCloverRunning = false; // Add this variable to control the loop
    let countdownIntervalId = null; // To store the interval ID for countdown

    div.innerHTML = `
        <h3>🌿 زراعة وحصاد تلقائي حسب اسم النبات</h3>
        <div style="color:white;margin-bottom:10px;">
            اختر نوع المزرعة:
        </div>
        <select id="farmType" style="margin-bottom:10px; width: 100%; padding: 8px; border-radius: 5px; border: 1px solid #555; background: #333; color: white;">
            <option value="both">المزرعتين (اذهب للرئيسية أولا)</option>
            <option value="farm1">المزرعة الأولي فقط</option>
            <option value="farm2">المزرعة الثانية فقط</option>
        </select>
        <div style="margin-bottom:10px;">
            <input type="text" id="plantSearch" placeholder="اكتب اسم النبات..." style="width:100%; padding:6px; font-size:16px; border-radius: 5px; border: 1px solid #555; background: #333; color: white;" />
<div id="suggestions" style="position:fixed;top:100px;right:20px;background:black;color:gold;max-height:150px;overflow-y:auto;border:1px solid #444;display:none;border-radius:5px;z-index:9999;padding:10px;width:250px;box-shadow:0 0 10px rgba(0,0,0,0.5);"></div>
            <div id="growTime" style="color:lightgreen;margin-top:5px;font-size:14px;display:none;"></div>
        </div>
        <button id="runClover" style="margin-top:15px; padding: 10px; border: none; border-radius: 8px; background-color: #28a745; color: white; font-weight: bold; cursor: pointer; transition: all 0.2s; width: 100%;">🚀 بدء التنفيذ</button>
        <div id="cloverStatus" style="color:white;margin-top:10px; padding: 8px; background: rgba(0,0,0,0.2); border-radius: 5px; text-align: center; min-height: 20px;"></div>
        <div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
    `;

    document.body.appendChild(div);

    const input = div.querySelector('#plantSearch');
    const suggestions = div.querySelector('#suggestions');
    const growTimeEl = div.querySelector('#growTime');
    const runButton = div.querySelector('#runClover');
    const statusEl = div.querySelector('#cloverStatus');
    let counterDiv = null; // Declare counterDiv outside to be accessible globally

    input.addEventListener('input', () => {
        const value = input.value.trim();
        suggestions.innerHTML = '';
        growTimeEl.style.display = 'none';
        if (value.length === 0) {
            suggestions.style.display = 'none';
            return;
        }
        const matches = plantList.filter(p => p.name.includes(value));
        matches.forEach(p => {
            const option = document.createElement('div');
            option.textContent = p.name;
            option.style.padding = '5px';
            option.style.cursor = 'pointer';
            option.onmouseover = () => option.style.backgroundColor = '#555';
            option.onmouseout = () => option.style.backgroundColor = 'black';
            option.onclick = () => {
                input.value = p.name;
                plantId = p.id;
                suggestions.style.display = 'none';

                // ✅ عرض وقت النمو
                const cropData = unsafeWindow.Config.Store_GetItemData(plantId);
                if (cropData?.collect_in) {
                    const seconds = cropData.collect_in;
                    currentGrowTime = Math.ceil(seconds / 60); // Convert to minutes
                    const minutes = Math.floor(seconds / 60);
                    const hours = Math.floor(minutes / 60);
                    const remainingMinutes = minutes % 60;
                    let growTime = '';
                    if (hours > 0) {
                        growTime = `${hours} ساعة${remainingMinutes > 0 ? ` و ${remainingMinutes} دقيقة` : ''}`;
                    } else {
                        growTime = `${remainingMinutes} دقيقة`;
                    }
                    growTimeEl.textContent = `⏱ وقت النمو: ${growTime}`;
                } else {
                    growTimeEl.textContent = '⏱ وقت النمو: غير معروف';
                    currentGrowTime = 15; // Default to 15 minutes if unknown
                }
                growTimeEl.style.display = 'block';
            };
            suggestions.appendChild(option);
        });
        suggestions.style.display = matches.length > 0 ? 'block' : 'none';
    });

    // تحميل المتجر تلقائيًا
    setTimeout(() => {
        if (unsafeWindow.Config && unsafeWindow.Config.Store) {
            // Filter for items of type 'seeds' or 'trees' that have a name and collect_in property
            plantList = Object.values(unsafeWindow.Config.Store).filter(item =>
                (item.type === 'seeds' || item.type === 'trees') && item.name && item.collect_in
            );
            console.log(`✅ تم تحميل ${plantList.length} نبات وشجر من المتجر.`);
        } else {
            console.warn("❌ لم يتم تحميل بيانات المتجر بعد. تأكد من فتح اللعبة.");
        }
    }, 30000);

    async function pollinateAll() {
        const map = unsafeWindow.GF.loginModel.AppData.map;
        const beeHouse = map.find(i => i.id === 203019);
        if (!beeHouse) {
            console.warn('لا توجد خلية نحل (ID: 203019) في المزرعة، التلقيح لن يتم.');
            return;
        }

        const allTargets = map.filter(item => {
            const data = unsafeWindow.Config.Store_GetItemData(item.id);
            // Filter: Only seeds or trees, not yet pollinated, and planted (have start_time)
            return (data?.type === 'seeds' || data?.type === 'trees') &&
                   item.pollinated !== '1' && item.start_time && data?.collect_in;
        });

        if (allTargets.length === 0) {
            console.log('لا توجد نباتات أو أشجار تحتاج للتلقيح');
            return;
        }

        let uniqueIdPollinate = 100000;
        let superSoilSeedsPollinatedCount = 0;
        let normalSeedsPollinatedCount = 0;
        let treesPollinatedCount = 0;

        for (const plant of allTargets) {
            // Check if the script should stop before processing each plant
            if (!isCloverRunning) {
                console.log('Pollination stopped by user.');
                break; // Exit the loop if stop is requested
            }

            const hiveId = getHiveId(plant.id);
            const data = unsafeWindow.Config.Store_GetItemData(plant.id);

            let pollinationRepeats = 1;
            // Apply 5 repeats only for 'seeds' (plants) on 'superSoil'
            if (data?.type === 'seeds' && plant.superSoil > 0) {
                pollinationRepeats = 5;
                superSoilSeedsPollinatedCount++;
            } else if (data?.type === 'seeds') { // Normal seeds (no superSoil)
                normalSeedsPollinatedCount++;
            } else if (data?.type === 'trees') { // Trees always 1 repeat
                treesPollinatedCount++;
            }

            for (let i = 0; i < pollinationRepeats; i++) {
                unsafeWindow.NetUtils.enqueue('pollinate_beehouse.save_data', {
                    unique_id: ++uniqueIdPollinate,
                    id: beeHouse.id,
                    x: beeHouse.x,
                    y: beeHouse.y,
                    flip: beeHouse.flipped || 0,
                    hive_id: hiveId,
                    plant_id: plant.id,
                    plant_x: plant.x,
                    plant_y: plant.y,
                    cur_sceneid: unsafeWindow.GF?.loginModel?.AppData?.cur_sceneid || 0,
                    needResponse: "pollinate_beehouse.save_data"
                });
            }
        }

        if (superSoilSeedsPollinatedCount > 0 || normalSeedsPollinatedCount > 0 || treesPollinatedCount > 0) {
            await unsafeWindow.NetUtils.flush();
            let statusMessage = `تم تلقيح ${allTargets.length} نبتة/شجرة بنجاح.`;
            if (superSoilSeedsPollinatedCount > 0) {
                statusMessage += ` (${superSoilSeedsPollinatedCount} نبتة بتربة خارقة تم تلقيحها 5 مرات).`;
            }
            if (normalSeedsPollinatedCount > 0) {
               statusMessage += ` (${normalSeedsPollinatedCount} نبتة بتربة عادية تم تلقيحها مرة واحدة).`;
            }
            if (treesPollinatedCount > 0) {
                statusMessage += ` (${treesPollinatedCount} شجرة تم تلقيحها مرة واحدة).`;
            }
            console.log(statusMessage);
        } else {
            console.log('لا توجد نباتات أو أشجار تحتاج للتلقيح');
        }
    }


    runButton.onclick = async () => {
    const farmType = div.querySelector('#farmType').value;
    statusEl.textContent = '⏳ جاري بدء العملية...';

    if (!plantId) {
        statusEl.textContent = '❌ الرجاء اختيار نبات أو شجرة للزراعة.';
        return; // متكملش تنفيذ
    }

    // هنا فقط بعد التأكد من صحة الإدخال، نخفي الواجهة
    div.style.display = 'none';

        isCloverRunning = true; // Set running state to true
        runButton.disabled = true; // Disable run button while running

        try {
            let uniqueId = 1000;
            let cycle = 1;

            if (!counterDiv) { // Create counterDiv only if it doesn't exist
                counterDiv = document.createElement('div');
                counterDiv.style.cssText = 'position: fixed; top: 50px; left: 50%; transform: translateX(-50%); background: rgba(0,0,0,0.7); color: white; padding: 5px 10px; border-radius: 5px; z-index: 10000; display: flex; align-items: center; font-size: 13px;'; // Flexbox for alignment

                counterDiv.innerHTML = `
                    <div id="counterText" style="margin-right: 10px;"></div>
                    <div id="countdownTimer" style="margin-right: 5px;"></div>
                    <span id="stopCloverFloat" title="إيقاف" style="
                        display: inline-block;
                        width: 12px; /* حجم النقطة */
                        height: 12px; /* حجم النقطة */
                        background-color: #dc3545; /* لون أحمر */
                        border-radius: 50%; /* لجعلها دائرة */
                        cursor: pointer;
                        position: relative; /* لتحديد مكان التولتييب */
                    "></span>
                `;
                document.body.appendChild(counterDiv);

                // Attach event listener to the new stop "dot"
                const stopDot = counterDiv.querySelector('#stopCloverFloat');
                stopDot.onclick = () => {
                    isCloverRunning = false; // Set the flag to false to stop the loop
                    statusEl.textContent = 'جاري إيقاف العملية... يرجى الانتظار.';
                    clearInterval(countdownIntervalId); // Clear the countdown interval immediately
                    if (counterDiv) {
                        counterDiv.remove();
                        counterDiv = null;
                    }
                    runButton.disabled = false; // Enable run button
                };
            }

            function updateCountdown(remainingTime) {
                const minutes = Math.floor(remainingTime / 60000);
                const seconds = Math.floor((remainingTime % 60000) / 1000);
                document.getElementById('countdownTimer').innerText = `الوقت المتبقي: ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            }

            while (isCloverRunning) { // Use the control variable here
                document.getElementById('counterText').innerText = `الزراعة الألية تعمل - الدورة الحالية ${cycle}`;

                // Check for stop request at the beginning of each major step
                if (!isCloverRunning) {
                    statusEl.textContent = 'تم إيقاف العملية.';
                    break;
                }

                // --- زراعة المزرعة الأولى (أو كلاهما) ---
                if (farmType === 'both' || farmType === 'farm1') {
                    for (let x = 0; x <= 152; x += 4) {
                        for (let y = 0; y <= 152; y += 4) {
                            if (!isCloverRunning) break; // Check for stop during planting loop
                            unsafeWindow.NetUtils.enqueue('add_plant.save_data', {
                                unique_id: ++uniqueId,
                                plant_id: plantId,
                                soil_x: x,
                                soil_y: y,
                                greenhouse_id: 204979,
                                greenhouse_x: x - 1,
                                greenhouse_y: y - 1,
                                qty: 1,
                            });
                        }
                        if (!isCloverRunning) break; // Check for stop during planting loop
                    }
                    await unsafeWindow.NetUtils.flush(); // Flush after planting all in this farm
                    statusEl.textContent = `✅ تم زراعة المزرعة الأولى (${farmType === 'both' ? 'وكلاهما' : ''}) في الدورة ${cycle}.`;
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 15000)); // Short delay after planting

                    if (farmType === 'farm1' && cycle === 1) { // Only load farm if it's farm1 and first cycle
                        if (!isCloverRunning) break;
                        await unsafeWindow.GF.loginController.loadFarm(unsafeWindow.snsid, 0);
                        if (!isCloverRunning) break;
                        await new Promise(resolve => setTimeout(resolve, 25000)); // 25 seconds for first load
                    }
                }

                // --- التبديل للمزرعة الثانية إذا كانت "كلاهما" ---
                if (farmType === 'both') {
                    if (!isCloverRunning) break;
                    await unsafeWindow.GF.loginController.loadFarm(unsafeWindow.snsid, 1);
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 25000)); // Fixed 25 seconds delay
                }

                // --- زراعة المزرعة الثانية (أو كلاهما) ---
                if (farmType === 'both' || farmType === 'farm2') {
                    for (let x = 0; x <= 152; x += 4) {
                        for (let y = 0; y <= 152; y += 4) {
                            if (!isCloverRunning) break; // Check for stop during planting loop
                            unsafeWindow.NetUtils.enqueue('add_plant.save_data', {
                                unique_id: ++uniqueId,
                                plant_id: plantId,
                                soil_x: x,
                                soil_y: y,
                                greenhouse_id: 204979,
                                greenhouse_x: x - 1,
                                greenhouse_y: y - 1,
                                qty: 1,
                            });
                        }
                        if (!isCloverRunning) break; // Check for stop during planting loop
                    }
                    await unsafeWindow.NetUtils.flush(); // Flush after planting all in this farm
                    statusEl.textContent = `✅ تم زراعة المزرعة الثانية (${farmType === 'both' ? 'وكلاهما' : ''}) في الدورة ${cycle}.`;
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 15000)); // Short delay after planting

                    if (farmType === 'farm2' && cycle === 1) { // Only load farm if it's farm2 and first cycle
                        if (!isCloverRunning) break;
                        await unsafeWindow.GF.loginController.loadFarm(unsafeWindow.snsid, 1);
                        if (!isCloverRunning) break;
                        await new Promise(resolve => setTimeout(resolve, 25000)); // 25 seconds for first load
                    }
                }

                // --- العودة للمزرعة الأولى إذا كانت "كلاهما" ---
                if (farmType === 'both') {
                    if (!isCloverRunning) break;
                    await unsafeWindow.GF.loginController.loadFarm(unsafeWindow.snsid, 0);
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 15000)); // Fixed 25 seconds delay
                }

                // --- انتظار وقت النمو ---
                const data = unsafeWindow.Config.Store_GetItemData(plantId);
                let effectiveGrowTime = data?.collect_in || (currentGrowTime * 60); // Use actual seconds if available, else estimated minutes to seconds
                const waitTime = Math.max(1000, effectiveGrowTime * 1000 * 0.45 - 30000); // 45% of grow time minus 30 seconds, min 1 second

                statusEl.textContent = `⏰ انتظار ${Math.ceil(waitTime / 60000)} دقيقة لنمو النباتات...`;
                let remainingTime = waitTime;

                clearInterval(countdownIntervalId); // Clear any previous interval
                countdownIntervalId = setInterval(() => {
                    remainingTime -= 1000;
                    if (remainingTime <= 0) {
                        clearInterval(countdownIntervalId);
                    }
                    updateCountdown(remainingTime);
                }, 1000);

                await new Promise(resolve => {
                    const timer = setTimeout(() => {
                        clearInterval(countdownIntervalId);
                        resolve();
                    }, waitTime);

                    // If stop is requested during the wait, clear timer and interval
                    const checkStopInterval = setInterval(() => {
                        if (!isCloverRunning) {
                            clearTimeout(timer);
                            clearInterval(countdownIntervalId);
                            clearInterval(checkStopInterval);
                            resolve(); // Resolve the promise to unblock
                        }
                    }, 500); // Check every 500ms
                });
                if (!isCloverRunning) break; // Check after wait

                statusEl.textContent = `🌱 النباتات جاهزة للحصاد في الدورة ${cycle}.`;
                if (!isCloverRunning) break;
                await new Promise(resolve => setTimeout(resolve, 3000)); // Small pause after countdown

                // --- حصاد وتلقيح المزرعة الأولى (أو كلاهما) ---
                if (farmType === 'both' || farmType === 'farm1') {
                    if (!isCloverRunning) break;
                    await pollinateAll(); // Pollinate before collecting
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 7000)); // Wait for pollination to register

                    // Collect all plants on farm1
                    for (let x = 0; x <= 152; x += 4) {
                        for (let y = 0; y <= 152; y += 4) {
                            if (!isCloverRunning) break;
                            unsafeWindow.NetUtils.enqueue('collect_product.save_data', {
                                unique_id: ++uniqueId,
                                id: plantId,
                                x: x,
                                y: y,
                                greenhouse_id: 204979,
                                greenhouse_x: x - 1,
                                greenhouse_y: y - 1,
                                qty: 1,
                                automatic: false,
                            });
                        }
                        if (!isCloverRunning) break;
                    }
                    await unsafeWindow.NetUtils.flush();
                    statusEl.textContent = `✅ تم حصاد المزرعة الأولى (${farmType === 'both' ? 'وكلاهما' : ''}) في الدورة ${cycle}.`;
                    if (!isCloverRunning) break;
                    if (unsafeWindow.GF?.loginModel?.addStorageOrDryMachine && unsafeWindow.dry?.TipsType?.BarnNewGoods) {
                        const plantData = unsafeWindow.Config.Store_GetItemData(plantId);
                        let actualHarvestedProductId;
                        if (plantData?.type === 'seeds') {
                            actualHarvestedProductId = plantData?.product || plantId;
                        } else if (plantData?.type === 'trees') {
                            actualHarvestedProductId = plantId + 1;
                        } else {
                            actualHarvestedProductId = plantId;
                        }
                        unsafeWindow.GF.loginModel.addStorageOrDryMachine(actualHarvestedProductId, 1521, unsafeWindow.dry.TipsType.BarnNewGoods);
                        console.log(`✅ تم إضافة حوالي 1521 وحدة من المحصول (ID: ${actualHarvestedProductId}) إلى الحظيرة.`);
                    } else {
                        console.warn('⚠️ دالة إضافة العناصر للحظيرة غير متاحة.');
                    }
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 7000));

                    for (let i = 1; i <= 100; i++) {
                        if (!isCloverRunning) break;
                        await unsafeWindow.NetUtils.enqueue('/Activity/UniversalDrop.save_data', {
                            action: 'getDrop',
                            type: 'seeds',
                            isDouble: false,
                        });
                    }
                    await unsafeWindow.NetUtils.flush();
                    statusEl.textContent = `✅ تم جمع الغنائم من المزرعة الأولى في الدورة ${cycle}.`;
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 7000));
                }

                // --- التبديل للمزرعة الثانية إذا كانت "كلاهما" ---
                if (farmType === 'both') {
                    if (!isCloverRunning) break;
                    await unsafeWindow.GF.loginController.loadFarm(unsafeWindow.snsid, 1);
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 25000));
                }

                // --- حصاد وتلقيح المزرعة الثانية (أو كلاهما) ---
                if (farmType === 'both' || farmType === 'farm2') {
                    if (!isCloverRunning) break;
                    await pollinateAll();
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 7000));

                    for (let x = 0; x <= 152; x += 4) {
                        for (let y = 0; y <= 152; y += 4) {
                            if (!isCloverRunning) break;
                            unsafeWindow.NetUtils.enqueue('collect_product.save_data', {
                                unique_id: ++uniqueId,
                                id: plantId,
                                x: x,
                                y: y,
                                greenhouse_id: 204979,
                                greenhouse_x: x - 1,
                                greenhouse_y: y - 1,
                                qty: 1,
                                automatic: false,
                            });
                        }
                        if (!isCloverRunning) break;
                    }
                    await unsafeWindow.NetUtils.flush();
                    statusEl.textContent = `✅ تم حصاد المزرعة الثانية (${farmType === 'both' ? 'وكلاهما' : ''}) في الدورة ${cycle}.`;
                    if (!isCloverRunning) break;
                    if (unsafeWindow.GF?.loginModel?.addStorageOrDryMachine && unsafeWindow.dry?.TipsType?.BarnNewGoods) {
                        const plantData = unsafeWindow.Config.Store_GetItemData(plantId);
                        let actualHarvestedProductId;
                        if (plantData?.type === 'seeds') {
                            actualHarvestedProductId = plantData?.product || plantId;
                        } else if (plantData?.type === 'trees') {
                            actualHarvestedProductId = plantId + 1;
                        } else {
                            actualHarvestedProductId = plantId;
                        }
                        unsafeWindow.GF.loginModel.addStorageOrDryMachine(actualHarvestedProductId, 1521, unsafeWindow.dry.TipsType.BarnNewGoods);
                        console.log(`✅ تم إضافة حوالي 1521 وحدة من المحصول (ID: ${actualHarvestedProductId}) إلى الحظيرة.`);
                    } else {
                        console.warn('⚠️ دالة إضافة العناصر للحظيرة غير متاحة.');
                    }
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 7000));

                    for (let i = 1; i <= 100; i++) {
                        if (!isCloverRunning) break;
                        await unsafeWindow.NetUtils.enqueue('/Activity/UniversalDrop.save_data', {
                            action: 'getDrop',
                            type: 'seeds',
                            isDouble: false,
                        });
                    }
                    await unsafeWindow.NetUtils.flush();
                    statusEl.textContent = `✅ تم جمع الغنائم من المزرعة الثانية في الدورة ${cycle}.`;
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 7000));
                }

                // --- العودة للمزرعة الأولى إذا كانت "كلاهما" ---
                if (farmType === 'both') {
                    if (!isCloverRunning) break;
                    await unsafeWindow.GF.loginController.loadFarm(unsafeWindow.snsid, 0);
                    if (!isCloverRunning) break;
                    await new Promise(resolve => setTimeout(resolve, 25000));
                }

                statusEl.textContent = `✅ تم الانتهاء من الدورة ${cycle} بنجاح!`;
                cycle++;
                if (!isCloverRunning) break; // Check one last time before starting next cycle
                await new Promise(resolve => setTimeout(resolve, 10000));
            }
            statusEl.textContent = 'تم إيقاف الزراعة التلقائية.';
        } catch (error) {
            statusEl.textContent = '❌ حدث خطأ أثناء التنفيذ: ' + error.message;
            console.error(error);
        } finally {
            isCloverRunning = false; // Ensure state is false on exit
            runButton.disabled = false; // Enable run button
            if (counterDiv) {
                counterDiv.remove(); // Remove counter
                counterDiv = null; // Reset counterDiv
            }
            clearInterval(countdownIntervalId); // Clear any active countdown
        }
    };

    // Helper function to get hive ID based on plant ID (reused from previous code)
    function getHiveId(plantId) {
        const plantGroups = {
            45: [4],
            30126: [30072, 100103, 300003, 204497, 206663, 207903],
            30082: [9117, 5005, 5007, 5003, 5009, 5001, 30078, 200300, 200227, 200424, 201579, 202701, 202896, 204396, 203751, 215633, 218612, 225933],
            201633: [200355, 9411, 201581, 30106, 100103, 202906],
            204241: [203676, 203684, 204159, 204533, 204514, 205006, 206411, 207393, 207406, 208483, 208232, 208106],
            209071: [208186, 205111, 206943, 206898, 208965, 202947, 207855, 208714, 209316],
            201375: [65008, 201037, 200600, 201311, 55005, 200984, 201233, 20102, 9005, 204445, 204835, 212616, 217526, 217924, 208925],
            203693: [203700, 201693, 202171, 202735, 203259, 200537, 202006]
        };

        const numericPlantId = Number(plantId);
        if (isNaN(numericPlantId)) {
            console.warn(`Warning: Invalid plant ID provided to getHiveId: ${plantId}. Returning default 45.`);
            return 45;
        }

        for (const [hiveId, plants] of Object.entries(plantGroups)) {
            if (plants.includes(numericPlantId)) {
                return Number(hiveId);
            }
        }
        return 45; // Default hive ID
    }

    // Modify the event listener for the close button
    div.querySelector('.close-btn').addEventListener('click', () => {
        // Only hide the panel, do not stop the automation
        div.style.display = 'none';
    });

    return div;
}


function createTreeRepeatPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    div.innerHTML = `
        <h3 style="color:#4CAF50;text-align:center;">🌳 تكرار سقاية شجرة</h3>
        <div id="panelInfoTextTree" style="color:white;margin-bottom:10px;">
            جاري تحميل بيانات الأشجار...
        </div>
        <div style="color:white;margin-bottom:10px;">
            ✅ الشرط 1: يجب وضع الشجرة في الموقع <b>(0,0)</b><br>
            ✅ الشرط 2: تأكد من وجود <b>دلو سقاية كافٍ</b> في آلة المزرعة
        </div>

        <div style="margin-bottom: 10px;">
            <button id="selectTreeAt00Btn" style="width:100%;padding:10px;background:#007bff;color:white;border:none;border-radius:5px;">🔍 اكتشاف الشجرة في (0,0)</button>
            <input type="hidden" id="selected_tree_id"> <div id="selectedTreeDisplay" style="color:lightgray; margin-top:5px; text-align:center; font-weight:bold; text-shadow: 0 0 5px rgba(173, 216, 230, 0.7), 0 0 10px rgba(173, 216, 230, 0.5);">
                لا توجد شجرة محددة.
            </div>
        </div>

        <input type="number" id="repeat_count_input" placeholder="🔁 عدد مرات التكرار" style="width:100%;margin-bottom:10px;padding:5px;">

        <div style="color:white;margin-bottom:10px;">
            <label for="bucket_select">اختر نوع الدلو:</label>
            <select id="bucket_select" style="width:100%;padding:5px;background:#34495e;color:white;border:none;border-radius:5px;">
                <option value="super" selected>دلو خارق</option>
                <option value="normal">دلو عادي</option>
            </select>
        </div>

        <button id="runTreeRepeat" style="width:100%;padding:10px;background:#4CAF50;color:white;border:none;border-radius:5px;">🚀 تنفيذ</button>
        <div id="treeRepeatMsg" style="color:white;margin-top:10px;text-align:center;"></div>
        <div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
    `;

    // Get elements
    const selectTreeAt00Btn = div.querySelector('#selectTreeAt00Btn');
    const selectedTreeIdInput = div.querySelector('#selected_tree_id');
    const selectedTreeDisplay = div.querySelector('#selectedTreeDisplay');
    const repeatCountInput = div.querySelector('#repeat_count_input');
    const bucketSelect = div.querySelector('#bucket_select');
    const runButton = div.querySelector('#runTreeRepeat');
    const msgDiv = div.querySelector('#treeRepeatMsg');
    const panelInfoTextTree = div.querySelector('#panelInfoTextTree');

    // Variable to hold our tree list, accessible throughout the panel's scope
    let treeList = [];
let refreshTreeListIntervalId;
let autoUpdateIntervalId = null;
let lastDetectedTreeIdAt00 = null;
let lastTreeStoreAccessFailed = false; // ✅ أضفنا الفلاج هنا

// Function to initialize/update the tree list
function initializeTreeList() {
    if (typeof unsafeWindow !== 'undefined' && unsafeWindow.Config && unsafeWindow.Config.Store) {
        lastTreeStoreAccessFailed = false; // ✅ نعيد الفلاج لو المتجر بقى متاح

        try {
            treeList = Object.values(unsafeWindow.Config.Store)
                .filter(item => item.type === 'trees')
                .map(item => ({
                    id: item.id,
                    name: item.name,
                    growTime: item.collect_in
                }));

            if (treeList.length > 0) {
                console.log(`[Tree Panel] Tree list initialized with ${treeList.length} trees.`);
                if (refreshTreeListIntervalId) {
                    clearInterval(refreshTreeListIntervalId);
                    refreshTreeListIntervalId = null;
                    console.log("[Tree Panel] Stopped refreshing tree list data.");
                    panelInfoTextTree.style.display = 'none'; // Hide the initial loading message
                }
            } else {
                panelInfoTextTree.textContent = "جاري تحميل بيانات الأشجار... (لم يتم العثور على أشجار بعد)";
                console.warn("[Tree Panel] treeList is empty. No items found with type 'trees' yet.");
            }

        } catch (e) {
            panelInfoTextTree.textContent = "خطأ في تحميل بيانات الأشجار. راجع Console.";
            console.error("[Tree Panel] Error initializing treeList from unsafeWindow.Config.Store:", e);
        }

    } else {
        panelInfoTextTree.textContent = "جاري تحميل بيانات الأشجار... (المتجر غير متاح بعد)";
        if (!lastTreeStoreAccessFailed) {
            console.warn("[Tree Panel] unsafeWindow.Config.Store is not accessible yet.");
            lastTreeStoreAccessFailed = true;
        }
    }
}

    // Set up a refresh interval to repeatedly try loading tree data
    refreshTreeListIntervalId = setInterval(initializeTreeList, 1000);

    // Initial call in case data is already available
    initializeTreeList();
let lastMapLoadFailed = false;

    // --- Function to auto-detect tree at (0,0) and update fields ---
   async function autoDetectTreeAt00(isManualClick = false) {
    try {
        const map = await unsafeWindow?.GF?.loginModel?.AppData?.map;
        if (!map || map.length === 0) {
            if (!lastMapLoadFailed) {
                console.warn('❌ (تلقائي) لم يتم تحميل الخريطة بعد، أو أنها فارغة.');
                lastMapLoadFailed = true;
            }

            if (lastDetectedTreeIdAt00 !== null || isManualClick) {
                selectedTreeIdInput.value = '';
                selectedTreeDisplay.textContent = 'لا يوجد شجرة في المنطقة 0,0.';
                selectedTreeDisplay.style.color = 'lightgray';
                selectedTreeDisplay.style.textShadow = '0 0 5px black';
                lastDetectedTreeIdAt00 = null;
            }
            return;
        }

        // ✅ تم تحميل الخريطة، نعيد الفلاج
        lastMapLoadFailed = false;

            const detectedObject = map.find(obj => obj?.x === 0 && obj?.y === 0);

            if (!detectedObject) {
                console.log('❌ (تلقائي) لا يوجد أي كائن في النقطة (0,0).');
                if (lastDetectedTreeIdAt00 !== null || isManualClick) {
                    selectedTreeIdInput.value = '';
                    selectedTreeDisplay.textContent = 'لا يوجد شيئ في المنطقه 0.0.';
                    selectedTreeDisplay.style.color = 'lightgray';
                    selectedTreeDisplay.style.textShadow = '0 0 5px black';
                    lastDetectedTreeIdAt00 = null;
                }
                return;
            }

            const itemData = unsafeWindow?.Config?.Store_GetItemData(detectedObject?.id);

            if (!itemData) {
                console.warn('❌ (تلقائي) لم يتم العثور على بيانات الكائن في (0,0).');
                if (lastDetectedTreeIdAt00 !== null || isManualClick) {
                    selectedTreeIdInput.value = '';
                    selectedTreeDisplay.textContent = 'انقر ليتم الكشف.';
                    selectedTreeDisplay.style.color = 'lightgray';
                    selectedTreeDisplay.style.textShadow = '0 0 5px black';
                    lastDetectedTreeIdAt00 = null;
                }
                return;
            }

            // Check if the detected object is a tree
            if (itemData.type === 'trees') {
                const treeName = itemData.name;
                const treeId = itemData.id;

                if (lastDetectedTreeIdAt00 !== treeId || isManualClick) {
                    selectedTreeIdInput.value = treeId;
                    selectedTreeDisplay.textContent = `${treeName} (ID: ${treeId})`;
                    selectedTreeDisplay.style.color = 'lightgreen';
                    selectedTreeDisplay.style.textShadow = '0 0 5px black';
                    lastDetectedTreeIdAt00 = treeId;

                    console.log(`✅ (تلقائي/يدوي) تم اكتشاف الشجرة في (0,0) وتحديث حقول اللوحة: ${treeName} (ID: ${treeId})`);

                    const name = itemData.name || "❓ غير معروف";
                    const status = detectedObject.under_construction ? "❗ غير مكتمل" : "✅ مكتمل";
                    const materials = detectedObject.currentMaterials || itemData.materials || [];
                    const obtained = detectedObject.obtained_materials || {};

                    const filtered = materials.filter(mat => {
                        const data = unsafeWindow.Config.Store_GetItemData(mat.id);
                        return data?.rp_price < 2;
                    });

                    const ids = [], qtys = [];
                    for (const mat of filtered) {
                        const owned = obtained[mat.id] || 0;
                        const needed = Math.max(mat.qty - owned, 0);
                        if (needed >= 3) {
                            ids.push(mat.id);
                            qtys.push(needed);
                        }
                    }

                    const msg = `
---------------------------{ النقطة 0,0 }-------------------------------
🔹 الاسم = ${name}
🆔 كود = ${detectedObject.id}
📦 الحالة = ${status}
----------------------------{  المواد  }-------------------------------
📌 الأكواد المطلوبة  = ${JSON.stringify(ids)}
📦 الكمية المطلوبة   = ${JSON.stringify(qtys)}
                    `;
                    console.log(msg);
                }
            } else {
                console.warn(`❌ (تلقائي) الكائن في (0,0) ليس شجرة (${itemData.type}).`);
                if (lastDetectedTreeIdAt00 !== null || isManualClick) {
                    selectedTreeIdInput.value = '';
                    selectedTreeDisplay.textContent = 'الكائن في (0,0) ليس شجرة.';
                    selectedTreeDisplay.style.color = 'lightcoral';
                    selectedTreeDisplay.style.textShadow = '0 0 5px black';
                    lastDetectedTreeIdAt00 = null;
                }
            }

        } catch (error) {
            console.error('حدث خطأ أثناء محاولة الكشف التلقائي عن الشجرة في (0,0):', error);
            selectedTreeIdInput.value = '';
            selectedTreeDisplay.textContent = 'حدث خطأ في التحديد.';
            selectedTreeDisplay.style.color = 'lightcoral';
            selectedTreeDisplay.style.textShadow = '0 0 5px black';
            lastDetectedTreeIdAt00 = null;
        }
    }

    selectTreeAt00Btn.addEventListener('click', () => {
        autoDetectTreeAt00(true);
    });

    // --- التعديل هنا لزر الإغلاق ---
    div.querySelector('.close-btn').onclick = () => {
        div.style.display = 'none'; // إخفاء اللوحة

        // مسح بيانات الشجرة المحددة وإعادة تعيينها (هذا ضروري لضمان تحديث جديد عند الفتح)
        selectedTreeIdInput.value = '';
        selectedTreeDisplay.textContent = 'قم بالضغط ليتم اكتشاف الشجرة تلقائيا.';
        selectedTreeDisplay.style.color = 'lightgray';
        selectedTreeDisplay.style.textShadow = '0 0 5px black';
        lastDetectedTreeIdAt00 = null; // إعادة تعيين آخر ID تم اكتشافه

        // إيقاف أي تحديثات تلقائية كانت شغالة
        if (refreshTreeListIntervalId) {
            clearInterval(refreshTreeListIntervalId);
            refreshTreeListIntervalId = null;
            console.log("[Tree Panel] Panel closed, refresh interval cleared.");
        }
        if (autoUpdateIntervalId) {
            clearInterval(autoUpdateIntervalId);
            autoUpdateIntervalId = null;
            console.log("[Tree Panel] Panel closed, auto-update interval cleared.");
        }

        console.log("[Tree Panel] Panel closed and tree detection data reset.");
    };
    // --- نهاية التعديل لزر الإغلاق ---

    runButton.onclick = async () => {
        const treeId = +selectedTreeIdInput.value;
        const repeatCount = +repeatCountInput.value;
        const bucketType = bucketSelect.value;

        if (!treeId || isNaN(treeId) || !repeatCount) {
            return alert("⚠️ يرجى تحديد شجرة أولاً باستخدام زر 'تحديد الشجرة في (0,0)' وإدخال عدد مرات التكرار!");
        }

        msgDiv.textContent = '⏳ جاري التنفيذ...';
        let unique_id = 3000;
        let now = 2780;

        let waterTreeId;
        let waterTreeUsesLeft;
        let waterOperationsPerRepeat;
        const harvestedQuantityPerSingleHarvest = 1;

        if (bucketType === 'normal') {
            waterTreeId = 10004;
            waterTreeUsesLeft = 4211;
            waterOperationsPerRepeat = 4;
        } else {
            waterTreeId = 10005;
            waterTreeUsesLeft = 721;
            waterOperationsPerRepeat = 1;
        }

        const expectedProductId = treeId + 1;

        try {
            for (let i = 0; i < repeatCount; i++) {
                for (let j = 0; j < waterOperationsPerRepeat; j++) {
                    unsafeWindow.NetUtils.enqueue('water_tree.save_data', {
                        id: waterTreeId,
                        uses_left: waterTreeUsesLeft,
                        unique_id,
                        tree_id: treeId,
                        tree_x: 0,
                        tree_y: 0,
                        src: "fusor",
                        needResponse: "water_tree.save_data",
                        cur_sceneid: 1
                    });
                    now += 2;
                    unique_id++;
                }

                const harvestRequestData = {
                    unique_id,
                    id: treeId,
                    x: 0,
                    y: 0,
                    qty: harvestedQuantityPerSingleHarvest,
                    tree_product: expectedProductId,
                    automatic: false,
                    flip: 0,
                    startTime_log: Date.now(),
                    needResponse: "collect_product.save_data",
                    cur_sceneid: 1,
                    achievement_add: `trees_${treeId}_0`
                };
                unsafeWindow.NetUtils.enqueue('collect_product.save_data', harvestRequestData);
                now += 3;
                unique_id++;
            }

            await unsafeWindow.NetUtils.flush();

            if (unsafeWindow.GF?.loginModel?.addStorageOrDryMachine && unsafeWindow.dry?.TipsType?.BarnNewGoods) {
                for (let i = 0; i < repeatCount; i++) {
                    console.log(`[Tree Panel] Adding product ${expectedProductId} with quantity ${harvestedQuantityPerSingleHarvest} to storage (Repeat ${i + 1}/${repeatCount}).`);
                    unsafeWindow.GF.loginModel.addStorageOrDryMachine(
                        expectedProductId,
                        harvestedQuantityPerSingleHarvest,
                        unsafeWindow.dry.TipsType.BarnNewGoods || 0
                    );
                }
                console.log(`✅ تم إضافة إجمالي ${repeatCount * harvestedQuantityPerSingleHarvest} منتج إلى الحظيرة.`);
            } else {
                console.warn("[Tree Panel] دالة إضافة العناصر للحظيرة غير متاحة.");
            }

            msgDiv.textContent = '✅ تم التنفيذ بنجاح!';
div.querySelector('.close-btn').click();
        } catch (err) {
            msgDiv.textContent = '❌ حدث خطأ أثناء التنفيذ!';
            console.error(err);
        }
    };

    document.body.appendChild(div);

    // --- New: Immediately attempt to auto-detect when the panel is created/opened ---
    autoDetectTreeAt00(false); // Call with false as it's not a manual click

    // Start the continuous auto-update only after the panel is added to the DOM and initial detection is attempted
    autoUpdateIntervalId = setInterval(() => {
        autoDetectTreeAt00(false);
    }, 3000);

    // The initial text for selectedTreeDisplay is now handled by autoDetectTreeAt00
    // so these lines are no longer strictly necessary here but don't hurt.
    // selectedTreeDisplay.textContent = 'قم بالضغط ليتم اكتشاف الشجرة تلقائيا.';
    // selectedTreeDisplay.style.color = 'lightgray';
    // selectedTreeDisplay.style.textShadow = '0 0 5px black';

    return div;
}
function createGiftClearPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    div.innerHTML = `
        <h3>🎁 تفريغ الهدايا </h3>
        <div id="signedRequestContainer" style="margin-bottom:30px;">
            <label for="signedRequestInput" style="color:white;">الريكويست:</label><br>
            <input type="text" id="signedRequestInput"
                   style="width:100%;padding:8px;border:1px solid #ccc;border-radius:8px;margin-top:5px;"
                   placeholder="أدخل الريكويست يدوياً" />
        </div>

        <div style="display:flex;flex-direction:column;gap:10px;margin-bottom:15px;">
            <button id="runBoth"
                    style="padding:10px;background:#6f42c1;color:white;border:none;
                           border-radius:8px;cursor:pointer;font-weight:bold;">
                ⚡ تفريغ الكل
            </button>

            <div style="display:flex;justify-content:space-between;gap:10px;">
                <button id="runWishClear"
                        style="padding:10px;background:#17a2b8;color:white;border:none;
                               border-radius:8px;cursor:pointer;font-weight:bold;flex:1;">
                    ارسال
                </button>
                <button id="runGiftClear"
                        style="padding:10px;background:#28a745;color:white;border:none;
                               border-radius:8px;cursor:pointer;font-weight:bold;flex:1;">
                    استلام
                </button>
            </div>
        </div>

        <div id="status" style="margin-top:15px;font-weight:bold;white-space:pre-wrap;color:white;
                               border-top:1px solid #eee;padding-top:10px;"></div>
        <div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
    `;

    // إنشاء عنصر الرسالة العائمة
    const floatingMsg = document.createElement('div');
    floatingMsg.id = 'floatingMessage';
    floatingMsg.style.position = 'fixed';
    floatingMsg.style.top = '20px';
    floatingMsg.style.left = '50%';
    floatingMsg.style.transform = 'translateX(-50%)';
    floatingMsg.style.backgroundColor = 'rgba(0,0,0,0.8)';
    floatingMsg.style.color = 'white';
    floatingMsg.style.padding = '15px 25px';
    floatingMsg.style.borderRadius = '10px';
    floatingMsg.style.zIndex = '9999';
    floatingMsg.style.display = 'none';
    floatingMsg.style.fontWeight = 'bold';
    floatingMsg.style.fontSize = '18px';
    floatingMsg.style.boxShadow = '0 4px 8px rgba(0,0,0,0.3)';
    document.body.appendChild(floatingMsg);

    const sleep = ms => new Promise(resolve => setTimeout(resolve, ms));

    // دالة لعرض الرسالة العائمة
    function showFloatingMessage(msg, duration = 3000) {
        floatingMsg.textContent = msg;
        floatingMsg.style.display = 'block';
        setTimeout(() => {
            floatingMsg.style.display = 'none';
        }, duration);
    }

    // دالة لإضافة كل system كهدية منفصلة
    async function addSystemGiftsIndividually(gifts) {
        try {
            let totalAdded = 0;

            for (const gift of gifts) {
                const giftId = gift.giftid;
                const requestIds = gift.requestIds?.replace(/'/g, "").split(", ") || [];
                const systemRequests = requestIds.filter(id => id.startsWith("system_"));

                for (const requestId of systemRequests) {
                    unsafeWindow.GF.loginModel.addGift(giftId, 1);
                    totalAdded++;
                }
            }

            return totalAdded;
        } catch (e) {
            console.error('حدث خطأ أثناء إضافة الهدايا:', e);
            return 0;
        }
    }

    async function fetchGifts(signedRequest) {
        try {
            const res = await fetch(`https://farm-us.centurygames.com/fbgifts/boxseeMoreGifts/?signed_request=${signedRequest}`);
            const data = await res.json();
            return data?.data?.gifts || [];
        } catch (e) {
            console.error('حدث خطأ أثناء جلب الهدايا:', e);
            return [];
        }
    }

    async function receiveGiftsBatch(batch, signedRequest) {
        try {
            const res = await fetch(`https://farm-us.centurygames.com/fbgifts/receivegifts_batch/?signed_request=${signedRequest}`, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(batch)
            });
            return await res.json();
        } catch (e) {
            console.error('حدث خطأ أثناء استلام الدفعة:', e);
            return {error: e};
        }
    }

    async function clearGifts(signedRequest) {
        const allReceivedGifts = [];
        let totalSystemGifts = 0;

        while (true) {
            const gifts = await fetchGifts(signedRequest);
            if (gifts.length === 0) break;

            // حساب عدد الهدايا System
            gifts.forEach(gift => {
                const requestIds = gift.requestIds?.replace(/'/g, "").split(", ") || [];
                totalSystemGifts += requestIds.filter(id => id.startsWith("system_")).length;
            });

            allReceivedGifts.push(...gifts);

            // تفريغ الهدايا
            const allBatches = gifts.map(gift => ({
                giftId: gift.giftid,
                requestIds: gift.requestIds?.replace(/'/g, "").split(", ") || []
            }));

            const batchSize = 300;
            for (let i = 0; i < allBatches.length; i += batchSize) {
                const batch = allBatches.slice(i, i + batchSize);
                await receiveGiftsBatch(batch, signedRequest);
            }
        }

        // إضافة الهدايا
        const addedCount = await addSystemGiftsIndividually(allReceivedGifts);
        return {totalSystemGifts, addedCount};
    }

    async function fetchWishes(signedRequest) {
        const url = `https://farm-us.centurygames.com/fbgifts/boxseeMoreWishes/?signed_request=${signedRequest}&whatever=1&slot=1&`;
        const res = await fetch(url);
        const json = await res.json();
        return json.data?.wishes || [];
    }

    function buildQueue(wishes) {
        const queue = [];
        for (const wish of wishes) {
            const giftId = wish.giftid;
            const snsids = wish.snsids || [];
            const rawRequestIds = wish.requestIds;

            if (!rawRequestIds || snsids.length === 0) continue;

            const wishids = rawRequestIds
                .split(',')
                .map(id => id.trim().replace(/^'+|'+$/g, ''))
                .filter(id => id.startsWith("system_"));

            if (wishids.length > 0) {
                queue.push({
                    ids: snsids,
                    giftId: giftId,
                    requestId: "",
                    tag: "gift.send",
                    wishids: wishids
                });
            }
        }
        return queue;
    }

    async function sendWishesBatch(queue, signedRequest) {
        const url = "https://farm-us.centurygames.com/fbgifts/sendgift_batch/?signed_request=" + signedRequest;
        const payload = {
            access_token: "",
            queue: queue
        };

        const res = await fetch(url, {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(payload)
        });

        return await res.json();
    }

    async function clearWishes(signedRequest) {
        while (true) {
            const wishes = await fetchWishes(signedRequest);
            if (wishes.length === 0) break;

            const queue = buildQueue(wishes);
            if (queue.length === 0) break;

            const batchSize = 300;
            for (let i = 0; i < queue.length; i += batchSize) {
                const batch = queue.slice(i, i + batchSize);
                await sendWishesBatch(batch, signedRequest);
            }
        }
    }

    async function runBothOperations(signedRequest) {
        // إخفاء الواجهة مباشرة عند البدء
        div.style.display = 'none';
        showFloatingMessage("جاري إرسال الهدايا...");

        await clearWishes(signedRequest);
        showFloatingMessage("جاري إستلام الهدايا...");

        const result = await clearGifts(signedRequest);
         unsafeWindow.ConfirmView?.Show(`✅ تم تفريغ ${result.totalSystemGifts} هدية بنجاح!`, 15000);

    }

    function getSignedRequest() {
        return document.getElementById("signedRequestInput").value.trim();
    }

    div.querySelector("#runGiftClear").addEventListener("click", async () => {
        const signedRequest = getSignedRequest();
        if (!signedRequest) return showFloatingMessage("الرجاء إدخال signed_request");

        div.style.display = 'none';
        showFloatingMessage("جاري تفريغ الهدايا...");

        const result = await clearGifts(signedRequest);
    unsafeWindow.ConfirmView.Show("تم تفريغ صندوق الهدايا بنجاح", "success");
        showFloatingMessage(`✅ تم تفريغ ${result.totalSystemGifts} هدية بنجاح!`, 5000);
    });

    div.querySelector("#runWishClear").addEventListener("click", async () => {
        const signedRequest = getSignedRequest();
        if (!signedRequest) return showFloatingMessage("الرجاء إدخال signed_request");

        div.style.display = 'none';
        showFloatingMessage("جاري تفريغ الأمنيات...");

        await clearWishes(signedRequest);
        showFloatingMessage("✅ تم تفريغ الأمنيات بنجاح!", 5000);
    });

    div.querySelector("#runBoth").addEventListener("click", async () => {
        const signedRequest = getSignedRequest();
        if (!signedRequest) return showFloatingMessage("الرجاء إدخال signed_request");
        await runBothOperations(signedRequest);
    });

    // استخراج signed_request تلقائياً
    try {
        const scripts = Array.from(document.scripts);
        const srScript = scripts.find(script => script.textContent.includes('var sr ='));
        if (srScript) {
            const match = srScript.textContent.match(/var\s+sr\s*=\s*"([^"]+)"/);
            if (match && match[1]) {
                const autoSignedRequest = match[1];
                div.querySelector("#signedRequestInput").value = autoSignedRequest;
                div.querySelector("#signedRequestContainer").style.display = "none";
            }
        }
    } catch (e) {
        console.warn("⚠️ فشل في استخراج signed_request تلقائيًا:", e);
    }

    document.body.appendChild(div);
    return div;
}

// إنشاء الواجهة عند تحميل الصفحة
if (document.readyState === 'complete') {
    createGiftClearPanel();
} else {
    window.addEventListener('load', createGiftClearPanel);
}



// دالة عرض النافذة المطلوبة
function createFarmPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    div.innerHTML = `
        <h3>🌾 فتح جميع المراحل</h3>
        <div style="color:white;margin-bottom:15px;">
            تنفيذ جميع عمليات المزرعة تلقائياً
        </div>
        <button id="runFarm" style="background:linear-gradient(135deg,#28a745,#218838);">
            🚀 بدء التنفيذ
        </button>
        <div id="farmStatus" style="color:white;margin-top:10px;"></div>
        <div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
    `;

    const fixedData = {
        method: "story_start",
        data_hash: "e2c7d5894ac548ad6d3efc6780f3e3ac",
        cur_sceneid: 0,
        base_story_type: "mousefamilyscampingtime"
    };

    const variations = ['a1','a2','a3','b1','b2','b3','c1','c2','c3','d1','d2','d3','e1','e2','e3','f1','f2','f3'];

    div.querySelector('#runFarm').onclick = async () => {
        const statusEl = div.querySelector('#farmStatus');
        statusEl.textContent = '⏳ جاري فتح جميع المراحل...';

        try {
            // تجميع كل الطلبات في queue بدون انتظار بينهم
            variations.forEach((variation, i) => {
                const storyId = 1012773 + (i * 4);
                unsafeWindow.NetUtils.enqueue('story_start', {
                    data_hash: fixedData.data_hash,
                    cur_sceneid: fixedData.cur_sceneid,
                    story_type: fixedData.base_story_type + variation,
                    story_id: storyId
                });
            });

            // تنفيذ كل العمليات دفعة واحدة
            await unsafeWindow.NetUtils.flush();

            statusEl.textContent = '✅ تم تنفيذ جميع العمليات بنجاح!';
        } catch (error) {
            statusEl.textContent = '❌ حدث خطأ أثناء التنفيذ';
            console.error('خطأ في عمليات المزرعة:', error);
        }
    };

    document.body.appendChild(div);
    return div;
}

    function createCardPanel() {
        const types = { 'أخضر': 0x3ACFE, 'أصفر': 0x3ACFF, 'فاخر': 0x3AD00, 'حصري': 0x3AD01, 'مؤقت': 0x3AD02 };
        const div = document.createElement('div');
        div.className = 'dr-panel';
        div.innerHTML = `
            <h3>فتح الكروت</h3>
            <select id="cardType">${Object.entries(types).map(([k, v]) => `<option value="${v}">${k}</option>`)}</select>
            <input type="number" id="cardQty" placeholder="عدد الكروت">
            <button id="runCard">🚀 تنفيذ</button>
            <div id="cardMsg" style="color:white;margin-top:10px;"></div>
<div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
        `;
        div.querySelector('#runCard').onclick = async () => {
            const id = +div.querySelector('#cardType').value;
            const qty = +div.querySelector('#cardQty').value;
            if (!id || !qty) return alert("❌ تحقق من المدخلات");
            div.querySelector('#cardMsg').textContent = '⏳ جاري التنفيذ...';
            await unsafeWindow.NetUtils.request('Activity/AlbumEvent', {
                action: 'useItem', itemId: id, qty: qty.toString(), needResponse: 'Activity/AlbumEvent1'
            });
                unsafeWindow.ConfirmView?.Show("✅ تم فتح الكروت!");
div.querySelector('.close-btn').click();
        };
        document.body.appendChild(div);
        return div;
    }





    function createLinkPanel() {
        const div = document.createElement('div');
        div.className = 'dr-panel';
        div.innerHTML = `
            <h3>فتح الروابط</h3>
            <textarea id="linksArea" rows="5" placeholder="ألصق الروابط هنا..." style="resize: none;"></textarea>
            <button id="launchLinks">🚀 فتح</button>
            <div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
<div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
        `;
        div.querySelector('#launchLinks').onclick = () => {
            const text = div.querySelector('#linksArea').value;
            const links = [...text.matchAll(/https?:\/\/[^\s<>"]+/g)].map(m => m[0]);
            if (!links.length) return alert("⚠️ لا توجد روابط!");
            links.forEach((l, i) => setTimeout(() => window.open(l, "_blank"), i * 300));
        };
        document.body.appendChild(div);
        return div;
    }

function createJuicerPanel() {
    // إنشاء العنصر الأساسي للوحة
    const div = document.createElement('div');
    div.className = 'dr-panel'; // يمكنك إضافة تنسيقات لهذه الفئة في ملف CSS الخاص بك

    div.innerHTML = `
        <div style="font-weight: bold; font-size: 20px; text-align: center; color: #ecf0f1; margin-bottom: 20px;">
            🛠️ أدوات متعددة
        </div>

        <div style="margin-bottom: 15px;">
            <label for="operationSelect" style="display: block; margin-bottom: 8px; font-size: 14px;">اختر العملية:</label>
            <select id="operationSelect" style="width: 100%; padding: 10px; border-radius: 4px; border: 1px solid #34495e; background-color: #34495e; color: white; font-size: 14px;">
                <option value="juicer">🥤 آلة العصير</option>
                <option value="purpleBird">🦜 طائر أرجواني</option>
                <option value="cream">🍦 آلة الكريمة الطازجة</option>
            </select>
        </div>

        <div style="text-align: center; margin-bottom: 20px;">
            <label for="repeats" style="display: block; margin-bottom: 8px; font-size: 14px;">عدد التكرار:</label>
            <input id="repeats" type="number" min="1" value="1" style="width: 80px; padding: 10px; border-radius: 4px; border: 1px solid #34495e; background-color: #34495e; color: white; text-align: center; font-size: 14px;">
        </div>

        <button id="runOperation" style="display: block; margin: 0 auto; padding: 12px 25px; background-color: #27ae60; color: white; border: none; border-radius: 5px; cursor: pointer; font-size: 16px; font-weight: bold; transition: background-color 0.2s ease;">
            🚀 ابدأ العملية
        </button>

        <div class="close-btn" onclick="this.parentElement.style.display='none'" style="position: absolute; top: 10px; right: 10px; color: #ecf0f1; cursor: pointer; font-size: 20px;">✖️</div>
                <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
                <div style="text-align:center;color:#bdc3c7;font-size:12px;margin-top:20px;">👑 بواسطة د.أحمد خالد</div>
        <div id="statusMsg" style="text-align: center; color: #2ecc71; margin-top: 15px; font-size: 14px; display: none;"></div>
    `;

    // إضافة اللوحة إلى جسم المستند
    document.body.appendChild(div);

    const operationSelect = div.querySelector('#operationSelect');
    const repeatsInput = div.querySelector('#repeats');
    const runButton = div.querySelector('#runOperation');
    const statusMsg = div.querySelector('#statusMsg');

    runButton.onclick = async () => {
        const selectedOperation = operationSelect.value;
        const repeats = +repeatsInput.value;

        if (!repeats || repeats < 1) {
            alert("⚠️ يجب تحديد عدد التكرار الصحيح (أكبر من صفر)!");
            return;
        }

        statusMsg.textContent = '⏳ جاري التنفيذ...';
        statusMsg.style.display = 'block';
        statusMsg.style.color = '#2ecc71'; // لون أخضر للفشل

        try {
            let unique_id = Date.now();

            for (let i = 0; i < repeats; i++) {
                if (selectedOperation === 'juicer') {
                    // آلة العصير
                    unsafeWindow.NetUtils.enqueue('add_object.save_data', {
                        unique_id, id: 0x30F11, x: 0, y: 0, flip: 0, is_storage: false, is_gift: false, is_circle: false, daily_limit: false
                    });
                    for (let j = 0; j < 5; j++) {
                        unsafeWindow.NetUtils.enqueue('use_gift.save_data', {
                            id: 0x2584, target_id: 0x30F11, target_x: 0, target_y: 0
                        });
                    }
                    for (let j = 0; j < 5; j++) {
                        unsafeWindow.NetUtils.enqueue('use_gift.save_data', {
                            id: 0x2585, target_id: 0x30F11, target_x: 0, target_y: 0
                        });
                    }
                    unsafeWindow.NetUtils.enqueue('remove_object.save_data', {
                        id: 0x30F11, x: 0, y: 0, flip: 0
                    });

                } else if (selectedOperation === 'purpleBird') {
                    // طائر أرجواني
                    unsafeWindow.NetUtils.enqueue('add_object.save_data', {
                        unique_id, id: 0x30FA3, x: 0, y: 0, flip: 0, is_storage: false, is_gift: false, is_circle: false, daily_limit: false
                    });
                    for (let j = 0; j < 5; j++) {
                        unsafeWindow.NetUtils.enqueue('use_gift.save_data', {
                            id: 0x30FA2, target_id: 0x30FA3, target_x: 0, target_y: 0
                        });
                    }
                    unsafeWindow.NetUtils.enqueue('remove_object.save_data', {
                        id: 0x30FA3, x: 0, y: 0, flip: 0
                    });

                } else if (selectedOperation === 'cream') {
                    // آلة الكريمة الطازجة
                    unsafeWindow.NetUtils.enqueue('add_object.save_data', {
                        unique_id, id: 0x33E51, x: 0, y: 0, flip: 0, is_storage: false, is_gift: false, is_circle: false, daily_limit: false
                    });
                    unsafeWindow.NetUtils.enqueue('finish_invite_object.save_data', {
                        id: 0x33E51, x: 0, y: 0, flipped: 0, needResponse: "finish_invite_object.save_data", cur_sceneid: 1
                    });
                    unsafeWindow.NetUtils.enqueue('finish_spend_rp_object.save_data', {
                        target_id: 0x33E51, target_x: 0, target_y: 0, target_scene: 1, type: "materials", needResponse: "finish_spend_rp_object.save_data", cur_sceneid: 1
                    });
                    unsafeWindow.NetUtils.enqueue('remove_object.save_data', {
                        id: 0x33E51, x: 0, y: 0, flip: 0
                    });
                }
                unique_id++;
            }

            await unsafeWindow.NetUtils.flush();
            statusMsg.textContent = '✅ تم التنفيذ بنجاح !';
            statusMsg.style.color = '#2ecc71'; // لون أخضر للنجاح

        } catch (error) {
            console.error('حدث خطأ أثناء التنفيذ:', error);
            statusMsg.textContent = '⚠️ حدث خطأ أثناء التنفيذ.';
            statusMsg.style.color = '#e74c3c'; // لون أحمر للخطأ
        }
    };

    return div;
}

function createTokenPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    div.innerHTML = `
        <h3>🎯 مشاركة الروابط (المهمات)</h3>
        <select id="missionSelect" style="margin-bottom:10px;">
            <option value="CruiseVacationFilm">مكسل اكتب اسمها</option>
            <option value="MysticTreasureHunt">مهمة الكنز الغامض</option>
            <option value="PinballGame">مهمة بلينكو</option>
            <option value="MysteryShopKeeper">مهمة التاجر</option>
        </select>
        <textarea id="ssidInput" placeholder="ssid1        ولوحبيت تكتب اسم جمبه(اختياري)
ssid2        ولوحبيت تكتب اسم جمبه(اختياري)
ssid3        ولوحبيت تكتب اسم جمبه(اختياري)"
            style="width: 100%; height: 100px; margin-top: 8px; resize: vertical;"></textarea>
        <div style="display: flex; gap: 8px; margin-top: 10px;">
            <button id="sendBtn">📤 إرسال</button>
            <button id="receiveBtn">📥 استقبال</button>
        </div>
        <div id="loadingSpinner" style="display:none;margin-top:10px;color:white;">🔄 جاري المعالجة...</div>
        <div id="resultMessage" style="margin-top:12px;color:white;font-weight:bold;white-space:pre-wrap;"></div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 سكريبت ميجا</div>
        <div style="text-align:center;color:white;font-size:14px;margin-top:10px;">👑 بواسطة د.أحمد خالد</div>
        <div class="close-btn" onclick="this.parentElement.style.display='none'">✖️</div>
    `;
    document.body.appendChild(div);

    const missionNames = {
        PinballGame: "مهمة بلينكو",
        MysteryShopKeeper: "مهمة التاجر",
StoneForestRuinsEncounter:"مهمة لقاء الانقاض"

    };

    const sleep = ms => new Promise(r => setTimeout(r, ms));

    async function handleAction(actionType) {
        const input = div.querySelector('#ssidInput').value.trim();
        const activity = div.querySelector('#missionSelect').value;
        const spinner = div.querySelector('#loadingSpinner');
        const resultMsg = div.querySelector('#resultMessage');
        resultMsg.textContent = '';
        resultMsg.style.color = 'white';

        if (!input || !activity) {
            resultMsg.style.color = 'red';
            resultMsg.textContent = "⚠️ من فضلك أدخل SSID واختر اسم المهمة";
            return;
        }

        const ssids = input.split('\n')
            .map(line => line.trim().match(/\d+/))
            .filter(Boolean)
            .map(match => match[0]);

        if (ssids.length === 0) {
            resultMsg.style.color = 'red';
            resultMsg.textContent = "⚠️ من فضلك أدخل SSID صحيح في كل سطر";
            return;
        }

        spinner.style.display = 'block';

        try {
            for (const ssid of ssids) {
                await unsafeWindow.NetUtils.request('Activity/SharingToken', {
                    action: actionType,
                    activity,
                    [`${actionType === 'send' ? 'to' : 'from'}Snsids`]: [ssid],
                    needResponse: actionType === 'send' ? 'Activity/SharingToken' : 'Activity/SharingToken3',
                    ...(actionType === 'accept' ? { opTime: 1011.327 } : { cur_sceneid: 2 })
                });
                await sleep(0);
            }
            resultMsg.style.color = '#0f0';
            resultMsg.textContent = `✅ تم ${actionType === 'send' ? 'إرسال' : 'استقبال'} العملات لـ (${missionNames[activity] || activity}) بنجاح!\nعدد الارسالات: ${ssids.length}`;
        } catch (e) {
            console.error(`${actionType === 'send' ? 'فشل الإرسال' : 'فشل الاستقبال'}:`, e);
            resultMsg.style.color = 'red';
            resultMsg.textContent = `❌ فشل تنفيذ العملية: ${e.message || e}`;
        } finally {
            spinner.style.display = 'none';
        }
    }

    div.querySelector('#sendBtn').onclick = () => handleAction('send');
    div.querySelector('#receiveBtn').onclick = () => handleAction('accept');

    return div;
}
// دالة إنشاء لوحة إرسال الهدايا
function createGiftSenderPanel() {
    const div = document.createElement('div');
    div.className = 'dr-panel';
    div.innerHTML = `
        <h3 style="margin-bottom: 10px; color: black;">🎁 إرسال هدية أو أمنية للجيران</h3>

        <div style="color:black; margin-bottom: 15px;">
            استخدم الأزرار أدناه لإرسال <b style="color:#28a745">هدية خاصة</b> أو <b style="color:#007bff">طلب Wish</b> أو <b style="color:#ffc107">هدية بكود</b> لجميع الجيران دفعة واحدة.
        </div>

        <div id="neighborCount" style="color:black; margin-bottom: 10px;">انتظر جاري جلب الجيران...</div>
        <input type="text" id="signedRequestInput" style="width:100%; display:none;" />

        <!-- 🎁 هدية خاصة -->
        <div style="border:1px solid #28a745; border-radius:8px; padding:10px; margin-bottom:15px;">
            <h4 style="color:black;">🎁 إرسال هدية خاصة (Gift ID ثابت)</h4>
            <button id="runGiftSender" style="width:100%; background:linear-gradient(135deg,#28a745,#218838); padding:8px; border:none; border-radius:5px; color:white; font-size:15px; display:none;">🚀 إرسال الهدية الخاصة</button>
        </div>

        <!-- 💫 طلب Wish -->
        <div style="border:1px solid #007bff; border-radius:8px; padding:10px; margin-bottom:15px;">
            <h4 style="color:black;">💫 طلب هدية بكود معين</h4>
            <input type="number" id="wishGiftIdInput" placeholder="أدخل كود الهدية" style="width:100%; padding:6px; margin-bottom:10px; border-radius:4px; border:1px solid #ccc; display:none;" />
            <button id="runWishSender" style="width:100%; background:linear-gradient(135deg,#007bff,#0056b3); padding:8px; border:none; border-radius:5px; color:white; font-size:15px; display:none;">💫 طلب الهدية</button>
        </div>

        <!-- 📦 إرسال بكود -->
        <div style="border:1px solid #ffc107; border-radius:8px; padding:10px;">
            <h4 style="color:black;">📦 إرسال هدية بكود معين</h4>
            <input type="number" id="giftIdInput" placeholder="أدخل كود الهدية" style="width:100%; padding:6px; margin-bottom:10px; border-radius:4px; border:1px solid #ccc; display:none;" />
            <button id="runGiftIdSender" style="width:100%; background:linear-gradient(135deg,#ffc107,#cc9a06); padding:8px; border:none; border-radius:5px; color:black; font-size:15px; display:none;">📦 إرسال الهدية بالكود</button>
        </div>

        <div id="giftSenderStatus" style="color:black; margin-top:15px;"></div>
        <div class="close-btn" onclick="this.parentElement.style.display='none'" style="position:absolute; top:10px; right:10px; cursor:pointer; color:black;">✖️</div>
        <div style="text-align:center; color:black; font-size:14px; margin-top:15px;">👑 سكريبت ميجا</div>
        <div style="text-align:center; color:black; font-size:14px;">👑 بواسطة د.أحمد خالد</div>
    `;

    function chunkArray(arr, size) {
        const chunks = [];
        for (let i = 0; i < arr.length; i += size) chunks.push(arr.slice(i, i + size));
        return chunks;
    }

    function getAllNeighbors() {
        return unsafeWindow.GF?.friendsController?.model?.backendFriendsData?.neighbors || [];
    }

    function updateNeighborCountAndButton() {
        const neighbors = getAllNeighbors();
        const hasNeighbors = neighbors.length > 0;
        div.querySelector('#neighborCount').textContent = hasNeighbors ? `عدد الجيران: ${neighbors.length}` : 'جاري جلب عدد الجيران...';
        ['#runGiftSender', '#runWishSender', '#runGiftIdSender', '#wishGiftIdInput', '#giftIdInput'].forEach(sel => {
            div.querySelector(sel).style.display = hasNeighbors ? 'block' : 'none';
        });
        return hasNeighbors;
    }

    async function sendGifts(signedRequest) {
        const uids = getAllNeighbors().map(n => n.uid);
        const batches = chunkArray(uids, 45);
        const status = div.querySelector('#giftSenderStatus');
        let sent = 0;
        for (let i = 0; i < batches.length; i++) {
            status.textContent = `⏳ إرسال هدية خاصة... ${i + 1}/${batches.length}`;
            try {
                const res = await fetch(`https://farm-us.centurygames.com/ar/fbgifts/sendgift_batch/?signed_request=${signedRequest}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ access_token: "", queue: [{ giftId: 29999, newgift: 1, requestId: "", ids: batches[i], tag: "gift.sendNew" }] })
                });
                const json = await res.json();
                if (json.success) sent += batches[i].length;
            } catch {}
        }
        status.textContent = `✅ تم إرسال ${sent} هدية خاصة.`;
    }

    async function sendWishes(signedRequest) {
        const giftId = div.querySelector('#wishGiftIdInput').value.trim();
        if (!giftId) return div.querySelector('#giftSenderStatus').textContent = '⚠️ أدخل كود الهدية للـ Wish';
        const uids = getAllNeighbors().map(n => n.uid);
        const batches = chunkArray(uids, 45);
        const status = div.querySelector('#giftSenderStatus');
        let sent = 0;
        for (let i = 0; i < batches.length; i++) {
            status.textContent = `💫 إرسال Wish... ${i + 1}/${batches.length}`;
            try {
                const form = new URLSearchParams();
                form.append('giftid', giftId);
                batches[i].forEach(uid => form.append('ids[]', uid));
                form.append('signed_request', signedRequest);
                const res = await fetch(`https://farm-us.centurygames.com/ar/fbgifts/sendwish/`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
                    body: form.toString()
                });
                const json = await res.json();
                if (json.rs === "success") sent += batches[i].length;
            } catch {}
        }
        status.textContent = `✅ تم إرسال Wish لـ ${sent} جار.`;
    }

    async function sendGiftWithCode(signedRequest) {
        const giftId = div.querySelector('#giftIdInput').value.trim();
        if (!giftId) return div.querySelector('#giftSenderStatus').textContent = '⚠️ أدخل كود الهدية';
        const uids = getAllNeighbors().map(n => n.uid);
        const batches = chunkArray(uids, 45);
        const status = div.querySelector('#giftSenderStatus');
        let sent = 0;
        for (let i = 0; i < batches.length; i++) {
            status.textContent = `📦 إرسال هدية بكود... ${i + 1}/${batches.length}`;
            try {
                const form = new URLSearchParams();
                form.append('giftid', giftId);
                batches[i].forEach(uid => form.append('ids[]', uid));
                form.append('signed_request', signedRequest);
                const res = await fetch(`https://farm-us.centurygames.com/ar/fbgifts/sendgift/`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
                    body: form.toString()
                });
                const json = await res.json();
                if (json.rs === "success") sent += batches[i].length;
            } catch {}
        }
        status.textContent = `✅ تم إرسال ${sent} هدية بالكود.`;
    }

    // استخراج signed_request تلقائيًا
    try {
        const scripts = [...document.scripts];
        const srScript = scripts.find(s => s.textContent.includes('var sr ='));
        if (srScript) {
            const match = srScript.textContent.match(/var\s+sr\s*=\s*"([^"]+)"/);
            if (match?.[1]) div.querySelector('#signedRequestInput').value = match[1];
        }
    } catch (e) { console.log('فشل استخراج signed_request'); }

    const checkInterval = setInterval(() => {
        if (updateNeighborCountAndButton()) clearInterval(checkInterval);
    }, 300);

    div.addEventListener('click', updateNeighborCountAndButton);

    div.querySelector('#runGiftSender').onclick = () => {
        const sr = div.querySelector('#signedRequestInput').value.trim();
        if (!sr) return div.querySelector('#giftSenderStatus').textContent = '⚠️ لم يتم العثور على signed_request';
        sendGifts(sr);
    };

    div.querySelector('#runWishSender').onclick = () => {
        const sr = div.querySelector('#signedRequestInput').value.trim();
        if (!sr) return div.querySelector('#giftSenderStatus').textContent = '⚠️ لم يتم العثور على signed_request';
        sendWishes(sr);
    };

    div.querySelector('#runGiftIdSender').onclick = () => {
        const sr = div.querySelector('#signedRequestInput').value.trim();
        if (!sr) return div.querySelector('#giftSenderStatus').textContent = '⚠️ لم يتم العثور على signed_request';
        sendGiftWithCode(sr);
    };

    document.body.appendChild(div);
    return div;
}

// ---

// دالة بدء تشغيل لوحة إرسال الهدايا بأمان بعد تحميل كائنات اللعبة
function initializeGiftSenderPanelSafely() {
    // التحقق من وجود كائنات اللعبة الضرورية
    if (unsafeWindow.GF &&
        unsafeWindow.GF.friendsController &&
        unsafeWindow.GF.friendsController.model) { // لا نحتاج backendFriendsData هنا بعد الآن

        // إذا كانت الكائنات موجودة، قم بإنشاء اللوحة.
        // دالة createGiftSenderPanel نفسها ستتولى أمر تحديث الجيران والزر الآن.
        createGiftSenderPanel();
        console.log("Gift Sender Panel Initialized Successfully.");
    } else {
        // إذا لم يتم تحميل الكائن بعد، حاول مرة أخرى بعد تأخير
        setTimeout(initializeGiftSenderPanelSafely, 10); // يمكننا استخدام 500ms هنا
    }
}

// ابدأ عملية التحقق والتنفيذ
initializeGiftSenderPanelSafely();

})();

