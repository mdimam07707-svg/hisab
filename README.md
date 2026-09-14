<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="theme-color" content="#F6F1E9">
<meta name="admob-app-id" content="ca-app-pub-7394143721524256~3959612609">
<title>হিসাব — Hisab</title>
<script src="https://cdn.tailwindcss.com"></script>
<script>
tailwind.config={theme:{extend:{colors:{cream:'#F6F1E9',ink:'#2B2620',muted:'#918A7C',clay:'#E8724C',clay2:'#F5905F',sage:'#3F9A6E',berry:'#D65B57',sand:'#EDE6D8',plum:'#7C5CBF',tealx:'#157E8E'},fontFamily:{sans:['"Plus Jakarta Sans"','sans-serif']}}}}
</script>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
body{font-family:'Plus Jakarta Sans',sans-serif;background:#F6F1E9}
.page{display:none}.page.active{display:block;animation:pageIn .3s ease}
@keyframes pageIn{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:none}}
[id$="-modal"]>div{animation:pop .22s ease}
@keyframes pop{from{opacity:0;transform:translateY(26px) scale(.98)}to{opacity:1;transform:none}}
.card{background:#FFF;border:1px solid rgba(43,38,32,.06);box-shadow:0 6px 20px rgba(43,38,32,.05)}
.hero-card{background:linear-gradient(160deg,#E8724C,#F5905F);box-shadow:0 14px 30px rgba(232,114,76,.35)}
.icon-well{background:#F6F1E9}
.btn-primary{background:#2B2620;color:#F6F1E9}
[data-logo]{filter:drop-shadow(0 5px 12px rgba(21,126,142,.35))}
.filter-tab{background:#FFF;color:#918A7C;border:1px solid rgba(43,38,32,.08)}
.filter-tab.active{background:#2B2620;color:#F6F1E9;border-color:#2B2620}
.sum-tab.active{background:#E8724C!important;color:#fff!important;border-color:#E8724C!important}
.nav-btn.active{background:rgba(255,255,255,.12);color:#F5905F}
.lang-pill{background:#2B2620;color:#F6F1E9;border-radius:999px;font-weight:700;font-size:11px;padding:6px 10px;border:none}
.hdr-icon{width:38px;height:38px;border-radius:14px;display:flex;align-items:center;justify-content:center}
.accordion-body{max-height:0;overflow:hidden;transition:max-height .3s ease}.accordion-body.open{max-height:2400px}
.chev{transition:transform .2s ease}.chev.open{transform:rotate(180deg)}
::-webkit-scrollbar{width:4px;height:4px}::-webkit-scrollbar-thumb{background:#DCD3C0;border-radius:10px}
input:focus,select:focus{outline:none}
svg.icon{display:inline-block;vertical-align:middle}
#toast{position:fixed;bottom:95px;left:50%;transform:translateX(-50%);z-index:999;transition:opacity .3s;opacity:0;pointer-events:none}
#toast.show{opacity:1}
input:disabled{opacity:.55;cursor:not-allowed}
.bar-wrap{display:flex;align-items:flex-end;gap:2px;height:70px}
.bar-col{flex:1;display:flex;flex-direction:column;justify-content:flex-end;gap:1px}
.budget-bar{height:10px;border-radius:99px;background:#EDE6D8;overflow:hidden}
.budget-fill{height:100%;border-radius:99px;background:#3F9A6E;transition:width .4s ease}
#admob-banner{display:none;position:fixed;bottom:74px;left:0;right:0;z-index:25;justify-content:center;pointer-events:none}
[id$="-modal"]{-webkit-overflow-scrolling:touch}
body.dark{background:#171310}
body.dark .card{background:#221D18;border-color:rgba(255,255,255,.07)}
body.dark .icon-well{background:#2B241E}
body.dark .text-ink{color:#F1EAE0!important}
body.dark .text-muted{color:#A79E8F!important}
body.dark .bg-cream{background:#2B241E!important;color:#F1EAE0}
body.dark .bg-cream\/95{background:rgba(23,19,16,.95)!important}
body.dark .bg-sand{background:#332B23!important}
body.dark .filter-tab{background:#221D18;color:#A79E8F;border-color:rgba(255,255,255,.09)}
body.dark .filter-tab.active{background:#F1EAE0;color:#2B2620}
body.dark .budget-bar{background:#332B23}
body.dark #toast{background:#F1EAE0;color:#2B2620}
body.dark input,body.dark select{color:#F1EAE0}
@media print{body *{visibility:hidden}#report-print-area,#report-print-area *{visibility:visible}#report-modal{position:fixed;inset:0;background:#fff!important}#report-print-area{position:absolute;left:0;top:0;width:100%;box-shadow:none!important;border:none!important}.no-print{display:none!important}}
@page{size:A4;margin:14mm}
</style>
</head>
<body class="text-ink min-h-screen flex flex-col selection:bg-clay selection:text-white">

<div id="app-root">

<!-- PAGE 1 : হোম -->
<div id="page-home" class="page active">
<header class="sticky top-0 z-40 px-4 pt-4 pb-3 bg-cream/95 backdrop-blur-sm flex justify-between items-center">
  <div class="w-11 h-11 shrink-0" data-logo></div>
  <div class="flex items-center gap-2">
    <button onclick="openReport()" title="প্রিন্ট / PDF" class="hdr-icon card text-ink"><span data-icon="printer" class="w-4 h-4"></span></button>
    <button onclick="openSaveFiles()" title="ডাউনলোড / সেভ" class="hdr-icon card text-clay"><span data-icon="download" class="w-4 h-4"></span></button>
    <select id="lang-top" onchange="setLanguage(this.value)" class="lang-pill"><option value="bn">🇧🇩 বাংলা</option><option value="en">🇬🇧 EN</option><option value="ar">🇸🇦 AR</option><option value="zh">🇨🇳 中</option></select>
  </div>
</header>

<main class="flex-grow container mx-auto px-5 py-3 max-w-md space-y-5 pb-6">
  <section onclick="openProfile()" class="card rounded-3xl p-4 flex items-center gap-3.5 cursor-pointer">
    <img id="summary-avatar" src="" class="w-16 h-16 rounded-2xl object-cover border-2 border-cream bg-sand">
    <div class="flex-1 min-w-0"><h2 id="summary-name" class="text-sm font-extrabold truncate">আপনার নাম</h2><p id="summary-bio" class="text-[11px] text-muted truncate">পরিচিতি যোগ করুন</p><p id="summary-phone" class="text-[11px] text-muted truncate"></p></div>
    <span class="w-9 h-9 rounded-xl icon-well flex items-center justify-center text-clay shrink-0" data-icon="pencil"></span>
  </section>

  <section class="card rounded-3xl p-5">
    <div class="flex items-center gap-2 mb-1"><div class="w-7 h-7 rounded-lg icon-well flex items-center justify-center text-clay"><span data-icon="clipboard" class="w-4 h-4"></span></div><h3 class="text-xs font-bold flex-1" data-i18n="sixSum">৬ মাসের সামারি</h3><span id="visual-period" class="text-[10px] font-bold text-clay bg-cream px-2.5 py-1 rounded-full"></span></div>
    <div class="flex items-center gap-4 mt-2"><div id="donut-box" class="shrink-0"></div><div id="donut-legend" class="flex-1 space-y-1.5 text-[11px]"></div></div>
    <div class="flex justify-between border-t border-black/10 mt-3 pt-2.5"><span class="text-[11px] font-semibold text-muted" data-i18n="balanceL">ব্যালেন্স</span><b id="visual-balance" class="text-sm text-clay"></b></div>
  </section>

  <section class="card rounded-3xl p-5">
    <h3 class="text-xs font-bold mb-3" data-i18n="trend">মাসভিত্তিক ধারা (শেষ ৬ মাস)</h3>
    <div id="bars-box" class="bar-wrap"></div><div id="bars-labels" class="flex gap-2 mt-1.5"></div>
    <div class="flex gap-4 mt-3 text-[10px] text-muted"><span class="flex items-center gap-1"><i class="w-2.5 h-2.5 rounded-full inline-block" style="background:#3F9A6E"></i><span data-i18n="income">আয়</span></span><span class="flex items-center gap-1"><i class="w-2.5 h-2.5 rounded-full inline-block" style="background:#D65B57"></i><span data-i18n="expense">ব্যয়</span></span></div>
  </section>

  <section>
    <div class="flex justify-between items-center mb-3"><h3 class="text-xs font-bold" data-i18n="quick">দ্রুত ক্যাটাগরি এড</h3><button onclick="openCategoriesModal()" class="text-[11px] font-semibold text-clay" data-i18n="viewAll">সব ক্যাটাগরি দেখুন</button></div>
    <div id="quick-grid-home" class="grid grid-cols-4 gap-2.5"></div>
  </section>
</main>
</div>

<!-- PAGE 2 : সব হিসাব -->
<div id="page-hisab" class="page">
<header class="sticky top-0 z-40 px-4 pt-4 pb-3 bg-cream/95 backdrop-blur-sm flex justify-between items-center">
  <div class="flex items-center gap-2.5">
    <div class="w-9 h-9 shrink-0" data-logo></div>
    <h1 class="text-base font-extrabold" data-i18n="accounts">সব হিসাব</h1>
  </div>
  <div class="flex items-center gap-2">
    <button onclick="openReport()" class="hdr-icon card text-ink"><span data-icon="printer" class="w-4 h-4"></span></button>
    <button onclick="openSaveFiles()" class="hdr-icon card text-clay"><span data-icon="download" class="w-4 h-4"></span></button>
  </div>
</header>
<main class="flex-grow container mx-auto px-5 py-2 max-w-md space-y-6 pb-4">
  <section class="hero-card rounded-[28px] p-6 relative overflow-hidden text-white">
    <div class="absolute -right-8 -top-10 w-36 h-36 bg-white/10 rounded-full"></div>
    <span class="text-[11px] font-semibold uppercase tracking-wide text-white/80" data-i18n="balance">মোট ব্যালেন্স</span>
    <h2 id="total-balance" class="text-4xl font-extrabold my-1.5">৳ 0</h2>
    <div class="grid grid-cols-2 gap-4 pt-4 border-t border-white/20 mt-4">
      <div><p class="text-[11px] text-white/75 flex items-center gap-1"><span data-icon="arrow-down" class="w-2.5 h-2.5"></span> <span data-i18n="income">আয়</span></p><p id="total-income" class="text-base font-bold">৳ 0</p></div>
      <div><p class="text-[11px] text-white/75 flex items-center gap-1"><span data-icon="arrow-up" class="w-2.5 h-2.5"></span> <span data-i18n="expense">ব্যয়</span></p><p id="total-expense" class="text-base font-bold">৳ 0</p></div>
    </div>
  </section>
  <div id="reminder-box" class="hidden card rounded-2xl p-4 border-l-[3px] border-l-clay">
    <div class="flex items-center gap-2 mb-1"><span class="w-6 h-6 rounded-lg icon-well flex items-center justify-center text-clay"><span data-icon="bell" class="w-3.5 h-3.5"></span></span><b class="text-xs">🔔 <span data-i18n="stNotif">রিমাইন্ডার</span></b></div>
    <p id="reminder-text" class="text-[11px] text-muted leading-relaxed"></p>
  </div>
  <section class="card rounded-3xl p-4">
    <h3 class="text-xs font-bold mb-2.5" data-i18n="summary">সামারি</h3>
    <div id="summary-tabs" class="grid grid-cols-2 gap-2 mb-3">
      <button onclick="setPeriod('month',this)" class="filter-tab sum-tab active text-[11px] font-semibold px-2 py-2 rounded-xl" data-i18n="thisMonth">এই মাস</button>
      <button onclick="setPeriod('h1',this)" class="filter-tab sum-tab text-[11px] font-semibold px-2 py-2 rounded-xl" data-i18n="h1">ফেব্রুয়ারি–জুলাই (৬ মাস)</button>
      <button onclick="setPeriod('h2',this)" class="filter-tab sum-tab text-[11px] font-semibold px-2 py-2 rounded-xl" data-i18n="h2">জুলাই–ফেব্রুয়ারি (৬ মাস)</button>
      <button onclick="setPeriod('year',this)" class="filter-tab sum-tab text-[11px] font-semibold px-2 py-2 rounded-xl" data-i18n="year">১ বছর</button>
    </div>
    <div id="summary-body" class="text-xs"></div>
  </section>
  <section id="budget-box" class="hidden card rounded-3xl p-4">
    <div class="flex justify-between items-center mb-2"><b class="text-xs">🎯 <span data-i18n="stBudget">মাসিক বাজেট</span></b><span id="budget-pct" class="text-[10px] font-bold text-clay bg-cream px-2 py-0.5 rounded-full"></span></div>
    <div class="budget-bar"><div id="budget-fill" class="budget-fill" style="width:0%"></div></div>
    <p id="budget-info" class="text-[10px] text-muted mt-2"></p>
  </section>
  <section>
    <div class="flex justify-between items-center mb-3"><h3 class="text-xs font-bold" data-i18n="quick">দ্রুত ক্যাটাগরি</h3><button onclick="openCategoriesModal()" class="text-[11px] font-semibold text-clay" data-i18n="viewAll">সব ক্যাটাগরি দেখুন</button></div>
    <div id="quick-grid-hisab" class="grid grid-cols-4 gap-2.5"></div>
  </section>
  <section class="card rounded-3xl p-4 border-l-[3px] border-l-clay">
    <div class="flex justify-between items-center mb-2"><div class="flex items-center gap-2"><div class="w-7 h-7 rounded-lg icon-well flex items-center justify-center text-clay"><span data-icon="coins" class="w-4 h-4"></span></div><h3 class="text-xs font-bold" data-i18n="loanSec">ঋণ ও পরিশোধ</h3></div><button onclick="openAddModal('','debt')" class="text-[11px] font-semibold text-clay">+ <span data-i18n="loan">ঋণ</span></button></div>
    <div id="loan-list" class="space-y-2"></div>
  </section>
  <section class="card rounded-3xl p-4 border-l-[3px] border-l-plum">
    <div class="flex justify-between items-center mb-2"><div class="flex items-center gap-2"><div class="w-7 h-7 rounded-lg icon-well flex items-center justify-center text-plum"><span data-icon="hand" class="w-4 h-4"></span></div><h3 class="text-xs font-bold" data-i18n="paonaSec">পাওনা আদায়</h3></div><button onclick="openAddModal('','paona')" class="text-[11px] font-semibold text-plum">+ <span data-i18n="paona">পাওনা</span></button></div>
    <div id="paona-list" class="space-y-2"></div>
  </section>
  <section class="card rounded-2xl p-4 border-l-[3px] border-l-clay">
    <div class="flex items-center space-x-2.5 mb-1.5"><div class="w-7 h-7 rounded-lg icon-well flex items-center justify-center text-clay"><span data-icon="sparkles" class="w-4 h-4"></span></div><h4 class="text-xs font-bold" data-i18n="advisor">স্মার্ট অ্যানালাইজার</h4></div>
    <p id="ai-advice-text" class="text-xs text-muted leading-relaxed"></p>
  </section>
  <section>
    <div class="flex justify-between items-center mb-3"><h3 class="text-xs font-bold" data-i18n="recent">সাম্প্রতিক লেনদেন (ট্যাপ = বিস্তারিত)</h3><button onclick="clearAllData()" class="text-xs text-berry font-semibold" data-i18n="clear">সব মুছুন</button></div>
    <div id="filter-tabs" class="flex gap-2 mb-3 overflow-x-auto pb-1">
      <button onclick="setFilter('all',this)" class="filter-tab active text-[11px] font-semibold px-3 py-1.5 rounded-full shrink-0" data-i18n="all">সব</button>
      <button onclick="setFilter('income',this)" class="filter-tab text-[11px] font-semibold px-3 py-1.5 rounded-full shrink-0" data-i18n="income">আয়</button>
      <button onclick="setFilter('expense',this)" class="filter-tab text-[11px] font-semibold px-3 py-1.5 rounded-full shrink-0" data-i18n="expense">ব্যয়</button>
      <button onclick="setFilter('debt',this)" class="filter-tab text-[11px] font-semibold px-3 py-1.5 rounded-full shrink-0" data-i18n="loan">ঋণ</button>
      <button onclick="setFilter('paona',this)" class="filter-tab text-[11px] font-semibold px-3 py-1.5 rounded-full shrink-0" data-i18n="paona">পাওনা</button>
    </div>
    <div id="transaction-list" class="space-y-3 max-h-80 overflow-y-auto pr-1"></div>
  </section>
</main>
</div>

<!-- PAGE 3 : সেটিংস -->
<div id="page-settings" class="page">
<header class="sticky top-0 z-40 px-4 pt-4 pb-3 bg-cream/95 backdrop-blur-sm flex justify-between items-center">
  <div class="flex items-center gap-2.5">
    <div class="w-9 h-9 shrink-0" data-logo></div>
    <h1 class="text-base font-extrabold">⚙️ <span data-i18n="settings">সেটিংস</span></h1>
  </div>
  <div class="flex items-center gap-2">
    <button onclick="openReport()" class="hdr-icon card text-ink"><span data-icon="printer" class="w-4 h-4"></span></button>
    <button onclick="openSaveFiles()" class="hdr-icon card text-clay"><span data-icon="download" class="w-4 h-4"></span></button>
  </div>
</header>
<main class="flex-grow container mx-auto px-5 py-3 max-w-md space-y-3.5 pb-6 text-xs">
  <section onclick="openProfile()" class="card rounded-3xl p-4 flex items-center gap-3.5 cursor-pointer">
    <img id="settings-avatar" src="" class="w-14 h-14 rounded-2xl object-cover border-2 border-cream bg-sand">
    <div class="flex-1 min-w-0"><b id="settings-name" class="text-sm truncate block">আপনার নাম</b><p id="settings-phone" class="text-[11px] text-muted truncate"></p><p class="text-[10px] text-clay font-semibold mt-0.5" data-i18n="editE">সম্পাদনা</p></div>
    <span class="w-9 h-9 rounded-xl icon-well flex items-center justify-center text-clay shrink-0" data-icon="pencil"></span>
  </section>

  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-notif">
    <button onclick="accToggle('acc-notif','accw-notif')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">🔔</span><span class="flex-1 font-bold" data-i18n="stNotif">নোটিফিকেশন</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-notif" class="accordion-body bg-white"><div class="p-4 space-y-3">
      <label class="flex justify-between items-center"><span>⏰ <span data-i18n="stKistiRem">কিস্তি রিমাইন্ডার</span></span><input type="checkbox" id="tg-kisti" class="accent-clay w-4 h-4"></label>
      <label class="flex justify-between items-center"><span>🤝 <span data-i18n="stPaonaRem">পাওনা রিমাইন্ডার</span></span><input type="checkbox" id="tg-paona" class="accent-clay w-4 h-4"></label>
      <label class="flex justify-between items-center"><span>💰 <span data-i18n="stDenaRem">দেনা রিমাইন্ডার</span></span><input type="checkbox" id="tg-dena" class="accent-clay w-4 h-4"></label>
      <label class="flex justify-between items-center border-t border-black/5 pt-3"><span>🔊 <span data-i18n="stSound">সাউন্ড ও ভাইব্রেশন</span></span><input type="checkbox" id="sound-toggle" checked class="accent-clay w-4 h-4"></label>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-sec">
    <button onclick="accToggle('acc-sec','accw-sec')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">🔐</span><span class="flex-1 font-bold" data-i18n="stSec">সিকিউরিটি ও প্রাইভেসি</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-sec" class="accordion-body bg-white"><div class="p-4 space-y-3">
      <label class="flex justify-between items-center"><span>🔒 App Lock</span><input type="checkbox" id="tg-applock" class="accent-clay w-4 h-4"></label>
      <label class="flex justify-between items-center"><span>🖐️ Fingerprint</span><input type="checkbox" id="tg-finger" class="accent-clay w-4 h-4"></label>
      <button onclick="changePin()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold">🔑 <span data-i18n="stChangePin">PIN সেট / পরিবর্তন</span></button>
      <details><summary class="font-semibold text-muted cursor-pointer">🛡️ <span data-i18n="stPrivacy">প্রাইভেসি</span></summary><p class="text-[10px] text-muted pt-2 leading-relaxed" data-i18n="privTxt">সব তথ্য শুধুমাত্র এই ডিভাইসেই থাকে।</p></details>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-theme">
    <button onclick="accToggle('acc-theme','accw-theme')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">🎨</span><span class="flex-1 font-bold" data-i18n="stAppear">থিম</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-theme" class="accordion-body bg-white"><div class="p-4 grid grid-cols-3 gap-2">
      <button onclick="setTheme('light')" id="th-light" class="filter-tab text-[11px] font-semibold py-2.5 rounded-xl">☀️ <span data-i18n="stLight">লাইট</span></button>
      <button onclick="setTheme('dark')" id="th-dark" class="filter-tab text-[11px] font-semibold py-2.5 rounded-xl">🌙 <span data-i18n="stDark">ডার্ক</span></button>
      <button onclick="setTheme('system')" id="th-system" class="filter-tab text-[11px] font-semibold py-2.5 rounded-xl">📱 System</button>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-lang">
    <button onclick="accToggle('acc-lang','accw-lang')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">🌐</span><span class="flex-1 font-bold" data-i18n="stLangReg">ভাষা ও অঞ্চল</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-lang" class="accordion-body bg-white"><div class="p-4 space-y-3">
      <div class="flex justify-between items-center"><span data-i18n="language">ভাষা</span><select id="lang-select" onchange="setLanguage(this.value)" class="bg-cream border border-black/5 rounded-xl px-3 py-2 font-semibold"><option value="bn">বাংলা</option><option value="en">English</option><option value="ar">العربية</option><option value="zh">中文</option></select></div>
      <div class="flex justify-between items-center border-t border-black/5 pt-3"><span data-i18n="stCurrency">মুদ্রা</span><b>৳ BDT</b></div>
      <div class="flex justify-between items-center border-t border-black/5 pt-3"><span data-i18n="stDateReg">তারিখ ও সময়</span><b id="now-dt" class="text-[10px]"></b></div>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-backup">
    <button onclick="accToggle('acc-backup','accw-backup')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">💾</span><span class="flex-1 font-bold" data-i18n="stBackup">ব্যাকআপ ও ডাটা</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-backup" class="accordion-body bg-white"><div class="p-4 space-y-2">
      <p id="drive-status2" class="text-[10px] font-semibold text-sage"></p>
      <button onclick="driveConnectAndSave()" class="w-full py-2.5 rounded-xl bg-clay text-white font-bold flex items-center justify-center gap-2"><span data-icon="cloud" class="w-4 h-4"></span><span data-i18n="driveSave">এক ক্লিকে ব্যাকআপ সেভ</span></button>
      <button onclick="openSaveFiles()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="download" class="w-4 h-4"></span><span data-i18n="stFileSave">ফাইল সেভ অপশন</span></button>
      <button onclick="exportData()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="download" class="w-4 h-4"></span><span data-i18n="stBackupJson">ব্যাকআপ (.json)</span></button>
      <label class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2 cursor-pointer"><span data-icon="upload" class="w-4 h-4"></span><span data-i18n="restore">রিস্টোর</span><input type="file" accept="application/json" class="hidden" onchange="importData(event)"></label>
      <button onclick="saveAsPdf()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="printer" class="w-4 h-4"></span><span data-i18n="pdfSave">PDF এক্সপোর্ট</span></button>
      <button onclick="downloadTxt()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="download" class="w-4 h-4"></span><span data-i18n="stExpTxt">TXT এক্সপোর্ট</span></button>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-hset">
    <button onclick="accToggle('acc-hset','accw-hset')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">📊</span><span class="flex-1 font-bold" data-i18n="stAccSet">হিসাবের সেটিংস</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-hset" class="accordion-body bg-white"><div class="p-4 space-y-3">
      <div><label class="block font-semibold text-muted mb-1">🏷️ <span data-i18n="stDefCat">ডিফল্ট ক্যাটাগরি</span></label><select id="default-cat" onchange="setSetting('defcat',this.value)" class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2"></select></div>
      <div><label class="block font-semibold text-muted mb-1">🎯 <span data-i18n="stBudget">মাসিক বাজেট (৳)</span></label><div class="flex gap-2"><input type="number" id="monthly-budget" class="flex-1 bg-cream border border-black/5 rounded-xl px-3 py-2"><button onclick="saveBudget()" class="px-4 rounded-xl bg-clay text-white font-bold"><span data-icon="save" class="w-4 h-4"></span></button></div></div>
      <div><label class="block font-semibold text-muted mb-1">📆 <span data-i18n="stKistiSet">কিস্তি — ডিফল্ট মাস</span></label><input type="number" id="default-months" min="1" onchange="setSetting('defmonths',this.value)" class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2"></div>
      <div><label class="block font-semibold text-muted mb-1">⏰ <span data-i18n="stRemDays">রিমাইন্ডার — দিন আগে</span></label><input type="number" id="reminder-days" min="1" onchange="setSetting('remdays',this.value)" class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2"></div>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-help">
    <button onclick="accToggle('acc-help','accw-help')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">🆘</span><span class="flex-1 font-bold" data-i18n="stHelp">সাহায্য</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-help" class="accordion-body bg-white"><div class="p-4 space-y-2">
      <details><summary class="font-semibold cursor-pointer">❓ কিভাবে ঋণ যোগ করব?</summary><p class="text-[10px] text-muted pt-1.5">+ বাটন → ধরণ "ঋণ (নেওয়া)" → ব্যক্তির নাম ও মাস দিন। ঋণ তালিকায় নামে ক্লিক করে পরিশোধ করুন।</p></details>
      <details><summary class="font-semibold cursor-pointer">❓ ডাটা হারাবো না তো?</summary><p class="text-[10px] text-muted pt-1.5">ডাটা ফোনেই থাকে। ব্যাকআপ নিলে ফাইল মেমোরিতে সেভ হয় — নিরাপদ।</p></details>
      <a href="mailto:support@hisab.app" class="block w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold text-center">✉️ <span data-i18n="stFeedback">ফিডব্যাক</span></a>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-about">
    <button onclick="accToggle('acc-about','accw-about')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">ℹ️</span><span class="flex-1 font-bold" data-i18n="stAbout">অ্যাপ সম্পর্কে</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-about" class="accordion-body bg-white"><div class="p-4 space-y-2">
      <div class="flex justify-between"><span data-i18n="stVersion">ভার্সন</span><b>v5.0</b></div>
      <details><summary class="font-semibold cursor-pointer">🛡️ <span data-i18n="stPolicy">প্রাইভেসি পলিসি</span></summary><p class="text-[10px] text-muted pt-1.5">সব ডাটা শুধুমাত্র আপনার ডিভাইসে থাকে। ব্যাকআপ ফাইল আপনি নিজেই সেভ করেন।</p></details>
      <details><summary class="font-semibold cursor-pointer">📜 <span data-i18n="stTerms">শর্তাবলি</span></summary><p class="text-[10px] text-muted pt-1.5">ব্যক্তিগত হিসাবের জন্য। আর্থিক সিদ্ধান্তের একমাত্র ভিত্তি ধরবেন না।</p></details>
    </div></div>
  </div>
  <button onclick="resetAllData()" class="w-full py-3.5 rounded-2xl bg-berry text-white font-bold flex items-center justify-center gap-2">🗑️ <span data-i18n="stReset">সব ডাটা মুছুন (রিসেট)</span></button>
</main>
</div>

<!-- Bottom Nav -->
<nav class="sticky bottom-0 z-30 px-4 py-2 flex justify-around items-center bg-ink rounded-t-3xl">
  <button id="nv-home" onclick="showPage('home')" class="nav-btn active px-4 py-1.5 rounded-xl flex flex-col items-center gap-0.5 text-cream/60"><span data-icon="house" class="w-5 h-5"></span><span class="text-[9px] font-bold" data-i18n="home">হোম</span></button>
  <button id="nv-hisab" onclick="showPage('hisab')" class="nav-btn px-4 py-1.5 rounded-xl flex flex-col items-center gap-0.5 text-cream/60 hover:text-cream"><span data-icon="layers" class="w-5 h-5"></span><span class="text-[9px] font-bold" data-i18n="accounts">হিসাব</span></button>
  <button onclick="openAddModal()" class="w-[52px] h-[52px] -mt-7 rounded-full bg-clay text-white flex items-center justify-center shadow-lg hover:scale-105 transition-transform"><span data-icon="plus" class="w-6 h-6"></span></button>
  <button id="nv-settings" onclick="showPage('settings')" class="nav-btn px-4 py-1.5 rounded-xl flex flex-col items-center gap-0.5 text-cream/60 hover:text-cream"><span data-icon="gear" class="w-5 h-5"></span><span class="text-[9px] font-bold" data-i18n="settings">সেটিংস</span></button>
</nav>
</div><!-- /app-root -->

<div id="admob-banner"></div>
<div id="toast" class="bg-ink text-cream text-xs font-semibold px-5 py-3 rounded-2xl shadow-xl"></div>

<div id="lock-screen" class="fixed inset-0 z-[100] bg-ink hidden flex-col items-center justify-center gap-4 p-8 text-center">
  <div class="w-16 h-16" data-logo></div>
  <b id="lock-name" class="text-cream text-lg"></b>
  <input type="password" id="lock-pin" maxlength="4" inputmode="numeric" placeholder="PIN" class="w-32 text-center tracking-[0.5em] text-lg bg-white/10 text-cream rounded-xl py-2.5 border border-white/20">
  <button onclick="tryUnlock()" class="px-8 py-3 rounded-2xl bg-clay text-white font-bold">🔓 আনলক</button>
</div>

<!-- PIN Modal -->
<div id="pin-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-center justify-center p-4">
  <div class="card w-full max-w-xs rounded-3xl p-6 text-center space-y-3">
    <h3 class="font-bold text-sm">🔑 নতুন PIN (৪ ডিজিট)</h3>
    <input type="password" id="pin-new" maxlength="4" inputmode="numeric" placeholder="****" class="w-full text-center tracking-[0.5em] text-lg bg-cream border border-black/5 rounded-xl py-2.5">
    <div class="flex gap-2"><button onclick="closePinModal()" class="flex-1 py-2.5 rounded-xl bg-cream border border-black/10 font-bold">বাতিল</button><button onclick="savePin()" class="flex-1 py-2.5 rounded-xl bg-clay text-white font-bold" data-i18n="save">সংরক্ষণ</button></div>
  </div>
</div>

<!-- Add/Edit Modal -->
<div id="add-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
  <div class="card w-full max-w-md rounded-t-[28px] sm:rounded-[28px] p-6 max-h-[90vh] overflow-y-auto">
    <div class="flex justify-between items-center mb-4"><h3 id="modal-title" class="font-bold text-sm">নতুন হিসাব</h3><button onclick="closeAddModal()" class="w-8 h-8 rounded-full icon-well flex items-center justify-center"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button></div>
    <form id="transaction-form" onsubmit="saveTransaction(event)" class="space-y-3.5">
      <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="cat">ক্যাটাগরি</label>
        <div class="flex items-center gap-2"><select id="trans-category-select" class="flex-1 bg-cream border border-black/5 rounded-xl px-3 py-2.5 text-xs"></select><button type="button" onclick="openCategoriesModal()" class="w-10 h-10 shrink-0 rounded-xl icon-well text-clay flex items-center justify-center"><span data-icon="layers" class="w-4 h-4"></span></button></div>
      </div>
      <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="desc">বিবরণ</label>
        <div class="flex items-center gap-2"><input type="text" id="trans-desc" required class="flex-1 bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-xs"><button type="submit" class="w-10 h-10 shrink-0 rounded-xl bg-clay text-white flex items-center justify-center active:scale-95"><span data-icon="save" class="w-4 h-4"></span></button></div>
      </div>
      <div class="grid grid-cols-2 gap-3">
        <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="amount">পরিমাণ (৳)</label><input type="number" step="any" id="trans-amount" required class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2.5 text-xs"></div>
        <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="type">ধরণ</label><select id="trans-type" class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2.5 text-xs"><option value="expense" data-i18n="expenseT">ব্যয়</option><option value="income" data-i18n="incomeT">আয়</option><option value="debt" data-i18n="debtT">ঋণ (নেওয়া)</option><option value="paona" data-i18n="paonaT">পাওনা</option></select></div>
      </div>
      <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="date">তারিখ</label><input type="date" id="trans-date" required class="w-full bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-xs"></div>
      <div id="debt-fields" class="hidden space-y-3">
        <div><label id="person-label" class="block text-[11px] font-semibold text-muted mb-1" data-i18n="personL">ব্যক্তির নাম</label><input type="text" id="trans-person" class="w-full bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-xs"></div>
        <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="monthsL">কত মাসে?</label><input type="number" id="trans-months" min="1" class="w-full bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-xs"></div>
      </div>
      <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="voucher">ভাউচার / ছবি</label>
        <label class="cursor-pointer bg-cream border border-dashed border-black/15 rounded-xl py-2.5 text-center text-xs text-clay font-semibold flex items-center justify-center gap-1.5"><span data-icon="camera" class="w-4 h-4"></span> <span data-i18n="photo">ছবি তুলুন / আপলোড</span><input type="file" id="voucher-file" accept="image/*" class="hidden" onchange="previewVoucher(event)"></label>
        <div id="voucher-preview-container" class="mt-2 hidden relative w-16 h-16 rounded-xl overflow-hidden border-2 border-clay"><img id="voucher-img-tag" class="w-full h-full object-cover"><button type="button" onclick="removeVoucher()" class="absolute top-0 right-0 bg-berry text-white p-1"><span data-icon="xmark" class="w-2.5 h-2.5"></span></button></div>
      </div>
      <button type="submit" class="w-full py-3.5 rounded-xl btn-primary font-bold text-xs flex items-center justify-center gap-2"><span data-icon="save" class="w-4 h-4"></span><span data-i18n="save">সংরক্ষণ</span></button>
    </form>
  </div>
</div>

<div id="categories-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
  <div class="card w-full max-w-md rounded-t-[28px] sm:rounded-[28px] p-6 max-h-[85vh] flex flex-col">
    <div class="flex justify-between items-center mb-2"><h3 class="font-bold text-sm"><span data-i18n="cat">সব ক্যাটাগরি</span> <span id="cat-count" class="text-clay"></span></h3><button onclick="closeCategoriesModal()" class="w-8 h-8 rounded-full icon-well flex items-center justify-center"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button></div>
    <div class="flex gap-2 mb-3"><input type="text" id="new-cat-name" placeholder="নতুন ক্যাটাগরির নাম" class="flex-1 bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-xs"><button onclick="addCategory()" class="px-4 rounded-xl bg-clay text-white font-bold text-xs">+ যোগ</button></div>
    <div id="category-groups" class="space-y-2.5 overflow-y-auto pr-1"></div>
  </div>
</div>

<div id="detail-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
  <div class="card w-full max-w-md rounded-t-[28px] p-6 max-h-[90vh] overflow-y-auto space-y-3">
    <div class="flex justify-between items-center"><h3 class="font-bold text-sm" data-i18n="detail">বিস্তারিত</h3><button onclick="closeDetail()" class="w-8 h-8 rounded-full icon-well flex items-center justify-center"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button></div>
    <div id="detail-body" class="text-xs space-y-2"></div>
    <div class="flex gap-2 pt-1">
      <button id="window.__editCat = t.category;" class="flex-1 py-2.5 rounded-xl bg-cream border border-black/10 font-bold flex items-center justify-center gap-1.5"><span data-icon="pencil" class="w-3.5 h-3.5"></span><span data-i18n="editE">সম্পাদনা</span></button>
      <button id="detail-del-btn" class="flex-1 py-2.5 rounded-xl bg-berry text-white font-bold flex items-center justify-center gap-1.5"><span data-icon="trash" class="w-3.5 h-3.5"></span><span data-i18n="del">মুছুন</span></button>
    </div>
  </div>
</div>

<div id="repay-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
  <div class="card w-full max-w-md rounded-t-[28px] p-6 max-h-[90vh] overflow-y-auto space-y-3">
    <div class="flex justify-between items-center"><h3 class="font-bold text-sm" data-i18n="repay">ঋণ পরিশোধ</h3><button onclick="closeRepay()" class="w-8 h-8 rounded-full icon-well flex items-center justify-center"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button></div>
    <p id="repay-person" class="text-xs font-bold text-clay"></p>
    <div id="repay-info" class="bg-cream rounded-2xl p-3.5 text-xs space-y-1.5"></div>
    <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="repayAmt">পরিশোধ (৳)</label><input type="number" step="any" id="repay-amount" class="w-full bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-sm font-bold"></div>
    <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="date">তারিখ</label><input type="date" id="repay-date" class="w-full bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-xs"></div>
    <button onclick="saveRepayment()" class="w-full py-3 rounded-xl btn-primary font-bold text-xs flex items-center justify-center gap-2"><span data-icon="save" class="w-4 h-4"></span><span data-i18n="saveRepay">সংরক্ষণ</span></button>
    <div id="repay-history" class="pt-1"></div>
  </div>
</div>

<div id="collect-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
  <div class="card w-full max-w-md rounded-t-[28px] p-6 max-h-[90vh] overflow-y-auto space-y-3">
    <div class="flex justify-between items-center"><h3 class="font-bold text-sm" data-i18n="collect">পাওনা আদায়</h3><button onclick="closeCollect()" class="w-8 h-8 rounded-full icon-well flex items-center justify-center"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button></div>
    <p id="collect-person" class="text-xs font-bold text-plum"></p>
    <div id="collect-info" class="bg-cream rounded-2xl p-3.5 text-xs space-y-1.5"></div>
    <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="collectAmt">আদায় (৳)</label><input type="number" step="any" id="collect-amount" class="w-full bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-sm font-bold"></div>
    <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="date">তারিখ</label><input type="date" id="collect-date" class="w-full bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-xs"></div>
    <button onclick="saveCollection()" class="w-full py-3 rounded-xl bg-plum text-white font-bold text-xs flex items-center justify-center gap-2"><span data-icon="save" class="w-4 h-4"></span><span data-i18n="saveCollect">সংরক্ষণ</span></button>
    <div id="collect-history" class="pt-1"></div>
  </div>
</div>

<div id="view-voucher-modal" class="fixed inset-0 z-50 bg-ink/85 backdrop-blur-sm hidden flex items-center justify-center p-4">
  <div class="relative max-w-md w-full text-center"><button onclick="closeVoucherModal()" class="absolute -top-10 right-0 text-white"><span data-icon="xmark" class="w-6 h-6"></span></button><img id="full-voucher-img" class="max-h-[80vh] mx-auto rounded-2xl border-2 border-clay"></div>
</div>

<div id="profile-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
  <div class="card w-full max-w-md rounded-t-[28px] p-6 text-center space-y-4 max-h-[90vh] overflow-y-auto">
    <div class="flex justify-between items-center mb-1"><h3 class="font-bold text-sm" data-i18n="profile">প্রোফাইল</h3>
      <div class="flex items-center gap-2">
        <button id="profile-edit-btn" onclick="toggleProfileEdit(true)" class="w-8 h-8 rounded-full bg-clay text-white flex items-center justify-center"><span data-icon="pencil" class="w-3.5 h-3.5"></span></button>
        <button id="profile-cancel-btn" onclick="toggleProfileEdit(false)" class="w-8 h-8 rounded-full icon-well hidden"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button>
        <button onclick="closeProfile()" class="w-8 h-8 rounded-full icon-well"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button>
      </div>
    </div>
    <div class="relative w-24 h-24 mx-auto"><img id="profile-avatar-preview" src="" class="w-24 h-24 rounded-full object-cover border-4 border-cream bg-sand"><label id="photo-label" class="absolute bottom-0 right-0 w-8 h-8 rounded-full bg-clay hidden items-center justify-center cursor-pointer border-2 border-white text-white"><span data-icon="camera" class="w-3.5 h-3.5"></span><input type="file" id="profile-photo-input" accept="image/*" class="hidden" disabled onchange="previewProfilePhoto(event)"></label></div>
    <div class="space-y-3 text-left">
      <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="name">নাম</label><input type="text" id="profile-name" class="w-full bg-cream border border-black/5 rounded-xl px-4 py-2.5 text-xs font-semibold" disabled></div>
      <div class="grid grid-cols-2 gap-3">
        <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="mobile">মোবাইল</label><input type="text" id="profile-phone" class="w-full bg-cream border border-black/5 rounded-xl px-4 py-2.5 text-xs" disabled></div>
        <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="occ">পেশা</label><input type="text" id="profile-occupation" class="w-full bg-cream border border-black/5 rounded-xl px-4 py-2.5 text-xs" disabled></div>
      </div>
      <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="email">ইমেইল</label><input type="email" id="profile-email" class="w-full bg-cream border border-black/5 rounded-xl px-4 py-2.5 text-xs" disabled></div>
      <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="address">ঠিকানা</label><input type="text" id="profile-address" class="w-full bg-cream border border-black/5 rounded-xl px-4 py-2.5 text-xs" disabled></div>
      <div><label class="block text-[11px] font-semibold text-muted mb-1" data-i18n="bio">Bio</label><input type="text" id="profile-bio" class="w-full bg-cream border border-black/5 rounded-xl px-4 py-2.5 text-xs" disabled></div>
    </div>
    <button id="profile-save-btn" onclick="updateProfile()" class="hidden w-full py-3 rounded-xl btn-primary font-bold text-xs flex items-center justify-center gap-2"><span data-icon="save" class="w-4 h-4"></span><span data-i18n="updateP">আপডেট</span></button>
  </div>
</div>

<div id="savefiles-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
  <div class="card w-full max-w-md rounded-t-[28px] p-6 space-y-3 text-xs max-h-[90vh] overflow-y-auto">
    <div class="flex justify-between items-center"><h3 class="font-bold text-sm" data-i18n="saveFileT">ফাইল সেভ / শেয়ার</h3><button onclick="closeSaveFiles()" class="w-8 h-8 rounded-full icon-well"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button></div>
    <p class="text-[11px] text-muted" data-i18n="emailOnPhone">নিচের বাটনে চাপলেই ব্যাকআপ ফাইল সরাসরি ডাউনলোড/মেমোরিতে সেভ হবে — কোনো সাইন-ইন লাগবে না।</p>
    <p id="drive-status" class="text-[10px] font-semibold text-sage"></p>
    <button onclick="driveConnectAndSave()" class="w-full py-3 rounded-xl bg-clay text-white font-bold flex items-center justify-center gap-2"><span data-icon="cloud" class="w-4 h-4"></span><span data-i18n="driveSave">এক ক্লিকে ব্যাকআপ সেভ</span></button>
    <button onclick="downloadTxt()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="download" class="w-4 h-4"></span><span data-i18n="memTxt">মেমোরিতে (.txt)</span></button>
    <button onclick="exportData()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="download" class="w-4 h-4"></span><span data-i18n="memJson">মেমোরিতে (.json)</span></button>
    <button onclick="saveAsPdf()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="printer" class="w-4 h-4"></span><span data-i18n="pdfSave">PDF</span></button>
  </div>
</div>

<div id="report-modal" class="fixed inset-0 z-50 bg-ink/60 backdrop-blur-sm hidden flex items-center justify-center p-2 sm:p-4">
  <div class="card w-full max-w-2xl rounded-2xl p-3 sm:p-6 max-h-[94vh] overflow-y-auto">
    <div class="flex justify-between items-center mb-4 no-print">
      <h3 class="font-bold text-sm" data-i18n="report">রিপোর্ট (A4)</h3>
      <div class="flex items-center gap-2"><button onclick="window.print()" class="px-3 py-2 rounded-xl btn-primary text-[11px] font-bold flex items-center gap-1.5"><span data-icon="printer" class="w-3.5 h-3.5"></span> প্রিন্ট</button><button onclick="closeReport()" class="w-8 h-8 rounded-full icon-well"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button></div>
    </div>
    <div id="report-print-area" class="bg-white p-4 sm:p-7 border border-black/5 rounded-xl overflow-x-auto"></div>
  </div>
</div>

<script>
/*================= ICONS =================*/
const ICON_PATHS={
house:'<path d="M3 10.5 12 3l9 7.5"/><path d="M5 9.5V20a1 1 0 0 0 1 1h4v-6h4v6h4a1 1 0 0 0 1-1V9.5"/>',
plus:'<path d="M12 5v14M5 12h14"/>',layers:'<path d="M12 3 3 8l9 5 9-5-9-5Z"/><path d="M3 12l9 5 9-5"/><path d="M3 16l9 5 9-5"/>',
gear:'<path d="M4 6h10M4 12h16M4 18h10"/><circle cx="17" cy="6" r="2"/><circle cx="8" cy="18" r="2"/>',
camera:'<path d="M4 8h3l2-2h6l2 2h3a1 1 0 0 1 1 1v9a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V9a1 1 0 0 1 1-1Z"/><circle cx="12" cy="13" r="3.3"/>',
xmark:'<path d="M6 6l12 12M18 6 6 18"/>',
receipt:'<path d="M6 3h12v18l-2.5-1.5L13 21l-2.5-1.5L8 21l-2-1.5V3Z"/><path d="M9 8h6M9 12h6M9 16h4"/>',
image:'<rect x="3" y="4" width="18" height="16" rx="2"/><circle cx="8.5" cy="9.5" r="1.4"/><path d="M21 16l-5-5-4 4-2-2-6 6"/>',
'graduation-cap':'<path d="M2 8 12 3l10 5-10 5-10-5Z"/><path d="M6 11v4c0 1.5 3 3 6 3s6-1.5 6-3v-4"/>',
car:'<path d="M3 14 5 8h14l2 6"/><path d="M3 14h18v3a1 1 0 0 1-1 1h-1a1 1 0 0 1-1-1v-1H6v1a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1v-3Z"/><circle cx="7.5" cy="17.3" r="1.4"/><circle cx="16.5" cy="17.3" r="1.4"/>',
coins:'<rect x="2" y="6" width="20" height="12" rx="2"/><circle cx="12" cy="12" r="3"/><path d="M6 9v.01M18 15v.01"/>',
box:'<path d="M21 8 12 3 3 8l9 5 9-5Z"/><path d="M3 8v9l9 5 9-5V8"/><path d="M12 13v9"/>',
basket:'<path d="M4 9h16l-1.5 9a2 2 0 0 1-2 1.7H7.5A2 2 0 0 1 5.5 18L4 9Z"/><path d="M8 9 10 4M16 9 14 4"/><path d="M9 13v3M12 13v3M15 13v3"/>',
sparkles:'<path d="M12 3l1.8 4.9L19 9.7l-4.9 1.8L12 16.4l-1.8-4.9L5 9.7l4.9-1.8L12 3Z"/><path d="M19 15l.8 2.2L22 18l-2.2.8L19 21l-.8-2.2L16 18l2.2-.8L19 15Z"/>',
cloud:'<path d="M7 18a4 4 0 0 1-1-7.87A5 5 0 0 1 16 7a4.5 4.5 0 0 1 1 8.9"/><path d="M9.5 15.5 12 18l2.5-2.5"/><path d="M12 12v6"/>',
'arrow-down':'<path d="M12 5v14M6 13l6 6 6-6"/>','arrow-up':'<path d="M12 19V5M6 11l6-6 6 6"/>',
trash:'<path d="M4 7h16"/><path d="M9 7V4h6v3"/><path d="M6 7l1 13a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2l1-13"/><path d="M10 11v6M14 11v6"/>',
download:'<path d="M12 3v12"/><path d="M7 10l5 5 5-5"/><path d="M5 21h14"/>',
upload:'<path d="M12 21V9"/><path d="M7 14l5-5 5 5"/><path d="M5 3h14"/>',
droplet:'<path d="M12 2s6.5 7.4 6.5 11.5a6.5 6.5 0 0 1-13 0C5.5 9.4 12 2 12 2Z"/>',
bolt:'<path d="M13 2 4 14h6l-1 8 9-12h-6l1-8Z"/>',
wifi:'<path d="M2 8.5a16 16 0 0 1 20 0"/><path d="M5.5 12.5a11 11 0 0 1 13 0"/><path d="M9 16.5a6 6 0 0 1 6 0"/><circle cx="12" cy="20" r="1"/>',
phone:'<rect x="7" y="2" width="10" height="20" rx="2"/><path d="M11 18h2"/>',
flame:'<path d="M12 2c1 4-4 5-4 9a4 4 0 0 0 8 0c0-1-.5-2-1-3 1 0 2 1 2 3a5 5 0 0 1-10 0c0-5 5-6 5-9Z"/>',
heart:'<path d="M12 21s-7-4.5-9.5-9A5.5 5.5 0 0 1 12 6a5.5 5.5 0 0 1 9.5 6c-2.5 4.5-9.5 9-9.5 9Z"/>',
shirt:'<path d="M8 3 3 7l3 3 2-1v12h8V9l2 1 3-3-5-4-3 2-3-2Z"/>',
gift:'<rect x="4" y="8" width="16" height="4" rx="1"/><rect x="5" y="12" width="14" height="9" rx="1"/><path d="M12 8v13"/><path d="M12 8c-1.4-4-6-3-6-.5C6 9.3 9 8.7 12 8Zm0 0c1.4-4 6-3 6-.5C18 9.3 15 8.7 12 8Z"/>',
plane:'<path d="M22 2 11 13"/><path d="M22 2 15 22l-4-9-9-4 20-7Z"/>',
building:'<rect x="4" y="3" width="16" height="18" rx="1"/><path d="M9 8h.01M15 8h.01M9 12h.01M15 12h.01M9 16h.01M15 16h.01"/>',
film:'<rect x="3" y="4" width="18" height="16" rx="2"/><path d="M7 4v16M17 4v16M3 9h4M17 9h4M3 15h4M17 15h4"/>',
fuel:'<path d="M4 21V8a2 2 0 0 1 2-2h5a2 2 0 0 1 2 2v13"/><path d="M4 12h9"/><path d="M15 6l3 3v7a1.5 1.5 0 0 0 3 0v-4l-2-2"/>',
wrench:'<path d="M14.7 6.3a4 4 0 0 0-5.4 5.4L3 18l3 3 6.3-6.3a4 4 0 0 0 5.4-5.4l-2.6 2.6-2-2 2.6-2.6Z"/>',
briefcase:'<rect x="2" y="7" width="20" height="13" rx="2"/><path d="M8 7V5a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"/><path d="M2 12h20"/>',
utensils:'<path d="M6 2v7a2 2 0 0 0 4 0V2M8 9v13"/><path d="M17 2c-1 2-1 5 0 7s1 5 0 7"/>',
dots:'<circle cx="6" cy="12" r="1.5"/><circle cx="12" cy="12" r="1.5"/><circle cx="18" cy="12" r="1.5"/>',
clipboard:'<rect x="6" y="4" width="12" height="16" rx="2"/><rect x="9" y="2" width="6" height="4" rx="1"/><path d="M9 10h6M9 13h6M9 16h4"/>',
printer:'<rect x="6" y="9" width="12" height="7" rx="1"/><path d="M6 9V4h12v5"/><path d="M6 16v4h12v-4"/>',
chevron:'<path d="M6 9l6 6 6-6"/>',
save:'<path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2Z"/><path d="M17 21v-8H7v8M7 3v5h8"/>',
bell:'<path d="M18 8a6 6 0 0 0-12 0c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.7 21a2 2 0 0 1-3.4 0"/>',
pencil:'<path d="M17 3a2.8 2.8 0 1 1 4 4L7.5 20.5 2 22l1.5-5.5L17 3Z"/>',
hand:'<path d="M18 11V6a2 2 0 0 0-4 0v5M14 10V4a2 2 0 0 0-4 0v6M10 10.5V6a2 2 0 0 0-4 0v8"/><path d="M18 8a2 2 0 1 1 4 0v6a8 8 0 0 1-8 8h-2c-2.8 0-4.5-.86-5.99-2.34l-3.6-3.6a2 2 0 0 1 2.83-2.82L7 15"/>'
};
function renderIcons(){document.querySelectorAll('[data-icon]').forEach(el=>{const k=el.dataset.icon;if(ICON_PATHS[k])el.innerHTML=`<svg class="icon ${el.className||''}" style="width:${el.classList.contains('w-4')?'1rem':el.classList.contains('w-5')?'1.25rem':el.classList.contains('w-6')?'1.5rem':el.classList.contains('w-2.5')?'0.625rem':el.classList.contains('w-3.5')?'0.875rem':'1em'};height:auto" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">${ICON_PATHS[k]}</svg>`})}
function renderLogo(){document.querySelectorAll('[data-logo]').forEach(el=>{el.innerHTML=`<svg viewBox="0 0 48 48" class="w-full h-full"><defs><linearGradient id="hlg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#157E8E"/><stop offset="1" stop-color="#3F9A6E"/></linearGradient></defs><rect x="2" y="2" width="44" height="44" rx="14" fill="url(#hlg)"/><path d="M15 26V18.5c0-1.4 1-2.5 2.4-2.5h13.2c1.4 0 2.4 1.1 2.4 2.5V26" stroke="#fff" stroke-width="2.6" fill="none" stroke-linecap="round"/><rect x="12" y="24" width="24" height="12" rx="4" fill="#F6F1E9"/><circle cx="29" cy="30" r="2.2" fill="#157E8E"/></svg>`})}

/*================= I18N =================*/
const I18N={
bn:{home:'হোম',accounts:'সব হিসাব',settings:'সেটিংস',income:'আয়',expense:'ব্যয়',loan:'ঋণ',paona:'পাওনা',all:'সব',balance:'মোট ব্যালেন্স',balanceL:'ব্যালেন্স',sixSum:'৬ মাসের সামারি',trend:'মাসভিত্তিক ধারা (শেষ ৬ মাস)',quick:'দ্রুত ক্যাটাগরি',viewAll:'সব ক্যাটাগরি দেখুন',summary:'সামারি',thisMonth:'এই মাস',h1:'শেষ ৬ মাস',h2:'তার আগের ৬ মাস',year:'১ বছর',loanSec:'ঋণ ও পরিশোধ',paonaSec:'পাওনা আদায়',advisor:'স্মার্ট অ্যানালাইজার',recent:'সাম্প্রতিক লেনদেন (ট্যাপ = বিস্তারিত)',clear:'সব মুছুন',editE:'সম্পাদনা',stNotif:'রিমাইন্ডার',stKistiRem:'কিস্তি রিমাইন্ডার',stPaonaRem:'পাওনা রিমাইন্ডার',stDenaRem:'দেনা রিমাইন্ডার',stSound:'সাউন্ড ও ভাইব্রেশন',stSec:'সিকিউরিটি ও প্রাইভেসি',stPrivacy:'প্রাইভেসি',privTxt:'সব তথ্য শুধুমাত্র এই ডিভাইসেই থাকে।',stAppear:'থিম',stLight:'লাইট',stDark:'ডার্ক',stLangReg:'ভাষা ও অঞ্চল',language:'ভাষা',stCurrency:'মুদ্রা',stDateReg:'তারিখ ও সময়',stBackup:'ব্যাকআপ ও ডাটা',driveSave:'এক ক্লিকে ব্যাকআপ সেভ',stFileSave:'ফাইল সেভ অপশন',stBackupJson:'ব্যাকআপ (.json)',restore:'রিস্টোর',pdfSave:'PDF এক্সপোর্ট',stExpTxt:'TXT এক্সপোর্ট',stAccSet:'হিসাবের সেটিংস',stDefCat:'ডিফল্ট ক্যাটাগরি',stBudget:'মাসিক বাজেট (৳)',stKistiSet:'কিস্তি — ডিফল্ট মাস',stRemDays:'রিমাইন্ডার — দিন আগে',stHelp:'সাহায্য',stFeedback:'ফিডব্যাক',stAbout:'অ্যাপ সম্পর্কে',stVersion:'ভার্সন',stPolicy:'প্রাইভেসি পলিসি',stTerms:'শর্তাবলি',stReset:'সব ডাটা মুছুন (রিসেট)',cat:'ক্যাটাগরি',desc:'বিবরণ',amount:'পরিমাণ (৳)',type:'ধরণ',expenseT:'ব্যয়',incomeT:'আয়',debtT:'ঋণ (নেওয়া)',paonaT:'পাওনা',date:'তারিখ',monthsL:'কত মাসে?',voucher:'ভাউচার / ছবি',photo:'ছবি তুলুন / আপলোড',save:'সংরক্ষণ',detail:'বিস্তারিত',del:'মুছুন',repay:'ঋণ পরিশোধ',repayAmt:'পরিশোধ (৳)',saveRepay:'সংরক্ষণ',collect:'পাওনা আদায়',collectAmt:'আদায় (৳)',saveCollect:'সংরক্ষণ',profile:'প্রোফাইল',name:'নাম',mobile:'মোবাইল',occ:'পেশা',email:'ইমেইল',address:'ঠিকানা',updateP:'আপডেট',saveFileT:'ফাইল সেভ / শেয়ার',emailOnPhone:'নিচের বাটনে চাপলেই ব্যাকআপ ফাইল সরাসরি ডাউনলোড/মেমোরিতে সেভ হবে — কোনো সাইন-ইন লাগবে না।',memTxt:'মেমোরিতে (.txt)',memJson:'মেমোরিতে (.json)',report:'রিপোর্ট (A4)',saved:'সেভ হয়েছে ✅',newT:'নতুন হিসাব',personL:'ব্যক্তির নাম',stChangePin:'PIN সেট / পরিবর্তন'},
en:{home:'Home',accounts:'Accounts',settings:'Settings',income:'Income',expense:'Expense',loan:'Loan',paona:'Receivable',all:'All',balance:'Total Balance',balanceL:'Balance',sixSum:'6-Month Summary',trend:'Monthly Trend (Last 6 Months)',quick:'Quick Categories',viewAll:'View All Categories',summary:'Summary',thisMonth:'This Month',h1:'Last 6 Months',h2:'Previous 6 Months',year:'1 Year',loanSec:'Loans & Repayment',paonaSec:'Receivables',advisor:'Smart Analyzer',recent:'Recent Transactions (tap = details)',clear:'Clear All',editE:'Edit',stNotif:'Reminders',stKistiRem:'Installment Reminder',stPaonaRem:'Receivable Reminder',stDenaRem:'Debt Reminder',stSound:'Sound & Vibration',stSec:'Security & Privacy',stPrivacy:'Privacy',privTxt:'All data stays on this device only.',stAppear:'Theme',stLight:'Light',stDark:'Dark',stLangReg:'Language & Region',language:'Language',stCurrency:'Currency',stDateReg:'Date & Time',stBackup:'Backup & Data',driveSave:'One-tap Backup',stFileSave:'File Save Options',stBackupJson:'Backup (.json)',restore:'Restore',pdfSave:'PDF Export',stExpTxt:'TXT Export',stAccSet:'Hisab Settings',stDefCat:'Default Category',stBudget:'Monthly Budget (৳)',stKistiSet:'Installment — Default Months',stRemDays:'Reminder — Days Before',stHelp:'Help',stFeedback:'Feedback',stAbout:'About App',stVersion:'Version',stPolicy:'Privacy Policy',stTerms:'Terms',stReset:'Delete All Data (Reset)',cat:'Category',desc:'Description',amount:'Amount (৳)',type:'Type',expenseT:'Expense',incomeT:'Income',debtT:'Loan (taken)',paonaT:'Receivable',date:'Date',monthsL:'In how many months?',voucher:'Voucher / Photo',photo:'Take / Upload Photo',save:'Save',detail:'Details',del:'Delete',repay:'Repay Loan',repayAmt:'Repay (৳)',saveRepay:'Save',collect:'Collect Receivable',collectAmt:'Collect (৳)',saveCollect:'Save',profile:'Profile',name:'Name',mobile:'Mobile',occ:'Occupation',email:'Email',address:'Address',updateP:'Update',saveFileT:'Save / Share File',emailOnPhone:'Tap below to save backup directly — no sign-in needed.',memTxt:'To memory (.txt)',memJson:'To memory (.json)',report:'Report (A4)',saved:'Saved ✅',newT:'New Entry',personL:'Person name',stChangePin:'Set / Change PIN'},
ar:{home:'الرئيسية',accounts:'الحسابات',settings:'الإعدادات',income:'دخل',expense:'مصروف',loan:'قرض',paona:'مستحق',all:'الكل',balance:'الرصيد الكلي',save:'حفظ',date:'التاريخ',profile:'الملف الشخصي',name:'الاسم',detail:'تفاصيل',del:'حذف',report:'تقرير'},
zh:{home:'首页',accounts:'所有账目',settings:'设置',income:'收入',expense:'支出',loan:'贷款',paona:'应收',all:'全部',balance:'总余额',save:'保存',date:'日期',profile:'个人资料',name:'姓名',detail:'详情',del:'删除',report:'报告'}
};
function t(k){const L=I18N[state.settings.lang]||I18N.bn;return L[k]||I18N.bn[k]||k}
function applyI18n(){document.querySelectorAll('[data-i18n]').forEach(el=>{el.textContent=t(el.dataset.i18n)});document.documentElement.lang=state.settings.lang;document.documentElement.dir=state.settings.lang==='ar'?'rtl':'ltr'}

/*================= STATE =================*/
const LS='hisab_data_v5';
const DEFAULT_CATS=[
{n:'বাজার',i:'basket',c:'#E8724C'},{n:'ভাড়া',i:'building',c:'#7C5CBF'},{n:'বিদ্যুৎ বিল',i:'bolt',c:'#F5905F'},{n:'গ্যাস',i:'flame',c:'#D65B57'},{n:'পানির বিল',i:'droplet',c:'#157E8E'},{n:'ইন্টারনেট',i:'wifi',c:'#157E8E'},{n:'রিচার্জ',i:'phone',c:'#3F9A6E'},{n:'যাতায়াত',i:'car',c:'#E8724C'},{n:'জ্বালানি',i:'fuel',c:'#918A7C'},{n:'শিক্ষা',i:'graduation-cap',c:'#7C5CBF'},{n:'চিকিৎসা',i:'heart',c:'#D65B57'},{n:'পোশাক',i:'shirt',c:'#F5905F'},{n:'উপহার',i:'gift',c:'#E8724C'},{n:'ভ্রমণ',i:'plane',c:'#157E8E'},{n:'বিনোদন',i:'film',c:'#7C5CBF'},{n:'খাবার',i:'utensils',c:'#3F9A6E'},{n:'মেরামত',i:'wrench',c:'#918A7C'},{n:'অন্যান্য খরচ',i:'dots',c:'#918A7C'},{n:'চাকরির বেতন',i:'briefcase',c:'#3F9A6E',inc:1},{n:'ব্যবসার আয়',i:'box',c:'#3F9A6E',inc:1},{n:'অন্যান্য আয়',i:'coins',c:'#3F9A6E',inc:1}];
let state={profile:{name:'আপনার নাম',phone:'',occupation:'',email:'',address:'',bio:'',photo:''},transactions:[],categories:JSON.parse(JSON.stringify(DEFAULT_CATS)),pin:'',settings:{lang:'bn',theme:'light',budget:0,defcat:'',defmonths:12,remdays:3,period:'month',filter:'all',kisti:true,paona:true,dena:true,sound:true,applock:false,finger:false}};
let editingId=null,tempVoucher='',tempPhoto='',currentDetailId=null,currentRepayId=null,currentCollectId=null;
const clone=o=>JSON.parse(JSON.stringify(o));
function load(){try{const d=JSON.parse(localStorage.getItem(LS));if(d){state=Object.assign(state,d);state.profile=Object.assign(clone({name:'আপনার নাম',phone:'',occupation:'',email:'',address:'',bio:'',photo:''}),d.profile||{});state.settings=Object.assign(clone(state.settings),d.settings||{});if(!state.categories||!state.categories.length)state.categories=clone(DEFAULT_CATS)}}catch(e){}}
function save(){try{localStorage.setItem(LS,JSON.stringify(state))}catch(e){toast('স্টোরেজ পূর্ণ! ছবি কম ব্যবহার করুন')}}
const uid=()=>Date.now()+''+Math.floor(Math.random()*9999);
const fmt=n=>'৳ '+(Math.round(n)||0).toLocaleString('en-IN');
const today=()=>new Date().toISOString().slice(0,10);
const esc=s=>(s||'').toString().replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const mKey=d=>(d||'').slice(0,7);
const BN_M=['জানু','ফেব','মার্চ','এপ্রি','মে','জুন','জুল','আগ','সেপ','অক্টো','নভে','ডিসে'],EN_M=['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
const mLabel=k=>{const m=+k.slice(5,7)-1;return (state.settings.lang==='bn'?BN_M:EN_M)[m]+' '+k.slice(2,4)};
function lastN(n){const a=[],d=new Date();for(let i=n-1;i>=0;i--){const x=new Date(d.getFullYear(),d.getMonth()-i,1);a.push(x.toISOString().slice(0,7))}return a}
function catOf(name){return state.categories.find(c=>c.n===name)||{n:name||'—',i:'dots',c:'#918A7C'}}
function paid(tx){return (tx.payments||[]).reduce((s,p)=>s+ +p.amount,0)}

/*================= TOAST =================*/
let toastT;function toast(msg){const el=document.getElementById('toast');el.textContent=msg;el.classList.add('show');clearTimeout(toastT);toastT=setTimeout(()=>el.classList.remove('show'),2200);if(state.settings.sound&&navigator.vibrate)try{navigator.vibrate(25)}catch(e){}}

/*================= NAV =================*/
function showPage(p){['home','hisab','settings'].forEach(x=>{document.getElementById('page-'+x).classList.toggle('active',x===p)});['home','hisab','settings'].forEach(x=>{const b=document.getElementById('nv-'+x);if(b)b.classList.toggle('active',x===p)});window.scrollTo(0,0)}
function accToggle(b,w){document.getElementById(b).classList.toggle('open');const c=document.querySelector('#'+w+' .chev');if(c)c.classList.toggle('open')}
function setSetting(k,v){state.settings[k]=isNaN(v)||v===''?v:+v;save();toast(t('saved'));if(k==='remdays')renderReminders()}

/*================= ADD/EDIT =================*/
function fillCatSelect(){const ex=state.categories.filter(c=>!c.inc),inc=state.categories.filter(c=>c.inc);document.getElementById('trans-category-select').innerHTML='<optgroup label="💸 খরচ">'+ex.map(c=>`<option>${esc(c.n)}</option>`).join('')+'</optgroup><optgroup label="💰 আয়">'+inc.map(c=>`<option>${esc(c.n)}</option>`).join('')+'</optgroup>';document.getElementById('default-cat').innerHTML=state.categories.map(c=>`<option value="${esc(c.n)}">${esc(c.n)}</option>`).join('');const d=document.getElementById('default-cat');if(state.settings.defcat)d.value=state.settings.defcat}
function openAddModal(cat,type){editingId=null;tempVoucher='';const f=document.getElementById('transaction-form');f.reset();document.getElementById('modal-title').textContent=t('newT');document.getElementById('trans-date').value=today();document.getElementById('trans-months').value=state.settings.defmonths||12;if(cat){const c=catOf(cat);fillCatSelect();document.getElementById('trans-category-select').value=c.n;if(c.inc)type=type||'income'}fillCatSelect();if(state.settings.defcat&&!cat)document.getElementById('trans-category-select').value=state.settings.defcat;if(type)document.getElementById('trans-type').value=type;typeToggle();document.getElementById('voucher-preview-container').classList.add('hidden');document.getElementById('add-modal').classList.remove('hidden');document.getElementById('add-modal').classList.add('flex')}
function closeAddModal(){document.getElementById('add-modal').classList.add('hidden');document.getElementById('add-modal').classList.remove('flex')}
function typeToggle(){const ty=document.getElementById('trans-type').value;document.getElementById('debt-fields').classList.toggle('hidden',!(ty==='debt'||ty==='paona'))}
function previewVoucher(e){const f=e.target.files[0];if(!f)return;const r=new FileReader();r.onload=ev=>{tempVoucher=ev.target.result;document.getElementById('voucher-img-tag').src=tempVoucher;document.getElementById('voucher-preview-container').classList.remove('hidden')};r.readAsDataURL(f)}
function removeVoucher(){tempVoucher='';document.getElementById('voucher-preview-container').classList.add('hidden');document.getElementById('voucher-file').value=''}
function saveTransaction(e){e.preventDefault();const ty=document.getElementById('trans-type').value;let person=document.getElementById('trans-person').value.trim();if((ty==='debt'||ty==='paona')&&!person){toast('ব্যক্তির নাম দিন');return}
const tx={id:editingId||uid(),type:ty,cat:document.getElementById('trans-category-select').value,desc:document.getElementById('trans-desc').value.trim(),amount:+document.getElementById('trans-amount').value,date:document.getElementById('trans-date').value,person,months:+document.getElementById('trans-months').value||0,voucher:tempVoucher};
if(editingId){const old=state.transactions.find(x=>x.id===editingId);tx.payments=old.payments||[];state.transactions=state.transactions.map(x=>x.id===editingId?tx:x)}else{tx.payments=[];state.transactions.push(tx)}
save();closeAddModal();renderAll();toast(t('saved'));maybeInterstitial()}
function setFilter(f,btn){state.settings.filter=f;save();document.querySelectorAll('#filter-tabs .filter-tab').forEach(b=>b.classList.remove('active'));if(btn)btn.classList.add('active');renderTx()}
function setPeriod(p,btn){state.settings.period=p;save();document.querySelectorAll('#summary-tabs .sum-tab').forEach(b=>b.classList.remove('active'));if(btn)btn.classList.add('active');renderSummary()}

/*================= DETAIL =================*/
function openDetail(id){const tx=state.transactions.find(x=>x.id===id);if(!tx)return;currentDetailId=id;const c=catOf(tx.cat);const tmap={income:['আয়','#3F9A6E'],expense:['ব্যয়','#D65B57'],debt:['ঋণ','#E8724C'],paona:['পাওনা','#7C5CBF']};const[tn,tc]=tmap[tx.type]||['—','#918A7C'];let h=`<div class="flex items-center gap-3"><span class="w-10 h-10 rounded-xl flex items-center justify-center text-white shrink-0" style="background:${c.c}"><span data-icon="${c.i}" class="w-4 h-4"></span></span><div><b class="text-sm">${esc(tx.desc)}</b><p class="text-[10px] text-muted">${esc(c.n)} • ${esc(tx.date)}</p></div></div>
<div class="flex justify-between border-t border-black/5 pt-2"><span class="text-muted">ধরণ</span><b style="color:${tc}">${tn}</b></div>
<div class="flex justify-between border-t border-black/5 pt-2"><span class="text-muted">${t('amount')}</span><b>${fmt(tx.amount)}</b></div>`;
if(tx.person)h+=`<div class="flex justify-between border-t border-black/5 pt-2"><span class="text-muted">${t('personL')}</span><b>${esc(tx.person)}</b></div>`;
if(tx.months)h+=`<div class="flex justify-between border-t border-black/5 pt-2"><span class="text-muted">${t('monthsL')}</span><b>${tx.months}</b></div>`;
if(tx.type==='debt'||tx.type==='paona'){const p=paid(tx);h+=`<div class="flex justify-between border-t border-black/5 pt-2"><span class="text-muted">পরিশোধিত</span><b class="text-sage">${fmt(p)}</b></div><div class="flex justify-between border-t border-black/5 pt-2"><span class="text-muted">বাকি</span><b class="text-berry">${fmt(tx.amount-p)}</b></div>`}
if(tx.voucher)h+=`<div class="border-t border-black/5 pt-2"><p class="text-muted mb-1.5">${t('voucher')}</p><img src="${tx.voucher}" onclick="openVoucher(this.src)" class="w-20 h-20 rounded-xl object-cover border border-black/10 cursor-pointer"></div>`;
document.getElementById('detail-body').innerHTML=h;renderIcons();document.getElementById('detail-edit-btn').onclick=()=>{closeDetail();editFromDetail(id)};document.getElementById('detail-del-btn').onclick=()=>deleteFromDetail(id);document.getElementById('detail-modal').classList.remove('hidden');document.getElementById('detail-modal').classList.add('flex')}
function closeDetail(){document.getElementById('detail-modal').classList.add('hidden');document.getElementById('detail-modal').classList.remove('flex')}
function editFromDetail(id){const tx=state.transactions.find(x=>x.id===id);if(!tx)return;editingId=id;fillCatSelect();document.getElementById('modal-title').textContent=t('editE');document.getElementById('trans-category-select').value=tx.cat;document.getElementById('trans-desc').value=tx.desc;document.getElementById('trans-amount').value=tx.amount;document.getElementById('trans-type').value=tx.type;document.getElementById('trans-date').value=tx.date;document.getElementById('trans-person').value=tx.person||'';document.getElementById('trans-months').value=tx.months||'';typeToggle();tempVoucher=tx.voucher||'';if(tempVoucher){document.getElementById('voucher-img-tag').src=tempVoucher;document.getElementById('voucher-preview-container').classList.remove('hidden')}document.getElementById('add-modal').classList.remove('hidden');document.getElementById('add-modal').classList.add('flex')}
function deleteFromDetail(id){if(!confirm('এই লেনদেন মুছে ফেলবেন?'))return;state.transactions=state.transactions.filter(x=>x.id!==id);save();closeDetail();renderAll();toast('মুছে ফেলা হয়েছে')}
function openVoucher(src){document.getElementById('full-voucher-img').src=src;document.getElementById('view-voucher-modal').classList.remove('hidden');document.getElementById('view-voucher-modal').classList.add('flex')}
function closeVoucherModal(){document.getElementById('view-voucher-modal').classList.add('hidden');document.getElementById('view-voucher-modal').classList.remove('flex')}

/*================= REPAY / COLLECT =================*/
function openRepay(id){const tx=state.transactions.find(x=>x.id===id);if(!tx)return;currentRepayId=id;fillLoanModal(tx,'repay');document.getElementById('repay-amount').value='';document.getElementById('repay-date').value=today();document.getElementById('repay-modal').classList.remove('hidden');document.getElementById('repay-modal').classList.add('flex')}
function fillLoanModal(tx,pre){const p=paid(tx),rem=tx.amount-p;document.getElementById(pre+'-person').textContent=tx.person+' — '+esc(tx.desc);let info=`<div class="flex justify-between"><span>মোট</span><b>${fmt(tx.amount)}</b></div><div class="flex justify-between"><span>পরিশোধিত</span><b class="text-sage">${fmt(p)}</b></div><div class="flex justify-between"><span>বাকি</span><b class="text-berry">${fmt(rem)}</b></div>`;if(tx.months)info+=`<div class="flex justify-between"><span>মাসিক কিস্তি (আন্দাজ)</span><b>${fmt(tx.amount/tx.months)}</b></div>`;document.getElementById(pre+'-info').innerHTML=info;const hist=(tx.payments||[]).map(x=>`<div class="flex justify-between text-[11px] border-b border-black/5 py-1"><span>${esc(x.date)}</span><b>${fmt(x.amount)}</b></div>`).join('');document.getElementById(pre+'-history').innerHTML=hist?('<p class="font-bold text-[11px] text-muted mb-1">ইতিহাস</p>'+hist):''}
function closeRepay(){document.getElementById('repay-modal').classList.add('hidden');document.getElementById('repay-modal').classList.remove('flex')}
function saveRepayment(){const tx=state.transactions.find(x=>x.id===currentRepayId);if(!tx)return;const amt=+document.getElementById('repay-amount').value;if(!amt||amt<=0){toast('সঠিক পরিমাণ দিন');return}tx.payments=tx.payments||[];tx.payments.push({amount:amt,date:document.getElementById('repay-date').value||today()});save();closeRepay();renderAll();toast(t('saved'));maybeInterstitial()}
function openCollect(id){const tx=state.transactions.find(x=>x.id===id);if(!tx)return;currentCollectId=id;fillLoanModal(tx,'collect');document.getElementById('collect-amount').value='';document.getElementById('collect-date').value=today();document.getElementById('collect-modal').classList.remove('hidden');document.getElementById('collect-modal').classList.add('flex')}
function closeCollect(){document.getElementById('collect-modal').classList.add('hidden');document.getElementById('collect-modal').classList.remove('flex')}
function saveCollection(){const tx=state.transactions.find(x=>x.id===currentCollectId);if(!tx)return;const amt=+document.getElementById('collect-amount').value;if(!amt||amt<=0){toast('সঠিক পরিমাণ দিন');return}tx.payments=tx.payments||[];tx.payments.push({amount:amt,date:document.getElementById('collect-date').value||today()});save();closeCollect();renderAll();toast(t('saved'));maybeInterstitial()}

/*================= CATEGORIES MODAL =================*/
function openCategoriesModal(){renderCatGroups();document.getElementById('categories-modal').classList.remove('hidden');document.getElementById('categories-modal').classList.add('flex')}
function closeCategoriesModal(){document.getElementById('categories-modal').classList.add('hidden');document.getElementById('categories-modal').classList.remove('flex')}
function renderCatGroups(){document.getElementById('cat-count').textContent='('+state.categories.length+')';const ex=state.categories.filter(c=>!c.inc),inc=state.categories.filter(c=>c.inc);const row=c=>`<div class="flex items-center gap-2.5 bg-cream rounded-xl px-3 py-2"><span class="w-8 h-8 rounded-lg flex items-center justify-center text-white shrink-0" style="background:${c.c}"><span data-icon="${c.i}" class="w-3.5 h-3.5"></span></span><span class="font-semibold flex-1">${esc(c.n)}</span></div>`;document.getElementById('category-groups').innerHTML='<p class="text-[10px] font-bold text-muted">💸 খরচের ক্যাটাগরি</p>'+ex.map(row).join('')+'<p class="text-[10px] font-bold text-muted pt-1">💰 আয়ের ক্যাটাগরি</p>'+inc.map(row).join('');renderIcons()}
function addCategory(){const inp=document.getElementById('new-cat-name');const n=inp.value.trim();if(!n){toast('নাম লিখুন');return}if(state.categories.some(c=>c.n===n)){toast(' already আছে');return}const pal=['#E8724C','#7C5CBF','#157E8E','#3F9A6E','#D65B57','#F5905F'];state.categories.push({n,i:'dots',c:pal[Math.floor(Math.random()*pal.length)]});save();inp.value='';renderCatGroups();fillCatSelect();renderQuick();toast(t('saved'))}

/*================= PROFILE =================*/
function openProfile(){const p=state.profile;['name','phone','occupation','email','address','bio'].forEach(k=>{document.getElementById('profile-'+k).value=p[k]||''});document.getElementById('profile-avatar-preview').src=p.photo||'';toggleProfileEdit(false);document.getElementById('profile-modal').classList.remove('hidden');document.getElementById('profile-modal').classList.add('flex')}
function closeProfile(){document.getElementById('profile-modal').classList.add('hidden');document.getElementById('profile-modal').classList.remove('flex')}
function toggleProfileEdit(on){['name','phone','occupation','email','address','bio'].forEach(k=>{document.getElementById('profile-'+k).disabled=!on});const pi=document.getElementById('profile-photo-input');pi.disabled=!on;document.getElementById('photo-label').classList.toggle('hidden',!on);document.getElementById('photo-label').classList.toggle('flex',on);document.getElementById('profile-save-btn').classList.toggle('hidden',!on);document.getElementById('profile-edit-btn').classList.toggle('hidden',on);document.getElementById('profile-cancel-btn').classList.toggle('hidden',!on);if(!on)tempPhoto=''}
function previewProfilePhoto(e){const f=e.target.files[0];if(!f)return;const r=new FileReader();r.onload=ev=>{tempPhoto=ev.target.result;document.getElementById('profile-avatar-preview').src=tempPhoto};r.readAsDataURL(f)}
function updateProfile(){const p=state.profile;['name','phone','occupation','email','address','bio'].forEach(k=>{p[k]=document.getElementById('profile-'+k).value.trim()});if(tempPhoto)p.photo=tempPhoto;save();syncProfileUI();toggleProfileEdit(false);toast(t('saved'))}
function syncProfileUI(){const p=state.profile;document.getElementById('summary-name').textContent=p.name||'আপনার নাম';document.getElementById('settings-name').textContent=p.name||'আপনার নাম';document.getElementById('lock-name').textContent=p.name||'';document.getElementById('summary-bio').textContent=p.bio||'পরিচিতি যোগ করুন';document.getElementById('summary-phone').textContent=p.phone||'';document.getElementById('settings-phone').textContent=p.phone||'';['summary-avatar','settings-avatar','profile-avatar-preview'].forEach(id=>{const el=document.getElementById(id);if(el)el.src=p.photo||''})}

/*================= RENDER =================*/
function inPeriod(tx){const k=mKey(tx.date),now=new Date();const cur=now.toISOString().slice(0,7);if(state.settings.period==='month')return k===cur;if(state.settings.period==='h1')return lastN(6).includes(k);if(state.settings.period==='h2'){const l6=lastN(6),p6=lastN(12).filter(x=>!l6.includes(x));return p6.includes(k)}const y=lastN(12);return y.includes(k)}
function sums(list){let inc=0,exp=0;list.forEach(x=>{if(x.type==='income')inc+=+x.amount;else if(x.type==='expense')exp+=+x.amount});return{inc,exp}}
function renderHome(){const l6=lastN(6);let inc=0,exp=0;state.transactions.forEach(x=>{if(l6.includes(mKey(x.date))){if(x.type==='income')inc+=+x.amount;else if(x.type==='expense')exp+=+x.amount}});
const tot=inc+exp,R=26,C=2*Math.PI*R;let arc='';if(tot>0){const a=C*inc/tot;arc=`<circle cx="35" cy="35" r="${R}" fill="none" stroke="#3F9A6E" stroke-width="9" stroke-dasharray="${a} ${C-a}" stroke-linecap="round" transform="rotate(-90 35 35)"/><circle cx="35" cy="35" r="${R}" fill="none" stroke="#D65B57" stroke-width="9" stroke-dasharray="${C-a} ${a}" stroke-dashoffset="${-a}" stroke-linecap="round" transform="rotate(-90 35 35)"/>`}
document.getElementById('donut-box').innerHTML=`<svg width="82" height="82" viewBox="0 0 70 70"><circle cx="35" cy="35" r="${R}" fill="none" stroke="#EDE6D8" stroke-width="9"/>${arc}<text x="35" y="39" text-anchor="middle" font-size="10" font-weight="800" fill="#2B2620">${tot>0?Math.round(inc/tot*100)+'%':'—'}</text></svg>`;
document.getElementById('donut-legend').innerHTML=`<div class="flex justify-between"><span class="flex items-center gap-1.5"><i class="w-2.5 h-2.5 rounded-full inline-block" style="background:#3F9A6E"></i>${t('income')}</span><b>${fmt(inc)}</b></div><div class="flex justify-between"><span class="flex items-center gap-1.5"><i class="w-2.5 h-2.5 rounded-full inline-block" style="background:#D65B57"></i>${t('expense')}</span><b>${fmt(exp)}</b></div>`;
document.getElementById('visual-balance').textContent=fmt(inc-exp);
const now=new Date();document.getElementById('visual-period').textContent=mLabel(now.toISOString().slice(0,7));
renderBars(l6)}
function renderBars(l6){const data=l6.map(k=>{let i=0,e=0;state.transactions.forEach(x=>{if(mKey(x.date)===k){if(x.type==='income')i+=+x.amount;else if(x.type==='expense')e+=+x.amount}});return{k,i,e}});const mx=Math.max(1,...data.map(d=>Math.max(d.i,d.e)));document.getElementById('bars-box').innerHTML=data.map(d=>`<div class="bar-col"><div style="height:${Math.max(2,d.i/mx*34)}px;background:#3F9A6E;border-radius:4px 4px 0 0"></div><div style="height:${Math.max(2,d.e/mx*34)}px;background:#D65B57;border-radius:0 0 4px 4px"></div></div>`).join('');document.getElementById('bars-labels').innerHTML=data.map(d=>`<span class="flex-1 text-center text-[8px] text-muted font-semibold">${mLabel(d.k).split(' ')[0]}</span>`).join('')}
function renderHisab(){let inc=0,exp=0;state.transactions.forEach(x=>{if(x.type==='income')inc+=+x.amount;else if(x.type==='expense')exp+=+x.amount});document.getElementById('total-income').textContent=fmt(inc);document.getElementById('total-expense').textContent=fmt(exp);document.getElementById('total-balance').textContent=fmt(inc-exp);renderSummary();renderLoans();renderPaona();renderAdvice();renderReminders()}
function renderSummary(){const list=state.transactions.filter(inPeriod);const{inc,exp}=sums(list);const cnt=list.length;let top='—',tmx=0;const byCat={};list.filter(x=>x.type==='expense').forEach(x=>{byCat[x.cat]=(byCat[x.cat]||0)+ +x.amount;if(byCat[x.cat]>tmx){tmx=byCat[x.cat];top=x.cat}});
document.getElementById('summary-body').innerHTML=`<div class="flex justify-between py-1.5 border-b border-black/5"><span class="text-muted">${t('income')}</span><b class="text-sage">${fmt(inc)}</b></div><div class="flex justify-between py-1.5 border-b border-black/5"><span class="text-muted">${t('expense')}</span><b class="text-berry">${fmt(exp)}</b></div><div class="flex justify-between py-1.5 border-b border-black/5"><span class="text-muted">${t('balanceL')}</span><b class="text-clay">${fmt(inc-exp)}</b></div><div class="flex justify-between py-1.5 border-b border-black/5"><span class="text-muted">লেনদেন</span><b>${cnt}</b></div><div class="flex justify-between py-1.5"><span class="text-muted">সর্বোচ্চ খরচ</span><b>${esc(top)}</b></div>`;
const b=+state.settings.budget||0,box=document.getElementById('budget-box');if(b>0){box.classList.remove('hidden');const me=sums(state.transactions.filter(x=>mKey(x.date)===new Date().toISOString().slice(0,7))).exp;const pct=Math.min(100,Math.round(me/b*100));document.getElementById('budget-pct').textContent=pct+'%';document.getElementById('budget-fill').style.width=pct+'%';document.getElementById('budget-fill').style.background=pct>90?'#D65B57':pct>70?'#F5905F':'#3F9A6E';document.getElementById('budget-info').textContent=`খরচ ${fmt(me)} / বাজেট ${fmt(b)}`+(me>b?' — ⚠️ বাজেট ছাড়িয়ে গেছে!':'')}else box.classList.add('hidden')}
function renderLoans(){const l=state.transactions.filter(x=>x.type==='debt'&&x.amount-paid(x)>0);document.getElementById('loan-list').innerHTML=l.length?l.map(x=>{const rem=x.amount-paid(x);return `<div class="flex items-center gap-2.5 bg-cream rounded-2xl p-3"><div class="flex-1 min-w-0"><b class="text-xs block truncate">${esc(x.person||x.desc)}</b><p class="text-[10px] text-muted">বাকি <b class="text-berry">${fmt(rem)}</b> / মোট ${fmt(x.amount)}${x.months?' • '+x.months+' মাস':''}</p></div><button onclick="openRepay('${x.id}')" class="px-3 py-1.5 rounded-xl bg-clay text-white text-[10px] font-bold shrink-0">${t('repay')}</button></div>`}).join(''):'<p class="text-[11px] text-muted">কোনো বাকি ঋণ নেই 🎉</p>'}
function renderPaona(){const l=state.transactions.filter(x=>x.type==='paona'&&x.amount-paid(x)>0);document.getElementById('paona-list').innerHTML=l.length?l.map(x=>{const rem=x.amount-paid(x);return `<div class="flex items-center gap-2.5 bg-cream rounded-2xl p-3"><div class="flex-1 min-w-0"><b class="text-xs block truncate">${esc(x.person||x.desc)}</b><p class="text-[10px] text-muted">আদায় বাকি <b class="text-plum">${fmt(rem)}</b> / মোট ${fmt(x.amount)}</p></div><button onclick="openCollect('${x.id}')" class="px-3 py-1.5 rounded-xl bg-plum text-white text-[10px] font-bold shrink-0">${t('collect')}</button></div>`}).join(''):'<p class="text-[11px] text-muted">কোনো পাওনা নেই 👍</p>'}
function renderAdvice(){const cur=new Date().toISOString().slice(0,7);const{s}=sums(state.transactions);const m=sums(state.transactions.filter(x=>mKey(x.date)===cur));let tips=[];if(m.exp>m.inc&&m.exp>0)tips.push('⚠️ এই মাসে আয়ের চেয়ে খরচ '+fmt(m.exp-m.inc)+' বেশি হয়েছে। অপ্রয়োজনীয় খরচ কমান।');else if(m.inc>0&&m.exp>0)tips.push('✅ দারুণ! এই মাসে '+fmt(m.inc-m.exp)+' সঞ্চয় হয়েছে। এভাবেই চালিয়ে যান।');const b=+state.settings.budget||0;if(b>0&&m.exp>b*0.8&&m.exp<=b)tips.push('🎯 বাজেটের ৮০%+ খরচ হয়ে গেছে — সাবধান!');if(m.exp>b&&b>0)tips.push('🚨 মাসিক বাজেট ছাড়িয়ে গেছে!');const l6=lastN(6);let mx=0,mc='';const bc={};state.transactions.filter(x=>x.type==='expense'&&l6.includes(mKey(x.date))).forEach(x=>{bc[x.cat]=(bc[x.cat]||0)+ +x.amount;if(bc[x.cat]>mx){mx=bc[x.cat];mc=x.cat}});if(mc)tips.push('📊 সর্বোচ্চ খরচের খাত: '+esc(mc)+' ('+fmt(mx)+')');const pd=state.transactions.filter(x=>x.type==='paona'&&x.amount-paid(x)>0).reduce((s,x)=>s+x.amount-paid(x),0);if(pd>0)tips.push('🤝 '+fmt(pd)+' পাওনা আদায় বাকি — তাগাদা দিন!');document.getElementById('ai-advice-text').textContent=tips.length?tips.join(' '):'💡 লেনদেন যোগ করুন — আমি আপনার খরচের ধরন বিশ্লেষণ করে পরামর্শ দেব।'}
function renderReminders(){const days=+state.settings.remdays||3;const items=[];state.transactions.forEach(x=>{const rem=x.amount-paid(x);if((x.type==='debt'&&state.settings.dena&&rem>0))items.push('💰 '+esc(x.person||x.desc)+'-কে '+fmt(rem)+' পরিশোধ করতে হবে');if(x.type==='paona'&&state.settings.paona&&rem>0)items.push('🤝 '+esc(x.person||x.desc)+' থেকে '+fmt(rem)+' আদায় বাকি')});const box=document.getElementById('reminder-box');if(items.length){box.classList.remove('hidden');document.getElementById('reminder-text').innerHTML=items.slice(0,3).join('<br>')+(items.length>3?('<br>+ আরও '+(items.length-3)+'টি…'):'')}else box.classList.add('hidden')}
function renderTx(){const f=state.settings.filter;let list=state.transactions.slice().sort((a,b)=>b.date.localeCompare(a.date));if(f!=='all')list=list.filter(x=>x.type===f);const tmap={income:['+','#3F9A6E'],expense:['-','#D65B57'],debt:['','#E8724C'],paona:['','#7C5CBF']};document.getElementById('transaction-list').innerHTML=list.length?list.slice(0,100).map(x=>{const[s,cl]=tmap[x.type];const c=catOf(x.cat);return `<div onclick="openDetail('${x.id}')" class="card rounded-2xl p-3 flex items-center gap-3 cursor-pointer"><span class="w-10 h-10 rounded-xl flex items-center justify-center text-white shrink-0" style="background:${c.c}"><span data-icon="${c.i}" class="w-4 h-4"></span></span><div class="flex-1 min-w-0"><b class="text-xs block truncate">${esc(x.desc)}</b><p class="text-[10px] text-muted truncate">${esc(c.n)} • ${esc(x.date)}${x.person?' • '+esc(x.person):''}</p></div><b class="text-xs shrink-0" style="color:${cl}">${s}${fmt(x.amount)}</b></div>`}).join(''):'<p class="text-[11px] text-muted text-center py-6">কোনো লেনদেন নেই — + বাটনে চাপুন</p>';renderIcons()}
function renderQuick(){const ex=state.categories.filter(c=>!c.inc).slice(0,8);const html=ex.map(c=>`<button onclick="openAddModal('${esc(c.n).replace(/'/g,"\\'")}')" class="card rounded-2xl p-2.5 flex flex-col items-center gap-1.5"><span class="w-9 h-9 rounded-xl flex items-center justify-center text-white" style="background:${c.c}"><span data-icon="${c.i}" class="w-4 h-4"></span></span><span class="text-[9px] font-semibold text-center leading-tight truncate w-full">${esc(c.n)}</span></button>`).join('');document.getElementById('quick-grid-home').innerHTML=html;document.getElementById('quick-grid-hisab').innerHTML=html;renderIcons()}
function renderAll(){syncProfileUI();renderHome();renderHisab();renderTx();renderQuick()}

/*================= THEME / LANG =================*/
function setTheme(th){state.settings.theme=th;save();applyTheme()}
function applyTheme(){const th=state.settings.theme;const dark=th==='dark'||(th==='system'&&window.matchMedia('(prefers-color-scheme: dark)').matches);document.body.classList.toggle('dark',dark);['light','dark','system'].forEach(x=>{const b=document.getElementById('th-'+x);if(b)b.classList.toggle('active',x===th)})}
function setLanguage(l){state.settings.lang=l;save();document.getElementById('lang-top').value=l;document.getElementById('lang-select').value=l;applyI18n();renderAll()}

/*================= BACKUP / EXPORT (Client ID ছাড়া) =================*/
function dl(name,content,mime){const blob=new Blob([content],{type:mime});const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download=name;document.body.appendChild(a);a.click();setTimeout(()=>{URL.revokeObjectURL(a.href);a.remove()},400)}
const fname=ext=>'Hisab_Backup_'+today()+'.'+ext;
function downloadTxt(){let s='হিসাব — Hisab ব্যাকআপ ('+today()+')\nনাম: '+(state.profile.name||'')+'\n'+'='.repeat(40)+'\n';let ti=0,te=0;state.transactions.slice().sort((a,b)=>a.date.localeCompare(b.date)).forEach(x=>{const sign=x.type==='income'?'+':x.type==='expense'?'-':'';if(x.type==='income')ti+=+x.amount;if(x.type==='expense')te+=+x.amount;s+=`${x.date} | ${x.cat} | ${x.desc}${x.person?' ('+x.person+')':''} | ${sign}${x.amount}\n`});s+='='.repeat(40)+'\nমোট আয়: '+ti+'\nমোট ব্যয়: '+te+'\nব্যালেন্স: '+(ti-te)+'\n';dl(fname('txt'),'\ufeff'+s,'text/plain;charset=utf-8');setStatus('✅ TXT ফাইল ডাউনলোড হয়েছে');toast('📁 TXT সেভ হয়েছে')}
function exportData(){dl(fname('json'),JSON.stringify(state,null,1),'application/json');setStatus('✅ JSON ব্যাকআপ ডাউনলোড হয়েছে');toast('📁 ব্যাকআপ সেভ হয়েছে')}
function driveConnectAndSave(){exportData()}
function setStatus(s){['drive-status','drive-status2'].forEach(id=>{const el=document.getElementById(id);if(el)el.textContent=s})}
function importData(e){const f=e.target.files[0];if(!f)return;const r=new FileReader();r.onload=ev=>{try{const d=JSON.parse(ev.target.result);if(!d.transactions)throw 0;localStorage.setItem(LS,JSON.stringify(d));toast('✅ রিস্টোর হয়েছে — রিলোড হচ্ছে');setTimeout(()=>location.reload(),800)}catch(x){toast('❌ ভুল ফাইল!')}};r.readAsText(f)}
function openSaveFiles(){document.getElementById('savefiles-modal').classList.remove('hidden');document.getElementById('savefiles-modal').classList.add('flex')}
function closeSaveFiles(){document.getElementById('savefiles-modal').classList.add('hidden');document.getElementById('savefiles-modal').classList.remove('flex')}

/*================= REPORT =================*/
function openReport(){const p=state.profile;let rows='';let ti=0,te=0;state.transactions.slice().sort((a,b)=>a.date.localeCompare(b.date)).forEach(x=>{const sign=x.type==='income'?'+':x.type==='expense'?'-':'';if(x.type==='income')ti+=+x.amount;if(x.type==='expense')te+=+x.amount;rows+=`<tr><td>${x.date}</td><td>${esc(x.cat)}</td><td>${esc(x.desc)}${x.person?' ('+esc(x.person)+')':''}</td><td style="color:${x.type==='income'?'#3F9A6E':x.type==='expense'?'#D65B57':'#918A7C'}">${sign}${(+x.amount).toLocaleString('en-IN')}</td></tr>`});
const loans=state.transactions.filter(x=>x.type==='debt'&&x.amount-paid(x)>0).map(x=>`<tr><td>${esc(x.person||x.desc)}</td><td>${(+x.amount).toLocaleString('en-IN')}</td><td>${paid(x).toLocaleString('en-IN')}</td><td>${(x.amount-paid(x)).toLocaleString('en-IN')}</td></tr>`).join('');
const pa=state.transactions.filter(x=>x.type==='paona'&&x.amount-paid(x)>0).map(x=>`<tr><td>${esc(x.person||x.desc)}</td><td>${(+x.amount).toLocaleString('en-IN')}</td><td>${paid(x).toLocaleString('en-IN')}</td><td>${(x.amount-paid(x)).toLocaleString('en-IN')}</td></tr>`).join('');
document.getElementById('report-print-area').innerHTML=`<div style="font-family:'Plus Jakarta Sans',sans-serif;color:#222">
<h2 style="margin:0">হিসাব — Hisab রিপোর্ট</h2><p style="font-size:12px;color:#666;margin:4px 0 12px">নাম: <b>${esc(p.name||'')}</b> ${p.phone?'| মোবাইল: '+esc(p.phone):''} ${p.address?'| '+esc(p.address):''} | তারিখ: ${today()}</p>
<table style="width:100%;border-collapse:collapse;font-size:12px;margin-bottom:14px"><tr><td style="border:1px solid #ddd;padding:6px"><b>মোট আয়</b><br>${ti.toLocaleString('en-IN')} ৳</td><td style="border:1px solid #ddd;padding:6px"><b>মোট ব্যয়</b><br>${te.toLocaleString('en-IN')} ৳</td><td style="border:1px solid #ddd;padding:6px"><b>ব্যালেন্স</b><br>${(ti-te).toLocaleString('en-IN')} ৳</td></tr></table>
<h4>লেনদেন তালিকা</h4><table style="width:100%;border-collapse:collapse;font-size:11px" border="1" cellpadding="4"><thead><tr style="background:#f3ede2"><th>তারিখ</th><th>ক্যাটাগরি</th><th>বিবরণ</th><th>৳</th></tr></thead><tbody>${rows||'<tr><td colspan="4">কোনো লেনদেন নেই</td></tr>'}</tbody></table>
 ${loans?`<h4>বাকি ঋণ</h4><table style="width:100%;border-collapse:collapse;font-size:11px" border="1" cellpadding="4"><tr style="background:#f3ede2"><th>ব্যক্তি</th><th>মোট</th><th>পরিশোধ</th><th>বাকি</th></tr>${loans}</table>`:''}
 ${pa?`<h4>আদায় বাকি পাওনা</h4><table style="width:100%;border-collapse:collapse;font-size:11px" border="1" cellpadding="4"><tr style="background:#f3ede2"><th>ব্যক্তি</th><th>মোট</th><th>আদায়</th><th>বাকি</th></tr>${pa}</table>`:''}
<p style="font-size:10px;color:#999;margin-top:14px">হিসাব — Hisab অ্যাপ দ্বারা তৈরি</p></div>`;
document.getElementById('report-modal').classList.remove('hidden');document.getElementById('report-modal').classList.add('flex')}
function closeReport(){document.getElementById('report-modal').classList.add('hidden');document.getElementById('report-modal').classList.remove('flex')}
function saveAsPdf(){closeSaveFiles();openReport();setTimeout(()=>window.print(),400)}

/*================= RESET / BUDGET / PIN =================*/
function clearAllData(){if(!confirm('সব লেনদেন মুছে যাবে। নিশ্চিত?'))return;state.transactions=[];save();renderAll();toast('মুছে ফেলা হয়েছে')}
function resetAllData(){if(!confirm('প্রোফাইলসহ সব ডাটা মুছে যাবে! নিশ্চিত?'))return;localStorage.removeItem(LS);location.reload()}
function saveBudget(){state.settings.budget=+document.getElementById('monthly-budget').value||0;save();renderSummary();toast(t('saved'))}
function openPinModal(){document.getElementById('pin-new').value='';document.getElementById('pin-modal').classList.remove('hidden');document.getElementById('pin-modal').classList.add('flex')}
function closePinModal(){document.getElementById('pin-modal').classList.add('hidden');document.getElementById('pin-modal').classList.remove('flex')}
function changePin(){openPinModal()}
function savePin(){const v=document.getElementById('pin-new').value;if(!/^\d{4}$/.test(v)){toast('৪ ডিজিটের নম্বর দিন');return}state.pin=v;state.settings.applock=true;save();document.getElementById('tg-applock').checked=true;closePinModal();toast('PIN সেট হয়েছে ✅')}
function tryUnlock(){if(document.getElementById('lock-pin').value===state.pin){const ls=document.getElementById('lock-screen');ls.classList.add('hidden');ls.classList.remove('flex');document.getElementById('lock-pin').value=''}else{toast('❌ ভুল PIN!');document.getElementById('lock-pin').value=''}}

/*================= ADMOB =================*/
const ADMOB_CONFIG={
  APP_ID:'ca-app-pub-7394143721524256~3959612609',
  BANNER_ID:'ca-app-pub-7394143721524256/7188411171',
  INTERSTITIAL_ID:'ca-app-pub-7394143721524256/7188411171'
};
function admobShowBanner(){const box=document.getElementById('admob-banner');if(!box)return;
try{if(window.AdmobAds&&window.AdmobAds.showBannerAd){window.AdmobAds.showBannerAd(ADMOB_CONFIG.BANNER_ID);box.style.display='flex';return}}catch(e){}
try{if(window.admob&&window.admob.BannerAd){new window.admob.BannerAd({adUnitId:ADMOB_CONFIG.BANNER_ID}).show();box.style.display='flex';return}}catch(e){}
try{if(window.Capacitor&&window.Capacitor.Plugins.AdMob){const A=window.Capacitor.Plugins.AdMob;A.initialize({requestTrackingAuthorization:true}).then(()=>A.showBanner({adId:ADMOB_CONFIG.BANNER_ID,position:'BOTTOM_CENTER'}));box.style.display='flex';return}}catch(e){}}
function admobShowInterstitial(){
try{if(window.AdmobAds&&window.AdmobAds.showInterstitialAd){window.AdmobAds.showInterstitialAd(ADMOB_CONFIG.INTERSTITIAL_ID);return}}catch(e){}
try{if(window.Capacitor&&window.Capacitor.Plugins.AdMob){const A=window.Capacitor.Plugins.AdMob;A.prepareInterstitial({adId:ADMOB_CONFIG.INTERSTITIAL_ID}).then(()=>A.showInterstitial())}}catch(e){}}
let _lastAd=0;function maybeInterstitial(){const n=Date.now();if(n-_lastAd>120000){_lastAd=n;admobShowInterstitial()}}

/*================= KEYBOARD FIX =================*/
document.addEventListener('focusin',e=>{const tg=e.target;if(tg&&(tg.tagName==='INPUT'||tg.tagName==='TEXTAREA'||tg.tagName==='SELECT')){setTimeout(()=>{try{tg.scrollIntoView({block:'center',behavior:'smooth'})}catch(err){}},350)}});

/*================= INIT =================*/
function updDT(){const el=document.getElementById('now-dt');if(el)el.textContent=new Date().toLocaleString(state.settings.lang==='bn'?'bn-BD':state.settings.lang==='ar'?'ar':'en-US',{dateStyle:'medium',timeStyle:'short'})}
function init(){load();renderIcons();renderLogo();applyI18n();applyTheme();fillCatSelect();
document.getElementById('lang-top').value=state.settings.lang;document.getElementById('lang-select').value=state.settings.lang;
document.getElementById('monthly-budget').value=state.settings.budget||'';document.getElementById('default-months').value=state.settings.defmonths||12;document.getElementById('reminder-days').value=state.settings.remdays||3;
document.getElementById('trans-type').addEventListener('change',typeToggle);
document.getElementById('tg-applock').addEventListener('change',e=>{state.settings.applock=e.target.checked;save();if(e.target.checked&&!state.pin)openPinModal()});
[['tg-kisti','kisti'],['tg-paona','paona'],['tg-dena','dena'],['sound-toggle','sound'],['tg-finger','finger']].forEach(([id,k])=>{const el=document.getElementById(id);if(el){el.checked=!!state.settings[k];el.addEventListener('change',e=>{state.settings[k]=e.target.checked;save()})}});
if(window.matchMedia)window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change',applyTheme);
renderAll();updDT();setInterval(updDT,30000);
if(state.settings.applock&&state.pin){const ls=document.getElementById('lock-screen');ls.classList.remove('hidden');ls.classList.add('flex')}
window.addEventListener('load',()=>setTimeout(admobShowBanner,800));document.addEventListener('deviceready',admobShowBanner)}
document.addEventListener('DOMContentLoaded',init);
</script>
  <!-- ═══════════ নতুন আপডেট: ফিক্স ১ + ২ + ৩ ═══════════ -->
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@700;800&display=swap" rel="stylesheet">
<style>
  [data-logo]{filter:drop-shadow(0 5px 12px rgba(47,143,60,.35))}
  [id$="-modal"]{transition:padding-bottom .15s ease}
  input,select,textarea{scroll-margin-bottom:16px}
</style>
<script>
/* ── ফিক্স ১: নতুন "হিসাব" লোগো ── */
(function(){
  const LOGO = `<svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg" style="width:100%;height:100%;display:block">
    <defs>
      <linearGradient id="hg" x1="0" y1="0" x2="1" y2="1">
        <stop offset="0%" stop-color="#63C566"/><stop offset="100%" stop-color="#2E8B3A"/>
      </linearGradient>
      <clipPath id="hc"><rect x="5" y="5" width="190" height="190" rx="48"/></clipPath>
    </defs>
    <rect x="5" y="5" width="190" height="190" rx="48" fill="url(#hg)"/>
    <g clip-path="url(#hc)"><ellipse cx="100" cy="12" rx="135" ry="48" fill="#fff" opacity=".22"/></g>
    <rect x="10" y="10" width="180" height="180" rx="42" fill="none" stroke="#fff" stroke-opacity=".85" stroke-width="4"/>
    <path d="M64 92 L64 50" stroke="#fff" stroke-width="6" stroke-linecap="round"/>
    <path d="M63 72 C46 70 37 58 39 44 C54 46 61 57 63 72 Z" fill="#fff"/>
    <path d="M65 72 C82 70 91 58 89 44 C74 46 67 57 65 72 Z" fill="#fff"/>
    <circle cx="64" cy="36" r="16" fill="#fff"/>
    <text x="64" y="45" text-anchor="middle" font-family="'Noto Sans Bengali',sans-serif" font-size="22" font-weight="800" fill="#2E8B3A">৳</text>
    <rect x="42" y="88" width="44" height="11" rx="5.5" fill="#fff"/>
    <path d="M47 99 L81 99 L75 126 Q64 132 53 126 Z" fill="#fff"/>
    <path d="M38 110 C36 125 47 137 63 139 L105 139 C113 139 118 134 118 128 C118 122 113 119 107 120 L87 124 C92 116 87 107 78 108 L58 111 C50 112 46 107 44 111 Z" fill="#fff"/>
    <rect x="27" y="110" width="13" height="26" rx="4.5" fill="#fff"/>
    <circle cx="33.5" cy="123" r="2.2" fill="#2E8B3A"/>
    <text x="143" y="96" text-anchor="middle" font-family="'Noto Sans Bengali',sans-serif" font-size="34" font-weight="800" fill="#fff">হিসাব</text>
    <text x="92" y="163" text-anchor="middle" font-family="'Noto Sans Bengali',sans-serif" font-size="19" font-weight="700" fill="#fff">— حساب —</text>
  </svg>`;
  const paint = () => document.querySelectorAll('[data-logo]').forEach(el => el.innerHTML = LOGO);
  paint();
  document.addEventListener('DOMContentLoaded', paint);
})();

/* ── ফিক্স ২: কিবোর্ডের নিচে ইনপুট চলে যাওয়া ── */
(function(){
  const typing = el => el && ['INPUT','TEXTAREA','SELECT'].includes(el.tagName);
  function adjust(){
    let kb = 0, vh = window.innerHeight;
    if (window.visualViewport){
      vh = window.visualViewport.height;
      kb = Math.max(0, Math.round(window.innerHeight - vh - window.visualViewport.offsetTop));
    }
    document.querySelectorAll('[id$="-modal"], #lock-screen').forEach(m => {
      const open = !m.classList.contains('hidden');
      m.style.paddingBottom = (open && kb) ? kb + 'px' : '';
      m.querySelectorAll(':scope > div').forEach(c => {
        c.style.maxHeight = (open && kb) ? (vh - 28) + 'px' : '';
      });
    });
    const ae = document.activeElement;
    if (typing(ae)){
      clearTimeout(adjust._t);
      adjust._t = setTimeout(() => { try { ae.scrollIntoView({block:'center', behavior:'smooth'}); } catch(e){} }, 130);
    }
  }
  if (window.visualViewport){
    window.visualViewport.addEventListener('resize', adjust);
    window.visualViewport.addEventListener('scroll', adjust);
  }
  window.addEventListener('resize', adjust);
  document.addEventListener('focusin', adjust);
})();

/* ── ফিক্স ৩ (অটো অংশ): এডিটে সঠিক ক্যাটাগরি বসানো ── */
(function(){
  const modal = document.getElementById('add-modal');
  const sel = document.getElementById('trans-category-select');
  if (!modal || !sel) return;
  function applyCat(){
    const target = window.__editCat;
    if (!target) return;
    if (!Array.from(sel.options).some(o => o.value === target)){
      const o = document.createElement('option');
      o.value = target; o.textContent = target;
      sel.appendChild(o);
    }
    sel.value = target;
  }
  new MutationObserver(() => {
    if (modal.classList.contains('hidden')){ window.__editCat = null; return; }
    [0, 80, 200, 400].forEach(ms => setTimeout(applyCat, ms));
  }).observe(modal, { attributes:true, attributeFilter:['class'] });
})();
</script>
</body>
</html>
