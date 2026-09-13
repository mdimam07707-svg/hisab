<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>হিসাব — Hisab</title>
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://accounts.google.com/gsi/client" async defer></script>
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
  <div class="flex items-center gap-2.5">
    <div class="w-11 h-11 shrink-0" data-logo></div>
    <div>
      <p class="text-[11px] text-muted leading-none" data-i18n="welcome">স্বাগতম,</p>
      <h1 id="header-name" class="text-base font-extrabold leading-tight">রাহিম আহমেদ</h1>
      <p class="text-[9px] font-bold text-tealx leading-none mt-0.5">হিসাব • Hisab</p>
    </div>
  </div>
  <div class="flex items-center gap-2">
    <button onclick="openReport()" title="প্রিন্ট / PDF" class="hdr-icon card text-ink"><span data-icon="printer" class="w-4 h-4"></span></button>
    <button onclick="openSaveFiles()" title="ডাউনলোড / সেভ" class="hdr-icon card text-clay"><span data-icon="download" class="w-4 h-4"></span></button>
    <select id="lang-top" onchange="setLanguage(this.value)" class="lang-pill"><option value="bn">🇧🇩 বাংলা</option><option value="en">🇬🇧 EN</option><option value="ar">🇸🇦 AR</option><option value="zh">🇨🇳 中</option></select>
    <button onclick="openProfile()" class="w-11 h-11 rounded-2xl overflow-hidden border-2 border-white shadow-md bg-sand"><img id="header-avatar" src="" class="w-full h-full object-cover"></button>
  </div>
</header>

<main class="flex-grow container mx-auto px-5 py-3 max-w-md space-y-5 pb-6">
  <section onclick="openProfile()" class="card rounded-3xl p-4 flex items-center gap-3.5 cursor-pointer">
    <img id="summary-avatar" src="" class="w-16 h-16 rounded-2xl object-cover border-2 border-cream bg-sand">
    <div class="flex-1 min-w-0"><h2 id="summary-name" class="text-sm font-extrabold truncate">রাহিম আহমেদ</h2><p id="summary-bio" class="text-[11px] text-muted truncate">পরিচিতি যোগ করুন</p><p id="summary-phone" class="text-[11px] text-muted truncate"></p></div>
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
    <div class="flex justify-between items-center mb-2"><div class="flex items-center gap-2"><div class="w-7 h-7 rounded-lg icon-well flex items-center justify-center text-clay"><span data-icon="coins" class="w-4 h-4"></span></div><h3 class="text-xs font-bold" data-i18n="loanSec">ঋণ ও পরিশোধ</h3></div><button onclick="openAddModal('ঋণ নেওয়া','debt')" class="text-[11px] font-semibold text-clay">+ <span data-i18n="loan">ঋণ</span></button></div>
    <div id="loan-list" class="space-y-2"></div>
  </section>
  <section class="card rounded-3xl p-4 border-l-[3px] border-l-plum">
    <div class="flex justify-between items-center mb-2"><div class="flex items-center gap-2"><div class="w-7 h-7 rounded-lg icon-well flex items-center justify-center text-plum"><span data-icon="hand" class="w-4 h-4"></span></div><h3 class="text-xs font-bold" data-i18n="paonaSec">পাওনা আদায়</h3></div><button onclick="openAddModal('পাওনা','paona')" class="text-[11px] font-semibold text-plum">+ <span data-i18n="paona">পাওনা</span></button></div>
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
    <div class="flex-1 min-w-0"><b id="settings-name" class="text-sm truncate block">রাহিম আহমেদ</b><p id="settings-phone" class="text-[11px] text-muted truncate"></p><p class="text-[10px] text-clay font-semibold mt-0.5" data-i18n="editE">সম্পাদনা</p></div>
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
      <button onclick="changePin()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold">🔑 <span data-i18n="stChangePin">PIN পরিবর্তন</span></button>
      <details><summary class="font-semibold text-muted cursor-pointer">🛡️ <span data-i18n="stPrivacy">প্রাইভেসি</span></summary><p class="text-[10px] text-muted pt-2 leading-relaxed" data-i18n="privTxt">সব তথ্য এই ডিভাইসে ও আপনার Drive-এই থাকে।</p></details>
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
      <button onclick="driveConnectAndSave()" class="w-full py-2.5 rounded-xl bg-clay text-white font-bold flex items-center justify-center gap-2"><span data-icon="cloud" class="w-4 h-4"></span><span data-i18n="driveSave">Google Drive Sync</span></button>
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
      <div><label class="block font-semibold text-muted mb-1">🏷️ <span data-i18n="stDefCat">ডিফল্ট ক্যাটাগরি</span></label><select id="default-cat" onchange="localStorage.setItem('hd_defcat',this.value);toast(t('saved'))" class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2"></select></div>
      <div><label class="block font-semibold text-muted mb-1">🎯 <span data-i18n="stBudget">মাসিক বাজেট (৳)</span></label><div class="flex gap-2"><input type="number" id="monthly-budget" class="flex-1 bg-cream border border-black/5 rounded-xl px-3 py-2"><button onclick="saveBudget()" class="px-4 rounded-xl bg-clay text-white font-bold"><span data-icon="save" class="w-4 h-4"></span></button></div></div>
      <div><label class="block font-semibold text-muted mb-1">📆 <span data-i18n="stKistiSet">কিস্তি — ডিফল্ট মাস</span></label><input type="number" id="default-months" min="1" onchange="localStorage.setItem('hd_defmonths',this.value);toast(t('saved'))" class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2"></div>
      <div><label class="block font-semibold text-muted mb-1">⏰ <span data-i18n="stRemDays">রিমাইন্ডার — দিন আগে</span></label><input type="number" id="reminder-days" min="1" onchange="localStorage.setItem('hd_remdays',this.value);toast(t('saved'));renderReminders()" class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2"></div>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-help">
    <button onclick="accToggle('acc-help','accw-help')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">🆘</span><span class="flex-1 font-bold" data-i18n="stHelp">সাহায্য</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-help" class="accordion-body bg-white"><div class="p-4 space-y-2">
      <details><summary class="font-semibold cursor-pointer">❓ কিভাবে ঋণ যোগ করব?</summary><p class="text-[10px] text-muted pt-1.5">+ বাটন → ধরণ "ঋণ (নেওয়া)" → ব্যক্তির নাম ও মাস দিন। ঋণ তালিকায় নামে ক্লিক করে পরিশোধ করুন।</p></details>
      <details><summary class="font-semibold cursor-pointer">❓ ডাটা হারাবো না তো?</summary><p class="text-[10px] text-muted pt-1.5">ডাটা ফোনেই থাকে। Drive Sync বা Backup নিলে নিরাপদ।</p></details>
      <a href="mailto:support@hisab.app" class="block w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold text-center">✉️ <span data-i18n="stFeedback">ফিডব্যাক</span></a>
    </div></div>
  </div>
  <div class="rounded-2xl border border-black/5 overflow-hidden card" id="accw-about">
    <button onclick="accToggle('acc-about','accw-about')" class="w-full flex items-center gap-2.5 px-4 py-3 bg-cream text-left"><span class="w-8 h-8 rounded-lg bg-white flex items-center justify-center">ℹ️</span><span class="flex-1 font-bold" data-i18n="stAbout">অ্যাপ সম্পর্কে</span><span class="chev w-4 h-4" data-icon="chevron"></span></button>
    <div id="acc-about" class="accordion-body bg-white"><div class="p-4 space-y-2">
      <div class="flex justify-between"><span data-i18n="stVersion">ভার্সন</span><b>v4.2</b></div>
      <details><summary class="font-semibold cursor-pointer">🛡️ <span data-i18n="stPolicy">প্রাইভেসি পলিসি</span></summary><p class="text-[10px] text-muted pt-1.5">সব ডাটা আপনার ডিভাইসে ও আপনার অনুমতিতে আপনার Google Drive-এ থাকে।</p></details>
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

<div id="toast" class="bg-ink text-cream text-xs font-semibold px-5 py-3 rounded-2xl shadow-xl"></div>

<div id="lock-screen" class="fixed inset-0 z-[100] bg-ink hidden flex-col items-center justify-center gap-4 p-8 text-center">
  <div class="w-16 h-16" data-logo></div>
  <img id="lock-avatar" src="" class="w-20 h-20 rounded-full border-4 border-clay2 object-cover">
  <b id="lock-name" class="text-cream text-lg"></b>
  <input type="password" id="lock-pin" maxlength="4" inputmode="numeric" placeholder="PIN" class="w-32 text-center tracking-[0.5em] text-lg bg-white/10 text-cream rounded-xl py-2.5 border border-white/20">
  <button onclick="tryUnlock()" class="px-8 py-3 rounded-2xl bg-clay text-white font-bold">🔓 আনলক</button>
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
        <div><label id="person-label" class="block text-[11px] font-semibold text-muted mb-1">ব্যক্তির নাম</label><input type="text" id="trans-person" class="w-full bg-cream border border-black/5 rounded-xl px-3.5 py-2.5 text-xs"></div>
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
    <div id="category-groups" class="space-y-2.5 overflow-y-auto pr-1"></div>
  </div>
</div>

<div id="detail-modal" class="fixed inset-0 z-50 bg-ink/50 backdrop-blur-sm hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
  <div class="card w-full max-w-md rounded-t-[28px] p-6 max-h-[90vh] overflow-y-auto space-y-3">
    <div class="flex justify-between items-center"><h3 class="font-bold text-sm" data-i18n="detail">বিস্তারিত</h3><button onclick="closeDetail()" class="w-8 h-8 rounded-full icon-well flex items-center justify-center"><span data-icon="xmark" class="w-3.5 h-3.5"></span></button></div>
    <div id="detail-body" class="text-xs space-y-2"></div>
    <div class="flex gap-2 pt-1">
      <button id="detail-edit-btn" class="flex-1 py-2.5 rounded-xl bg-cream border border-black/10 font-bold flex items-center justify-center gap-1.5"><span data-icon="pencil" class="w-3.5 h-3.5"></span><span data-i18n="editE">সম্পাদনা</span></button>
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
    <div class="relative w-24 h-24 mx-auto"><img id="profile-avatar-preview" src="" class="w-24 h-24 rounded-full object-cover border-4 border-cream bg-sand"><label id="photo-label" class="absolute bottom-0 right-0 w-8 h-8 rounded-full bg-clay flex items-center justify-center cursor-pointer border-2 border-white text-white"><span data-icon="camera" class="w-3.5 h-3.5"></span><input type="file" id="profile-photo-input" accept="image/*" class="hidden" disabled onchange="previewProfilePhoto(event)"></label></div>
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
    <p class="text-[11px] text-muted" data-i18n="emailOnPhone">ফোনে সাইন-ইন থাকা Gmail-এর Drive-এ “হিসাব_ব্যাকআপ/তারিখ” ফোল্ডারে ফাইল সেভ হবে।</p>
    <p id="drive-status" class="text-[10px] font-semibold text-sage"></p>
    <button onclick="driveConnectAndSave()" class="w-full py-3 rounded-xl bg-clay text-white font-bold flex items-center justify-center gap-2"><span data-icon="cloud" class="w-4 h-4"></span><span data-i18n="driveSave">Drive-এ সেভ</span></button>
    <button onclick="downloadTxt()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="download" class="w-4 h-4"></span><span data-i18n="memTxt">মেমোরিতে (.txt)</span></button>
    <button onclick="exportData()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="download" class="w-4 h-4"></span><span data-i18n="memJson">মেমোরিতে (.json)</span></button>
    <button onclick="saveAsPdf()" class="w-full py-2.5 rounded-xl bg-cream border border-black/10 font-semibold flex items-center justify-center gap-2"><span data-icon="printer" class="w-4 h-4"></span><span data-i18n="pdfSave">PDF</span></button>
    <details><summary class="font-semibold text-muted cursor-pointer">Client ID</summary><input type="text" id="gcid" placeholder="Google OAuth Client ID" class="w-full bg-cream border border-black/5 rounded-xl px-3 py-2.5 text-[10px] mt-2"></details>
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
/* ============ ICONS ============ */
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
'file-invoice':'<path d="M7 3h7l4 4v14H7Z"/><path d="M14 3v4h4"/><path d="M9 9h2M9 12h6M9 15h6"/>',
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
pencil:'<path d="M12 20h9"/><path d="M16.5 3.5a2.1 2.1 0 0 1 3 3L7 19l-4 1 1-4Z"/>',
save:'<path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2Z"/><path d="M17 21v-8H7v8M7 3v5h8"/>',
hand:'<path d="M8 12V6a1.5 1.5 0 0 1 3 0v5"/><path d="M11 11V4.5a1.5 1.5 0 0 1 3 0V11"/><path d="M14 11V6a1.5 1.5 0 0 1 3 0v7a7 7 0 0 1-7 7h-.5a6 6 0 0 1-5-2.7L2.7 14A1.5 1.5 0 0 1 5 12l3 2"/>',
bell:'<path d="M6 8a6 6 0 0 1 12 0c0 7 2 8 2 8H4s2-1 2-8Z"/><path d="M10 20a2 2 0 0 0 4 0"/>',
tractor:'<circle cx="7" cy="17" r="3.5"/><circle cx="17.5" cy="18.5" r="2.5"/><path d="M4 13V7h5l2 6h5l2.5 4"/><path d="M9 7V4h3"/>',
leaf:'<path d="M5 19C5 9 13 5 20 4c0 8-4 15-13 15"/><path d="M5 19c3-5 7-8 11-10"/>',
sprout:'<path d="M12 21v-8"/><path d="M12 13c0-4 3-6 7-6 0 4-3 6-7 6Z"/><path d="M12 13c0-4-3-6-7-6 0 4 3 6 7 6Z"/>',
chicken:'<path d="M4 11c2-5 8-7 12-4 2 1.5 3 4 3 6 0 4-3 7-8 7-4 0-7-2-7-6Z"/><path d="M12 20v-3M8 20v-3"/><circle cx="15.5" cy="9" r=".6"/>',
cow:'<path d="M4 5v4M20 5v4"/><path d="M4 9h16v6a5 5 0 0 1-5 5h-6a5 5 0 0 1-5-5V9Z"/><circle cx="9" cy="13" r=".5"/><circle cx="15" cy="13" r=".5"/>',
fish:'<path d="M3 12s4-6 9-6c4 0 7 2.5 9 6-2 3.5-5 6-9 6-5 0-9-6-9-6Z"/><circle cx="8" cy="11" r=".7"/><path d="M21 12l2-3M21 12l2 3"/>',
baby:'<circle cx="12" cy="9" r="5"/><path d="M10 8.5h.01M14 8.5h.01M10.5 11c.8.8 2.2.8 3 0"/><path d="M4 21c0-4 3.5-6 8-6s8 2 8 6"/>',
dog:'<path d="M5 4c2 0 3 1.5 3 3M19 4c-2 0-3 1.5-3 3"/><path d="M8 7h8v6a4 4 0 0 1-8 0V7Z"/><path d="M8 9H5v4h3M16 9h3v4h-3"/><path d="M10 19v2M14 19v2"/>',
soap:'<rect x="4" y="9" width="16" height="10" rx="3"/><circle cx="9" cy="14" r="1"/><circle cx="15" cy="14" r="1"/><path d="M9 5c0-1.5 1-2 1.5-2.5M14 5c0-1.5 1-2 1.5-2.5"/>',
hammer:'<path d="M14 6l4 4-2 2-4-4Z"/><path d="M12 8 4 16l4 4 8-8"/>',
paint:'<rect x="3" y="3" width="18" height="8" rx="1"/><path d="M12 11v3"/><rect x="9" y="14" width="6" height="7" rx="1"/>',
cake:'<rect x="5" y="13" width="14" height="7"/><path d="M5 16c2 2 4-1 7 0s5-2 7-1"/><path d="M12 9V6"/><path d="M12 3c-1 1.5-1 2 0 3 1-1 1-1.5 0-3Z"/>',
music:'<path d="M9 18V5l10-2v13"/><circle cx="6.5" cy="18" r="2.5"/><circle cx="16.5" cy="16" r="2.5"/>',
ball:'<circle cx="12" cy="12" r="9"/><path d="M12 3c3 3 3 15 0 18M3.5 9c5 2 12 2 17 0M3.5 15c5-2 12-2 17 0"/>',
umbrella:'<path d="M12 3a9 9 0 0 1 9 9H3a9 9 0 0 1 9-9Z"/><path d="M12 12v6a2 2 0 0 0 4 0"/>',
clock:'<circle cx="12" cy="12" r="9"/><path d="M12 7v5l3 2"/>',
ticket:'<rect x="3" y="7" width="18" height="10" rx="2"/><path d="M15 7v10" stroke-dasharray="2 2"/>',
flower:'<circle cx="12" cy="9" r="2"/><circle cx="9" cy="11.5" r="2"/><circle cx="15" cy="11.5" r="2"/><circle cx="10.5" cy="14.5" r="2"/><circle cx="13.5" cy="14.5" r="2"/><path d="M12 17v4"/>',
broom:'<path d="M19 3l-7 7"/><path d="M12 10l-4 4 2 2 4-4"/><path d="M8 14c-3 1-4 4-4 7 3 0 6-1 7-4Z"/>',
bucket:'<path d="M5 7h14l-1.5 12a2 2 0 0 1-2 1.7h-7A2 2 0 0 1 6.5 19L5 7Z"/><path d="M5 7a7 2.5 0 0 1 14 0"/>',
key:'<circle cx="8" cy="15" r="4"/><path d="M11 12 20 3M16 7l3 3M13 10l2 2"/>',
book:'<path d="M12 6c-2-1.5-5-2-9-2v14c4 0 7 .5 9 2 2-1.5 5-2 9-2V4c-4 0-7 .5-9 2Z"/><path d="M12 6v14"/>',
star:'<path d="M12 3l2.7 5.5 6.3.9-4.5 4.4 1 6.2-5.5-3-5.5 3 1-6.2L3 9.4l6.3-.9L12 3Z"/>',
map:'<path d="M9 4 3 6v14l6-2 6 2 6-2V4l-6 2-6-2Z"/><path d="M9 4v14M15 6v14"/>',
mic:'<rect x="9" y="3" width="6" height="11" rx="3"/><path d="M5 11a7 7 0 0 0 14 0M12 18v3"/>',
speaker:'<rect x="6" y="3" width="12" height="18" rx="2"/><circle cx="12" cy="15" r="3.5"/><circle cx="12" cy="7.5" r="1"/>',
sun:'<circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2M2 12h2M20 12h2M4.9 4.9l1.4 1.4M17.7 17.7l1.4 1.4M19.1 4.9l-1.4 1.4M6.3 17.7l-1.4 1.4"/>',
milk:'<path d="M8 2h8v3l2 5v11a1 1 0 0 1-1 1H7a1 1 0 0 1-1-1V10l2-5V2Z"/><path d="M6 12h12"/>',
bread:'<path d="M4 11c0-2 1.5-3.5 3.5-3.5.3-1.5 2-2.5 4.5-2.5s4.2 1 4.5 2.5c2 0 3.5 1.5 3.5 3.5 0 1.2-.6 2.2-1.5 2.8V19a1 1 0 0 1-1 1H6.5a1 1 0 0 1-1-1v-5.2C4.6 13.2 4 12.2 4 11Z"/>',
truck:'<path d="M2 6h11v10H2z"/><path d="M13 9h4l3 3v4h-7"/><circle cx="6" cy="18" r="1.6"/><circle cx="16.5" cy="18" r="1.6"/>',
boat:'<path d="M4 15h16l-2 4H6Z"/><path d="M12 15V4l6 8Z"/>'};
function iconSvg(n){return `<svg class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" width="100%" height="100%">${ICON_PATHS[n]||ICON_PATHS.dots}</svg>`}
/* ★ অ্যাপ লোগো */
const LOGO_SVG=`<svg viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg" style="width:100%;height:100%;display:block">
<rect width="120" height="120" rx="30" fill="#157E8E"/>
<rect x="18" y="80" width="12" height="18" rx="4" fill="#fff"/><circle cx="24" cy="92" r="2" fill="#157E8E"/>
<path d="M28 96c2-12 14-18 30-18h18c9 0 12 10 4 15l-12 6c-13 5-29 4-40-3z" fill="#fff"/>
<path d="M44 66h26l-4 13H48z" fill="#fff"/>
<rect x="55" y="44" width="4" height="24" rx="2" fill="#fff"/>
<path d="M55 54C45 54 38 48 38 39c10 0 17 6 17 15z" fill="#fff"/>
<path d="M59 54c10 0 17-6 17-15-10 0-17 6-17 15z" fill="#fff"/>
<circle cx="57" cy="29" r="13" fill="#fff"/>
<text x="57" y="35.5" text-anchor="middle" font-size="17" font-weight="800" fill="#157E8E">৳</text>
</svg>`;
function mountIcons(){document.querySelectorAll('[data-icon]').forEach(el=>el.innerHTML=iconSvg(el.getAttribute('data-icon')));
document.querySelectorAll('[data-logo]').forEach(el=>el.innerHTML=LOGO_SVG)}

/* ============ i18N ============ */
let LANG=localStorage.getItem('hd_lang')||'bn';
const MONTHS={bn:['জানুয়ারি','ফেব্রুয়ারি','মার্চ','এপ্রিল','মে','জুন','জুলাই','আগস্ট','সেপ্টেম্বর','অক্টোবর','নভেম্বর','ডিসেম্বর'],en:['January','February','March','April','May','June','July','August','September','October','November','December'],ar:['يناير','فبراير','مارس','أبريل','مايو','يونيو','يوليو','أغسطس','سبتمبر','أكتوبر','نوفمبر','ديسمبر'],zh:['一月','二月','三月','四月','五月','六月','七月','八月','九月','十月','十一月','十二月']};
const T={
bn:{welcome:'স্বাগতম,',balance:'মোট ব্যালেন্স',income:'আয়',expense:'ব্যয়',loan:'ঋণ',debtT:'ঋণ (নেওয়া)',paona:'পাওনা',paonaT:'পাওনা',paonaSec:'পাওনা আদায়',loanSec:'ঋণ ও পরিশোধ',quick:'দ্রুত ক্যাটাগরি',viewAll:'সব ক্যাটাগরি দেখুন',recent:'সাম্প্রতিক লেনদেন (ট্যাপ = বিস্তারিত)',all:'সব',clear:'সব মুছুন',summary:'সামারি',thisMonth:'এই মাস',h1:'ফেব্রুয়ারি–জুলাই (৬ মাস)',h2:'জুলাই–ফেব্রুয়ারি (৬ মাস)',year:'১ বছর',desc:'বিবরণ',amount:'টাকার পরিমাণ (৳)',type:'ধরণ',expenseT:'ব্যয়',incomeT:'আয়',cat:'ক্যাটাগরি',lenderDebt:'কার কাছ থেকে ঋণ?',lenderPaona:'কার কাছে পাওনা আছে?',monthsL:'কত মাসে?',voucher:'ভাউচার / ছবি',photo:'ছবি তুলুন / আপলোড',save:'সংরক্ষণ',profile:'প্রোফাইল',name:'নাম',mobile:'মোবাইল',occ:'পেশা',email:'ইমেইল',address:'ঠিকানা',bio:'Bio',updateP:'আপডেট',settings:'সেটিংস',language:'ভাষা',report:'রিপোর্ট (A4)',restore:'রিস্টোর',saveFileT:'ফাইল সেভ / শেয়ার',driveSave:'Google Drive-এ সেভ',memTxt:'মেমোরিতে (.txt)',memJson:'মেমোরিতে (.json)',pdfSave:'PDF (প্রিন্ট)',emailOnPhone:'ফোনে সাইন-ইন থাকা Gmail-এর Drive-এ তারিখের ফোল্ডারে ফাইল সেভ হবে।',repay:'ঋণ পরিশোধ',total:'মোট',monthly:'মাসিক কিস্তি',repaid:'পরিশোধিত',remaining:'বাকি',repayAmt:'পরিশোধ (৳)',saveRepay:'সংরক্ষণ',collect:'পাওনা আদায়',collectAmt:'আদায় (৳)',saveCollect:'সংরক্ষণ',given:'পাওনা',collected:'আদায়',noLoan:'কোনো ঋণ নেই',noPaona:'কোনো পাওনা নেই',saved:'সংরক্ষিত ✓',empty:'কোনো তথ্য নেই',date:'তারিখ',advisor:'স্মার্ট অ্যানালাইজার',loanTaken:'ঋণ নেওয়া',balanceL:'ব্যালেন্স',detail:'বিস্তারিত',editE:'সম্পাদনা',del:'মুছুন',history:'ইতিহাস',editTitle:'এন্ট্রি সম্পাদনা',person:'ব্যক্তি',typeL:'ধরণ',home:'হোম',accounts:'সব হিসাব',sixSum:'৬ মাসের সামারি',trend:'মাসভিত্তিক ধারা',stNotif:'নোটিফিকেশন',stKistiRem:'কিস্তি রিমাইন্ডার',stPaonaRem:'পাওনা রিমাইন্ডার',stDenaRem:'দেনা রিমাইন্ডার',stSound:'সাউন্ড ও ভাইব্রেশন',stSec:'সিকিউরিটি ও প্রাইভেসি',stChangePin:'PIN পরিবর্তন',stPrivacy:'প্রাইভেসি',privTxt:'সব তথ্য ডিভাইসে ও আপনার Drive-এই থাকে।',stAppear:'থিম',stLight:'লাইট',stDark:'ডার্ক',stLangReg:'ভাষা ও অঞ্চল',stCurrency:'মুদ্রা',stDateReg:'তারিখ ও সময়',stBackup:'ব্যাকআপ ও ডাটা',stFileSave:'ফাইল সেভ',stBackupJson:'ব্যাকআপ (.json)',stExpTxt:'TXT এক্সপোর্ট',stAccSet:'হিসাবের সেটিংস',stDefCat:'ডিফল্ট ক্যাটাগরি',stBudget:'মাসিক বাজেট (৳)',stKistiSet:'কিস্তি — ডিফল্ট মাস',stRemDays:'রিমাইন্ডার — দিন আগে',stHelp:'সাহায্য',stFeedback:'ফিডব্যাক',stAbout:'অ্যাপ সম্পর্কে',stVersion:'ভার্সন',stPolicy:'প্রাইভেসি পলিসি',stTerms:'শর্তাবলি',stReset:'সব ডাটা মুছুন (রিসেট)'},
en:{welcome:'Welcome,',balance:'Total Balance',income:'Income',expense:'Expense',loan:'Loan',debtT:'Loan (taken)',paona:'Receivable',paonaT:'Receivable',paonaSec:'Receivables',loanSec:'Loans & Repayment',quick:'Quick Categories',viewAll:'View all categories',recent:'Recent (tap for details)',all:'All',clear:'Clear all',summary:'Summary',thisMonth:'This Month',h1:'Feb–Jul (6 mo)',h2:'Jul–Feb (6 mo)',year:'1 Year',desc:'Description',amount:'Amount (৳)',type:'Type',expenseT:'Expense',incomeT:'Income',cat:'Category',lenderDebt:'Borrowed from whom?',lenderPaona:'Who owes you?',monthsL:'How many months?',voucher:'Voucher / photo',photo:'Take / upload',save:'Save',profile:'Profile',name:'Name',mobile:'Mobile',occ:'Occupation',email:'Email',address:'Address',bio:'Bio',updateP:'Update',settings:'Settings',language:'Language',report:'Report (A4)',restore:'Restore',saveFileT:'Save / Share files',driveSave:'Save to Drive',memTxt:'Memory (.txt)',memJson:'Memory (.json)',pdfSave:'PDF (print)',emailOnPhone:'Files saved to Drive of signed-in Gmail, in a date folder.',repay:'Repay',total:'Total',monthly:'Monthly',repaid:'Repaid',remaining:'Remaining',repayAmt:'Amount (৳)',saveRepay:'Save',collect:'Collect',collectAmt:'Amount (৳)',saveCollect:'Save',given:'Receivable',collected:'Collected',noLoan:'No loans yet',noPaona:'No receivables',saved:'Saved ✓',empty:'No data',date:'Date',advisor:'Smart Analyzer',loanTaken:'Loan taken',balanceL:'Balance',detail:'Details',editE:'Edit',del:'Delete',history:'History',editTitle:'Edit entry',person:'Person',typeL:'Type',home:'Home',accounts:'Accounts',sixSum:'6-Month Summary',trend:'Monthly trend',stNotif:'Notifications',stKistiRem:'Installment reminder',stPaonaRem:'Receivable reminder',stDenaRem:'Debt reminder',stSound:'Sound & Vibration',stSec:'Security & Privacy',stChangePin:'Change PIN',stPrivacy:'Privacy',privTxt:'All data stays on device & your Drive.',stAppear:'Appearance',stLight:'Light',stDark:'Dark',stLangReg:'Language & Region',stCurrency:'Currency',stDateReg:'Date & Time',stBackup:'Backup & Data',stFileSave:'File save',stBackupJson:'Backup (.json)',stExpTxt:'Export TXT',stAccSet:'Accounting settings',stDefCat:'Default category',stBudget:'Monthly budget (৳)',stKistiSet:'Installments — months',stRemDays:'Reminder — days before',stHelp:'Help',stFeedback:'Feedback',stAbout:'About',stVersion:'Version',stPolicy:'Privacy Policy',stTerms:'Terms',stReset:'Reset all data'},
ar:{welcome:'مرحباً،',balance:'الرصيد',income:'دخل',expense:'مصروف',loan:'قرض',debtT:'قرض (مأخوذ)',paona:'مديونية له',paonaT:'مديونية له',paonaSec:'تحصيل المديونيات',loanSec:'القروض',quick:'فئات سريعة',viewAll:'كل الفئات',recent:'المعاملات الأخيرة',all:'الكل',clear:'حذف الكل',summary:'ملخص',thisMonth:'هذا الشهر',h1:'فبراير–يوليو',h2:'يوليو–فبراير',year:'سنة',desc:'الوصف',amount:'المبلغ',type:'النوع',expenseT:'مصروف',incomeT:'دخل',cat:'الفئة',lenderDebt:'ممن؟',lenderPaona:'من عليه؟',monthsL:'كم شهراً؟',voucher:'سند',photo:'صورة',save:'حفظ',profile:'الملف',name:'الاسم',mobile:'الهاتف',occ:'المهنة',email:'البريد',address:'العنوان',bio:'نبذة',updateP:'تحديث',settings:'الإعدادات',language:'اللغة',report:'تقرير',restore:'استعادة',saveFileT:'حفظ الملفات',driveSave:'حفظ في Drive',memTxt:'ذاكرة (.txt)',memJson:'ذاكرة (.json)',pdfSave:'PDF',emailOnPhone:'تُحفظ في Drive لحساب Gmail.',repay:'سداد',total:'الإجمالي',monthly:'شهري',repaid:'المسدد',remaining:'المتبقي',repayAmt:'المبلغ',saveRepay:'حفظ',collect:'تحصيل',collectAmt:'المبلغ',saveCollect:'حفظ',given:'مديونية',collected:'المحصّل',noLoan:'لا قروض',noPaona:'لا مديونيات',saved:'تم ✓',empty:'لا بيانات',date:'التاريخ',advisor:'محلل ذكي',loanTaken:'قرض',balanceL:'الرصيد',detail:'تفاصيل',editE:'تعديل',del:'حذف',history:'السجل',editTitle:'تعديل',person:'الشخص',typeL:'النوع',home:'الرئيسية',accounts:'الحسابات',sixSum:'ملخص ٦ أشهر',trend:'الاتجاه الشهري',stNotif:'الإشعارات',stKistiRem:'تذكير الأقساط',stPaonaRem:'تذكير المديونيات',stDenaRem:'تذكير الديون',stSound:'الصوت',stSec:'الأمان',stChangePin:'تغيير PIN',stPrivacy:'الخصوصية',privTxt:'البيانات على الجهاز و Drive.',stAppear:'المظهر',stLight:'فاتح',stDark:'داكن',stLangReg:'اللغة والمنطقة',stCurrency:'العملة',stDateReg:'التاريخ',stBackup:'النسخ الاحتياطي',stFileSave:'حفظ',stBackupJson:'نسخة (.json)',stExpTxt:'تصدير TXT',stAccSet:'إعدادات الحسابات',stDefCat:'الفئة الافتراضية',stBudget:'الميزانية',stKistiSet:'أقساط — أشهر',stRemDays:'تذكير — أيام',stHelp:'المساعدة',stFeedback:'ملاحظات',stAbout:'حول',stVersion:'الإصدار',stPolicy:'الخصوصية',stTerms:'الشروط',stReset:'إعادة تعيين الكل'},
zh:{welcome:'欢迎，',balance:'总余额',income:'收入',expense:'支出',loan:'贷款',debtT:'贷款（借入）',paona:'应收款',paonaT:'应收款',paonaSec:'应收款收回',loanSec:'贷款与还款',quick:'快速分类',viewAll:'所有分类',recent:'最近交易',all:'全部',clear:'全部删除',summary:'汇总',thisMonth:'本月',h1:'2月–7月',h2:'7月–2月',year:'1年',desc:'描述',amount:'金额',type:'类型',expenseT:'支出',incomeT:'收入',cat:'分类',lenderDebt:'向谁？',lenderPaona:'谁欠您？',monthsL:'几个月？',voucher:'凭证',photo:'拍照',save:'保存',profile:'资料',name:'姓名',mobile:'手机',occ:'职业',email:'邮箱',address:'地址',bio:'简介',updateP:'更新',settings:'设置',language:'语言',report:'报告',restore:'恢复',saveFileT:'保存文件',driveSave:'保存到云端硬盘',memTxt:'存储 (.txt)',memJson:'存储 (.json)',pdfSave:'PDF',emailOnPhone:'文件将保存到本机 Gmail 的云端硬盘。',repay:'还款',total:'总计',monthly:'每月',repaid:'已还',remaining:'剩余',repayAmt:'金额',saveRepay:'保存',collect:'收回',collectAmt:'金额',saveCollect:'保存',given:'应收款',collected:'已收回',noLoan:'暂无贷款',noPaona:'暂无应收款',saved:'已保存 ✓',empty:'暂无数据',date:'日期',advisor:'智能分析',loanTaken:'贷款',balanceL:'余额',detail:'详情',editE:'编辑',del:'删除',history:'记录',editTitle:'编辑',person:'人员',typeL:'类型',home:'主页',accounts:'账目',sixSum:'6个月汇总',trend:'月度趋势',stNotif:'通知',stKistiRem:'分期提醒',stPaonaRem:'应收提醒',stDenaRem:'债务提醒',stSound:'声音与震动',stSec:'安全与隐私',stChangePin:'更改 PIN',stPrivacy:'隐私',privTxt:'数据保存在设备和云端硬盘。',stAppear:'外观',stLight:'浅色',stDark:'深色',stLangReg:'语言与地区',stCurrency:'货币',stDateReg:'日期与时间',stBackup:'备份与数据',stFileSave:'保存',stBackupJson:'备份 (.json)',stExpTxt:'导出 TXT',stAccSet:'记账设置',stDefCat:'默认分类',stBudget:'月度预算',stKistiSet:'分期 — 月数',stRemDays:'提醒 — 提前天数',stHelp:'帮助',stFeedback:'反馈',stAbout:'关于',stVersion:'版本',stPolicy:'隐私政策',stTerms:'条款',stReset:'重置所有数据'}};
function t(k){return (T[LANG]&&T[LANG][k])||T.bn[k]||k}
const BN_D='০১২৩৪৫৬৭৮৯',toBn=s=>String(s).replace(/[0-9]/g,d=>BN_D[d]);
function money(n){n=Number(n)||0;const s=n.toLocaleString('en-IN',{maximumFractionDigits:2});return '৳ '+(LANG==='bn'?toBn(s):s)}
function todayIso(){const d=new Date();return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0')}
function fmtDate(iso){if(!iso)return '';const d=new Date(iso+'T00:00:00');const loc={bn:'bn-BD',en:'en-GB',ar:'ar-EG',zh:'zh-CN'}[LANG]||'bn-BD';try{return d.toLocaleDateString(loc,{day:'numeric',month:'long',year:'numeric'})}catch(e){return iso}}
function typeLabel(ty){return ty==='income'?t('income'):ty==='expense'?t('expense'):ty==='debt'?t('debtT'):t('paonaT')}
function typeColor(ty){return ty==='income'?'text-sage':ty==='debt'?'text-clay':ty==='paona'?'text-plum':'text-berry'}
function setLanguage(l){LANG=l;localStorage.setItem('hd_lang',l);applyLanguage();toast(t('saved'))}

/* ============ ক্যাটাগরি অনুবাদ ============ */
const GTX={'বিল ও ইউটিলিটি':['Bills & Utilities','الفواتير والمرافق','账单与公用事业'],'খাদ্য ও বাজার':['Food & Market','الطعام والسوق','食品与市场'],'যাতায়াত':['Transportation','المواصلات','交通'],'শিক্ষা':['Education','التعليم','教育'],'বাসস্থান':['Housing','المسكن','住房'],'স্বাস্থ্য':['Health','الصحة','健康'],'ঋণ ও কিস্তি':['Loans & Installments','القروض والأقساط','贷款与分期'],'ব্যবসা':['Business','الأعمال','商业'],'পরিবার ও ব্যক্তিগত':['Family & Personal','الأسرة والشخصي','家庭与个人'],'আয়':['Income','الدخل','收入'],'দান ও ধর্মীয়':['Charity & Religious','الصدقات والدين','慈善与宗教'],'সঞ্চয় ও বিনিয়োগ':['Savings & Investment','الادخار والاستثمار','储蓄与投资'],'কৃষি ও খামার':['Agriculture & Farming','الزراعة والثروة الحيوانية','农业与养殖'],'গৃহস্থালি ও পরিষ্কার':['Household & Cleaning','المنزلية والتنظيف','家居与清洁'],'মেরামত ও যন্ত্রপাতি':['Repair & Tools','الإصلاح والأدوات','维修与工具'],'অনুষ্ঠান ও উৎসব':['Events & Festivals','المناسبات والأعياد','活动与节日'],'শিশু ও মাতৃত্ব':['Children & Maternity','الأطفال والأمومة','儿童与母婴'],'পশু-পাখি ও পোষা':['Animals & Pets','الحيوانات','动物与宠物'],'দৈনন্দিন বিবিধ':['Daily Misc','متنوع يومي','日常杂项']};
const CATX={
'বিদ্যুৎ বিল':['Electricity bill','فاتورة الكهرباء','电费'],'পানির বিল':['Water bill','فاتورة المياه','水费'],'গ্যাস বিল (পাইপলাইন)':['Gas bill','فاتورة الغاز','燃气费'],'গ্যাস সিলিন্ডার':['Gas cylinder','أسطوانة غاز','煤气罐'],'ইন্টারনেট বিল':['Internet bill','فاتورة الإنترنت','网费'],'মোবাইল রিচার্জ':['Mobile recharge','شحن الهاتف','手机充值'],'ডিশ / ক্যাবল বিল':['Cable bill','فاتورة الكابل','有线电视费'],'বর্জ্য ও সার্ভিস চার্জ':['Waste & service','رسوم النظافة','垃圾服务费'],'টেলিফোন বিল':['Telephone bill','فاتورة الهاتف','电话费'],'ক্লাউড স্টোরেজ':['Cloud storage','تخزين سحابي','云存储'],'ডোমেইন / সার্ভার':['Domain/Server','دومين','域名服务器'],'জেনারেটর তেল':['Generator oil','زيت المولد','发电机油'],'মিটার ভাড়া':['Meter rent','إيجار العداد','电表租金'],'রিচার্জ বান্ডেল':['Recharge bundle','باقة شحن','充值套餐'],
'প্রতিদিনের বাজার':['Daily market','السوق اليومي','日常买菜'],'মুদি দোকান':['Grocery','بقالة','杂货店'],'চাল':['Rice','أرز','大米'],'ডাল':['Lentils','عدس','豆类'],'তেল ও ঘি':['Oil & ghee','زيت وسمن','食用油'],'মসলা':['Spices','بهارات','调料'],'সবজি':['Vegetables','خضروات','蔬菜'],'মৌসুমি ফল':['Seasonal fruits','فواكه موسمية','时令水果'],'ফলমূল':['Fruits','فواكه','水果'],'মাছ':['Fish','سمك','鱼'],'মাংস':['Meat','لحم','肉类'],'ডিম ও দুধ':['Eggs & milk','بيض وحليب','蛋奶'],'হোটেল / রেস্টুরেন্ট':['Restaurant','مطعم','餐厅'],'চা-কফি':['Tea-Coffee','شاي وقهوة','茶咖啡'],'মিষ্টান্ন':['Sweets','حلويات','甜点'],'ফাস্টফুড':['Fast food','وجبات سريعة','快餐'],'আইসক্রিম':['Ice cream','آيس كريم','冰淇淋'],'স্ন্যাকস':['Snacks','وجبات خفيفة','零食'],'শিশুর খাবার':['Baby food','طعام الأطفال','婴儿食品'],'বেকারি / রুটি':['Bakery','مخبز','面包店'],'ফলের জুস':['Fruit juice','عصير','果汁'],'হিমায়িত খাবার':['Frozen food','أطعمة مجمدة','冷冻食品'],
'লোকাল বাস':['Local bus','باس محلي','本地公交'],'মটর বাইক':['Motorcycle','دراجة نارية','摩托车'],'সিএনজি / রিকশা':['CNG/Rickshaw','توك توك','三轮车'],'ই-রিকশা':['E-rickshaw','ريكسة كهربائية','电动三轮车'],'উবার / পাঠাও':['Uber/Pathao','أوبر','网约车'],'রাইড শেয়ারিং বাইক':['Bike sharing','مشاركة الدراجات','共享摩托'],'ট্রেন ভাড়া':['Train fare','تذكرة قطار','火车票'],'লঞ্চ / স্টিমার':['Launch/Ferry','عبّارة','轮渡'],'দূরপাল্লার বাস':['Long-distance bus','باس بعيد','长途汽车'],'প্লেন টিকিট':['Plane ticket','تذكرة طيران','机票'],'পেট্রোল':['Petrol','بنزين','汽油'],'অকটেন':['Octane','أوكتان','高级汽油'],'ডিজেল':['Diesel','ديزل','柴油'],'সিএনজি গ্যাস':['CNG gas','غاز CNG','压缩天然气'],'বাইক মেরামত':['Bike repair','إصلاح دراجة','摩托维修'],'গাড়ি মেরামত':['Car repair','إصلاح سيارة','汽车维修'],'টায়ার কেনা':['Tires','إطارات','轮胎'],'ব্যাটারি':['Battery','بطارية','电池'],'পার্কিং খরচ':['Parking','وقوف السيارات','停车费'],'টোল ফি':['Toll fee','رسوم الطريق','过路费'],'লাইসেন্স / ফিটনেস':['License','رخصة','执照年检'],'বাইক ওয়াশ':['Bike wash','غسيل دراجة','洗摩托'],'গাড়ি ধোয়া':['Car wash','غسيل سيارة','洗车'],'বাইক কিস্তি':['Bike installment','قسط الدراجة','摩托分期'],
'টিউশন ফি':['Tuition fee','رسوم دراسية','学费'],'স্কুল ফি':['School fee','رسوم المدرسة','学校费用'],'কলেজ ফি':['College fee','رسوم الكلية','学院费用'],'কোচিং ফি':['Coaching fee','رسوم الدروس','补习费'],'টিউটর বেতন':['Tutor salary','راتب المعلم','家教工资'],'বই ও খাতা':['Books','كتب ودفاتر','书本笔记本'],'কলম-পেন্সিল':['Pen-pencil','أقلام','笔类'],'শিক্ষা উপকরণ':['Edu supplies','مستلزمات تعليمية','教育用品'],'ইউনিফর্ম':['Uniform','زي مدرسي','校服'],'পরীক্ষার ফি':['Exam fee','رسوم الامتحان','考试费'],'ভর্তি ফি':['Admission fee','رسوم القبول','报名费'],'লাইব্রেরি ফি':['Library fee','رسوم المكتبة','图书馆费'],'অনলাইন কোর্স':['Online course','دورة أونلاين','在线课程'],'প্রশিক্ষণ ফি':['Training fee','رسوم تدريب','培训费'],'শিক্ষা ট্যুর':['Study tour','رحلة تعليمية','游学'],'টিফিন খরচ':['Tiffin cost','مصروف الطعام','午餐费'],'হোস্টেল ফি':['Hostel fee','رسوم السكن','宿舍费'],'স্কুল ব্যাগ / বোতল':['School bag','حقيبة مدرسية','书包水壶'],
'বাসা ভাড়া':['House rent','إيجار المنزل','房租'],'বিল্ডিং সার্ভিস চার্জ':['Building charge','رسوم الخدمة','楼宇服务费'],'বাড়ি মেরামত':['House repair','إصلاح المنزل','房屋维修'],'রং-পুটি':['Paint','دهان','油漆'],'আসবাবপত্র':['Furniture','أثاث','家具'],'ইলেকট্রনিক্স':['Electronics','إلكترونيات','电子产品'],'রান্নার সরঞ্জাম':['Kitchen tools','أدوات المطبخ','厨具'],'বিছানা-বালিশ':['Bedding','مفروشات','床品'],'পর্দা-কার্পেট':['Curtain-Carpet','ستائر وسجاد','窗帘地毯'],'গৃহকর্মী বেতন':['Housemaid pay','راتب العاملة','保姆工资'],'সিকিউরিটি মানি':['Security money','مبلغ التأمين','押金'],'শিফটিং খরচ':['Shifting cost','تكاليف النقل','搬家费'],'বারান্দা গাছ / টব':['Balcony plants','نباتات','阳台植物'],'পরিষ্কার-পরিচ্ছন্ন':['Cleaning','تنظيف','清洁'],
'ডাক্তার ফি':['Doctor fee','أتعاب الطبيب','挂号费'],'ওষুধ':['Medicine','أدوية','药品'],'হাসপাতাল খরচ':['Hospital cost','المستشفى','住院费'],'টেস্ট / ডায়াগনস্টিক':['Tests','تحاليل','检查费'],'স্বাস্থ্য চেকআপ':['Checkup','فحص صحي','体检'],'দাঁতের চিকিৎসা':['Dental','الأسنان','牙科'],'চোখের চিকিৎসা':['Eye care','العيون','眼科'],'চশমা':['Glasses','نظارات','眼镜'],'স্বাস্থ্য বীমা':['Health insurance','تأمين صحي','医保'],'জিম ফি':['Gym fee','النادي','健身房'],'যোগা ক্লাস':['Yoga class','يوغا','瑜伽课'],'প্রসূতি খরচ':['Maternity cost','الولادة','产检分娩'],'টিকা':['Vaccine','تطعيم','疫苗'],'ফিজিওথেরাপি':['Physiotherapy','علاج طبيعي','理疗'],'নার্সিং খরচ':['Nursing','تمريض','护理费'],
'ঋণ নেওয়া':['Loan taken','قرض مأخوذ','借入贷款'],'ঋণ পরিশোধ':['Loan repayment','سداد القرض','还贷款'],'পাওনা':['Receivable','مديونية له','应收款'],'পাওনা আদায়':['Receivable collected','تحصيل','收回应收款'],'কিস্তি (Loan)':['Installment','قسط','分期付款'],'ক্রেডিট কার্ড বিল':['Credit card bill','فاتورة البطاقة','信用卡账单'],'ব্যাংক চার্জ':['Bank charge','رسوم بنكية','银行手续费'],'সুদ প্রদান':['Interest paid','فوائد','利息支出'],'এনজিও কিস্তি':['NGO installment','قسط منظمة','NGO分期'],'সমবায় কিস্তি':['Co-op installment','قسط تعاونية','合作社分期'],
'পণ্য ক্রয়':['Goods purchase','شراء بضائع','进货'],'কাঁচামাল':['Raw materials','مواد خام','原材料'],'কর্মচারী বেতন':['Employee salary','رواتب الموظفين','员工工资'],'দোকান ভাড়া':['Shop rent','إيجار المحل','店铺租金'],'বিজ্ঞাপন খরচ':['Advertising','إعلانات','广告费'],'প্যাকেজিং':['Packaging','تغليف','包装'],'মালামাল পরিবহন':['Goods transport','نقل البضائع','货物运输'],'গুদাম ভাড়া':['Warehouse rent','إيجار مستودع','仓库租金'],'দোকানের বিদ্যুৎ':['Shop electricity','كهرباء المحل','店铺电费'],'মেশিনারি কেনা':['Machinery','شراء آلات','机械设备'],'রক্ষণাবেক্ষণ':['Maintenance','صيانة','维护保养'],'ট্রেড লাইসেন্স':['Trade license','رخصة تجارية','营业执照'],'ট্যাক্স / ভ্যাট':['Tax/VAT','ضريبة','税费'],'কমিশন':['Commission','عمولة','佣金'],'ডেলিভারি চার্জ':['Delivery charge','رسوم توصيل','配送费'],'ওয়েবসাইট / অ্যাপ':['Website/App','موقع/تطبيق','网站应用'],'অফিস সামগ্রী':['Office supplies','مستلزمات مكتبية','办公用品'],'নমুনা পণ্য':['Samples','عينات','样品'],'ট্রেড ফেয়ার':['Trade fair','معرض تجاري','商贸展会'],'স্পিকার / সাউন্ড ভাড়া':['Speaker rent','تأجير صوتيات','音响租赁'],
'পোশাক':['Clothing','ملابس','服装'],'জুতা':['Shoes','أحذية','鞋类'],'টেইলার বিল':['Tailor bill','خياط','裁缝费'],'লন্ড্রি':['Laundry','مغسلة','洗衣'],'প্রসাধনী':['Cosmetics','مستحضرات تجميل','化妆品'],'সালুন / পার্লার':['Salon','صالون','美容美发'],'উপহার':['Gift','هدية','礼物'],'বিবাহ অনুষ্ঠান':['Wedding','حفل زفاف','婚礼'],'বিনোদন':['Entertainment','ترفيه','娱乐'],'সিনেমা':['Cinema','سينما','电影'],'কনসার্ট':['Concert','حفل موسيقي','演唱会'],'ভ্রমণ / ছুটি':['Travel/Vacation','سفر','旅行度假'],'হোটেল বিল':['Hotel bill','فاتورة فندق','酒店账单'],'খেলাধুলা':['Sports','رياضة','体育运动'],'শখ / হবি':['Hobby','هواية','兴趣爱好'],'ব্যক্তিগত বই':['Personal books','كتب شخصية','个人书籍'],'মোবাইল কেনা':['Buying mobile','شراء هاتف','购买手机'],'গ্যাজেট':['Gadget','أدوات ذكية','数码产品'],'সাবস্ক্রিপশন (OTT)':['Subscription','اشتراك','订阅服务'],'গেম / ইন-অ্যাপ':['Games','ألعاب','游戏'],'পোষা প্রাণী':['Pet','حيوان أليف','宠物'],'ব্যক্তিগত যত্ন':['Personal care','عناية شخصية','个人护理'],
'বেতন':['Salary','راتب','工资'],'ব্যবসার আয়':['Business income','دخل الأعمال','经营收入'],'বোনাস':['Bonus','مكافأة','奖金'],'ওভারটাইম':['Overtime','عمل إضافي','加班费'],'ফ্রিল্যান্সিং':['Freelancing','عمل حر','自由职业'],'ভাড়া আয়':['Rental income','دخل الإيجار','租金收入'],'লাভ / মুনাফা':['Profit','ربح','利润'],'উপহার প্রাপ্তি':['Gift received','هدية مستلمة','收到礼物'],'বৃত্তি':['Scholarship','منحة','奖学金'],'কমিশন আয়':['Commission income','دخل العمولة','佣金收入'],'বিনিয়োগ রিটার্ন':['Investment return','عائد استثمار','投资回报'],'বিবিধ আয়':['Misc income','دخل متنوع','其他收入'],
'দান-খয়রাত':['Charity','صدقة','慈善捐助'],'জাকাত':['Zakat','زكاة','天课'],'সদকা':['Sadaqah','صدقة جارية','施舍'],'ফিতরা':['Fitra','فطرة','开斋捐'],'কোরবানি':['Qurbani','أضحية','宰牲'],'মসজিদ / মন্দির চাঁদা':['Mosque/Temple','تبرعات','寺庙捐献'],'হজ / উমরাহ সঞ্চয়':['Hajj savings','توفير الحج','朝觐储蓄'],'ধর্মীয় অনুষ্ঠান':['Religious event','مناسبة دينية','宗教活动'],'অনাথালয় অনুদান':['Orphanage donation','للأيتام','孤儿院捐助'],'মিলাদ / শোক খরচ':['Milad/funeral','مناسبات','纪念活动'],
'ব্যাংক জমা':['Bank deposit','إيداع بنكي','银行存款'],'সঞ্চয়ন পত্র':['Savings certificate','شهادة ادخار','储蓄债券'],'ফিক্সড ডিপোজিট':['Fixed deposit','وديعة ثابتة','定期存款'],'ডিপিএস':['DPS','ادخار شهري','零存整取'],'মিউচুয়াল ফান্ড':['Mutual fund','صندوق مشترك','共同基金'],'শেয়ার বাজার':['Stock market','سوق الأسهم','股票市场'],'সোনা / গহনা ক্রয়':['Gold/Jewelry','شراء ذهب','购买金饰'],'জমি / প্লট কেনা':['Land purchase','شراء أرض','购买土地'],'ইমারজেন্সি ফান্ড':['Emergency fund','صندوق طوارئ','应急基金'],'পেনশন জমা':['Pension','تقاعد','养老金'],
'বীজ ও চারা':['Seeds','بذور وشتلات','种子秧苗'],'সার ও কীটনাশক':['Fertilizer','أسمدة','化肥农药'],'ট্র্যাক্টর ভাড়া':['Tractor rent','تأجير جرار','拖拉机租金'],'সেচ / পানি খরচ':['Irrigation','ري','灌溉水费'],'মুরগির খামার':['Poultry farm','مزرعة دواجن','养鸡场'],'গরু-ছাগল পালন':['Cattle rearing','تربية المواشي','牛羊养殖'],'মাছ চাষ':['Fish farming','تربية الأسماك','养鱼'],'গোখাদ্য / খড়':['Cattle feed','علف','饲料'],'ফসল কাটাই খরচ':['Harvest cost','الحصاد','收割费用'],'জমি লিজ / পাট্টা':['Land lease','إيجار أرض','租地'],'কৃষি যন্ত্রপাতি':['Agri equipment','معدات زراعية','农业机械'],'বাগান পরিচর্যা':['Garden care','العناية بالبستان','果园护理'],
'সাবান / শ্যাম্পু':['Soap/Shampoo','صابون وشامبو','香皂洗发水'],'ডিটারজেন্ট / পাউডার':['Detergent','مسحوق غسيل','洗衣粉'],'ঝাড়ু / মপ':['Broom/Mop','مكنسة','扫帚拖把'],'মশকরোধী স্প্রে / কয়েল':['Mosquito spray','مبيد بعوض','驱蚊用品'],'বালতি / গামলা':['Bucket','دلو','水桶'],'বেডশিট / কম্বল':['Bedding','ملاءات','床单毯子'],'পর্দা / মশারি':['Curtain/Net','ستائر','窗帘蚊帐'],'টুথপেস্ট / ব্রাশ':['Toothpaste','معجون أسنان','牙刷牙膏'],'টিস্যু / স্যানিটারি':['Tissue/Sanitary','مناديل','纸巾卫生用品'],'গার্বেজ ব্যাগ':['Garbage bag','أكياس قمامة','垃圾袋'],
'হাতুড়ি-পেরেক':['Hammer-nails','مطرقة','锤子钉子'],'প্লাম্বিং / পানির লাইন':['Plumbing','سباكة','水管维修'],'ইলেকট্রিশিয়ান খরচ':['Electrician','كهربائي','电工费'],'তালা / চাবি':['Lock/Key','قفل ومفتاح','锁匙'],'রং / ব্রাশ':['Paint/Brush','دهان','油漆刷子'],'স্ক্রু-ড্রিল':['Screw-Drill','براغي','螺丝电钻'],'ফার্নিচার মেরামত':['Furniture repair','إصلاح أثاث','家具维修'],'ফ্যান / পাখি মেরামত':['Fan repair','إصلاح مروحة','电扇维修'],'জেনারেটর / আইপিএস':['Generator/IPS','مولد','发电机UPS'],
'আকিকা':['Aqiqah','عقيقة','婴儿剃发礼'],'মঞ্চ / চেয়ার ভাড়া':['Stage/Chair rent','تأجير كراسي','舞台椅子租赁'],'ব্যান্ড / গায়ক':['Band/Singer','فرقة موسيقية','乐队歌手'],'ফটোগ্রাফি / ভিডিও':['Photography','تصوير','摄影摄像'],'বিয়ের কেক':['Wedding cake','كعكة الزفاف','婚礼蛋糕'],'পোশাক ভাড়া':['Dress rent','تأجير ملابس','礼服租赁'],'মেহমানদারি (অনুষ্ঠান)':['Event hospitality','ضيافة','宴请'],'জন্মদিনের পার্টি':['Birthday party','حفل عيد ميلاد','生日派对'],'উৎসব স্টল / মেলা':['Festival fair','مهرجان','节日集市'],
'ডায়াপার':['Diaper','حفاضات','纸尿裤'],'শিশুর দুধ / ফিডার':['Baby milk/Feeder','حليب أطفال','婴儿奶粉奶瓶'],'শিশুর পোশাক':['Baby clothes','ملابس أطفال','婴儿服装'],'খেলনা':['Toys','ألعاب','玩具'],'বেবি প্রাম / স্ট্রলার':['Baby stroller','عربة أطفال','婴儿车'],'মায়ের ভিটামিন':['Mother vitamins','فيتامينات الأم','母亲维生素'],'শিশু বিশেষজ্ঞ ফি':['Pediatrician','طبيب أطفال','儿科医生'],'শিশুর গোসলের সামগ্রী':['Baby bath items','مستلزمات استحمام','婴儿洗护'],
'পোষা প্রাণীর খাবার':['Pet food','طعام الحيوانات','宠物食品'],'পশু চিকিৎসক ফি':['Vet fee','طبيب بيطري','宠物医生'],'পাখির খাবার / খাঁচা':['Bird food/Cage','طعام الطيور','鸟食鸟笼'],'বিড়ালের লিটার':['Cat litter','رمل قطط','猫砂'],'পোষা সামগ্রী':['Pet supplies','مستلزمات','宠物用品'],'পশুর টিকা':['Animal vaccine','تطعيم الحيوان','宠物疫苗'],
'টিপস / বকশিশ':['Tips','بقشيش','小费'],'অগ্রিম প্রদান':['Advance payment','دفعة مقدمة','预付款'],'ফটোকপি / প্রিন্ট':['Photocopy/Print','نسخ وطباعة','复印打印'],'ডাক / কুরিয়ার':['Post/Courier','بريد','邮寄快递'],'জরিমানা / ফাইন':['Fine','غرامة','罚款'],'আইনি খরচ':['Legal cost','رسوم قانونية','法律费用'],'চাবি হারানো / লক':['Lost key/Lock','فقدان المفتاح','配钥匙'],'ক্ষতিপূরণ':['Compensation','تعويض','赔偿'],'ঘড়ি / সময় সেবা':['Clock service','ساعة','钟表服务'],'ছাতা / বৃষ্টি সামগ্রী':['Umbrella/Rain','مظلة','雨具'],'ঘড়ির ব্যাটারি':['Watch battery','بطارية الساعة','手表电池'],'সানস্ক্রিন':['Sunscreen','واقي شمس','防晒霜'],
'অন্যান্য':['Others','أخرى','其他'],'আরও':['More','المزيد','更多'],'বিশেষ':['Special','خاص','特殊']};
const LI={en:0,ar:1,zh:2};
function catL(n){if(LANG==='bn')return n;const m=CATX[n];return m?m[LI[LANG]]:n}
function gtL(n){if(LANG==='bn')return n;const m=GTX[n];return m?m[LI[LANG]]:n}
function applyLanguage(){document.documentElement.lang=LANG;document.documentElement.dir=LANG==='ar'?'rtl':'ltr';
const ls=document.getElementById('lang-select'),lt=document.getElementById('lang-top');if(ls)ls.value=LANG;if(lt)lt.value=LANG;
document.querySelectorAll('[data-i18n]').forEach(el=>{el.textContent=t(el.getAttribute('data-i18n'))});
populateCategorySelect();renderQuickCategories();renderCategoryGroups();renderTransactions();renderLoans();renderPaona();renderSummary();updateAdvisor();renderProfile();renderVisual();renderDriveUI();renderReminders();renderBudget();renderHeaderMonth();updateNowDT()}

/* ============ ক্যাটাগরি ডাটা (২৫০+) ============ */
const C=(n,i)=>({name:n,icon:i});
const CATEGORY_GROUPS=[
{title:'বিল ও ইউটিলিটি',icon:'bolt',items:[C('বিদ্যুৎ বিল','bolt'),C('পানির বিল','droplet'),C('গ্যাস বিল (পাইপলাইন)','flame'),C('গ্যাস সিলিন্ডার','flame'),C('ইন্টারনেট বিল','wifi'),C('মোবাইল রিচার্জ','phone'),C('ডিশ / ক্যাবল বিল','film'),C('বর্জ্য ও সার্ভিস চার্জ','trash'),C('টেলিফোন বিল','phone'),C('ক্লাউড স্টোরেজ','cloud'),C('ডোমেইন / সার্ভার','wifi'),C('জেনারেটর তেল','fuel'),C('মিটার ভাড়া','bolt'),C('রিচার্জ বান্ডেল','phone')]},
{title:'খাদ্য ও বাজার',icon:'basket',items:[C('প্রতিদিনের বাজার','basket'),C('মুদি দোকান','box'),C('চাল','box'),C('ডাল','box'),C('তেল ও ঘি','box'),C('মসলা','box'),C('সবজি','basket'),C('মৌসুমি ফল','basket'),C('ফলমূল','basket'),C('মাছ','fish'),C('মাংস','basket'),C('ডিম ও দুধ','milk'),C('হোটেল / রেস্টুরেন্ট','utensils'),C('চা-কফি','utensils'),C('মিষ্টান্ন','cake'),C('ফাস্টফুড','utensils'),C('আইসক্রিম','cake'),C('স্ন্যাকস','basket'),C('শিশুর খাবার','baby'),C('বেকারি / রুটি','bread'),C('ফলের জুস','droplet'),C('হিমায়িত খাবার','box')]},
{title:'যাতায়াত',icon:'car',items:[C('লোকাল বাস','car'),C('মটর বাইক','car'),C('সিএনজি / রিকশা','car'),C('ই-রিকশা','car'),C('উবার / পাঠাও','car'),C('রাইড শেয়ারিং বাইক','car'),C('ট্রেন ভাড়া','car'),C('লঞ্চ / স্টিমার','boat'),C('দূরপাল্লার বাস','truck'),C('প্লেন টিকিট','plane'),C('পেট্রোল','fuel'),C('অকটেন','fuel'),C('ডিজেল','fuel'),C('সিএনজি গ্যাস','fuel'),C('বাইক মেরামত','wrench'),C('গাড়ি মেরামত','wrench'),C('টায়ার কেনা','car'),C('ব্যাটারি','bolt'),C('পার্কিং খরচ','car'),C('টোল ফি','ticket'),C('লাইসেন্স / ফিটনেস','file-invoice'),C('বাইক ওয়াশ','droplet'),C('গাড়ি ধোয়া','droplet'),C('বাইক কিস্তি','file-invoice')]},
{title:'শিক্ষা',icon:'graduation-cap',items:[C('টিউশন ফি','graduation-cap'),C('স্কুল ফি','graduation-cap'),C('কলেজ ফি','graduation-cap'),C('কোচিং ফি','graduation-cap'),C('টিউটর বেতন','graduation-cap'),C('বই ও খাতা','book'),C('কলম-পেন্সিল','pencil'),C('শিক্ষা উপকরণ','box'),C('ইউনিফর্ম','shirt'),C('পরীক্ষার ফি','file-invoice'),C('ভর্তি ফি','file-invoice'),C('লাইব্রেরি ফি','book'),C('অনলাইন কোর্স','wifi'),C('প্রশিক্ষণ ফি','graduation-cap'),C('শিক্ষা ট্যুর','plane'),C('টিফিন খরচ','utensils'),C('হোস্টেল ফি','building'),C('স্কুল ব্যাগ / বোতল','box')]},
{title:'বাসস্থান',icon:'building',items:[C('বাসা ভাড়া','building'),C('বিল্ডিং সার্ভিস চার্জ','building'),C('বাড়ি মেরামত','wrench'),C('রং-পুটি','paint'),C('আসবাবপত্র','box'),C('ইলেকট্রনিক্স','bolt'),C('রান্নার সরঞ্জাম','utensils'),C('বিছানা-বালিশ','box'),C('পর্দা-কার্পেট','box'),C('গৃহকর্মী বেতন','briefcase'),C('সিকিউরিটি মানি','coins'),C('শিফটিং খরচ','truck'),C('বারান্দা গাছ / টব','flower'),C('পরিষ্কার-পরিচ্ছন্ন','broom')]},
{title:'স্বাস্থ্য',icon:'heart',items:[C('ডাক্তার ফি','heart'),C('ওষুধ','heart'),C('হাসপাতাল খরচ','heart'),C('টেস্ট / ডায়াগনস্টিক','heart'),C('স্বাস্থ্য চেকআপ','heart'),C('দাঁতের চিকিৎসা','heart'),C('চোখের চিকিৎসা','heart'),C('চশমা','heart'),C('স্বাস্থ্য বীমা','file-invoice'),C('জিম ফি','heart'),C('যোগা ক্লাস','heart'),C('প্রসূতি খরচ','baby'),C('টিকা','heart'),C('ফিজিওথেরাপি','heart'),C('নার্সিং খরচ','heart')]},
{title:'ঋণ ও কিস্তি',icon:'coins',items:[C('ঋণ নেওয়া','coins'),C('ঋণ পরিশোধ','coins'),C('পাওনা','hand'),C('পাওনা আদায়','hand'),C('কিস্তি (Loan)','file-invoice'),C('ক্রেডিট কার্ড বিল','file-invoice'),C('ব্যাংক চার্জ','file-invoice'),C('সুদ প্রদান','coins'),C('এনজিও কিস্তি','file-invoice'),C('সমবায় কিস্তি','file-invoice')]},
{title:'ব্যবসা',icon:'briefcase',items:[C('পণ্য ক্রয়','box'),C('কাঁচামাল','box'),C('কর্মচারী বেতন','briefcase'),C('দোকান ভাড়া','building'),C('বিজ্ঞাপন খরচ','mic'),C('প্যাকেজিং','box'),C('মালামাল পরিবহন','truck'),C('গুদাম ভাড়া','building'),C('দোকানের বিদ্যুৎ','bolt'),C('মেশিনারি কেনা','wrench'),C('রক্ষণাবেক্ষণ','wrench'),C('ট্রেড লাইসেন্স','file-invoice'),C('ট্যাক্স / ভ্যাট','file-invoice'),C('কমিশন','coins'),C('ডেলিভারি চার্জ','truck'),C('ওয়েবসাইট / অ্যাপ','wifi'),C('অফিস সামগ্রী','box'),C('নমুনা পণ্য','box'),C('ট্রেড ফেয়ার','building'),C('স্পিকার / সাউন্ড ভাড়া','speaker')]},
{title:'পরিবার ও ব্যক্তিগত',icon:'shirt',items:[C('পোশাক','shirt'),C('জুতা','shirt'),C('টেইলার বিল','shirt'),C('লন্ড্রি','soap'),C('প্রসাধনী','gift'),C('সালুন / পার্লার','gift'),C('উপহার','gift'),C('বিবাহ অনুষ্ঠান','gift'),C('বিনোদন','film'),C('সিনেমা','ticket'),C('কনসার্ট','music'),C('ভ্রমণ / ছুটি','plane'),C('হোটেল বিল','building'),C('খেলাধুলা','ball'),C('শখ / হবি','star'),C('ব্যক্তিগত বই','book'),C('মোবাইল কেনা','phone'),C('গ্যাজেট','bolt'),C('সাবস্ক্রিপশন (OTT)','film'),C('গেম / ইন-অ্যাপ','ball'),C('পোষা প্রাণী','dog'),C('ব্যক্তিগত যত্ন','soap')]},
{title:'আয়',icon:'coins',items:[C('বেতন','coins'),C('ব্যবসার আয়','briefcase'),C('বোনাস','gift'),C('ওভারটাইম','coins'),C('ফ্রিল্যান্সিং','wifi'),C('ভাড়া আয়','building'),C('লাভ / মুনাফা','coins'),C('উপহার প্রাপ্তি','gift'),C('বৃত্তি','graduation-cap'),C('কমিশন আয়','coins'),C('বিনিয়োগ রিটার্ন','coins'),C('বিবিধ আয়','coins')]},
{title:'দান ও ধর্মীয়',icon:'heart',items:[C('দান-খয়রাত','heart'),C('জাকাত','heart'),C('সদকা','heart'),C('ফিতরা','heart'),C('কোরবানি','cow'),C('মসজিদ / মন্দির চাঁদা','heart'),C('হজ / উমরাহ সঞ্চয়','plane'),C('ধর্মীয় অনুষ্ঠান','heart'),C('অনাথালয় অনুদান','heart'),C('মিলাদ / শোক খরচ','heart')]},
{title:'সঞ্চয় ও বিনিয়োগ',icon:'box',items:[C('ব্যাংক জমা','file-invoice'),C('সঞ্চয়ন পত্র','file-invoice'),C('ফিক্সড ডিপোজিট','file-invoice'),C('ডিপিএস','file-invoice'),C('মিউচুয়াল ফান্ড','coins'),C('শেয়ার বাজার','coins'),C('সোনা / গহনা ক্রয়','gift'),C('জমি / প্লট কেনা','map'),C('ইমারজেন্সি ফান্ড','box'),C('পেনশন জমা','file-invoice')]},
{title:'কৃষি ও খামার',icon:'sprout',items:[C('বীজ ও চারা','sprout'),C('সার ও কীটনাশক','sprout'),C('ট্র্যাক্টর ভাড়া','tractor'),C('সেচ / পানি খরচ','droplet'),C('মুরগির খামার','chicken'),C('গরু-ছাগল পালন','cow'),C('মাছ চাষ','fish'),C('গোখাদ্য / খড়','sprout'),C('ফসল কাটাই খরচ','leaf'),C('জমি লিজ / পাট্টা','map'),C('কৃষি যন্ত্রপাতি','tractor'),C('বাগান পরিচর্যা','flower')]},
{title:'গৃহস্থালি ও পরিষ্কার',icon:'soap',items:[C('সাবান / শ্যাম্পু','soap'),C('ডিটারজেন্ট / পাউডার','soap'),C('ঝাড়ু / মপ','broom'),C('মশকরোধী স্প্রে / কয়েল','sprout'),C('বালতি / গামলা','bucket'),C('বেডশিট / কম্বল','box'),C('পর্দা / মশারি','box'),C('টুথপেস্ট / ব্রাশ','soap'),C('টিস্যু / স্যানিটারি','box'),C('গার্বেজ ব্যাগ','trash')]},
{title:'মেরামত ও যন্ত্রপাতি',icon:'hammer',items:[C('হাতুড়ি-পেরেক','hammer'),C('প্লাম্বিং / পানির লাইন','wrench'),C('ইলেকট্রিশিয়ান খরচ','bolt'),C('তালা / চাবি','key'),C('রং / ব্রাশ','paint'),C('স্ক্রু-ড্রিল','wrench'),C('ফার্নিচার মেরামত','hammer'),C('ফ্যান / পাখি মেরামত','bolt'),C('জেনারেটর / আইপিএস','bolt')]},
{title:'অনুষ্ঠান ও উৎসব',icon:'cake',items:[C('আকিকা','cake'),C('মঞ্চ / চেয়ার ভাড়া','building'),C('ব্যান্ড / গায়ক','music'),C('ফটোগ্রাফি / ভিডিও','camera'),C('বিয়ের কেক','cake'),C('পোশাক ভাড়া','shirt'),C('মেহমানদারি (অনুষ্ঠান)','utensils'),C('জন্মদিনের পার্টি','cake'),C('উৎসব স্টল / মেলা','ticket')]},
{title:'শিশু ও মাতৃত্ব',icon:'baby',items:[C('ডায়াপার','baby'),C('শিশুর দুধ / ফিডার','milk'),C('শিশুর পোশাক','shirt'),C('খেলনা','ball'),C('বেবি প্রাম / স্ট্রলার','baby'),C('মায়ের ভিটামিন','heart'),C('শিশু বিশেষজ্ঞ ফি','heart'),C('শিশুর গোসলের সামগ্রী','soap')]},
{title:'পশু-পাখি ও পোষা',icon:'chicken',items:[C('পোষা প্রাণীর খাবার','dog'),C('পশু চিকিৎসক ফি','heart'),C('পাখির খাবার / খাঁচা','chicken'),C('বিড়ালের লিটার','bucket'),C('পোষা সামগ্রী','box'),C('পশুর টিকা','heart')]},
{title:'দৈনন্দিন বিবিধ',icon:'dots',items:[C('টিপস / বকশিশ','coins'),C('অগ্রিম প্রদান','coins'),C('ফটোকপি / প্রিন্ট','file-invoice'),C('ডাক / কুরিয়ার','box'),C('জরিমানা / ফাইন','file-invoice'),C('আইনি খরচ','file-invoice'),C('চাবি হারানো / লক','key'),C('ক্ষতিপূরণ','coins'),C('ঘড়ি / সময় সেবা','clock'),C('ছাতা / বৃষ্টি সামগ্রী','umbrella'),C('ঘড়ির ব্যাটারি','clock'),C('সানস্ক্রিন','sun')]}
];
const TOTAL_ITEMS=CATEGORY_GROUPS.reduce((a,g)=>a+g.items.length,0);
const ALL_CAT_NAMES=CATEGORY_GROUPS.flatMap(g=>g.items.map(i=>i.name));
const QUICK_CATEGORIES=[{name:'লোকাল বাস',icon:'car'},{name:'মটর বাইক',icon:'car'},{name:'প্রতিদিনের বাজার',icon:'basket'},{name:'বাসা ভাড়া',icon:'building'},{name:'বিদ্যুৎ বিল',icon:'bolt'},{name:'ঋণ নেওয়া',icon:'coins',ty:'debt'},{name:'পাওনা',icon:'hand',ty:'paona'},{name:'টিউশন ফি',icon:'graduation-cap'}];

/* ============ STATE (লগইন ছাড়া — সরাসরি ডাটা) ============ */
const DEFAULT_AVATAR='data:image/svg+xml;utf8,'+encodeURIComponent('<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><rect width="100" height="100" fill="#F5905F"/><circle cx="50" cy="40" r="18" fill="#FFF"/><path d="M20 88c0-22 15-33 30-33s30 11 30 33Z" fill="#FFF"/></svg>');
let transactions=JSON.parse(localStorage.getItem('nex_transactions_2030')||'[]');
let profile=JSON.parse(localStorage.getItem('nex_profile_2030')||'null')||{name:'রাহিম আহমেদ',phone:'',occupation:'',email:'',address:'',bio:'',photo:DEFAULT_AVATAR};
let currentVoucherBase64=null,pendingProfilePhoto=null,currentFilter='all',currentPeriod='month',targetPerson=null,editingId=null;
function safeSave(k,v){try{localStorage.setItem(k,JSON.stringify(v));return true}catch(e){alert('স্টোরেজ পূর্ণ!');return false}}
function saveTx(){safeSave('nex_transactions_2030',transactions)}
function toast(msg){const el=document.getElementById('toast');el.textContent=msg;el.classList.add('show');clearTimeout(el._t);el._t=setTimeout(()=>el.classList.remove('show'),2200)}
function playBeep(type){if(!document.getElementById('sound-toggle')||!document.getElementById('sound-toggle').checked)return;try{const ac=new (window.AudioContext||window.webkitAudioContext)();const o=ac.createOscillator(),g=ac.createGain();o.connect(g);g.connect(ac.destination);if(type==='success'){o.frequency.setValueAtTime(600,ac.currentTime);o.frequency.setValueAtTime(900,ac.currentTime+.1);g.gain.setValueAtTime(.08,ac.currentTime);g.gain.exponentialRampToValueAtTime(.001,ac.currentTime+.3)}else{o.frequency.setValueAtTime(400,ac.currentTime);g.gain.setValueAtTime(.05,ac.currentTime);g.gain.exponentialRampToValueAtTime(.001,ac.currentTime+.15)}o.start();o.stop(ac.currentTime+.3)}catch(e){}}
function compressImage(file,maxDim,q,cb){const r=new FileReader();r.onload=e=>{const img=new Image();img.onload=()=>{let{width:w,height:h}=img;if(w>h&&w>maxDim){h=Math.round(h*(maxDim/w));w=maxDim}else if(h>maxDim){w=Math.round(w*(maxDim/h));h=maxDim}const c=document.createElement('canvas');c.width=w;c.height=h;c.getContext('2d').drawImage(img,0,0,w,h);cb(c.toDataURL('image/jpeg',q))};img.onerror=()=>alert('ছবিটি পড়া যায়নি।');img.src=e.target.result};r.readAsDataURL(file)}
function resetAllData(){if(!confirm('⚠️ সব হিসাব, প্রোফাইল ও সেটিংস স্থায়ীভাবে মুছে যাবে! নিশ্চিত?'))return;
if(!confirm('শেষবার — সবকিছু মুছবেন?'))return;
['nex_transactions_2030','nex_profile_2030','hd_pin','hd_applock','hd_budget','hd_defcat','hd_defmonths','hd_remdays','hd_rem_kisti','hd_rem_paona','hd_rem_dena','hd_gt','hd_gcid','hd_last_sync'].forEach(k=>localStorage.removeItem(k));
alert('রিসেট সম্পন্ন।');location.reload()}

/* ============ PAGE SWITCH ============ */
function showPage(p){document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
const pg=document.getElementById('page-'+p);pg.classList.remove('active');void pg.offsetWidth;pg.classList.add('active');
['home','hisab','settings'].forEach(x=>{const b=document.getElementById('nv-'+x);if(b)b.classList.toggle('active',x===p)});
window.scrollTo({top:0});playBeep('click');
if(p==='home')renderVisual();if(p==='settings')renderSettings()}

/* ============ RENDERS ============ */
function renderQuickCategories(){const html=QUICK_CATEGORIES.map(c=>`<button onclick="openAddModal('${c.name}','${c.ty||''}')" class="card p-2.5 rounded-2xl flex flex-col items-center justify-center hover:-translate-y-0.5 transition-transform"><div class="w-10 h-10 rounded-xl icon-well flex items-center justify-center ${c.ty==='paona'?'text-plum':'text-clay'} mb-1.5">${iconSvg(c.icon)}</div><span class="text-[10px] font-semibold text-center leading-tight">${catL(c.name)}</span></button>`).join('')+`<button onclick="openCategoriesModal()" class="card p-2.5 rounded-2xl flex flex-col items-center justify-center"><div class="w-10 h-10 rounded-xl icon-well flex items-center justify-center text-ink mb-1.5">${iconSvg('layers')}</div><span class="text-[10px] font-semibold text-center leading-tight">${catL('আরও')} (${TOTAL_ITEMS}+)</span></button>`;
const h=document.getElementById('quick-grid-home'),a=document.getElementById('quick-grid-hisab');if(h)h.innerHTML=html;if(a)a.innerHTML=html}
function renderCategoryGroups(){const el=document.getElementById('category-groups');if(!el)return;document.getElementById('cat-count').textContent='('+TOTAL_ITEMS+')';
el.innerHTML=CATEGORY_GROUPS.map((g,gi)=>`<div class="rounded-2xl border border-black/5 overflow-hidden"><button type="button" onclick="toggleGroup(${gi})" class="w-full flex items-center gap-2.5 px-3.5 py-3 bg-cream text-left"><div class="w-8 h-8 rounded-lg icon-well flex items-center justify-center text-clay shrink-0">${iconSvg(g.icon)}</div><span class="text-xs font-bold flex-1">${gtL(g.title)}</span><span class="text-[10px] text-muted">${g.items.length}</span><span id="chev-${gi}" class="chev w-4 h-4">${iconSvg('chevron')}</span></button><div id="group-${gi}" class="accordion-body bg-white"><div class="grid grid-cols-3 gap-2 p-3">${g.items.map(it=>`<button type="button" onclick="pickCategory('${it.name.replace(/'/g,"\\'")}')" class="flex flex-col items-center justify-center p-2 rounded-xl hover:bg-cream"><div class="w-9 h-9 rounded-lg icon-well flex items-center justify-center text-clay mb-1">${iconSvg(it.icon)}</div><span class="text-[10px] font-medium text-center leading-tight">${catL(it.name)}</span></button>`).join('')}</div></div></div>`).join('')}
function toggleGroup(gi){const b=document.getElementById('group-'+gi),c=document.getElementById('chev-'+gi),o=b.classList.contains('open');document.querySelectorAll('#category-groups .accordion-body').forEach(x=>x.classList.remove('open'));document.querySelectorAll('#category-groups .chev').forEach(x=>x.classList.remove('open'));if(!o){b.classList.add('open');c.classList.add('open')}}
function openCategoriesModal(){playBeep('click');renderCategoryGroups();document.getElementById('categories-modal').classList.remove('hidden')}
function closeCategoriesModal(){document.getElementById('categories-modal').classList.add('hidden')}
function pickCategory(name){const addOpen=!document.getElementById('add-modal').classList.contains('hidden');closeCategoriesModal();
if(addOpen){document.getElementById('trans-category-select').value=name;onCatChange();toast('✓ '+catL(name))}else openAddModal(name)}

/* ============ ঋণ + পাওনা ============ */
function sumPay(x){return (x.repayments||[]).reduce((a,r)=>a+r.amount,0)}
function personGroups(type){const m={};transactions.filter(x=>x.type===type).forEach(x=>{const P=x.person||'অজানা';m[P]=m[P]||{person:P,total:0,monthly:0,paid:0,items:[]};m[P].total+=x.amount;m[P].monthly+=x.amount/(x.months||1);m[P].paid+=sumPay(x);m[P].items.push(x)});return Object.values(m)}
function renderLoans(){const gs=personGroups('debt'),el=document.getElementById('loan-list');
if(!gs.length){el.innerHTML=`<p class="text-[11px] text-muted py-3">${t('noLoan')}</p>`;return}
el.innerHTML=gs.map(g=>{const rem=g.total-g.paid;return `<button type="button" onclick="openRepay('${(g.person||'অজানা').replace(/'/g,"\\'")}')" class="w-full flex items-center justify-between bg-cream rounded-2xl p-3 text-left hover:bg-sand"><div class="flex items-center gap-2.5 min-w-0"><div class="w-9 h-9 rounded-xl bg-white flex items-center justify-center text-clay shrink-0">${iconSvg('coins')}</div><div class="min-w-0"><p class="text-xs font-bold truncate">${g.person}</p><p class="text-[10px] text-muted">${t('monthly')}: ${money(g.monthly)} • ${t('repaid')}: ${money(g.paid)}</p></div></div><div class="text-right shrink-0"><p class="text-xs font-extrabold ${rem>0?'text-berry':'text-sage'}">${money(rem)}</p><p class="text-[9px] text-muted">${rem>0?t('remaining'):''}</p></div></button>`}).join('')}
function renderPaona(){const gs=personGroups('paona'),el=document.getElementById('paona-list');
if(!gs.length){el.innerHTML=`<p class="text-[11px] text-muted py-3">${t('noPaona')}</p>`;return}
el.innerHTML=gs.map(g=>{const rem=g.total-g.paid;return `<button type="button" onclick="openCollect('${(g.person||'অজানা').replace(/'/g,"\\'")}')" class="w-full flex items-center justify-between bg-cream rounded-2xl p-3 text-left hover:bg-sand"><div class="flex items-center gap-2.5 min-w-0"><div class="w-9 h-9 rounded-xl bg-white flex items-center justify-center text-plum shrink-0">${iconSvg('hand')}</div><div class="min-w-0"><p class="text-xs font-bold truncate">${g.person}</p><p class="text-[10px] text-muted">${t('monthly')}: ${money(g.monthly)} • ${t('collected')}: ${money(g.paid)}</p></div></div><div class="text-right shrink-0"><p class="text-xs font-extrabold ${rem>0?'text-plum':'text-sage'}">${money(rem)}</p><p class="text-[9px] text-muted">${rem>0?t('remaining'):''}</p></div></button>`}).join('')}
function openRepay(person){targetPerson=person;const g=personGroups('debt').find(x=>x.person===person);if(!g)return;const rem=g.total-g.paid;
document.getElementById('repay-person').textContent='👤 '+person;
document.getElementById('repay-info').innerHTML=`<div class="flex justify-between"><span>${t('total')}</span><b>${money(g.total)}</b></div><div class="flex justify-between text-clay"><span>${t('monthly')}</span><b>${money(g.monthly)}</b></div><div class="flex justify-between text-sage"><span>${t('repaid')}</span><b>${money(g.paid)}</b></div><div class="flex justify-between text-berry border-t border-black/10 pt-1.5"><span>${t('remaining')}</span><b>${money(rem)}</b></div>`;
document.getElementById('repay-amount').value='';document.getElementById('repay-date').value=todayIso();
const hist=[];g.items.forEach(d=>(d.repayments||[]).forEach(r=>hist.push(r)));
document.getElementById('repay-history').innerHTML=hist.length?`<p class="text-[11px] font-bold text-muted mb-1.5">${t('history')}</p>`+hist.slice(-8).reverse().map(r=>`<div class="flex justify-between text-[11px] py-1 border-b border-black/5"><span class="text-muted">${fmtDate(r.date)}</span><b class="text-sage">− ${money(r.amount)}</b></div>`).join(''):'';
document.getElementById('repay-modal').classList.remove('hidden')}
function closeRepay(){document.getElementById('repay-modal').classList.add('hidden')}
function saveRepayment(){const amt=parseFloat(document.getElementById('repay-amount').value);if(!amt||amt<=0){alert('সংখ্যা লিখুন');return}
let left=amt;const items=transactions.filter(x=>x.type==='debt'&&(x.person||'অজানা')===targetPerson).sort((a,b)=>a.date<b.date?-1:1);
for(const d of items){if(left<=0)break;const r=d.amount-sumPay(d);if(r<=0)continue;const p=Math.min(r,left);d.repayments=d.repayments||[];d.repayments.push({amount:p,date:document.getElementById('repay-date').value||todayIso()});left-=p}
saveTx();playBeep('success');toast(t('saved'));closeRepay();initAll();syncToDrive(true)}
function openCollect(person){targetPerson=person;const g=personGroups('paona').find(x=>x.person===person);if(!g)return;const rem=g.total-g.paid;
document.getElementById('collect-person').textContent='👤 '+person;
document.getElementById('collect-info').innerHTML=`<div class="flex justify-between"><span>${t('given')}</span><b>${money(g.total)}</b></div><div class="flex justify-between text-plum"><span>${t('monthly')}</span><b>${money(g.monthly)}</b></div><div class="flex justify-between text-sage"><span>${t('collected')}</span><b>${money(g.paid)}</b></div><div class="flex justify-between text-plum border-t border-black/10 pt-1.5"><span>${t('remaining')}</span><b>${money(rem)}</b></div>`;
document.getElementById('collect-amount').value='';document.getElementById('collect-date').value=todayIso();
const hist=[];g.items.forEach(d=>(d.repayments||[]).forEach(r=>hist.push(r)));
document.getElementById('collect-history').innerHTML=hist.length?`<p class="text-[11px] font-bold text-muted mb-1.5">${t('history')}</p>`+hist.slice(-8).reverse().map(r=>`<div class="flex justify-between text-[11px] py-1 border-b border-black/5"><span class="text-muted">${fmtDate(r.date)}</span><b class="text-plum">+ ${money(r.amount)}</b></div>`).join(''):'';
document.getElementById('collect-modal').classList.remove('hidden')}
function closeCollect(){document.getElementById('collect-modal').classList.add('hidden')}
function saveCollection(){const amt=parseFloat(document.getElementById('collect-amount').value);if(!amt||amt<=0){alert('সংখ্যা লিখুন');return}
let left=amt;const items=transactions.filter(x=>x.type==='paona'&&(x.person||'অজানা')===targetPerson).sort((a,b)=>a.date<b.date?-1:1);
for(const d of items){if(left<=0)break;const r=d.amount-sumPay(d);if(r<=0)continue;const p=Math.min(r,left);d.repayments=d.repayments||[];d.repayments.push({amount:p,date:document.getElementById('collect-date').value||todayIso()});left-=p}
saveTx();playBeep('success');toast(t('saved'));closeCollect();initAll();syncToDrive(true)}

/* ============ Add / Edit ============ */
function populateCategorySelect(){const sel=document.getElementById('trans-category-select');if(!sel)return;
let html=`<option value="">— ${t('cat')} —</option>`;
CATEGORY_GROUPS.forEach(g=>{html+=`<optgroup label="${gtL(g.title)}">`+g.items.map(it=>`<option value="${it.name}">${catL(it.name)}</option>`).join('')+'</optgroup>'});
html+=`<optgroup label="${catL('বিশেষ')}"><option value="ঋণ নেওয়া">${catL('ঋণ নেওয়া')}</option><option value="পাওনা">${catL('পাওনা')}</option></optgroup>`;
sel.innerHTML=html;
const dc=document.getElementById('default-cat');if(dc){dc.innerHTML=`<option value="">—</option>`+ALL_CAT_NAMES.map(n=>`<option value="${n}">${catL(n)}</option>`).join('')+`<option value="ঋণ নেওয়া">${catL('ঋণ নেওয়া')}</option><option value="পাওনা">${catL('পাওনা')}</option>`;dc.value=localStorage.getItem('hd_defcat')||''}}
function onCatChange(){const v=document.getElementById('trans-category-select').value;const ty=document.getElementById('trans-type');
if(v==='ঋণ নেওয়া')ty.value='debt';else if(v==='পাওনা')ty.value='paona';updatePersonLabel()}
function onTypeChange(){const ty=document.getElementById('trans-type').value;const cs=document.getElementById('trans-category-select');
if(ty==='debt')cs.value='ঋণ নেওয়া';else if(ty==='paona')cs.value='পাওনা';updatePersonLabel()}
function updatePersonLabel(){const ty=document.getElementById('trans-type').value;document.getElementById('person-label').textContent=ty==='debt'?t('lenderDebt'):t('lenderPaona');document.getElementById('debt-fields').classList.toggle('hidden',!(ty==='debt'||ty==='paona'))}
function openAddModal(cat,ty,tx){playBeep('click');
document.getElementById('modal-title').textContent=tx?t('editTitle'):t('save');
if(tx){editingId=tx.id;document.getElementById('trans-type').value=tx.type;document.getElementById('trans-category-select').value=tx.category||'';document.getElementById('trans-desc').value=tx.desc;document.getElementById('trans-amount').value=tx.amount;document.getElementById('trans-date').value=tx.date||todayIso();document.getElementById('trans-months').value=tx.months||'';document.getElementById('trans-person').value=tx.person||'';currentVoucherBase64=tx.voucher||null;if(tx.voucher){document.getElementById('voucher-img-tag').src=tx.voucher;document.getElementById('voucher-preview-container').classList.remove('hidden')}else removeVoucher()}
else{editingId=null;document.getElementById('transaction-form').reset();document.getElementById('trans-date').value=todayIso();
if(ty)document.getElementById('trans-type').value=ty;
const dc=localStorage.getItem('hd_defcat');if(!cat&&dc)document.getElementById('trans-category-select').value=dc;if(cat)document.getElementById('trans-category-select').value=cat;
if((ty==='debt'||ty==='paona')&&!document.getElementById('trans-months').value){const dm=localStorage.getItem('hd_defmonths');if(dm)document.getElementById('trans-months').value=dm}
removeVoucher()}
updatePersonLabel();document.getElementById('add-modal').classList.remove('hidden')}
function closeAddModal(){document.getElementById('add-modal').classList.add('hidden');document.getElementById('transaction-form').reset();document.getElementById('debt-fields').classList.add('hidden');removeVoucher();editingId=null}
function previewVoucher(e){const f=e.target.files[0];if(!f)return;compressImage(f,900,.7,d=>{currentVoucherBase64=d;document.getElementById('voucher-img-tag').src=d;document.getElementById('voucher-preview-container').classList.remove('hidden')})}
function removeVoucher(){currentVoucherBase64=null;document.getElementById('voucher-file').value='';document.getElementById('voucher-preview-container').classList.add('hidden')}
function saveTransaction(e){e.preventDefault();
const type=document.getElementById('trans-type').value;
const data={category:document.getElementById('trans-category-select').value||'অন্যান্য',desc:document.getElementById('trans-desc').value.trim(),amount:parseFloat(document.getElementById('trans-amount').value),type,months:parseInt(document.getElementById('trans-months').value)||1,person:(type==='debt'||type==='paona')?(document.getElementById('trans-person').value.trim()||document.getElementById('trans-desc').value.trim()):'',date:document.getElementById('trans-date').value||todayIso()};
data.voucher=currentVoucherBase64;
if(editingId){const ix=transactions.findIndex(x=>x.id===editingId);if(ix>-1){data.id=editingId;data.repayments=transactions[ix].repayments||[];data.ts=transactions[ix].ts;transactions[ix]=data}}
else{data.id=Date.now();data.repayments=[];data.ts=Date.now();transactions.unshift(data)}
saveTx();playBeep('success');toast(t('saved'));closeAddModal();initAll();syncToDrive(true)}

/* ============ Detail ============ */
function openDetail(id){const x=transactions.find(t=>t.id===id);if(!x)return;const rem=(x.type==='debt'||x.type==='paona')?x.amount-sumPay(x):0;
const rows=[['📝 '+t('desc'),x.desc],['🏷️ '+t('cat'),catL(x.category)],['📌 '+t('typeL'),typeLabel(x.type)],['💰 '+t('amount'),money(x.amount)],['📅 '+t('date'),fmtDate(x.date)]];
if(x.person)rows.push(['👤 '+t('person'),x.person]);
if((x.type==='debt'||x.type==='paona')&&x.months>1)rows.push(['📆 '+t('monthly'),money(x.amount/x.months)+' × '+x.months]);
if(x.type==='debt'||x.type==='paona')rows.push(['📊 '+t('remaining'),money(rem)]);
const hist=(x.repayments||[]).map(r=>`<div class="flex justify-between text-[11px] py-1 border-b border-black/5"><span class="text-muted">${fmtDate(r.date)}</span><b class="${x.type==='paona'?'text-plum':'text-sage'}">${x.type==='paona'?'+':'−'} ${money(r.amount)}</b></div>`).join('');
document.getElementById('detail-body').innerHTML=`${rows.map(([k,v])=>`<div class="flex justify-between gap-3 border-b border-black/5 pb-1.5"><span class="text-muted shrink-0">${k}</span><b class="text-right">${v}</b></div>`).join('')}
 ${x.voucher?`<img src="${x.voucher}" onclick="viewVoucher(${x.id})" class="w-24 h-24 rounded-xl object-cover border-2 border-clay cursor-pointer mt-1">`:''}
 ${hist?`<p class="text-[11px] font-bold text-muted pt-1">${t('history')}</p>${hist}`:''}`;
document.getElementById('detail-edit-btn').onclick=()=>{closeDetail();openAddModal(x.category,x.type,x)};
document.getElementById('detail-del-btn').onclick=()=>{closeDetail();deleteTransaction(x.id)};
document.getElementById('detail-modal').classList.remove('hidden')}
function closeDetail(){document.getElementById('detail-modal').classList.add('hidden')}
function deleteTransaction(id){if(!confirm('মুছে ফেলতে চান?'))return;transactions=transactions.filter(x=>x.id!==id);saveTx();playBeep('click');initAll();syncToDrive(true)}
function clearAllData(){if(!confirm('সব লেনদেন মুছবেন? প্রোফাইল থাকবে।'))return;transactions=[];saveTx();initAll();syncToDrive(true)}
function setFilter(f,btn){currentFilter=f;document.querySelectorAll('#filter-tabs .filter-tab').forEach(b=>b.classList.remove('active'));btn.classList.add('active');renderTransactions()}
function viewVoucher(id){const x=transactions.find(t=>t.id===id);if(x&&x.voucher){document.getElementById('full-voucher-img').src=x.voucher;document.getElementById('view-voucher-modal').classList.remove('hidden')}}
function closeVoucherModal(){document.getElementById('view-voucher-modal').classList.add('hidden')}
function renderTransactions(){const el=document.getElementById('transaction-list');const list=currentFilter==='all'?transactions:transactions.filter(x=>x.type===currentFilter);
if(!list.length){el.innerHTML=`<div class="text-center py-8 text-muted text-xs card rounded-2xl">${t('empty')}</div>`;return}
el.innerHTML=list.map(x=>{const sign=(x.type==='income'||x.type==='debt')?'+':'−';const rem=(x.type==='debt'||x.type==='paona')?x.amount-sumPay(x):0;
return `<div onclick="openDetail(${x.id})" class="card p-3 rounded-2xl flex justify-between items-center cursor-pointer"><div class="flex items-center space-x-3 min-w-0"><div class="w-10 h-10 rounded-xl icon-well flex items-center justify-center ${typeColor(x.type)} p-2.5 shrink-0">${iconSvg(x.type==='paona'?'hand':'receipt')}</div><div class="min-w-0"><h5 class="text-xs font-bold truncate">${x.desc}</h5><p class="text-[10px] text-muted truncate">${catL(x.category)} • ${fmtDate(x.date)}${x.person?' • 👤'+x.person:''}</p>${(x.type==='debt'||x.type==='paona')?`<p class="text-[9px] ${typeColor(x.type)}">${t('monthly')}: ${money(x.amount/(x.months||1))} • ${t('remaining')}: ${money(rem)}</p>`:''}</div></div><div class="flex items-center space-x-2 shrink-0">${x.voucher?`<span class="text-clay icon-well p-1.5 rounded-lg w-7 h-7">${iconSvg('image')}</span>`:''}<span class="text-xs font-bold ${typeColor(x.type)}">${sign}${money(x.amount)}</span></div></div>`}).join('')}

/* ============ সামারি ============ */
function periodRange(k){const now=new Date();if(k==='month')return[new Date(now.getFullYear(),now.getMonth(),1),now];
let ay=now.getFullYear();if(now.getMonth()===0)ay-=1;
if(k==='h1')return[new Date(ay,1,1),new Date(ay,7,0)];
if(k==='h2')return[new Date(ay,7,1),new Date(ay+1,1,0)];
return[new Date(ay,1,1),new Date(ay+1,1,0)]}
function isoOf(d){return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0')}
function sumPeriod(k){const[s,e]=periodRange(k),sI=isoOf(s),eI=isoOf(e);let r={income:0,expense:0,debt:0,repaid:0,paona:0,collected:0};
transactions.forEach(t=>{if(!t.date||t.date<sI||t.date>eI)return;if(t.type==='income')r.income+=t.amount;else if(t.type==='expense')r.expense+=t.amount;else if(t.type==='debt'){r.debt+=t.amount;r.repaid+=sumPay(t)}else if(t.type==='paona'){r.paona+=t.amount;r.collected+=sumPay(t)}});
r.balance=r.income+r.debt+r.collected-r.expense-r.paona-r.repaid;return r}
function currentHalf(){const m=new Date().getMonth();return (m>=1&&m<=6)?'h1':'h2'}
function setPeriod(k,btn){currentPeriod=k;document.querySelectorAll('#summary-tabs button').forEach(b=>b.classList.remove('active'));btn.classList.add('active');renderSummary()}
function renderSummary(){const s=sumPeriod(currentPeriod);
document.getElementById('summary-body').innerHTML=`<p class="text-[10px] text-muted mb-1.5">${t(currentPeriod==='month'?'thisMonth':currentPeriod)}</p><div class="space-y-1.5">
<div class="flex justify-between"><span class="text-muted">${t('income')}</span><b class="text-sage">${money(s.income)}</b></div>
<div class="flex justify-between"><span class="text-muted">${t('expense')}</span><b class="text-berry">${money(s.expense)}</b></div>
<div class="flex justify-between"><span class="text-muted">${t('loanTaken')}</span><b class="text-clay">${money(s.debt)}</b></div>
<div class="flex justify-between"><span class="text-muted">${t('repaid')}</span><b class="text-sage">${money(s.repaid)}</b></div>
<div class="flex justify-between"><span class="text-muted">${t('given')}</span><b class="text-plum">${money(s.paona)}</b></div>
<div class="flex justify-between"><span class="text-muted">${t('collected')}</span><b class="text-plum">${money(s.collected)}</b></div>
<div class="flex justify-between border-t border-black/10 pt-1.5"><span class="font-semibold">${t('balanceL')}</span><b class="text-clay text-sm">${money(s.balance)}</b></div></div>`}
function calculateSummary(){let i=0,x=0,d=0,rp=0,p=0,c=0;transactions.forEach(t=>{if(t.type==='income')i+=t.amount;else if(t.type==='expense')x+=t.amount;else if(t.type==='debt'){d+=t.amount;rp+=sumPay(t)}else if(t.type==='paona'){p+=t.amount;c+=sumPay(t)}});
document.getElementById('total-balance').textContent=money(i+d+c-x-p-rp);document.getElementById('total-income').textContent=money(i);document.getElementById('total-expense').textContent=money(x)}
function updateAdvisor(){const dr=personGroups('debt').reduce((a,g)=>a+g.total-g.paid,0);const pr=personGroups('paona').reduce((a,g)=>a+g.total-g.paid,0);
const dm=personGroups('debt').reduce((a,g)=>a+g.monthly,0),pm=personGroups('paona').reduce((a,g)=>a+g.monthly,0);
let msg=[];if(dr>0)msg.push(`বাকি ঋণ ${money(dr)} (মাসিক ${money(dm)})`);if(pr>0)msg.push(`আদায় বাকি পাওনা ${money(pr)} (মাসিক ${money(pm)})`);
document.getElementById('ai-advice-text').textContent=msg.length?`আপনার ${msg.join(' এবং ')}। তালিকায় নামে ক্লিক করে পরিশোধ বা আদায় করুন।`:'আপনার কোনো ঋণ বা পাওনা নেই।'}

/* ============ বাজেট + রিমাইন্ডার ============ */
function saveBudget(){const v=parseFloat(document.getElementById('monthly-budget').value)||0;localStorage.setItem('hd_budget',v);toast(t('saved'));renderBudget()}
function renderBudget(){const box=document.getElementById('budget-box');if(!box)return;const budget=parseFloat(localStorage.getItem('hd_budget'))||0;
if(budget<=0){box.classList.add('hidden');return}
box.classList.remove('hidden');
const now=new Date(),key=now.getFullYear()+'-'+String(now.getMonth()+1).padStart(2,'0');
let spent=0;transactions.forEach(x=>{if((x.date||'').startsWith(key)&&x.type==='expense')spent+=x.amount});
const pct=Math.min(100,Math.round(spent/budget*100));
document.getElementById('budget-fill').style.width=pct+'%';
document.getElementById('budget-fill').style.background=spent>budget?'#D65B57':(pct>75?'#E8724C':'#3F9A6E');
document.getElementById('budget-pct').textContent=(LANG==='bn'?toBn(pct):pct)+'%';
document.getElementById('budget-info').textContent=`${t('expense')}: ${money(spent)} / ${money(budget)} — ${spent>budget?'⚠️ বাজেট ছাড়িয়েছে!':(t('remaining')+': '+money(Math.max(0,budget-spent)))}`}
function renderReminders(){const box=document.getElementById('reminder-box');if(!box)return;
const kisti=localStorage.getItem('hd_rem_kisti')==='1',paona=localStorage.getItem('hd_rem_paona')==='1',dena=localStorage.getItem('hd_rem_dena')==='1';
const dm=personGroups('debt').reduce((a,g)=>a+g.monthly,0),pm=personGroups('paona').reduce((a,g)=>a+g.monthly,0);
const dr=personGroups('debt').reduce((a,g)=>a+g.total-g.paid,0),pr=personGroups('paona').reduce((a,g)=>a+g.total-g.paid,0);
let msgs=[];
if(kisti&&dm>0)msgs.push(`⏰ কিস্তি: প্রতি মাসে ${money(dm)} পরিশোধ করতে হবে`);
if(paona&&pm>0)msgs.push(`🤝 পাওনা: প্রতি মাসে ${money(pm)} আদায় করার কথা`);
if(dena&&dr>0)msgs.push(`💰 মোট বাকি ঋণ ${money(dr)}`);
if(paona&&pr>0)msgs.push(`📥 আদায় বাকি পাওনা ${money(pr)}`);
if(msgs.length){box.classList.remove('hidden');document.getElementById('reminder-text').innerHTML=msgs.join('<br>')}else box.classList.add('hidden')}

/* ============ ভিজ্যুয়াল সামারি ============ */
function renderVisual(){const box=document.getElementById('donut-box');if(!box)return;
const k=currentHalf(),s=sumPeriod(k);
document.getElementById('visual-period').textContent=t(k);
const data=[{l:t('income'),v:s.income,c:'#3F9A6E'},{l:t('expense'),v:s.expense,c:'#D65B57'},{l:t('loanTaken')+' ('+t('remaining')+')',v:Math.max(0,s.debt-s.repaid),c:'#E8724C'},{l:t('given')+' ('+t('remaining')+')',v:Math.max(0,s.paona-s.collected),c:'#7C5CBF'}];
const total=data.reduce((a,d)=>a+d.v,0);
document.getElementById('visual-balance').textContent=money(s.balance);
if(total<=0){box.innerHTML=`<div class="w-32 h-32 rounded-full flex items-center justify-center" style="background:#EDE6D8"><span class="text-[10px] text-muted text-center px-2">${t('empty')}</span></div>`;document.getElementById('donut-legend').innerHTML='';}
else{
const R=40,CIRC=2*Math.PI*R;let off=0,segs='';
data.forEach(d=>{if(d.v<=0)return;const len=d.v/total*CIRC;
segs+=`<circle cx="60" cy="60" r="${R}" fill="none" stroke="${d.c}" stroke-width="15" stroke-dasharray="${len} ${CIRC-len}" stroke-dashoffset="${-off}" transform="rotate(-90 60 60)"/>`;off+=len});
box.innerHTML=`<svg viewBox="0 0 120 120" class="w-32 h-32"><circle cx="60" cy="60" r="${R}" fill="none" stroke="#EDE6D8" stroke-width="15"/>${segs}<text x="60" y="57" text-anchor="middle" font-size="10" font-weight="800" fill="#2B2620">${LANG==='bn'?toBn(Math.round(s.income-s.expense).toLocaleString('en-IN')):Math.round(s.income-s.expense).toLocaleString('en-IN')}</text><text x="60" y="70" text-anchor="middle" font-size="6.5" fill="#918A7C">৳ (${t('income')}−${t('expense')})</text></svg>`;
document.getElementById('donut-legend').innerHTML=data.map(d=>`<div class="flex items-center gap-1.5"><i class="w-2.5 h-2.5 rounded-full shrink-0" style="background:${d.c}"></i><span class="text-muted truncate flex-1">${d.l}</span><b>${money(d.v)}</b></div>`).join('')}
const now=new Date(),cols=[];
for(let i=5;i>=0;i--){const d=new Date(now.getFullYear(),now.getMonth()-i,1);const key=d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0');
let inc=0,exp=0;transactions.forEach(x=>{if((x.date||'').startsWith(key)){if(x.type==='income')inc+=x.amount;else if(x.type==='expense')exp+=x.amount}});
cols.push({key,inc,exp,label:MONTHS[LANG][d.getMonth()].slice(0,LANG==='bn'?4:3)})}
const max=Math.max(1,...cols.map(c=>Math.max(c.inc,c.exp)));
document.getElementById('bars-box').innerHTML=cols.map(c=>`<div class="bar-col"><div style="height:${Math.round(c.inc/max*66)}px;background:#3F9A6E" class="rounded-t-md min-h-[2px]"></div><div style="height:${Math.round(c.exp/max*66)}px;background:#D65B57" class="rounded-b-md min-h-[2px]"></div></div>`).join('');
document.getElementById('bars-labels').innerHTML=cols.map(c=>`<span class="flex-1 text-center text-[8.5px] text-muted">${c.label}</span>`).join('')}

/* ============ Profile ============ */
function renderProfile(){['header-avatar','summary-avatar','settings-avatar','lock-avatar','profile-avatar-preview'].forEach(id=>{const el=document.getElementById(id);if(el)el.src=profile.photo||DEFAULT_AVATAR});
document.getElementById('header-name').textContent=profile.name||'ব্যবহারকারী';document.getElementById('summary-name').textContent=profile.name||'ব্যবহারকারী';
document.getElementById('summary-bio').textContent=profile.bio||profile.occupation||'পরিচিতি যোগ করুন';
document.getElementById('summary-phone').textContent=profile.phone?'📞 '+profile.phone:'';
document.getElementById('settings-name').textContent=profile.name||'ব্যবহারকারী';document.getElementById('settings-phone').textContent=profile.phone||'';
document.getElementById('lock-name').textContent=profile.name||'ব্যবহারকারী';
document.getElementById('profile-name').value=profile.name||'';document.getElementById('profile-phone').value=profile.phone||'';document.getElementById('profile-occupation').value=profile.occupation||'';document.getElementById('profile-email').value=profile.email||'';document.getElementById('profile-address').value=profile.address||'';document.getElementById('profile-bio').value=profile.bio||''}
function toggleProfileEdit(on){['profile-name','profile-phone','profile-occupation','profile-email','profile-address','profile-bio'].forEach(id=>document.getElementById(id).disabled=!on);document.getElementById('profile-photo-input').disabled=!on;document.getElementById('photo-label').style.pointerEvents=on?'auto':'none';document.getElementById('photo-label').style.opacity=on?1:.5;document.getElementById('profile-edit-btn').classList.toggle('hidden',on);document.getElementById('profile-save-btn').classList.toggle('hidden',!on);document.getElementById('profile-cancel-btn').classList.toggle('hidden',!on)}
function openProfile(){playBeep('click');pendingProfilePhoto=null;renderProfile();toggleProfileEdit(false);document.getElementById('profile-modal').classList.remove('hidden')}
function closeProfile(){document.getElementById('profile-modal').classList.add('hidden')}
function previewProfilePhoto(e){const f=e.target.files[0];if(!f)return;compressImage(f,500,.85,d=>{pendingProfilePhoto=d;document.getElementById('profile-avatar-preview').src=d})}
function updateProfile(){profile.name=document.getElementById('profile-name').value.trim()||'ব্যবহারকারী';profile.phone=document.getElementById('profile-phone').value.trim();profile.occupation=document.getElementById('profile-occupation').value.trim();profile.email=document.getElementById('profile-email').value.trim();profile.address=document.getElementById('profile-address').value.trim();profile.bio=document.getElementById('profile-bio').value.trim();
if(pendingProfilePhoto){profile.photo=pendingProfilePhoto;pendingProfilePhoto=null}
if(safeSave('nex_profile_2030',profile)){playBeep('success');toast(t('saved'));renderProfile();toggleProfileEdit(false);closeProfile();syncToDrive(true)}}

/* ============ সেটিংস ============ */
function accToggle(bodyId,wrapId){document.getElementById(bodyId).classList.toggle('open');document.getElementById(wrapId).classList.toggle('open')}
function setTheme(th){localStorage.setItem('hd_theme',th);applyTheme();renderThemeBtns();toast(t('saved'))}
function applyTheme(){const th=localStorage.getItem('hd_theme')||'system';
const dark=th==='dark'||(th==='system'&&window.matchMedia('(prefers-color-scheme: dark)').matches);
document.body.classList.toggle('dark',dark)}
function renderThemeBtns(){const th=localStorage.getItem('hd_theme')||'system';['light','dark','system'].forEach(x=>{const b=document.getElementById('th-'+x);if(b)b.classList.toggle('active',x===th)})}
function changePin(){const cur=localStorage.getItem('hd_pin');
if(cur){const p=prompt('বর্তমান PIN:');if(p===null)return;if(p!==cur){alert('❌ ভুল PIN!');return}}
const np=prompt('নতুন ৪ ডিজিটের PIN:');if(np===null)return;
if(!/^\d{4}$/.test(np)){alert('PIN অবশ্যই ৪ ডিজিটের');return}
localStorage.setItem('hd_pin',np);toast('✅ PIN সেট')}
function showLock(){const L=document.getElementById('lock-screen');L.classList.remove('hidden');L.classList.add('flex');renderProfile()}
function tryUnlock(){const pin=localStorage.getItem('hd_pin');
if(pin){if(document.getElementById('lock-pin').value===pin)hideLock();else{toast('❌ ভুল PIN!');document.getElementById('lock-pin').value=''}}
else hideLock()}
function hideLock(){const L=document.getElementById('lock-screen');L.classList.add('hidden');L.classList.remove('flex')}
function renderSettings(){document.getElementById('tg-kisti').checked=localStorage.getItem('hd_rem_kisti')==='1';
document.getElementById('tg-paona').checked=localStorage.getItem('hd_rem_paona')==='1';
document.getElementById('tg-dena').checked=localStorage.getItem('hd_rem_dena')==='1';
document.getElementById('tg-finger').checked=localStorage.getItem('hd_finger')==='1';
document.getElementById('tg-applock').checked=localStorage.getItem('hd_applock')==='1';
document.getElementById('monthly-budget').value=localStorage.getItem('hd_budget')||'';
document.getElementById('default-months').value=localStorage.getItem('hd_defmonths')||'';
document.getElementById('reminder-days').value=localStorage.getItem('hd_remdays')||'';
renderThemeBtns();updateNowDT()}
function updateNowDT(){const el=document.getElementById('now-dt');if(!el)return;const loc={bn:'bn-BD',en:'en-GB',ar:'ar-EG',zh:'zh-CN'}[LANG]||'bn-BD';
try{el.textContent=new Date().toLocaleString(loc,{dateStyle:'medium',timeStyle:'short'})}catch(e){el.textContent=new Date().toLocaleString()}}

/* ============ Files / Report / Drive ============ */
function openSaveFiles(){playBeep('click');document.getElementById('gcid').value=localStorage.getItem('hd_gcid')||'';renderDriveUI();document.getElementById('savefiles-modal').classList.remove('hidden')}
function closeSaveFiles(){document.getElementById('savefiles-modal').classList.add('hidden')}
function saveAsPdf(){closeSaveFiles();openReport();setTimeout(()=>window.print(),400)}
function openReport(){playBeep('click');buildReport();document.getElementById('report-modal').classList.remove('hidden')}
function closeReport(){document.getElementById('report-modal').classList.add('hidden')}
function buildTextReport(){const L=[];const P=[['month',t('thisMonth')],[currentHalf(),t(currentHalf())],['year',t('year')]];
L.push('========== হিসাব রিপোর্ট ==========');L.push('নাম: '+(profile.name||'')+'  |  তৈরি: '+new Date().toLocaleString('bn-BD'));L.push('');
P.forEach(([k,l])=>{const s=sumPeriod(k);L.push('--- '+l+' ---');L.push(`আয়: ${s.income} | ব্যয়: ${s.expense} | ঋণ: ${s.debt} | পরিশোধ: ${s.repaid} | পাওনা: ${s.paona} | আদায়: ${s.collected} | ব্যালেন্স: ${s.balance}`)});
L.push('');L.push('--- ঋণ ---');personGroups('debt').forEach(g=>L.push(`${g.person}: মোট ${g.total} | মাসিক ${g.monthly.toFixed(0)} | পরিশোধিত ${g.paid} | বাকি ${g.total-g.paid}`));
L.push('');L.push('--- পাওনা ---');personGroups('paona').forEach(g=>L.push(`${g.person}: পাওনা ${g.total} | মাসিক ${g.monthly.toFixed(0)} | আদায় ${g.paid} | বাকি ${g.total-g.paid}`));
L.push('');L.push('--- সব লেনদেন ---');
transactions.slice().sort((a,b)=>a.date<b.date?-1:1).forEach(x=>L.push(`${x.date} | ${typeLabel(x.type)} | ${x.desc} | ${catL(x.category)}${x.person?' | '+x.person:''} | ${x.amount}`));
return L.join('\n')}
function downloadTxt(){const b=new Blob([buildTextReport()],{type:'text/plain;charset=utf-8'});const a=document.createElement('a');a.href=URL.createObjectURL(b);a.download='হিসাব-'+todayIso()+'.txt';a.click();toast(t('saved'))}
function exportData(){const b=new Blob([JSON.stringify({profile,transactions},null,1)],{type:'application/json'});const a=document.createElement('a');a.href=URL.createObjectURL(b);a.download='hisab-backup-'+todayIso()+'.json';a.click();toast(t('saved'))}
function importData(e){const f=e.target.files[0];if(!f)return;const r=new FileReader();r.onload=ev=>{try{const d=JSON.parse(ev.target.result);if(d.transactions)transactions=d.transactions;if(d.profile)profile=Object.assign(profile,d.profile);saveTx();safeSave('nex_profile_2030',profile);toast(t('saved'));initAll();renderProfile();syncToDrive(true)}catch(x){alert('ফাইলটি পড়া যায়নি')}};r.readAsText(f)}
function buildReport(){const P=[['month','এই মাস'],['h1','ফেব্রুয়ারি–জুলাই (৬ মাস)'],['h2','জুলাই–ফেব্রুয়ারি (৬ মাস)'],['year','১ বছর']];
const rows=P.map(([k,l])=>{const s=sumPeriod(k);return `<tr><td>${l}</td><td>${s.income.toLocaleString('en-IN')}</td><td>${s.expense.toLocaleString('en-IN')}</td><td>${s.debt.toLocaleString('en-IN')}</td><td>${s.repaid.toLocaleString('en-IN')}</td><td>${s.paona.toLocaleString('en-IN')}</td><td>${s.collected.toLocaleString('en-IN')}</td><td><b>${s.balance.toLocaleString('en-IN')}</b></td></tr>`}).join('');
const lg=personGroups('debt').map(g=>`<tr><td>${g.person}</td><td>${g.total.toLocaleString('en-IN')}</td><td>${g.monthly.toFixed(0)}</td><td>${g.paid.toLocaleString('en-IN')}</td><td><b>${(g.total-g.paid).toLocaleString('en-IN')}</b></td></tr>`).join('');
const pg=personGroups('paona').map(g=>`<tr><td>${g.person}</td><td>${g.total.toLocaleString('en-IN')}</td><td>${g.monthly.toFixed(0)}</td><td>${g.paid.toLocaleString('en-IN')}</td><td><b>${(g.total-g.paid).toLocaleString('en-IN')}</b></td></tr>`).join('');
const byM={};transactions.forEach(t=>{const k=(t.date||'').slice(0,7);(byM[k]=byM[k]||[]).push(t)});
const detail=Object.keys(byM).sort().reverse().map(k=>`<h4 style="margin:14px 0 6px">${MONTHS.bn[+k.slice(5,7)-1]} ${k.slice(0,4)}</h4><table style="width:100%;border-collapse:collapse;font-size:11px"><tr style="background:#EDE6D8"><th style="padding:4px">তারিখ</th><th>বিবরণ</th><th>খাত</th><th>ধরণ</th><th>৳</th></tr>${byM[k].map(x=>`<tr><td style="padding:3px;text-align:center">${x.date}</td><td>${x.desc}${x.person?' ('+x.person+')':''}</td><td>${catL(x.category)}</td><td>${typeLabel(x.type)}</td><td style="text-align:right">${x.amount.toLocaleString('en-IN')}</td></tr>`).join('')}</table>`).join('');
document.getElementById('report-print-area').innerHTML=`
<div style="text-align:center"><h2 style="margin:0">হিসাব — সম্পূর্ণ রিপোর্ট</h2><p style="color:#918A7C;font-size:11px">${profile.name||''} • তৈরি: ${new Date().toLocaleString('bn-BD')}</p></div>
<h3 style="font-size:13px;border-bottom:2px solid #E8724C;padding-bottom:4px">সামারি</h3>
<table style="width:100%;border-collapse:collapse;font-size:11px"><tr style="background:#EDE6D8"><th style="padding:4px">সময়কাল</th><th>আয়</th><th>ব্যয়</th><th>ঋণ</th><th>পরিশোধ</th><th>পাওনা</th><th>আদায়</th><th>ব্যালেন্স</th></tr>${rows}</table>
<h3 style="font-size:13px;border-bottom:2px solid #E8724C;padding-bottom:4px;margin-top:16px">ঋণ</h3>
<table style="width:100%;border-collapse:collapse;font-size:11px"><tr style="background:#EDE6D8"><th style="padding:4px">ঋণদাতা</th><th>মোট</th><th>মাসিক</th><th>পরিশোধিত</th><th>বাকি</th></tr>${lg||'<tr><td colspan="5" style="text-align:center;padding:6px">—</td></tr>'}</table>
<h3 style="font-size:13px;border-bottom:2px solid #7C5CBF;padding-bottom:4px;margin-top:16px">পাওনা</h3>
<table style="width:100%;border-collapse:collapse;font-size:11px"><tr style="background:#EDE6D8"><th style="padding:4px">ব্যক্তি</th><th>পাওনা</th><th>মাসিক</th><th>আদায়</th><th>বাকি</th></tr>${pg||'<tr><td colspan="5" style="text-align:center;padding:6px">—</td></tr>'}</table>
<h3 style="font-size:13px;border-bottom:2px solid #E8724C;padding-bottom:4px;margin-top:16px">বিস্তারিত</h3>${detail||'<p style="font-size:11px">কোনো তথ্য নেই</p>'}`}
let driveToken=localStorage.getItem('hd_gt')||null;
function renderDriveUI(){const txt=driveToken?`✅ সংযুক্ত — সর্বশেষ সেভ: ${localStorage.getItem('hd_last_sync')||'—'}`:'⛔ সংযোগ হয়নি';
['drive-status','drive-status2'].forEach(id=>{const el=document.getElementById(id);if(el)el.textContent=txt})}
function driveConnectAndSave(){const cid=(document.getElementById('gcid').value||localStorage.getItem('hd_gcid')||'').trim();if(!cid){alert('Save Files মোডালে Client ID বসান।');return}if(!window.google||!google.accounts){alert('Google লাইব্রেরি লোড হয়নি।');return}
localStorage.setItem('hd_gcid',cid);
google.accounts.oauth2.initTokenClient({client_id:cid,scope:'https://www.googleapis.com/auth/drive.file',callback:r=>{if(r.access_token){driveToken=r.access_token;localStorage.setItem('hd_gt',driveToken);renderDriveUI();toast('সংযুক্ত ✓');syncToDrive(true)}}}).requestAccessToken()}
async function dApi(url,opt){const res=await fetch(url,{...opt,headers:{Authorization:'Bearer '+driveToken,...(opt&&opt.headers||{})}});if(res.status===401){driveToken=null;localStorage.removeItem('hd_gt');renderDriveUI();throw new Error('token')}return res}
async function driveFindFolder(name,parent){let q=`name='${name}' and mimeType='application/vnd.google-apps.folder' and trashed=false`;if(parent)q+=` and '${parent}' in parents`;const j=await(await dApi('https://www.googleapis.com/drive/v3/files?q='+encodeURIComponent(q)+'&fields=files(id)')).json();return j.files&&j.files[0]?j.files[0].id:null}
async function driveCreate(name,parent){const meta={name,mimeType:'application/vnd.google-apps.folder'};if(parent)meta.parents=[parent];const j=await(await dApi('https://www.googleapis.com/drive/v3/files',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify(meta)})).json();return j.id}
async function driveUploadFile(name,parent,content,mime){const q=`name='${name}' and '${parent}' in parents and trashed=false`;const fj=await(await dApi('https://www.googleapis.com/drive/v3/files?q='+encodeURIComponent(q)+'&fields=files(id)')).json();const exist=fj.files&&fj.files[0];
const b='hb'+Date.now();const body=`--${b}\r\nContent-Type: application/json; charset=UTF-8\r\n\r\n${JSON.stringify({name,parents:[parent]})}\r\n--${b}\r\nContent-Type: ${mime}\r\n\r\n${content}\r\n--${b}--`;
await dApi(exist?`https://www.googleapis.com/upload/drive/v3/files/${exist.id}?uploadType=multipart`:'https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart',{method:exist?'PATCH':'POST',headers:{'Content-Type':'multipart/related; boundary='+b},body})}
async function syncToDrive(manual){if(!driveToken){if(manual)driveConnectAndSave();return}
try{const day=todayIso();let root=await driveFindFolder('হিসাব_ব্যাকআপ');if(!root)root=await driveCreate('হিসাব_ব্যাকআপ');
let dayF=await driveFindFolder(day,root);if(!dayF)dayF=await driveCreate(day,root);
await driveUploadFile('hisab-report.txt',dayF,buildTextReport(),'text/plain; charset=UTF-8');
await driveUploadFile('hisab-data.json',dayF,JSON.stringify({profile,transactions,savedAt:new Date().toISOString()}),'application/json');
localStorage.setItem('hd_last_sync',new Date().toLocaleString('bn-BD'));renderDriveUI();if(manual)toast('Drive-এ সেভ ✓')}catch(e){if(manual)toast('Drive সেভ ব্যর্থ')}}

/* ============ INIT ============ */
function renderHeaderMonth(){const d=new Date();const el=document.getElementById('header-month');if(el)el.textContent='📅 '+(LANG==='bn'?toBn(String(d.getDate())):d.getDate())+' '+MONTHS[LANG][d.getMonth()]+' '+(LANG==='bn'?toBn(String(d.getFullYear())):d.getFullYear())}
function initAll(){calculateSummary();renderTransactions();renderLoans();renderPaona();renderSummary();updateAdvisor();renderHeaderMonth();renderVisual();renderBudget();renderReminders()}
function bindToggle(id,key,extra){const el=document.getElementById(id);if(!el)return;el.addEventListener('change',()=>{localStorage.setItem(key,el.checked?'1':'0');toast(t('saved'));playBeep('click');if(extra)extra(el.checked)})}
function initApp(){
mountIcons();populateCategorySelect();renderQuickCategories();renderCategoryGroups();applyTheme();applyLanguage();renderThemeBtns();
document.getElementById('trans-type').addEventListener('change',onTypeChange);
document.getElementById('trans-category-select').addEventListener('change',onCatChange);
bindToggle('sound-toggle','hd_sound');
bindToggle('tg-kisti','hd_rem_kisti',()=>renderReminders());
bindToggle('tg-paona','hd_rem_paona',()=>renderReminders());
bindToggle('tg-dena','hd_rem_dena',()=>renderReminders());
bindToggle('tg-finger','hd_finger',on=>{if(on)toast('🖐️ ডিভাইস সাপোর্ট নির্ভর')});
const al=document.getElementById('tg-applock');
al.addEventListener('change',()=>{if(al.checked){let pin=localStorage.getItem('hd_pin');
if(!pin){const np=prompt('App Lock চালু করতে ৪ ডিজিটের PIN দিন:');if(!np||!/^\d{4}$/.test(np)){al.checked=false;return}localStorage.setItem('hd_pin',np)}
localStorage.setItem('hd_applock','1');toast('🔒 App Lock চালু')}
else{localStorage.setItem('hd_applock','0');toast('App Lock বন্ধ')}});
setInterval(updateNowDT,30000);
renderProfile();
/* ★ App Lock চালু থাকলে লক-স্ক্রিন */
if(localStorage.getItem('hd_applock')==='1')showLock();
}
initApp();
</script>
</body>
</html>
