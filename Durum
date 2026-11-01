<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Profesyonel Site Yönetim Paneli</title>
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
<!-- jsPDF, AutoTable ve Chart.js Kütüphaneleri -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.28/jspdf.plugin.autotable.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
body {
  background: linear-gradient(135deg, #0f172a 0%, #1e3a8a 35%, #3b82f6 70%, #60a5fa 100%);
  background-attachment: fixed;
  min-height: 100vh;
}
.card-3d {
  background: linear-gradient(145deg, #ffffff 0%, #f8fafc 100%);
  border: 1px solid rgba(226, 232, 240, 0.9);
  box-shadow: 0 12px 30px -10px rgba(0, 0, 0, 0.12), 0 8px 15px -6px rgba(30, 58, 138, 0.08), inset 0 1px 0 rgba(255, 255, 255, 0.9);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.card-3d:hover {
  transform: translateY(-4px);
  box-shadow: 0 22px 40px -12px rgba(30, 58, 138, 0.22), 0 12px 20px -8px rgba(0, 0, 0, 0.1);
}
.panel-3d-animasyon {
  transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.4s ease;
  transform-style: preserve-3d;
}
.icon-3d {
  box-shadow: 0 8px 20px -4px rgba(37, 99, 235, 0.4), inset 0 2px 4px rgba(255, 255, 255, 0.5), inset 0 -2px 4px rgba(0, 0, 0, 0.2);
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
.icon-3d-red {
  box-shadow: 0 8px 20px -4px rgba(220, 38, 38, 0.4), inset 0 2px 4px rgba(255, 255, 255, 0.5), inset 0 -2px 4px rgba(0, 0, 0, 0.2);
}
.icon-3d-emerald {
  box-shadow: 0 8px 20px -4px rgba(5, 150, 105, 0.4), inset 0 2px 4px rgba(255, 255, 255, 0.5), inset 0 -2px 4px rgba(0, 0, 0, 0.2);
}
.icon-3d-amber {
  box-shadow: 0 8px 20px -4px rgba(217, 119, 6, 0.4), inset 0 2px 4px rgba(255, 255, 255, 0.5), inset 0 -2px 4px rgba(0, 0, 0, 0.2);
}
.btn-3d {
  box-shadow: 0 6px 15px -3px rgba(0, 0, 0, 0.15), inset 0 2px 3px rgba(255, 255, 255, 0.4), inset 0 -2px 3px rgba(0, 0, 0, 0.2);
  transition: all 0.2s ease;
}
.btn-3d:active {
  transform: translateY(2px);
  box-shadow: 0 2px 5px -1px rgba(0, 0, 0, 0.2), inset 0 1px 2px rgba(0, 0, 0, 0.3);
}
.trash-btn-3d {
  box-shadow: 0 4px 10px -2px rgba(220, 38, 38, 0.3), inset 0 1px 2px rgba(255, 255, 255, 0.6);
  transition: all 0.2s ease;
}
.trash-btn-3d:hover {
  transform: scale(1.08);
  box-shadow: 0 6px 14px -2px rgba(220, 38, 38, 0.5);
}
.nowrap-date { white-space: nowrap !important; }
</style>
</head>
<body class="font-sans text-slate-800 antialiased selection:bg-blue-600 selection:text-white">

<!-- UYGULAMA GİRİŞ ŞİFRE MODALI (SABİT PANEL) -->
<div id="sifreModal" style="position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; z-index: 99999;" class="bg-slate-950/85 backdrop-blur-xl flex items-center justify-center p-4">
  <div class="bg-white rounded-3xl p-8 w-full max-w-md shadow-2xl border border-white/20 card-3d text-center">
    <div class="w-16 h-16 bg-gradient-to-br from-blue-600 to-indigo-900 text-white rounded-2xl mx-auto flex items-center justify-center text-2xl icon-3d mb-4">
      <i class="fa-solid fa-shield-halved"></i>
    </div>
    <h2 class="text-xl font-black text-slate-900 mb-1">Site Yönetimi Giriş</h2>
    <p class="text-xs text-slate-500 font-medium mb-6">Devam etmek için lütfen yönetim şifresini girin veya daire şifrenizi kullanın.</p>

    <div id="girisFormBolumu" class="space-y-4">
      <input type="text" id="girisKullaniciInput" placeholder="Kullanıcı adı (yönetici veya daire no)" autocomplete="username"
        class="w-full border border-slate-300 rounded-2xl p-4 text-center font-bold text-lg focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm"
        onkeydown="if(event.key === 'Enter') sifreKontrolEt()">
      <input type="password" id="girisSifreInput" placeholder="Şifre" autocomplete="current-password"
        class="w-full border border-slate-300 rounded-2xl p-4 text-center font-bold tracking-widest text-lg focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm"
        onkeydown="if(event.key === 'Enter') sifreKontrolEt()">
      
      <!-- Beni Hatırla Seçeneği -->
      <div class="flex items-center gap-2 text-xs font-bold text-slate-600 text-left px-1">
        <input type="checkbox" id="beniHatirlaCheckbox" class="w-4 h-4 text-blue-900 rounded focus:ring-blue-600 border-slate-300 cursor-pointer">
        <label for="beniHatirlaCheckbox" class="cursor-pointer select-none">Beni Hatırla</label>
      </div>

      <p id="girisHataMesaji" class="hidden text-xs font-bold text-rose-600 bg-rose-50 border border-rose-200 rounded-xl px-3 py-2"></p>
      <button onclick="sifreKontrolEt()" class="w-full bg-gradient-to-r from-blue-900 to-indigo-900 hover:from-blue-800 hover:to-indigo-800 text-white rounded-2xl py-4 font-black btn-3d active:scale-95 transition-all text-sm shadow-lg flex items-center justify-center gap-2">
        <i class="fa-solid fa-lock-open"></i> Giriş Yap
      </button>
      <div class="text-center text-xs text-slate-500 pt-2">
        Kullanıcı adı: <b>yönetici</b> veya <b>1–20</b> &nbsp;|&nbsp; Varsayılan daire şifresi: <b>12345</b>
      </div>
    </div>

    <p class="text-[10px] text-slate-400 mt-6">Yetkili: Kasım Taha Yamak</p>
  </div>
</div>

<!-- ÜST KİMLİK VE KONTROL ALANI -->
<header class="bg-gradient-to-r from-blue-950 via-blue-900 to-indigo-950 text-white shadow-2xl p-5 sticky top-0 z-50 border-b border-blue-700/50 backdrop-blur-md">
  <div class="container mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
    <div class="flex items-center gap-3.5">
      <div class="bg-gradient-to-br from-blue-500 to-indigo-700 p-3.5 rounded-2xl border border-white/25 shadow-xl icon-3d text-white">
        <i class="fa-solid fa-building-shield text-xl"></i>
      </div>
      <div>
        <h1 class="text-lg font-extrabold tracking-tight flex items-center gap-2 bg-gradient-to-r from-white via-blue-100 to-indigo-200 bg-clip-text text-transparent">
          Profesyonel Site Yönetimi
        </h1>
        <p id="rolGostergeMetin" class="text-[11px] text-blue-300 font-medium tracking-wide">Holding Seviyesi Kurumsal Finans ve Varlık Altyapısı</p>
      </div>
    </div>
    <div class="flex items-center gap-4 flex-wrap justify-end">
      <div class="text-right hidden sm:block border-r border-blue-700/80 pr-4">
        <p class="text-[10px] uppercase font-bold text-blue-300 tracking-wider">Aktif Oturum / Yetkili</p>
        <p id="aktifKullaniciAd" class="text-sm font-extrabold text-amber-300">Kasım Taha Yamak (Yönetici)</p>
      </div>
      <div id="yoneticiAyarlariButonAlani" class="flex items-center gap-2">
        <button onclick="yoneticiAyarlariModalAc()" title="Yönetici Ayarları ve Yetki Konfigürasyonu" class="bg-gradient-to-r from-indigo-700 to-purple-800 hover:from-indigo-800 hover:to-purple-900 text-white text-xs px-4 py-2.5 rounded-xl transition btn-3d flex items-center gap-1.5 font-bold active:scale-95 border border-purple-500/30">
          <i class="fa-solid fa-gears"></i> Yönetici Ayarları
        </button>
        <button id="btnPdfRapor" onclick="pdfRaporuOlustur()" title="Mali Rapor PDF İndir" class="bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-700 hover:to-teal-700 text-white text-xs px-4 py-2.5 rounded-xl transition btn-3d flex items-center gap-1.5 font-bold active:scale-95 border border-emerald-500/30">
          <i class="fa-solid fa-file-pdf"></i> PDF Rapor
        </button>
        <button id="btnYedekAl" onclick="verileriDisariAktar()" title="Verileri Yedekle" class="bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-700 hover:to-indigo-700 text-white text-xs px-4 py-2.5 rounded-xl transition btn-3d flex items-center gap-1.5 font-bold active:scale-95 border border-blue-500/30">
          <i class="fa-solid fa-cloud-arrow-down"></i> Yedek Al
        </button>
        <label id="lblYedekYukle" title="Yedek Dosyasını Yükle" class="bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-700 hover:to-indigo-700 text-white text-xs px-4 py-2.5 rounded-xl transition btn-3d flex items-center gap-1.5 font-bold cursor-pointer active:scale-95 border border-blue-500/30">
          <i class="fa-solid fa-cloud-arrow-up"></i> Yükle
          <input type="file" id="yedekDosyaInput" onchange="verileriIceAktar(event)" class="hidden" accept=".json">
        </label>
        <button onclick="oturumuKapat()" title="Oturumu Kapat" class="bg-rose-700 hover:bg-rose-800 text-white text-xs px-3 py-2.5 rounded-xl transition font-bold"><i class="fa-solid fa-right-from-bracket"></i></button>
      </div>
    </div>
  </div>
</header>

<main class="container mx-auto p-4 md:p-6 max-w-7xl pb-24">

<!-- ANA ÖZET KARTLARI -->
<div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-8">
  <div id="kartVarlik" onclick="detayModalAc('varlik')" class="bg-white p-5 rounded-3xl card-3d group cursor-pointer hover:ring-2 hover:ring-blue-500/50 transition">
    <div class="flex items-center justify-between">
      <p class="text-[11px] text-slate-500 font-bold tracking-wider uppercase flex items-center gap-1">Toplam Varlık <i class="fa-solid fa-arrow-up-right-from-square text-[9px]"></i></p>
      <div class="w-11 h-11 rounded-2xl bg-gradient-to-br from-blue-500 to-indigo-600 text-white flex items-center justify-center font-bold text-sm icon-3d group-hover:scale-110 transition"><i class="fa-solid fa-wallet"></i></div>
    </div>
    <p id="lblKasa" class="text-2xl font-black text-blue-900 mt-3 tracking-tight">0,00 TL</p>
    <p class="text-[10px] text-blue-600/80 mt-1 font-semibold">Kasa + Banka Net Bakiye (Detay için tıkla)</p>
  </div>

  <div id="kartGelir" onclick="detayModalAc('gelir')" class="bg-white p-5 rounded-3xl card-3d group cursor-pointer hover:ring-2 hover:ring-emerald-500/50 transition">
    <div class="flex items-center justify-between">
      <p class="text-[11px] text-emerald-700 font-bold tracking-wider uppercase flex items-center gap-1">Toplam Gelir <i class="fa-solid fa-arrow-up-right-from-square text-[9px]"></i></p>
      <div class="w-11 h-11 rounded-2xl bg-gradient-to-br from-emerald-500 to-teal-600 text-white flex items-center justify-center font-bold text-sm icon-3d icon-3d-emerald group-hover:scale-110 transition"><i class="fa-solid fa-arrow-trend-up"></i></div>
    </div>
    <p id="lblGelir" class="text-2xl font-black text-emerald-600 mt-3 tracking-tight">0,00 TL</p>
    <p class="text-[10px] text-emerald-600/80 mt-1 font-semibold">Tüm Zamanların Girişleri (Detay için tıkla)</p>
  </div>

  <div id="kartGider" onclick="detayModalAc('gider')" class="bg-white p-5 rounded-3xl card-3d group cursor-pointer hover:ring-2 hover:ring-rose-500/50 transition">
    <div class="flex items-center justify-between">
      <p class="text-[11px] text-rose-700 font-bold tracking-wider uppercase flex items-center gap-1">Toplam Gider <i class="fa-solid fa-arrow-up-right-from-square text-[9px]"></i></p>
      <div class="w-11 h-11 rounded-2xl bg-gradient-to-br from-rose-500 to-pink-600 text-white flex items-center justify-center font-bold text-sm icon-3d icon-3d-red group-hover:scale-110 transition"><i class="fa-solid fa-arrow-trend-down"></i></div>
    </div>
    <p id="lblGider" class="text-2xl font-black text-rose-600 mt-3 tracking-tight">0,00 TL</p>
    <p class="text-[10px] text-rose-600/80 mt-1 font-semibold">Tüm Zamanların Çıkışları (Detay için tıkla)</p>
  </div>

  <div id="kartBorc" onclick="detayModalAc('borc')" class="bg-white p-5 rounded-3xl card-3d group cursor-pointer hover:ring-2 hover:ring-amber-500/50 transition">
    <div class="flex items-center justify-between">
      <p class="text-[11px] text-amber-700 font-bold tracking-wider uppercase flex items-center gap-1">Ödenmeyen Aidat <i class="fa-solid fa-arrow-up-right-from-square text-[9px]"></i></p>
      <div class="w-11 h-11 rounded-2xl bg-gradient-to-br from-amber-500 to-orange-600 text-white flex items-center justify-center font-bold text-sm icon-3d icon-3d-amber group-hover:scale-110 transition"><i class="fa-solid fa-triangle-exclamation"></i></div>
    </div>
    <p id="lblBorc" class="text-2xl font-black text-amber-600 mt-3 tracking-tight">0,00 TL</p>
    <p class="text-[10px] text-amber-600/80 mt-1 font-semibold">Seçili Dönem Alacakları (Detay için tıkla)</p>
  </div>
</div>

<!-- SEKME SIRALAMASI -->
<div id="navigasyonSekmeKapsayici" class="flex flex-wrap bg-white rounded-3xl shadow-lg p-2.5 mb-8 border border-slate-200/90 gap-1.5 card-3d">
  <button onclick="tabDegis('aidat')" id="btnTabAidat" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl bg-gradient-to-r from-blue-900 to-indigo-900 text-white transition btn-3d flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-blue-600 text-white inline-flex items-center justify-center text-xs icon-3d"><i class="fa-solid fa-file-invoice-dollar"></i></span> Aidat Takibi
  </button>
  <button onclick="tabDegis('kasa')" id="btnTabKasa" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-gradient-to-br from-emerald-500 to-teal-600 text-white inline-flex items-center justify-center text-xs icon-3d-emerald"><i class="fa-solid fa-wallet"></i></span> Gelir / Gider
  </button>
  <button onclick="tabDegis('kontrol')" id="btnTabKontrol" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-gradient-to-br from-purple-500 to-indigo-600 text-white inline-flex items-center justify-center text-xs icon-3d"><i class="fa-solid fa-chart-pie"></i></span> Kontrol Paneli
  </button>
  <button onclick="tabDegis('banka')" id="btnTabBanka" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-gradient-to-br from-rose-500 to-red-600 text-white inline-flex items-center justify-center text-xs icon-3d-red"><i class="fa-solid fa-landmark"></i></span> Banka
  </button>
  <button onclick="tabDegis('toplanti')" id="btnTabToplanti" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-gradient-to-br from-amber-500 to-orange-600 text-white inline-flex items-center justify-center text-xs icon-3d-amber"><i class="fa-solid fa-handshake"></i></span> Toplantı
  </button>
  <button onclick="tabDegis('arsiv')" id="btnTabArsiv" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-gradient-to-br from-cyan-500 to-blue-600 text-white inline-flex items-center justify-center text-xs icon-3d"><i class="fa-solid fa-box-archive"></i></span> Arşiv
  </button>
  <button onclick="tabDegis('duyurular')" id="btnTabDuyurular" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-gradient-to-br from-amber-500 to-yellow-600 text-white inline-flex items-center justify-center text-xs icon-3d-amber"><i class="fa-solid fa-bullhorn"></i></span> Duyurular
  </button>
  <button onclick="tabDegis('arizalar')" id="btnTabArizalar" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-gradient-to-br from-rose-500 to-pink-600 text-white inline-flex items-center justify-center text-xs icon-3d-red"><i class="fa-solid fa-screwdriver-wrench"></i></span> Arıza Takip
  </button>
  <button onclick="tabDegis('rehber')" id="btnTabRehber" class="flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2">
    <span class="w-7 h-7 rounded-xl bg-gradient-to-br from-indigo-500 to-purple-600 text-white inline-flex items-center justify-center text-xs icon-3d"><i class="fa-solid fa-address-book"></i></span> Bina Rehberi
  </button>
</div>

<!-- BÖLÜM 1: AİDAT -->
<div id="bolumAidat" class="space-y-6 panel-3d-animasyon">
  <div class="bg-white p-6 rounded-3xl flex flex-col md:flex-row justify-between items-center gap-4 card-3d">
    <div class="flex items-center gap-4 w-full md:w-auto">
      <div class="bg-gradient-to-br from-blue-500 to-indigo-600 text-white p-3.5 rounded-2xl font-bold icon-3d"><i class="fa-solid fa-calendar-days text-lg"></i></div>
      <div class="w-full">
        <label class="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1">Dönem Seçimi (Gün, Ay, Yıl)</label>
        <div class="grid grid-cols-3 gap-2">
          <select id="donemGunSecici" onchange="guncelleEkran()" class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs font-extrabold text-blue-900 focus:ring-2 focus:ring-blue-600 outline-none shadow-sm"></select>
          <select id="donemAySecici" onchange="guncelleEkran()" class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs font-extrabold text-blue-900 focus:ring-2 focus:ring-blue-600 outline-none shadow-sm">
            <option value="01">Ocak</option><option value="02">Şubat</option><option value="03">Mart</option>
            <option value="04">Nisan</option><option value="05">Mayıs</option><option value="06">Haziran</option>
            <option value="07">Temmuz</option><option value="08">Ağustos</option><option value="09">Eylül</option>
            <option value="10">Ekim</option><option value="11">Kasım</option><option value="12">Aralık</option>
          </select>
          <select id="donemYilSecici" onchange="guncelleEkran()" class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs font-extrabold text-blue-900 focus:ring-2 focus:ring-blue-600 outline-none shadow-sm"></select>
        </div>
      </div>
    </div>
    <button id="btnDaireEkle" onclick="daireModalAc()" class="w-full md:w-auto bg-gradient-to-r from-blue-900 to-indigo-900 hover:from-blue-800 hover:to-indigo-800 text-white px-6 py-3.5 rounded-2xl font-extrabold btn-3d active:scale-95 transition-all text-sm flex items-center justify-center gap-2">
      <i class="fa-solid fa-user-plus"></i> Daire Ekle
    </button>
  </div>

  <div class="bg-white rounded-3xl overflow-hidden card-3d">
    <div class="p-5 bg-slate-50/90 border-b border-slate-200 flex justify-between items-center">
      <span class="text-xs font-extrabold text-slate-700 uppercase tracking-wider">Seçilen Dönem Daire Listesi ve Ödeme Detayları</span>
      <span id="seciliDonemBaslik" class="text-xs font-black text-blue-700 bg-blue-50 px-4 py-1.5 rounded-xl border border-blue-100 shadow-sm nowrap-date"></span>
    </div>
    <div class="overflow-x-auto">
      <table class="w-full text-left border-collapse">
        <thead>
          <tr class="border-b border-slate-200 text-slate-600 text-xs uppercase tracking-wider bg-white">
            <th class="p-4 font-bold">Daire No / Malik &amp; Tel</th>
            <th class="p-4 font-bold text-center">Aylık Tutar</th>
            <th class="p-4 font-bold text-center">Durum</th>
            <th id="thIslemBaslik" class="p-4 font-bold text-center">İşlem / SMS / Düzenle</th>
          </tr>
        </thead>
        <tbody id="daireListesiBody" class="divide-y divide-slate-100 text-sm"></tbody>
      </table>
    </div>
  </div>

  <!-- TÜM YILLIK ÖDEME GEÇMİŞİ ÖZET TABLOSU -->
  <div class="bg-white rounded-3xl p-6 mt-8 card-3d">
    <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4 mb-6">
      <h3 class="font-black text-slate-800 text-base flex items-center gap-2">
        <i class="fa-solid fa-table-cells text-blue-700"></i> Tüm Yıl Aidat Ödeme Matrisi
      </h3>
      <div class="flex items-center gap-3">
        <label class="text-xs font-bold text-slate-600 uppercase">Yıl Seçin:</label>
        <select id="matrisYilSecici" onchange="guncelleEkran()" class="bg-slate-50 border border-slate-200 rounded-xl px-4 py-2 text-sm font-bold text-slate-700 outline-none shadow-sm"></select>
      </div>
    </div>
    <div class="overflow-x-auto">
      <table class="w-full text-left border-collapse text-xs">
        <thead><tr id="matrisHead" class="bg-slate-50 border-b border-slate-200 text-slate-700"></tr></thead>
        <tbody id="matrisBody" class="divide-y divide-slate-100"></tbody>
      </table>
    </div>
  </div>
</div>

<!-- BÖLÜM: GELİR / GİDER -->
<div id="bolumKasa" class="hidden space-y-6 panel-3d-animasyon">
  <div id="yoneticiIslemBolumu" class="bg-white p-6 md:p-8 rounded-3xl card-3d">
    <div class="flex justify-between items-center mb-6">
      <h2 class="font-black text-slate-800 text-lg flex items-center gap-2.5"><i class="fa-solid fa-file-invoice-dollar text-blue-700"></i> Yeni Finansal İşlem Ekle</h2>
    </div>
    <form id="islemForm" onsubmit="islemEkle(event)" class="space-y-4">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div>
          <label class="block text-xs font-bold text-slate-600 uppercase mb-1">İşlem Türü</label>
          <select id="islemTip" onchange="kategoriDoldur()" class="w-full border border-slate-200 rounded-2xl p-3.5 text-sm font-bold focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
            <option value="gelir">Gelir (+)</option>
            <option value="gider">Gider (-)</option>
          </select>
        </div>
        <div>
          <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Kategori</label>
          <select id="islemKategori" class="w-full border border-slate-200 rounded-2xl p-3.5 text-sm font-bold focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm"></select>
        </div>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 shadow-sm">
          <label class="block text-xs font-bold text-slate-700 uppercase mb-2"><i class="fa-solid fa-calendar-days text-blue-700 mr-1"></i> İşlem Tarihi</label>
          <div class="grid grid-cols-3 gap-2">
            <div>
              <label class="block text-[10px] font-bold text-slate-500 mb-1">Gün</label>
              <select id="islemGun" class="w-full border border-slate-200 rounded-xl p-2 text-xs font-bold focus:ring-2 focus:ring-blue-600 outline-none bg-white shadow-sm"></select>
            </div>
            <div>
              <label class="block text-[10px] font-bold text-slate-500 mb-1">Ay</label>
              <select id="islemAy" class="w-full border border-slate-200 rounded-xl p-2 text-xs font-bold focus:ring-2 focus:ring-blue-600 outline-none bg-white shadow-sm">
                <option value="1">Ocak</option><option value="2">Şubat</option><option value="3">Mart</option>
                <option value="4">Nisan</option><option value="5">Mayıs</option><option value="6">Haziran</option>
                <option value="7">Temmuz</option><option value="8">Ağustos</option><option value="9">Eylül</option>
                <option value="10">Ekim</option><option value="11">Kasım</option><option value="12">Aralık</option>
              </select>
            </div>
            <div>
              <label class="block text-[10px] font-bold text-slate-500 mb-1">Yıl</label>
              <select id="islemYil" class="w-full border border-slate-200 rounded-xl p-2 text-xs font-bold focus:ring-2 focus:ring-blue-600 outline-none bg-white shadow-sm"></select>
            </div>
          </div>
        </div>

        <div>
          <label class="block text-xs font-bold text-slate-600 uppercase mb-1">İşlem Kaynağı</label>
          <select id="islemKaynak" class="w-full border border-slate-200 rounded-2xl p-3.5 text-sm font-bold focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 mt-1 shadow-sm">
            <option value="Ziraat Bankası">Ziraat Bankası</option>
            <option value="Nakit Kasa">Nakit Kasa</option>
          </select>
        </div>

        <div>
          <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Tutar (TL)</label>
          <input type="number" step="0.01" id="islemTutar" placeholder="0,00" required class="w-full border border-slate-200 rounded-2xl p-3.5 text-sm font-bold focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 mt-1 shadow-sm">
        </div>
      </div>

      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Açıklama (Örn: 10 Nolu Daire Aidat Ödemesi)</label>
        <input type="text" id="islemAciklama" placeholder="Örn: 10 Nolu Daire veya Blok Temizlik Ücreti" required class="w-full border border-slate-200 rounded-2xl p-3.5 text-sm font-bold focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
      </div>

      <div class="border border-dashed border-slate-300 rounded-2xl p-4 bg-slate-50 flex flex-col md:flex-row items-center justify-between gap-4 shadow-sm">
        <div>
          <p class="text-xs font-bold text-slate-800"><i class="fa-solid fa-file-arrow-up mr-1 text-blue-700"></i> Belge / Dekont Ekle</p>
          <p class="text-[11px] text-slate-600">İşleme ait fiş, fatura veya dekont görseli ekleyebilirsiniz.</p>
        </div>
        <input type="file" id="islemBelgeDosya" accept="image/*,.pdf" class="text-xs font-bold text-slate-700 file:mr-4 file:py-2 file:px-4 file:rounded-xl file:border-0 file:text-xs file:font-bold file:bg-blue-900 file:text-white hover:file:bg-blue-800 cursor-pointer">
      </div>

      <button type="submit" class="w-full bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-700 hover:to-teal-700 text-white rounded-2xl py-3.5 font-extrabold btn-3d active:scale-95 transition-all text-sm flex items-center justify-center gap-2">
        <i class="fa-solid fa-floppy-disk"></i> İşlemi ve Belgeyi Kaydet
      </button>
    </form>
  </div>

  <!-- LİSTE VE TOPLU SİLME -->
  <div class="bg-white rounded-3xl p-6 card-3d space-y-4">
    <div class="flex flex-col md:flex-row justify-between items-center gap-4 border-b border-slate-200 pb-4">
      <h3 class="font-black text-slate-800 text-base flex items-center gap-2">
        <i class="fa-solid fa-list text-blue-700"></i> Finansal İşlemler Listesi
      </h3>
      <div id="yoneticiTopluSilBolumu" class="flex items-center gap-2 flex-wrap">
        <button onclick="secilenleriSil()" class="bg-gradient-to-r from-rose-600 to-red-600 hover:from-rose-700 hover:to-red-700 text-white text-xs px-4 py-2.5 rounded-xl transition btn-3d font-bold flex items-center gap-1.5 shadow-sm active:scale-95">
          <i class="fa-solid fa-trash-can"></i> Seçilenleri Sil
        </button>
        <button onclick="tumunuSil()" class="bg-gradient-to-r from-red-800 to-rose-900 hover:from-red-900 hover:to-rose-950 text-white text-xs px-4 py-2.5 rounded-xl transition btn-3d font-bold flex items-center gap-1.5 shadow-sm active:scale-95">
          <i class="fa-solid fa-triangle-exclamation"></i> Tümünü Sil
        </button>
      </div>
    </div>
    <div class="overflow-x-auto">
      <table class="w-full text-left border-collapse">
        <thead>
          <tr class="bg-slate-50 border-b border-slate-200 text-slate-700 text-xs uppercase tracking-wider">
            <th id="thSecimKolon" class="p-4 text-center w-10">
              <input type="checkbox" id="tumunuSecCheckbox" onclick="tumunuSecToggle(this)" class="w-4 h-4 text-blue-900 rounded focus:ring-blue-600 border-slate-300 cursor-pointer">
            </th>
            <th class="p-4 font-bold">Tarih</th>
            <th class="p-4 font-bold">Kaynak</th>
            <th class="p-4 font-bold">Kategori</th>
            <th class="p-4 font-bold">Açıklama</th>
            <th class="p-4 font-bold text-center">Tutar</th>
            <th class="p-4 font-bold text-center">Belge</th>
            <th id="thSilKolon" class="p-4 font-bold text-center">Sil</th>
          </tr>
        </thead>
        <tbody id="islemListesiBody" class="divide-y divide-slate-100 text-sm"></tbody>
      </table>
    </div>
  </div>
</div>

<!-- BÖLÜM 2: KONTROL PANELİ -->
<div id="bolumKontrol" class="hidden space-y-6 panel-3d-animasyon">
  <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
    <div class="bg-white p-6 rounded-3xl card-3d">
      <h3 class="font-black text-slate-800 text-base mb-4 flex items-center gap-2"><i class="fa-solid fa-chart-pie text-blue-700"></i> Gelir ve Gider Dağılımı</h3>
      <div class="relative h-64 flex justify-center items-center"><canvas id="gelirGiderChart"></canvas></div>
    </div>
    <div class="bg-white p-6 rounded-3xl card-3d">
      <h3 class="font-black text-slate-800 text-base mb-4 flex items-center gap-2"><i class="fa-solid fa-chart-column text-blue-700"></i> Kasa / Banka Varlık Dağılımı</h3>
      <div class="relative h-64 flex justify-center items-center"><canvas id="bankaChart"></canvas></div>
    </div>
  </div>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
    <div class="bg-white p-6 rounded-3xl card-3d">
      <h3 class="font-black text-slate-800 text-base mb-4 flex items-center gap-2"><i class="fa-solid fa-chart-bar text-blue-700"></i> Kategori Bazlı Gider Dağılımı</h3>
      <div class="relative h-64 flex justify-center items-center"><canvas id="kategoriGiderChart"></canvas></div>
    </div>
    <div class="bg-white p-6 rounded-3xl card-3d">
      <h3 class="font-black text-slate-800 text-base mb-4 flex items-center gap-2"><i class="fa-solid fa-chart-line text-blue-700"></i> Aylık Gelir / Gider Karşılaştırması</h3>
      <div class="relative h-64 flex justify-center items-center"><canvas id="aylikKarsilastirmaChart"></canvas></div>
    </div>
  </div>
</div>

<!-- BÖLÜM 4: BANKA HESAPLARI -->
<div id="bolumBanka" class="hidden space-y-6 panel-3d-animasyon">
  <div class="bg-white p-6 md:p-8 rounded-3xl card-3d">
    <h2 class="font-black text-slate-800 text-lg mb-6 flex items-center gap-2.5"><i class="fa-solid fa-building-columns text-blue-700"></i> Banka ve Kasa Hesapları Yönetimi</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6" id="bankaHesapListesi"></div>
  </div>
</div>

<!-- BÖLÜM 5: TOPLANTI KARARLARI -->
<div id="bolumToplanti" class="hidden space-y-6 panel-3d-animasyon">
  <div class="bg-white p-6 md:p-8 rounded-3xl flex flex-col md:flex-row justify-between items-center gap-4 card-3d">
    <div>
      <h2 class="font-black text-slate-800 text-lg flex items-center gap-2.5"><i class="fa-solid fa-handshake text-blue-700"></i> Kat Maliki / Yönetim Kurulu Toplantı Kararları</h2>
      <p class="text-xs text-slate-600 mt-1">Bina genel kurul toplantılarını ve alınan kararları buradan takip edin.</p>
    </div>
    <button id="btnToplantiEkle" onclick="toplantiModalAc()" class="w-full md:w-auto bg-gradient-to-r from-blue-900 to-indigo-900 hover:from-blue-800 hover:to-indigo-800 text-white px-6 py-3.5 rounded-2xl font-extrabold btn-3d active:scale-95 transition-all text-sm flex items-center justify-center gap-2">
      <i class="fa-solid fa-plus"></i> Yeni Toplantı Ekle
    </button>
  </div>
  <div class="bg-white rounded-3xl p-6 card-3d">
    <div class="space-y-4" id="toplantiListesiContainer"></div>
  </div>
</div>

<!-- BÖLÜM 6: DİJİTAL ARŞİV -->
<div id="bolumArsiv" class="hidden space-y-6 panel-3d-animasyon">
  <div class="bg-white p-6 md:p-8 rounded-3xl flex flex-col md:flex-row justify-between items-center gap-4 card-3d">
    <div>
      <h2 class="font-black text-slate-800 text-lg flex items-center gap-2.5"><i class="fa-solid fa-box-archive text-blue-700"></i> Dijital Belge ve Arşiv Yönetimi</h2>
      <p class="text-xs text-slate-600 mt-1">Karar defteri, işletme defteri ve bina evraklarını taratarak saklayın.</p>
    </div>
    <button id="btnArsivEkle" onclick="arsivModalAc()" class="w-full md:w-auto bg-gradient-to-r from-blue-900 to-indigo-900 hover:from-blue-800 hover:to-indigo-800 text-white px-6 py-3.5 rounded-2xl font-extrabold btn-3d active:scale-95 transition-all text-sm flex items-center justify-center gap-2">
      <i class="fa-solid fa-file-arrow-up"></i> Yeni Belge Yükle
    </button>
  </div>
  <div class="bg-white rounded-3xl p-6 card-3d">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6" id="arsivListesiContainer"></div>
  </div>
</div>

<!-- BÖLÜM: DUYURULAR SEKMESİ -->
<div id="bolumDuyurular" class="hidden space-y-6 panel-3d-animasyon">
  <div class="bg-white p-6 md:p-8 rounded-3xl flex flex-col md:flex-row justify-between items-center gap-4 card-3d">
    <div>
      <h2 class="font-black text-slate-800 text-lg flex items-center gap-2.5"><i class="fa-solid fa-bullhorn text-amber-600"></i> Bina Genel Duyuruları ve Sistem Mesajları</h2>
      <p class="text-xs text-slate-600 mt-1">Yönetim tarafından yayınlanan tüm duyuruları buradan takip edebilirsiniz.</p>
    </div>
  </div>
  <div class="bg-white rounded-3xl p-6 card-3d">
    <div id="duyurularListesiniContainer" class="space-y-4"></div>
  </div>
</div>

<!-- BÖLÜM: ARIZA TAKİP MODÜLÜ -->
<div id="bolumArizalar" class="hidden space-y-6 panel-3d-animasyon">
  <div class="bg-white p-6 md:p-8 rounded-3xl card-3d">
    <h2 class="font-black text-slate-800 text-lg mb-2 flex items-center gap-2.5"><i class="fa-solid fa-screwdriver-wrench text-rose-600"></i> Bina Arıza ve Bakım Takip Paneli</h2>
    <p class="text-xs text-slate-600 mb-6">Ortak alan veya daire içi arıza/bakım taleplerinizi buradan iletebilir, mevcut taleplerin durumunu takip edebilirsiniz.</p>

    <div class="bg-slate-50 p-5 rounded-2xl border border-slate-200 mb-6 shadow-sm" id="arizaTalepFormu">
      <h3 class="font-extrabold text-slate-800 text-sm mb-3">Yeni Arıza / Bakım Talebi Oluştur</h3>
      <div class="space-y-3">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Daireniz / Adınız</label>
            <input type="text" id="arizaDaireBilgi" placeholder="Örn: 5 Nolu Daire - Serhat OYTUKKAYA" class="w-full border border-slate-300 rounded-xl p-3 text-xs font-bold bg-white outline-none">
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Arıza Türü / Kategori</label>
            <select id="arizaKategori" class="w-full border border-slate-300 rounded-xl p-3 text-xs font-bold bg-white outline-none">
              <option value="Asansör Arızası">Asansör Arızası</option>
              <option value="Su / Tesisat Sorunu">Su / Tesisat Sorunu</option>
              <option value="Elektrik / Aydınlatma">Elektrik / Aydınlatma</option>
              <option value="Temizlik / Çöp">Temizlik / Çöp</option>
              <option value="Ortak Alan / Kapı">Ortak Alan / Kapı</option>
              <option value="Diğer">Diğer</option>
            </select>
          </div>
        </div>
        <div>
          <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Arıza / Sorun Açıklaması</label>
          <textarea id="arizaAciklama" rows="2" placeholder="Arızanın detaylarını ve konumunu yazınız..." class="w-full border border-slate-300 rounded-xl p-3 text-xs font-bold bg-white outline-none"></textarea>
        </div>
        <button onclick="arizaTalebiEkle()" class="bg-gradient-to-r from-rose-600 to-red-600 text-white px-6 py-3 rounded-xl font-bold text-xs btn-3d shadow-sm flex items-center gap-2">
          <i class="fa-solid fa-paper-plane"></i> Arıza Talebini Gönder
        </button>
      </div>
    </div>

    <div class="overflow-x-auto">
      <table class="w-full text-left border-collapse">
        <thead>
          <tr class="bg-slate-50 border-b border-slate-200 text-slate-700 text-xs uppercase tracking-wider">
            <th class="p-4 font-bold">Tarih</th>
            <th class="p-4 font-bold">Daire / Sakin</th>
            <th class="p-4 font-bold">Kategori</th>
            <th class="p-4 font-bold">Açıklama</th>
            <th class="p-4 font-bold text-center">Durum</th>
            <th class="p-4 font-bold text-center">İşlem</th>
          </tr>
        </thead>
        <tbody id="arizaListesiBody" class="divide-y divide-slate-100 text-sm"></tbody>
      </table>
    </div>
  </div>
</div>

<!-- BÖLÜM 7: BİNA REHBERİ -->
<div id="bolumRehber" class="hidden space-y-6 panel-3d-animasyon">
  <div class="bg-white p-6 md:p-8 rounded-3xl card-3d">
    <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4 mb-6">
      <div>
        <h2 class="font-black text-slate-800 text-lg mb-1 flex items-center gap-2.5"><i class="fa-solid fa-address-book text-blue-700"></i> Bina Sakinleri İletişim Rehberi</h2>
        <p class="text-xs text-slate-600">Tüm kat maliklerinin ve kiracıların iletişim bilgilerine, arama ve WhatsApp butonlarına hızlıca buradan ulaşabilirsiniz.</p>
      </div>
      <input type="text" id="rehberAramaInput" onkeyup="binaRehberiniGuncelle()" placeholder="İsim veya daire ara..." class="border border-slate-300 rounded-2xl p-3 text-xs font-bold outline-none w-full md:w-72 bg-slate-50 shadow-sm">
    </div>
    <div class="overflow-x-auto">
      <table class="w-full text-left border-collapse">
        <thead>
          <tr class="bg-slate-50 border-b border-slate-200 text-slate-700 text-xs uppercase tracking-wider">
            <th class="p-4 font-bold">Daire No</th>
            <th class="p-4 font-bold">Kat Maliki / Sakin</th>
            <th class="p-4 font-bold">İletişim / Telefon</th>
            <th class="p-4 font-bold text-center">Hızlı İşlem (Arama / WhatsApp / SMS)</th>
          </tr>
        </thead>
        <tbody id="rehberListesiBody" class="divide-y divide-slate-100 text-sm"></tbody>
      </table>
    </div>
  </div>
</div>
</main>

<!-- YÖNETİCİ AYARLARI VE YETKİ MODALI -->
<div id="yoneticiAyarlariModal" class="fixed inset-0 bg-slate-900/65 backdrop-blur-md hidden flex items-center justify-center p-4 z-50">
  <div class="bg-white rounded-3xl p-6 md:p-8 w-full max-w-xl shadow-2xl border border-slate-100 card-3d max-h-[90vh] overflow-auto">
    <div class="flex justify-between items-center mb-6">
      <h3 class="font-black text-xl text-slate-800 flex items-center gap-3">
        <i class="fa-solid fa-gears text-purple-700"></i> Yönetici Ayarları ve Yetki Paneli
      </h3>
      <button onclick="yoneticiAyarlariModalKapat()" class="text-slate-400 hover:text-rose-600 text-xl font-bold p-2"><i class="fa-solid fa-xmark"></i></button>
    </div>

    <div class="space-y-6">
      <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200">
        <h4 class="font-extrabold text-slate-800 text-sm mb-2"><i class="fa-solid fa-shield-halved text-blue-700 mr-1.5"></i> Daire Bazlı Yetkilendirme ve Şifre Yönetimi (Varsayılan: 12345)</h4>
        <p class="text-xs text-slate-600 mb-3">Her dairenin özel şifresini (varsayılan 12345) belirleyebilir ve kat maliki modunda görebileceği sekmeleri ayarlayabilirsiniz.</p>
        <div id="daireYetkiListesiContainer" class="space-y-3 max-h-56 overflow-auto pr-2"></div>
      </div>

      <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 space-y-4">
        <h4 class="font-extrabold text-slate-800 text-sm mb-1"><i class="fa-solid fa-sliders text-blue-700 mr-1.5"></i> Gelişmiş Sistem Ayarları</h4>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <label class="block text-[10px] font-bold text-slate-500 uppercase mb-1">Otomatik SMS Hatırlatıcı</label>
            <select id="ayarSmsKurali" class="w-full border border-slate-300 rounded-xl p-2.5 text-xs font-bold bg-white outline-none">
              <option value="aylik_1">Her Ayın 1'inde Otomatik</option>
              <option value="gecikme_3">Gecikmedeki Aidatlar İçin 3 Günde Bir</option>
              <option value="manuel">Sadece Manuel Gönderim</option>
            </select>
          </div>
          <div>
            <label class="block text-[10px] font-bold text-slate-500 uppercase mb-1">Otomatik Yedekleme Sıklığı</label>
            <select id="ayarYedekSikligi" class="w-full border border-slate-300 rounded-xl p-2.5 text-xs font-bold bg-white outline-none">
              <option value="her_islem">Her İşlem Sonrası</option>
              <option value="haftalik">Haftalık Periyot</option>
              <option value="manuel">Yalnızca Manuel Yedek</option>
            </select>
          </div>
        </div>
        <div>
          <label class="block text-[10px] font-bold text-slate-500 uppercase mb-1"><i class="fa-solid fa-bullhorn text-amber-600 mr-1"></i> Bina Genel Duyuru / Sistem Mesajı Paneli</label>
          <textarea id="ayarGenelDuyuru" rows="2" placeholder="Buraya yazdığınız duyuru ana sayfada ve duyurular sekmesinde görünür..." class="w-full border border-slate-300 rounded-xl p-2.5 text-xs font-bold bg-white outline-none">Lütfen yazıları dikkate alın!</textarea>
        </div>
        <button onclick="gelismisAyarlariKaydet()" class="w-full bg-emerald-700 hover:bg-emerald-800 text-white rounded-xl py-2.5 text-xs font-bold btn-3d shadow-sm">Ayarları ve Duyuruyu Kaydet</button>
      </div>

      <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200">
        <h4 class="font-extrabold text-slate-800 text-sm mb-2"><i class="fa-solid fa-key text-blue-700 mr-1.5"></i> Yönetici Şifre Değiştirme</h4>
        <div class="space-y-3 mt-2">
          <div>
            <label class="block text-[10px] font-bold text-slate-500 uppercase mb-1">Yeni Yönetim Şifresi</label>
            <input type="password" id="modalYeniSifreInput" placeholder="Yeni şifrenizi girin" class="w-full border border-slate-300 rounded-xl p-3 text-sm font-bold bg-white outline-none focus:ring-2 focus:ring-blue-600 shadow-sm">
          </div>
          <button onclick="modalSifreGuncelle()" class="w-full bg-blue-900 hover:bg-blue-800 text-white rounded-xl py-2.5 text-xs font-bold btn-3d shadow-sm">Şifreyi Güncelle</button>
        </div>
      </div>
    </div>

    <div class="flex justify-end gap-3 mt-8">
      <button onclick="yoneticiAyarlariModalKapat()" class="px-6 py-2.5 rounded-2xl font-bold border border-slate-200 text-slate-600 hover:bg-slate-50 transition shadow-sm text-sm">Kapat</button>
    </div>
  </div>
</div>

<!-- Daire Ekle / Düzenle Modal -->
<div id="daireModal" class="fixed inset-0 bg-slate-900/65 backdrop-blur-md hidden flex items-center justify-center p-4 z-50">
  <div class="bg-white rounded-3xl p-6 md:p-8 w-full max-w-md shadow-2xl border border-slate-100 card-3d">
    <h3 id="daireModalBaslik" class="font-black text-xl text-slate-800 mb-6 flex items-center gap-3">
      <i class="fa-solid fa-user-plus text-blue-700"></i> Yeni Daire Tanımla
    </h3>
    <input type="hidden" id="duzenlenenDaireId">
    <div class="space-y-4">
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Daire No / Blok No</label>
        <input type="text" id="yeniDaireNo" placeholder="Örn: 1 Nolu Daire" class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
      </div>
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Kat Maliki / Kiracı Adı</label>
        <input type="text" id="yeniDaireSahip" placeholder="Örn: Abdulkadir DAĞDEVİREN" class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
      </div>
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Cep Telefonu (Arama, WhatsApp, SMS için)</label>
        <input type="text" id="yeniDaireTelefon" placeholder="Örn: 05425583831" class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
      </div>
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Aylık Aidat Tutarı (TL)</label>
        <input type="number" id="yeniDaireTutar" placeholder="Örn: 350,00" class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
      </div>
      <div class="flex items-center gap-3 pt-2">
        <input type="checkbox" id="yeniDaireYonetici" class="w-5 h-5 text-blue-900 rounded focus:ring-blue-600 border-slate-300">
        <label for="yeniDaireYonetici" class="text-sm font-bold text-slate-700">Yönetici / Aidat Ödemez (Muaf)</label>
      </div>
    </div>
    <div class="flex justify-end gap-3 mt-8">
      <button onclick="daireModalKapat()" class="px-6 py-3 rounded-2xl font-bold flex-1 md:flex-none border border-slate-200 text-slate-600 hover:bg-slate-50 transition active:scale-95 shadow-sm">İptal</button>
      <button onclick="daireKaydet()" class="px-6 py-3 rounded-2xl font-bold flex-1 md:flex-none bg-gradient-to-r from-blue-900 to-indigo-900 text-white btn-3d hover:from-blue-800 hover:to-indigo-800 transition active:scale-95">Kaydet</button>
    </div>
  </div>
</div>

<!-- Toplantı Ekle Modal -->
<div id="toplantiModal" class="fixed inset-0 bg-slate-900/65 backdrop-blur-md hidden flex items-center justify-center p-4 z-50">
  <div class="bg-white rounded-3xl p-6 md:p-8 w-full max-w-md shadow-2xl border border-slate-100 card-3d">
    <h3 class="font-black text-xl text-slate-800 mb-6 flex items-center gap-3">
      <i class="fa-solid fa-handshake text-blue-700"></i> Yeni Toplantı Kararı Ekle
    </h3>
    <div class="space-y-4">
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Toplantı Konusu / Başlığı</label>
        <input type="text" id="toplantiBaslik" placeholder="Örn: Yıllık Olağan Kurul" class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
      </div>
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Toplantı Tarihi</label>
        <input type="date" id="toplantiTarih" class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
      </div>
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Alınan Kararlar / Gündem Detayları</label>
        <textarea id="toplantiKararlar" rows="4" placeholder="1. Asansör bakımı onaylandı..." class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm"></textarea>
      </div>
    </div>
    <div class="flex justify-end gap-3 mt-8">
      <button onclick="toplantiModalKapat()" class="px-6 py-3 rounded-2xl font-bold flex-1 md:flex-none border border-slate-200 text-slate-600 hover:bg-slate-50 transition active:scale-95 shadow-sm">İptal</button>
      <button onclick="toplantiKaydet()" class="px-6 py-3 rounded-2xl font-bold flex-1 md:flex-none bg-gradient-to-r from-blue-900 to-indigo-900 text-white btn-3d hover:from-blue-800 hover:to-indigo-800 transition active:scale-95">Kaydet</button>
    </div>
  </div>
</div>

<!-- Arşiv Belge Ekle Modal -->
<div id="arsivModal" class="fixed inset-0 bg-slate-900/65 backdrop-blur-md hidden flex items-center justify-center p-4 z-50">
  <div class="bg-white rounded-3xl p-6 md:p-8 w-full max-w-md shadow-2xl border border-slate-100 card-3d">
    <h3 class="font-black text-xl text-slate-800 mb-6 flex items-center gap-3">
      <i class="fa-solid fa-file-arrow-up text-blue-700"></i> Dijital Arşive Belge Ekle
    </h3>
    <div class="space-y-4">
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Belge Türü</label>
        <select id="arsivTip" class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
          <option value="Karar Defteri">Karar Defteri</option>
          <option value="İşletme Defteri">İşletme Defteri</option>
          <option value="Fatura / Fiş">Fatura / Fiş</option>
          <option value="Bina Evrakı">Bina Evrakı</option>
          <option value="Diğer">Diğer</option>
        </select>
      </div>
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Belge Başlığı / Açıklama</label>
        <input type="text" id="arsivBaslik" placeholder="Örn: Ekim Elektrik Faturası" class="w-full border border-slate-200 rounded-2xl p-3.5 font-bold text-sm focus:ring-2 focus:ring-blue-600 outline-none bg-slate-50 shadow-sm">
      </div>
      <div>
        <label class="block text-xs font-bold text-slate-600 uppercase mb-1">Belge Dosyası</label>
        <input type="file" id="arsivDosyaInput" accept="image/*,.pdf" class="w-full border border-slate-200 rounded-2xl p-3 text-xs font-bold file:mr-4 file:py-2 file:px-4 file:rounded-xl file:border-0 file:text-xs file:font-bold file:bg-blue-50 file:text-blue-900 hover:file:bg-blue-100 cursor-pointer shadow-sm">
      </div>
    </div>
    <div class="flex justify-end gap-3 mt-8">
      <button onclick="arsivModalKapat()" class="px-6 py-3 rounded-2xl font-bold flex-1 md:flex-none border border-slate-200 text-slate-600 hover:bg-slate-50 transition active:scale-95 shadow-sm">İptal</button>
      <button onclick="arsivBelgeKaydet()" class="px-6 py-3 rounded-2xl font-bold flex-1 md:flex-none bg-gradient-to-r from-blue-900 to-indigo-900 text-white btn-3d hover:from-blue-800 hover:to-indigo-800 transition active:scale-95">Kaydet</button>
    </div>
  </div>
</div>

<!-- Belge Görüntüleme Modal -->
<div id="belgeGosterModal" class="fixed inset-0 bg-slate-900/80 backdrop-blur-md hidden flex items-center justify-center p-4 z-50">
  <div class="bg-white rounded-3xl p-6 w-full max-w-2xl shadow-2xl border border-slate-100 relative card-3d">
    <div class="flex justify-between items-center mb-4">
      <h3 id="belgeGosterBaslik" class="font-black text-base text-slate-800">Belge Görüntüleme</h3>
      <button onclick="belgeGosterKapat()" class="text-slate-400 hover:text-rose-600 text-xl font-bold p-2"><i class="fa-solid fa-xmark"></i></button>
    </div>
    <div id="belgeGosterIcerik" class="flex justify-center items-center bg-slate-50 rounded-2xl p-4 max-h-[70vh] overflow-auto shadow-inner"></div>
  </div>
</div>

<!-- Detay Modal -->
<div id="detayModal" class="fixed inset-0 bg-slate-900/80 backdrop-blur-md hidden flex items-center justify-center p-4 z-50">
  <div class="bg-white rounded-3xl p-6 md:p-8 w-full max-w-3xl shadow-2xl border border-slate-100 relative card-3d">
    <div class="flex justify-between items-center mb-4 border-b border-slate-200 pb-4">
      <h3 id="detayModalBaslik" class="font-black text-lg text-slate-800 flex items-center gap-2">Detaylar</h3>
      <button onclick="detayModalKapat()" class="text-slate-400 hover:text-rose-600 text-xl font-bold p-2"><i class="fa-solid fa-xmark"></i></button>
    </div>
    <div class="max-h-[60vh] overflow-auto">
      <table class="w-full text-left border-collapse text-sm">
        <thead><tr id="detayModalTableHead" class="bg-slate-50 border-b border-slate-200 text-slate-700 text-xs uppercase"></tr></thead>
        <tbody id="detayModalBody" class="divide-y divide-slate-100"></tbody>
      </table>
    </div>
  </div>
</div>

<script>
const KATEGORILER = {
  gelir: ["Aidat Ödemesi", "Gecikme Faizi", "Dış Cephe Reklam", "Demirbaş Toplanan", "Diğer", "Devir / Bakiye"],
  gider: ["Elektrik Faturası", "Su Faturası", "Doğalgaz Faturası", "Personel Maaşı", "Temizlik Malzemesi", "Asansör Bakım", "Genel Tamirat / Tadilat", "Yönetici Hizmet Bedeli", "Kırtasiye / Posta", "Hırdavat", "Diğer"]
};

const AYLAR_ISIM = ["Ocak", "Şubat", "Mart", "Nisan", "Mayıs", "Haziran", "Temmuz", "Ağustos", "Eylül", "Ekim", "Kasım", "Aralık"];

let aktifKullaniciRol = 'yonetici';
let aktifKatMalikiDaireId = null;

const VARSAYILAN_IZINLER = { aidat: true, duyurular: true, arizalar: true, kontrol: false, kasa: false, banka: false, toplanti: false, arsiv: false, rehber: true };

let daireler = [
  { id: 1, no: "1 Nolu Daire", sahip: "Abdulkadir DAĞDEVİREN", telefon: "05425583831", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 2, no: "2 Nolu Daire", sahip: "İsa ÇORUK", telefon: "0505397773375", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 3, no: "3 Nolu Daire", sahip: "Recep KOÇOĞULLU", telefon: "050592488051", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 4, no: "4 Nolu Daire", sahip: "Kadriye ÖZTÜRK", telefon: "033611304836", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 5, no: "5 Nolu Daire", sahip: "Serhat OYTUKKAYA", telefon: "0905077092322", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 6, no: "6 Nolu Daire", sahip: "Hilmi YEŞİL", telefon: "0905376770403", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 7, no: "7 Nolu Daire", sahip: "Esat AYKULUĞ", telefon: "090533 417 28 13", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 8, no: "8 Nolu Daire", sahip: "Hüseyin YILDIZ", telefon: "0905362868104", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 9, no: "9 Nolu Daire", sahip: "Zafer OYGUR", telefon: "090542 337 12 10", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 10, no: "10 Nolu Daire", sahip: "Gökhan SARGIN", telefon: "05548268116", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: { "2026-10": true } },
  { id: 11, no: "11 Nolu Daire", sahip: "Ali ÜSTÜN", telefon: "0905506266867", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} },
  { id: 12, no: "12 Nolu Daire", sahip: "Erkut İŞLER", telefon: "090535317404", sifre: "12345", tutar: 350, yoneticiMuaf: false, izinler: { ...VARSAYILAN_IZINLER }, odemeGecmisi: {} }
];

function daireleriYirmiyeTamamla() {
  for (let no = 1; no <= 20; no++) {
    let mevcut = daireler.find(d => Number((d.no || '').replace(/[^0-9]/g, '')) === no);
    if (!mevcut) {
      daireler.push({
        id: Date.now() + no,
        no: `${no} Nolu Daire`,
        sahip: `Daire ${no} Sakini`,
        telefon: '',
        sifre: '12345',
        tutar: 350,
        yoneticiMuaf: false,
        izinler: { ...VARSAYILAN_IZINLER },
        odemeGecmisi: {}
      });
    } else {
      if (!mevcut.sifre) mevcut.sifre = '12345';
      if (!mevcut.izinler) mevcut.izinler = { ...VARSAYILAN_IZINLER };
      if (!mevcut.odemeGecmisi) mevcut.odemeGecmisi = {};
    }
  }
}

let islemler = [
  { id: 1, tip: 'gider', kategori: 'Asansör Bakım', kaynak: 'Ziraat Bankası', aciklama: 'Asansör', tutar: 1350, gun: 30, ay: 10, yil: 2026, tarih: '2026-10-30', belgeData: null },
  { id: 2, tip: 'gelir', kategori: 'Aidat Ödemesi', kaynak: 'Ziraat Bankası', aciklama: '10 Nolu Daire (Gökhan SARGIN) Ödemesi', tutar: 350, gun: 29, ay: 10, yil: 2026, tarih: '2026-10-29', daireId: 10, islemAy: '2026-10', belgeData: null },
  { id: 3, tip: 'gelir', kategori: 'Demirbaş Toplanan', kaynak: 'Nakit Kasa', aciklama: 'Demirbaş harici toplanan', tutar: 20000, gun: 29, ay: 10, yil: 2026, tarih: '2026-10-29', belgeData: null }
];

let arsivBelgeleri = [];
let toplantilar = [
  { id: 1, baslik: "Asansör Bakım ve Genel Kurul", tarih: "2026-10-15", kararlar: "Yıllık bakım ve asansör revizyonu görüşüldü." }
];

let arizalar = [
  { id: 1, daire: "1 Nolu Daire - Abdulkadir DAĞDEVİREN", kategori: "Asansör Arızası", aciklama: "Asansör 3. katta duruyor.", tarih: "2026-10-28", durum: "İşlemde" }
];

let bankaHesaplari = [
  { id: 1, ad: "Ziraat Bankası" },
  { id: 2, ad: "Nakit Kasa" }
];

let sistemAyarlari = {
  smsKurali: "aylik_1",
  yedekSikligi: "her_islem",
  genelDuyuru: "Lütfen yazıları dikkate alın!",
  duyuruTarihi: "01.11.2026 03:58"
};

let gelirGiderChartInstance = null;
let bankaChartInstance = null;
let kategoriGiderChartInstance = null;
let aylikKarsilastirmaChartInstance = null;

// ---------- GİRİŞ / GÜVENLİK ----------
function getYoneticSifre() {
  return localStorage.getItem('site_yonetici_sifre') || "135790";
}

function girisHataGoster(mesaj) {
  const el = document.getElementById('girisHataMesaji');
  if (mesaj) {
    el.innerText = mesaj;
    el.classList.remove('hidden');
  } else {
    el.classList.add('hidden');
  }
}

function sifreKontrolEt() {
  const kullaniciAdi = (document.getElementById('girisKullaniciInput')?.value || '').trim().toLocaleLowerCase('tr');
  const girilenSifre = (document.getElementById('girisSifreInput')?.value || '').trim();
  const beniHatirla = document.getElementById('beniHatirlaCheckbox')?.checked;

  if (!kullaniciAdi || !girilenSifre) {
    girisHataGoster('Lütfen kullanıcı adı ve şifre alanlarını doldurun.');
    return;
  }

  if ((kullaniciAdi === 'yönetici' || kullaniciAdi === 'yonetici') && girilenSifre === getYoneticSifre()) {
    aktifKullaniciRol = 'yonetici';
    aktifKatMalikiDaireId = null;
    girisHataGoster(null);
    if (beniHatirla) {
      localStorage.setItem('site_hatirlanan_kullanici', kullaniciAdi);
      localStorage.setItem('site_hatirlanan_sifre', girilenSifre);
      localStorage.setItem('site_beni_hatirla_aktif', 'true');
    } else {
      localStorage.removeItem('site_hatirlanan_kullanici');
      localStorage.removeItem('site_hatirlanan_sifre');
      localStorage.removeItem('site_beni_hatirla_aktif');
    }
    rolArayuzunuUyarla();
    document.getElementById('sifreModal').classList.add('hidden');
    return;
  }

  const daireNo = Number(kullaniciAdi);
  const eslesenDaire = Number.isInteger(daireNo) && daireNo >= 1 && daireNo <= 20
    ? daireler.find(d => Number((d.no || '').replace(/[^0-9]/g, '')) === daireNo)
    : null;

  if (eslesenDaire && girilenSifre === (eslesenDaire.sifre || '12345')) {
    aktifKatMalikiDaireId = eslesenDaire.id;
    aktifKullaniciRol = 'kat_maliki';
    girisHataGoster(null);
    if (beniHatirla) {
      localStorage.setItem('site_hatirlanan_kullanici', kullaniciAdi);
      localStorage.setItem('site_hatirlanan_sifre', girilenSifre);
      localStorage.setItem('site_beni_hatirla_aktif', 'true');
    } else {
      localStorage.removeItem('site_hatirlanan_kullanici');
      localStorage.removeItem('site_hatirlanan_sifre');
      localStorage.removeItem('site_beni_hatirla_aktif');
    }
    rolArayuzunuUyarla();
    document.getElementById('sifreModal').classList.add('hidden');
    alert(`${eslesenDaire.no} görüntüleme hesabıyla giriş yapıldı.`);
    return;
  }

  girisHataGoster('Hatalı kullanıcı adı veya şifre! Lütfen tekrar deneyin.');
  document.getElementById('girisSifreInput').value = '';
}

function oturumuKapat() {
  aktifKullaniciRol = 'yonetici';
  aktifKatMalikiDaireId = null;
  localStorage.removeItem('site_beni_hatirla_aktif');
  localStorage.removeItem('site_hatirlanan_kullanici');
  localStorage.removeItem('site_hatirlanan_sifre');
  document.getElementById('girisKullaniciInput').value = '';
  document.getElementById('girisSifreInput').value = '';
  if (document.getElementById('beniHatirlaCheckbox')) {
    document.getElementById('beniHatirlaCheckbox').checked = false;
  }
  girisHataGoster(null);
  document.getElementById('sifreModal').classList.remove('hidden');
}

// ---------- YÖNETİCİ AYARLARI ----------
function yoneticiAyarlariModalAc() {
  if (aktifKullaniciRol !== 'yonetici') return;
  document.getElementById('modalYeniSifreInput').value = '';
  document.getElementById('ayarSmsKurali').value = sistemAyarlari.smsKurali || "aylik_1";
  document.getElementById('ayarYedekSikligi').value = sistemAyarlari.yedekSikligi || "her_islem";
  document.getElementById('ayarGenelDuyuru').value = sistemAyarlari.genelDuyuru || "Lütfen yazıları dikkate alın!";

  let container = document.getElementById('daireYetkiListesiContainer');
  container.innerHTML = '';
  daireler.forEach(d => {
    if (!d.izinler) d.izinler = { ...VARSAYILAN_IZINLER };
    if (!d.sifre) d.sifre = "12345";
    container.innerHTML += `
      <div class="bg-white p-3 rounded-xl border border-slate-200 flex flex-col md:flex-row justify-between items-start md:items-center gap-2 shadow-sm">
        <div class="flex items-center gap-2">
          <span class="font-extrabold text-xs text-slate-800">${d.no} (${d.sahip})</span>
          <input type="text" id="sifre_d_${d.id}" value="${d.sifre}" class="w-24 border border-slate-300 rounded px-2 py-1 text-xs font-mono text-center font-bold bg-slate-50" placeholder="Şifre" title="Daire Şifresi">
        </div>
        <div class="flex items-center gap-2 flex-wrap text-[10px] font-bold text-slate-600">
          <label><input type="checkbox" id="iz_aid_${d.id}" ${d.izinler.aidat ? 'checked' : ''}> Aidat</label>
          <label><input type="checkbox" id="iz_duy_${d.id}" ${d.izinler.duyurular ? 'checked' : ''}> Duyuru</label>
          <label><input type="checkbox" id="iz_arz_${d.id}" ${d.izinler.arizalar ? 'checked' : ''}> Arıza</label>
          <label><input type="checkbox" id="iz_top_${d.id}" ${d.izinler.toplanti ? 'checked' : ''}> Toplantı</label>
          <label><input type="checkbox" id="iz_reh_${d.id}" ${d.izinler.rehber ? 'checked' : ''}> Rehber</label>
        </div>
      </div>`;
  });

  document.getElementById('yoneticiAyarlariModal').classList.remove('hidden');
}

function gelismisAyarlariKaydet() {
  daireler.forEach(d => {
    if (!d.izinler) d.izinler = { ...VARSAYILAN_IZINLER };
    let sifreInput = document.getElementById(`sifre_d_${d.id}`);
    if (sifreInput) d.sifre = sifreInput.value.trim() || "12345";

    const cb = (id) => document.getElementById(id);
    if (cb(`iz_aid_${d.id}`)) d.izinler.aidat = cb(`iz_aid_${d.id}`).checked;
    if (cb(`iz_duy_${d.id}`)) d.izinler.duyurular = cb(`iz_duy_${d.id}`).checked;
    if (cb(`iz_arz_${d.id}`)) d.izinler.arizalar = cb(`iz_arz_${d.id}`).checked;
    if (cb(`iz_top_${d.id}`)) d.izinler.toplanti = cb(`iz_top_${d.id}`).checked;
    if (cb(`iz_reh_${d.id}`)) d.izinler.rehber = cb(`iz_reh_${d.id}`).checked;
  });

  sistemAyarlari.smsKurali = document.getElementById('ayarSmsKurali').value;
  sistemAyarlari.yedekSikligi = document.getElementById('ayarYedekSikligi').value;
  sistemAyarlari.genelDuyuru = document.getElementById('ayarGenelDuyuru').value.trim();

  let now = new Date();
  sistemAyarlari.duyuruTarihi = `${String(now.getDate()).padStart(2,'0')}.${String(now.getMonth()+1).padStart(2,'0')}.${now.getFullYear()} ${String(now.getHours()).padStart(2,'0')}:${String(now.getMinutes()).padStart(2,'0')}`;

  verileriKaydet();
  alert("Ayarlar ve daire şifreleri başarıyla kaydedildi!");
  yoneticiAyarlariModalKapat();
}

function yoneticiAyarlariModalKapat() {
  document.getElementById('yoneticiAyarlariModal').classList.add('hidden');
}

function modalSifreGuncelle() {
  if (aktifKullaniciRol !== 'yonetici') return;
  const yeniSifre = document.getElementById('modalYeniSifreInput').value.trim();
  if (!yeniSifre || yeniSifre.length < 4) {
    alert("Lütfen en az 4 karakterli bir şifre girin.");
    return;
  }
  localStorage.setItem('site_yonetici_sifre', yeniSifre);
  if (localStorage.getItem('site_beni_hatirla_aktif') === 'true') {
    localStorage.setItem('site_hatirlanan_sifre', yeniSifre);
  }
  document.getElementById('modalYeniSifreInput').value = '';
  alert("Yönetici şifresi başarıyla güncellendi.");
}

// ---------- ROL ARAYÜZÜ ----------
function rolArayuzunuUyarla() {
  const kullaniciAdEl = document.getElementById('aktifKullaniciAd');
  const rolMetinEl = document.getElementById('rolGostergeMetin');
  const btnDaireEkle = document.getElementById('btnDaireEkle');
  const yoneticiIslem = document.getElementById('yoneticiIslemBolumu');
  const yoneticiTopluSil = document.getElementById('yoneticiTopluSilBolumu');
  const btnYedekAl = document.getElementById('btnYedekAl');
  const lblYedekYukle = document.getElementById('lblYedekYukle');
  const btnToplantiEkle = document.getElementById('btnToplantiEkle');
  const arizaTalepFormu = document.getElementById('arizaTalepFormu');
  const btnArsivEkle = document.getElementById('btnArsivEkle');
  const btnPdfRapor = document.getElementById('btnPdfRapor');
  const btnAyarlar = document.getElementById('yoneticiAyarlariButonAlani')?.querySelector('button');
  const kartVarlik = document.getElementById('kartVarlik');
  const kartGelir = document.getElementById('kartGelir');
  const kartGider = document.getElementById('kartGider');
  const kartBorc = document.getElementById('kartBorc');

  if (aktifKullaniciRol === 'kat_maliki') {
    let secilenDaire = daireler.find(x => x.id === aktifKatMalikiDaireId);
    if (kullaniciAdEl) kullaniciAdEl.innerText = secilenDaire ? `${secilenDaire.no} (${secilenDaire.sahip})` : "Kat Maliki";
    if (rolMetinEl) rolMetinEl.innerText = "Daire Özel Şifreli Sakin Portalı";
    [btnDaireEkle, yoneticiIslem, yoneticiTopluSil, btnYedekAl, lblYedekYukle, btnToplantiEkle, btnArsivEkle, btnPdfRapor, btnAyarlar].forEach(el => { if (el) el.classList.add('hidden'); });
    
    // ARITMA/ARIZA TALEP FORMUNU KAT MALİKLERİ İÇİN AÇIK BIRAKIYORUZ (İSTEĞİNİZ ÜZERE)
    if (arizaTalepFormu) arizaTalepFormu.classList.remove('hidden');

    [kartVarlik, kartGelir, kartGider, kartBorc].forEach(k => {
      if (!k) return;
      k.onclick = null;
      k.style.cursor = 'default';
    });

    uygulamaSekmeIzinleriniKontrolEt();
  } else {
    if (kullaniciAdEl) kullaniciAdEl.innerText = "Kasım Taha Yamak (Yönetici)";
    if (rolMetinEl) rolMetinEl.innerText = "Holding Seviyesi Kurumsal Finans ve Varlık Altyapısı";
    [btnDaireEkle, yoneticiIslem, yoneticiTopluSil, btnYedekAl, lblYedekYukle, btnToplantiEkle, arizaTalepFormu, btnArsivEkle, btnPdfRapor, btnAyarlar].forEach(el => { if (el) el.classList.remove('hidden'); });

    if (kartVarlik) kartVarlik.onclick = () => detayModalAc('varlik');
    if (kartGelir) kartGelir.onclick = () => detayModalAc('gelir');
    if (kartGider) kartGider.onclick = () => detayModalAc('gider');
    if (kartBorc) kartBorc.onclick = () => detayModalAc('borc');
    [kartVarlik, kartGelir, kartGider, kartBorc].forEach(k => { if (k) k.style.cursor = 'pointer'; });

    ['aidat', 'kasa', 'kontrol', 'banka', 'toplanti', 'arsiv', 'duyurular', 'arizalar', 'rehber'].forEach(t => {
      let btn = document.getElementById(`btnTab${t.charAt(0).toUpperCase() + t.slice(1)}`);
      if (btn) btn.style.display = 'flex';
    });
    tabDegis('aidat');
  }
  guncelleEkran();
}

function uygulamaSekmeIzinleriniKontrolEt() {
  if (aktifKullaniciRol !== 'kat_maliki') return;
  let d = daireler.find(x => x.id === aktifKatMalikiDaireId);
  if (!d || !d.izinler) return;

  let izinMap = {
    aidat: d.izinler.aidat,
    kasa: false,
    kontrol: false,
    banka: false,
    toplanti: d.izinler.toplanti,
    arsiv: false,
    duyurular: d.izinler.duyurular,
    arizalar: true, // KAT MALİKLERİ ARIZA SEKMESİNİ KULLANABİLSİN
    rehber: d.izinler.rehber
  };

  let ilkAcilacakTab = 'aidat';
  let buldu = false;

  ['aidat', 'kasa', 'kontrol', 'banka', 'toplanti', 'arsiv', 'duyurular', 'arizalar', 'rehber'].forEach(t => {
    let btn = document.getElementById(`btnTab${t.charAt(0).toUpperCase() + t.slice(1)}`);
    if (btn) {
      if (izinMap[t]) {
        btn.style.display = 'flex';
        if (!buldu) { ilkAcilacakTab = t; buldu = true; }
      } else {
        btn.style.display = 'none';
      }
    }
  });

  tabDegis(ilkAcilacakTab);
}

// ---------- VERİ SAKLAMA ----------
function verileriYukle() {
  try {
    let kayitliDaire = JSON.parse(localStorage.getItem('site_daireler'));
    if (kayitliDaire && kayitliDaire.length > 0) daireler = kayitliDaire;

    let kayitliIslem = JSON.parse(localStorage.getItem('site_islemler'));
    if (kayitliIslem && kayitliIslem.length > 0) islemler = kayitliIslem;

    let kayitliArsiv = JSON.parse(localStorage.getItem('site_arsiv'));
    if (kayitliArsiv) arsivBelgeleri = kayitliArsiv;

    let kayitliToplanti = JSON.parse(localStorage.getItem('site_toplantilar'));
    if (kayitliToplanti) toplantilar = kayitliToplanti;

    let kayitliArizalar = JSON.parse(localStorage.getItem('site_arizalar'));
    if (kayitliArizalar) arizalar = kayitliArizalar;

    let kayitliAyarlar = JSON.parse(localStorage.getItem('site_sistem_ayarlari'));
    if (kayitliAyarlar) sistemAyarlari = kayitliAyarlar;
  } catch (e) {
    console.error("Yükleme hatası:", e);
  }
}

function verileriKaydet() {
  try {
    localStorage.setItem('site_daireler', JSON.stringify(daireler));
    localStorage.setItem('site_islemler', JSON.stringify(islemler));
    localStorage.setItem('site_arsiv', JSON.stringify(arsivBelgeleri));
    localStorage.setItem('site_toplantilar', JSON.stringify(toplantilar));
    localStorage.setItem('site_arizalar', JSON.stringify(arizalar));
    localStorage.setItem('site_sistem_ayarlari', JSON.stringify(sistemAyarlari));
  } catch (e) {
    console.error("Kayıt hatası:", e);
  }
  guncelleEkran();
}

// GÜNCELLENEN YEDEKLEME FONKSİYONU (BLOB KULLANARAK BÜYÜK DOSYA/DEKONT HATASINI ÖNLER)
function verileriDisariAktar() {
  try {
    const veriPaketi = {
      daireler: daireler,
      islemler: islemler,
      arsivBelgeleri: arsivBelgeleri,
      toplantilar: toplantilar,
      arizalar: arizalar,
      sistemAyarlari: sistemAyarlari,
      yoneticiSifre: getYoneticSifre(),
      tarih: new Date().toISOString()
    };
    const blob = new Blob([JSON.stringify(veriPaketi, null, 2)], { type: 'application/json;charset=utf-8' });
    const url = URL.createObjectURL(blob);
    const downloadAnchor = document.createElement('a');
    downloadAnchor.href = url;
    downloadAnchor.download = 'site_yonetim_yedek.json';
    document.body.appendChild(downloadAnchor);
    downloadAnchor.click();
    document.body.removeChild(downloadAnchor);
    URL.revokeObjectURL(url);
  } catch (err) {
    console.error("Yedek alma hatası:", err);
    alert("Yedek oluşturulurken bir hata oluştu.");
  }
}

// GÜNCELLENEN YÜKLEME FONKSİYONU
function verileriIceAktar(event) {
  const file = event.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = function (e) {
    try {
      const icerik = JSON.parse(e.target.result);
      if (icerik && (icerik.daireler || icerik.islemler)) {
        if (icerik.daireler) daireler = icerik.daireler;
        if (icerik.islemler) islemler = icerik.islemler;
        if (icerik.arsivBelgeleri) arsivBelgeleri = icerik.arsivBelgeleri;
        if (icerik.toplantilar) toplantilar = icerik.toplantilar;
        if (icerik.arizalar) arizalar = icerik.arizalar;
        if (icerik.sistemAyarlari) sistemAyarlari = icerik.sistemAyarlari;
        if (icerik.yoneticiSifre) localStorage.setItem('site_yonetici_sifre', icerik.yoneticiSifre);
        
        verileriKaydet();
        alert("Veriler başarıyla yüklendi!");
        location.reload();
      } else {
        alert("Geçersiz yedek dosyası!");
      }
    } catch (err) {
      console.error(err);
      alert("Dosya okunurken hata oluştu.");
    }
  };
  reader.readAsText(file);
  event.target.value = '';
}

// ---------- TARİH SEÇİCİLERİ ----------
function aySeciciDoldur() {
  const donemGunSecici = document.getElementById('donemGunSecici');
  const donemAySecici = document.getElementById('donemAySecici');
  const donemYilSecici = document.getElementById('donemYilSecici');
  const matrisYilSecici = document.getElementById('matrisYilSecici');
  if (!donemGunSecici || !donemAySecici || !donemYilSecici || !matrisYilSecici) return;

  donemGunSecici.innerHTML = '';
  donemYilSecici.innerHTML = '';
  matrisYilSecici.innerHTML = '';

  const simdi = new Date();
  const mevcutYil = simdi.getFullYear();
  const mevcutAy = simdi.getMonth() + 1;
  const mevcutGun = simdi.getDate();

  for (let g = 1; g <= 31; g++) {
    let opt = document.createElement('option');
    opt.value = String(g).padStart(2, '0');
    opt.text = g;
    if (g === mevcutGun) opt.selected = true;
    donemGunSecici.appendChild(opt);
  }

  donemAySecici.value = String(mevcutAy).padStart(2, '0');

  for (let yil = 2026; yil <= 2050; yil++) {
    let optYil = document.createElement('option');
    optYil.value = yil;
    optYil.text = yil;
    if (yil === mevcutYil) optYil.selected = true;
    matrisYilSecici.appendChild(optYil);

    let optDonemYil = document.createElement('option');
    optDonemYil.value = yil;
    optDonemYil.text = yil;
    if (yil === mevcutYil) optDonemYil.selected = true;
    donemYilSecici.appendChild(optDonemYil);
  }

  islemTarihSecicileriDoldur();
}

function islemTarihSecicileriDoldur() {
  const gunSecici = document.getElementById('islemGun');
  const aySecici = document.getElementById('islemAy');
  const yilSecici = document.getElementById('islemYil');
  if (!gunSecici || !aySecici || !yilSecici) return;

  gunSecici.innerHTML = '';
  yilSecici.innerHTML = '';

  const simdi = new Date();
  const mevcutGun = simdi.getDate();
  const mevcutAy = simdi.getMonth() + 1;
  const mevcutYil = simdi.getFullYear();

  for (let g = 1; g <= 31; g++) {
    let opt = document.createElement('option');
    opt.value = g;
    opt.text = g;
    if (g === mevcutGun) opt.selected = true;
    gunSecici.appendChild(opt);
  }

  aySecici.value = mevcutAy;
  for (let y = 2026; y <= 2050; y++) {
    let opt = document.createElement('option');
    opt.value = y;
    opt.text = y;
    if (y === mevcutYil) opt.selected = true;
    yilSecici.appendChild(opt);
  }
}

// ---------- SEKME YÖNETİMİ ----------
function tabDegis(tab) {
  if (aktifKullaniciRol === 'kat_maliki') {
    let d = daireler.find(x => x.id === aktifKatMalikiDaireId);
    if (d && d.izinler && d.izinler[tab] === false && tab !== 'arizalar') return;
  }

  ['aidat', 'kasa', 'kontrol', 'banka', 'toplanti', 'arsiv', 'duyurular', 'arizalar', 'rehber'].forEach(t => {
    const bolumEl = document.getElementById(`bolum${t.charAt(0).toUpperCase() + t.slice(1)}`);
    const btnEl = document.getElementById(`btnTab${t.charAt(0).toUpperCase() + t.slice(1)}`);
    if (bolumEl) {
      bolumEl.classList.add('hidden');
      bolumEl.style.transform = 'rotateY(-20deg) scale(0.97)';
      bolumEl.style.opacity = '0';
    }
    if (btnEl) {
      if (aktifKullaniciRol === 'yonetici' || (aktifKullaniciRol === 'kat_maliki' && (daireler.find(x => x.id === aktifKatMalikiDaireId)?.izinler?.[t] || t === 'arizalar'))) {
        btnEl.className = "flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl text-slate-600 hover:text-slate-900 hover:bg-slate-50 transition flex items-center justify-center gap-2";
      }
    }
  });

  const aktifBolum = document.getElementById(`bolum${tab.charAt(0).toUpperCase() + tab.slice(1)}`);
  const aktifBtn = document.getElementById(`btnTab${tab.charAt(0).toUpperCase() + tab.slice(1)}`);

  if (aktifBolum) {
    aktifBolum.classList.remove('hidden');
    aktifBolum.style.transform = 'rotateY(20deg) scale(0.97)';
    aktifBolum.style.opacity = '0';
    setTimeout(() => {
      aktifBolum.style.transform = 'rotateY(0deg) scale(1)';
      aktifBolum.style.opacity = '1';
    }, 40);
  }
  if (aktifBtn) aktifBtn.className = "flex-1 py-3 px-3 text-xs md:text-sm font-bold rounded-2xl bg-gradient-to-r from-blue-900 to-indigo-900 text-white transition btn-3d flex items-center justify-center gap-2";

  if (tab === 'banka') bankaKartlariniGuncelle();
  if (tab === 'arsiv') arsivListesiniGuncelle();
  if (tab === 'toplanti') toplantiListesiniGuncelle();
  if (tab === 'duyurular') duyurularListesiniGuncelle();
  if (tab === 'arizalar') arizaListesiniGuncelle();
  if (tab === 'kontrol') grafikleriniGuncelle();
  if (tab === 'rehber') binaRehberiniGuncelle();
}

// ---------- FİNANSAL İŞLEMLER ----------
function kategoriDoldur() {
  const tip = document.getElementById('islemTip').value;
  const katSecici = document.getElementById('islemKategori');
  if (!katSecici) return;
  katSecici.innerHTML = '';
  KATEGORILER[tip].forEach(kat => {
    katSecici.innerHTML += `<option value="${kat}">${kat}</option>`;
  });
}

function islemEkle(event) {
  event.preventDefault();
  if (aktifKullaniciRol !== 'yonetici') return;

  let tip = document.getElementById('islemTip').value;
  let kategori = document.getElementById('islemKategori').value;
  let kaynak = document.getElementById('islemKaynak').value;
  let tutar = Number(document.getElementById('islemTutar').value);
  let aciklama = document.getElementById('islemAciklama').value.trim();
  let gun = Number(document.getElementById('islemGun').value);
  let ay = Number(document.getElementById('islemAy').value);
  let yil = Number(document.getElementById('islemYil').value);

  if (!aciklama || isNaN(tutar) || tutar <= 0) {
    alert("Lütfen geçerli bir açıklama ve tutar giriniz.");
    return;
  }

  let tarihStr = `${yil}-${String(ay).padStart(2, '0')}-${String(gun).padStart(2, '0')}`;
  let ayKodStr = `${yil}-${String(ay).padStart(2, '0')}`;

  let eslesenDaire = null;
  if (tip === 'gelir' && kategori === 'Aidat Ödemesi') {
    let altAciklama = aciklama.toLocaleLowerCase('tr');
    eslesenDaire = daireler.find(d => {
      let dNoTemiz = d.no.toLocaleLowerCase('tr').replace(/[^0-9]/g, '');
      return altAciklama.includes(dNoTemiz + ' nolu') || altAciklama.includes(d.no.toLocaleLowerCase('tr'));
    });
  }

  let dosyaInput = document.getElementById('islemBelgeDosya');

  const kayitIsleminiBitir = (belgeDataVerisi) => {
    let yeniIslemObj = {
      id: Date.now(),
      tip: tip,
      kategori: kategori,
      kaynak: kaynak,
      aciklama: aciklama,
      tutar: tutar,
      gun: gun,
      ay: ay,
      yil: yil,
      tarih: tarihStr,
      belgeData: belgeDataVerisi
    };

    if (eslesenDaire) {
      yeniIslemObj.daireId = eslesenDaire.id;
      yeniIslemObj.islemAy = ayKodStr;
      if (!eslesenDaire.odemeGecmisi) eslesenDaire.odemeGecmisi = {};
      eslesenDaire.odemeGecmisi[ayKodStr] = true;
    }

    islemler.unshift(yeniIslemObj);
    islemFormSifirla();
    verileriKaydet();

    if (eslesenDaire) {
      alert(`İşlem başarıyla kaydedildi ve ${eslesenDaire.no} (${eslesenDaire.sahip}) için aidat tablosuna ödendi olarak işlendi!`);
    } else {
      alert("İşlem başarıyla kaydedildi.");
    }
  };

  if (dosyaInput.files && dosyaInput.files[0]) {
    let reader = new FileReader();
    reader.onload = function (e) {
      kayitIsleminiBitir(e.target.result);
    };
    reader.readAsDataURL(dosyaInput.files[0]);
  } else {
    kayitIsleminiBitir(null);
  }
}

function islemFormSifirla() {
  document.getElementById('islemTutar').value = '';
  document.getElementById('islemAciklama').value = '';
  document.getElementById('islemBelgeDosya').value = '';
  islemListesiniGuncelle();
}

function islemSil(id) {
  if (aktifKullaniciRol !== 'yonetici') return;
  if (confirm("Bu finansal işlemi silmek istediğinize emin misiniz?")) {
    let silinenIslem = islemler.find(x => x.id === id);
    
    // Eğer silinen işlem bir aidat ödemesi ise dairenin geçmişinden de kaldır
    if (silinenIslem && silinenIslem.daireId && silinenIslem.islemAy) {
      let daire = daireler.find(d => d.id === silinenIslem.daireId);
      if (daire && daire.odemeGecmisi) {
        delete daire.odemeGecmisi[silinenIslem.islemAy];
      }
    }

    islemler = islemler.filter(x => x.id !== id);
    verileriKaydet();
    islemListesiniGuncelle();

  
  }
}

function tumunuSil() {
  if (aktifKullaniciRol !== 'yonetici') return;
  if (confirm("TÜM finansal işlemleri silmek istediğinize emin misiniz? Bu işlem geri alınamaz!")) {
    islemler = [];
    // Tüm dairelerin ödeme geçmişini temizle
    daireler.forEach(d => {
      d.odemeGecmisi = {};
    });
    verileriKaydet();
    islemListesiniGuncelle();
  }
}

function secilenleriSil() {
  if (aktifKullaniciRol !== 'yonetici') return;
  let checkboxes = document.querySelectorAll('.islem-secim-cb:checked');
  if (checkboxes.length === 0) {
    alert("Lütfen silmek için en az bir işlem seçin.");
    return;
  }
  if (confirm(`Seçilen ${checkboxes.length} işlemi silmek istediğinize emin misiniz?`)) {
    let silinecekIds = Array.from(checkboxes).map(cb => Number(cb.value));
    
    // Seçilenler arasındaki aidat ödemelerini ilgili dairelerden düş
    silinecekIds.forEach(id => {
      let silinenIslem = islemler.find(x => x.id === id);
      if (silinenIslem && silinenIslem.daireId && silinenIslem.islemAy) {
        let daire = daireler.find(d => d.id === silinenIslem.daireId);
        if (daire && daire.odemeGecmisi) {
          delete daire.odemeGecmisi[silinenIslem.islemAy];
        }
      }
    });

    islemler = islemler.filter(x => !silinecekIds.includes(x.id));
    verileriKaydet();
    islemListesiniGuncelle();
  
  }
}

function tumunuSecToggle(master) {
  let cbs = document.querySelectorAll('.islem-secim-cb');
  cbs.forEach(cb => cb.checked = master.checked);
}

function islemListesiniGuncelle() {
  const tbody = document.getElementById('islemListesiBody');
  if (!tbody) return;
  tbody.innerHTML = '';

  const secimBaslik = document.getElementById('thSecimKolon');
  const silBaslik = document.getElementById('thSilKolon');
  if (secimBaslik) secimBaslik.style.display = aktifKullaniciRol === 'yonetici' ? '' : 'none';
  if (silBaslik) silBaslik.style.display = aktifKullaniciRol === 'yonetici' ? '' : 'none';

  if (!islemler || islemler.length === 0) {
    tbody.innerHTML = `<tr><td colspan="8" class="p-6 text-center text-slate-400">Kayıtlı finansal işlem bulunmuyor.</td></tr>`;
    return;
  }

  islemler.forEach(i => {
    let tarihStr = '';
    if (i.gun && i.ay && i.yil) {
      let ayIsmi = AYLAR_ISIM[i.ay - 1] || i.ay;
      tarihStr = `${i.gun} ${ayIsmi} ${i.yil}`;
    } else {
      tarihStr = i.tarih || '';
    }

    let tutarStr = `${i.tip === 'gelir' ? '+' : '-'}${Number(i.tutar || 0).toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`;

    let belgeCell = i.belgeData
      ? `<button onclick="belgeGoster(${i.id}, 'islem')" class="bg-blue-50 text-blue-700 hover:bg-blue-100 px-2.5 py-1 rounded-xl text-xs font-bold border border-blue-200"><i class="fa-solid fa-file-image"></i> İncele</button>`
      : `<span class="text-xs text-slate-400">Yok</span>`;

    let secimCell = aktifKullaniciRol === 'yonetici'
      ? `<td class="p-4 text-center"><input type="checkbox" class="islem-secim-cb w-4 h-4 text-blue-900 rounded focus:ring-blue-600 border-slate-300 cursor-pointer" value="${i.id}"></td>`
      : '';

    let silCell = aktifKullaniciRol === 'yonetici'
      ? `<td class="p-4 text-center"><button onclick="islemSil(${i.id})" class="text-rose-500 hover:text-rose-700 p-2 bg-rose-50 rounded-xl trash-btn-3d"><i class="fa-solid fa-trash-can"></i></button></td>`
      : '';

    tbody.innerHTML += `<tr class="hover:bg-slate-50">
      ${secimCell}
      <td class="p-4 font-bold text-xs text-slate-600 nowrap-date">${tarihStr}</td>
      <td class="p-4 font-extrabold text-slate-800">${i.kaynak}</td>
      <td class="p-4 text-slate-600">${i.kategori}</td>
      <td class="p-4 font-semibold text-slate-800">${i.aciklama}</td>
      <td class="p-4 text-center font-black ${i.tip === 'gelir' ? 'text-emerald-600' : 'text-rose-600'}">${tutarStr}</td>
      <td class="p-4 text-center">${belgeCell}</td>
      ${silCell}
    </tr>`;
  });
}

// ---------- ARIZA TAKİP (KAT MALİKLERİ VE KİŞİLER TARAFINDAN KULLANILABİLİR) ----------
function arizaTalebiEkle() {
  let daireBilgi = document.getElementById('arizaDaireBilgi').value.trim();
  let kategori = document.getElementById('arizaKategori').value;
  let aciklama = document.getElementById('arizaAciklama').value.trim();

  if (!daireBilgi || !aciklama) {
    alert("Lütfen daire bilgisi ve arıza açıklaması giriniz.");
    return;
  }

  arizalar.unshift({
    id: Date.now(),
    daire: daireBilgi,
    kategori: kategori,
    aciklama: aciklama,
    tarih: new Date().toISOString().split('T')[0],
    durum: "Beklemede"
  });

  document.getElementById('arizaAciklama').value = '';
  verileriKaydet();
  arizaListesiniGuncelle();
  alert("Arıza talebiniz başarıyla kaydedildi.");
}

function arizaDurumDegistir(id, yeniDurum) {
  if (aktifKullaniciRol !== 'yonetici') return;
  let arz = arizalar.find(x => x.id === id);
  if (arz) {
    arz.durum = yeniDurum;
    verileriKaydet();
    arizaListesiniGuncelle();
  }
}

function arizaSil(id) {
  if (aktifKullaniciRol !== 'yonetici') return;
  if (confirm("Bu arıza kaydını silmek istediğinize emin misiniz?")) {
    arizalar = arizalar.filter(x => x.id !== id);
    verileriKaydet();
    arizaListesiniGuncelle();
  }
}

function arizaListesiniGuncelle() {
  const tbody = document.getElementById('arizaListesiBody');
  if (!tbody) return;
  tbody.innerHTML = '';

  if (!arizalar || arizalar.length === 0) {
    tbody.innerHTML = `<tr><td colspan="6" class="p-6 text-center text-slate-400">Kayıtlı arıza talebi bulunmuyor.</td></tr>`;
    return;
  }

  arizalar.forEach(a => {
    let tarihStr = a.tarih ? a.tarih.split('-').reverse().join('.') : '';
    let durumBadge = '';
    if (a.durum === 'Beklemede') durumBadge = `<span class="bg-amber-100 text-amber-700 px-3 py-1 rounded-full text-xs font-bold">Beklemede</span>`;
    else if (a.durum === 'İşlemde') durumBadge = `<span class="bg-blue-100 text-blue-700 px-3 py-1 rounded-full text-xs font-bold">İşlemde</span>`;
    else durumBadge = `<span class="bg-emerald-100 text-emerald-700 px-3 py-1 rounded-full text-xs font-bold">Çözüldü</span>`;

    let islemCell = '';
    if (aktifKullaniciRol === 'yonetici') {
      islemCell = `<div class="flex items-center justify-center gap-1.5">
        <select onchange="arizaDurumDegistir(${a.id}, this.value)" class="border border-slate-200 rounded-lg p-1.5 text-xs font-bold bg-white">
          <option value="Beklemede" ${a.durum === 'Beklemede' ? 'selected' : ''}>Beklemede</option>
          <option value="İşlemde" ${a.durum === 'İşlemde' ? 'selected' : ''}>İşlemde</option>
          <option value="Çözüldü" ${a.durum === 'Çözüldü' ? 'selected' : ''}>Çözüldü</option>
        </select>
        <button onclick="arizaSil(${a.id})" class="text-rose-500 hover:text-rose-700 p-1.5 bg-rose-50 rounded-lg"><i class="fa-solid fa-trash-can"></i></button>
      </div>`;
    } else {
      islemCell = `<span class="text-xs text-slate-500 font-medium">Durum: ${a.durum}</span>`;
    }

    tbody.innerHTML += `<tr class="hover:bg-slate-50">
      <td class="p-4 font-bold text-xs text-slate-600 nowrap-date">${tarihStr}</td>
      <td class="p-4 font-extrabold text-slate-800">${a.daire}</td>
      <td class="p-4 font-semibold text-slate-700">${a.kategori}</td>
      <td class="p-4 text-slate-600">${a.aciklama}</td>
      <td class="p-4 text-center">${durumBadge}</td>
      <td class="p-4 text-center">${islemCell}</td>
    </tr>`;
  });
}

// ---------- DUYURULAR ----------
function duyurularListesiniGuncelle() {
  const container = document.getElementById('duyurularListesiniContainer');
  if (!container) return;

  let duyuruMetni = sistemAyarlari.genelDuyuru || "Lütfen yazıları dikkate alın!";
  let tarihDamgasi = sistemAyarlari.duyuruTarihi || "01.11.2026 03:58";

  container.innerHTML = `<div class="bg-amber-50 border border-amber-200 rounded-3xl p-6 shadow-sm flex items-start gap-4">
    <div class="w-12 h-12 rounded-2xl bg-gradient-to-br from-amber-500 to-yellow-600 text-white flex items-center justify-center font-bold text-lg icon-3d icon-3d-amber shrink-0">
      <i class="fa-solid fa-bullhorn"></i>
    </div>
    <div class="w-full">
      <div class="flex justify-between items-center mb-1">
        <h4 class="font-black text-slate-900 text-base">Bina Yönetim Duyurusu</h4>
        <span class="text-xs font-bold text-amber-800 bg-amber-100/80 px-3 py-1 rounded-xl"><i class="fa-regular fa-clock mr-1"></i> Yayın Tarihi: ${tarihDamgasi}</span>
      </div>
      <p class="text-sm text-slate-700 whitespace-pre-line font-medium leading-relaxed mt-2">${duyuruMetni}</p>
    </div>
  </div>`;
}

// ---------- ANA EKRAN GÜNCELLEME ----------
function guncelleEkran() {
  const donemGunEl = document.getElementById('donemGunSecici');
  const donemAyEl = document.getElementById('donemAySecici');
  const donemYilEl = document.getElementById('donemYilSecici');
  if (!donemGunEl || !donemAyEl || !donemYilEl) return;

  let gunVal = donemGunEl.value;
  let ayVal = donemAyEl.value;
  let yilVal = donemYilEl.value;

  const seciliAyKod = `${yilVal}-${ayVal}`;
  const ayIsmiStr = AYLAR_ISIM[parseInt(ayVal, 10) - 1] || ayVal;
  document.getElementById('seciliDonemBaslik').innerText = `${parseInt(gunVal, 10)} ${ayIsmiStr} ${yilVal}`;

  let tbodyDaire = document.getElementById('daireListesiBody');
  tbodyDaire.innerHTML = '';
  let toplamBorc = 0;

  if (!daireler || daireler.length === 0) {
    tbodyDaire.innerHTML = `<tr><td colspan="4" class="p-8 text-center text-slate-400 font-medium">Henüz daire eklenmedi.</td></tr>`;
  } else {
    daireler.forEach((d, index) => {
      if (!d.odemeGecmisi) d.odemeGecmisi = {};

      let odendiMi = d.odemeGecmisi[seciliAyKod] === true;
      let muafMi = d.yoneticiMuaf === true;
      if (!muafMi && !odendiMi) toplamBorc += Number(d.tutar || 0);

      let durumHtml = '';
      let aksiyonHtml = '';

      if (muafMi) {
        durumHtml = `<span class="px-4 py-1.5 rounded-full text-xs font-bold bg-amber-50 text-amber-700 border border-amber-200 shadow-sm"><i class="fa-solid fa-shield-halved mr-1.5"></i> Muaf / Ödemez</span>`;
        aksiyonHtml = `<span class="text-xs text-amber-600 font-bold bg-amber-50 px-3 py-1.5 rounded-xl border border-amber-200">Aidat Muaf</span>`;
      } else {
        durumHtml = `<span class="px-4 py-1.5 rounded-full text-xs font-bold transition shadow-sm border ${odendiMi ? 'bg-emerald-50 text-emerald-700 border-emerald-200 shadow-emerald-100' : 'bg-rose-50 text-rose-700 border-rose-200 shadow-rose-100'}">
          <i class="fa-solid ${odendiMi ? 'fa-circle-check' : 'fa-circle-xmark'} mr-1.5"></i>${odendiMi ? 'Ödendi' : 'Ödenmedi'}
        </span>`;

        if (aktifKullaniciRol === 'yonetici') {
          let smsBtn = d.telefon ? `<button onclick="smsHatirlaticiGonder(${d.id}, '${seciliAyKod}')" title="SMS Hatırlat Gönder" class="bg-blue-50 text-blue-700 hover:bg-blue-100 p-2 rounded-xl border border-blue-200 transition shadow-sm"><i class="fa-solid fa-sms"></i></button>` : '';
          aksiyonHtml = `<div class="flex items-center justify-center gap-1.5">
            ${smsBtn}
            <button onclick="aidatDurumDegistir(${d.id}, '${seciliAyKod}', ${gunVal}, ${ayVal}, ${yilVal})" class="px-3 py-1.5 rounded-xl text-xs font-bold transition border shadow-sm ${odendiMi ? 'bg-amber-50 text-amber-700 border-amber-200 hover:bg-amber-100' : 'bg-emerald-50 text-emerald-700 border-emerald-200 hover:bg-emerald-100'}">
              ${odendiMi ? 'Ödenmedi Yap' : 'Ödendi Yap'}
            </button>
          </div>`;
        } else {
          aksiyonHtml = `<span class="text-xs text-slate-400 font-medium">Görüntüleme Modu</span>`;
        }
      }

      let tutarGosterim = muafMi
        ? `<span class="text-amber-600 font-extrabold">Muaf (0,00 TL)</span>`
        : `${Number(d.tutar || 0).toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`;

      let yukariBtn = (aktifKullaniciRol === 'yonetici' && index > 0)
        ? `<button onclick="daireTasi(${index}, -1)" title="Yukarı Taşı" class="text-slate-400 hover:text-blue-700 p-1.5"><i class="fa-solid fa-arrow-up"></i></button>` : '';
      let asagiBtn = (aktifKullaniciRol === 'yonetici' && index < daireler.length - 1)
        ? `<button onclick="daireTasi(${index}, 1)" title="Aşağı Taşı" class="text-slate-400 hover:text-blue-700 p-1.5"><i class="fa-solid fa-arrow-down"></i></button>` : '';
      let duzenleBtn = (aktifKullaniciRol === 'yonetici')
        ? `<button onclick="daireDuzenleModalAc(${d.id})" title="Düzenle" class="text-blue-600 hover:text-blue-800 p-2 bg-blue-50 rounded-xl shadow-sm"><i class="fa-solid fa-pen-to-square"></i></button>` : '';
      let silBtn = (aktifKullaniciRol === 'yonetici')
        ? `<button onclick="daireSil(${d.id})" title="Sil" class="text-rose-500 hover:text-rose-700 transition p-2 bg-rose-50 rounded-xl trash-btn-3d"><i class="fa-solid fa-trash-can"></i></button>` : '';

      let yonetimIslemHucre = aktifKullaniciRol === 'yonetici'
        ? `<td class="p-4 text-center"><div class="flex items-center justify-center gap-2">${aksiyonHtml}${duzenleBtn}${silBtn}</div></td>`
        : `<td class="p-4 text-center">${aksiyonHtml}</td>`;

      let thIslem = document.getElementById('thIslemBaslik');
      if (thIslem) thIslem.innerText = aktifKullaniciRol === 'yonetici' ? 'İşlem / SMS / Düzenle' : 'Durum Bilgisi';

      tbodyDaire.innerHTML += `<tr class="hover:bg-slate-50/80 transition">
        <td class="p-4">
          <div class="flex items-center gap-2">
            <div class="flex flex-col">${yukariBtn}${asagiBtn}</div>
            <div>
              <div class="font-extrabold text-slate-800">${d.no}</div>
              <div class="text-xs text-slate-600 font-medium">${d.sahip}</div>
              <div class="text-xs text-slate-600 font-medium">${d.telefon || ''}</div>
            </div>
          </div>
        </td>
        <td class="p-4 font-extrabold text-center text-sm text-slate-700">${tutarGosterim}</td>
        <td class="p-4 text-center">${durumHtml}</td>
        ${yonetimIslemHucre}
      </tr>`;
    });
  }

  matrisOlustur();

  let toplamGelir = islemler.filter(i => i.tip === 'gelir').reduce((acc, curr) => acc + Number(curr.tutar || 0), 0);
  let toplamGider = islemler.filter(i => i.tip === 'gider').reduce((acc, curr) => acc + Number(curr.tutar || 0), 0);
  let netVarlik = toplamGelir - toplamGider;

  document.getElementById('lblKasa').innerText = netVarlik.toLocaleString('tr-TR', { style: 'currency', currency: 'TRY' });
  document.getElementById('lblGelir').innerText = toplamGelir.toLocaleString('tr-TR', { style: 'currency', currency: 'TRY' });
  document.getElementById('lblGider').innerText = toplamGider.toLocaleString('tr-TR', { style: 'currency', currency: 'TRY' });
  document.getElementById('lblBorc').innerText = toplamBorc.toLocaleString('tr-TR', { style: 'currency', currency: 'TRY' });

  bankaKartlariniGuncelle();
  toplantiListesiniGuncelle();
  duyurularListesiniGuncelle();
  arizaListesiniGuncelle();
  binaRehberiniGuncelle();
  islemListesiniGuncelle();
}

// ---------- AİDAT MATRİSİ ----------
function matrisOlustur() {
  let yilSelect = document.getElementById('matrisYilSecici');
  let yil = yilSelect ? yilSelect.value : "2026";
  let head = document.getElementById('matrisHead');
  let body = document.getElementById('matrisBody');

  if (!head || !body) return;

  let headHtml = '<th class="p-3 font-bold sticky left-0 bg-slate-50 z-10">Daire / Ay</th>';
  AYLAR_ISIM.forEach(ay => {
    headHtml += `<th class="p-3 font-bold text-center nowrap-date">${ay.substring(0, 3)} ${yil}</th>`;
  });
  head.innerHTML = headHtml;

  body.innerHTML = '';
  if (!daireler || daireler.length === 0) {
    body.innerHTML = `<tr><td colspan="13" class="p-4 text-center text-slate-400">Kayıtlı daire bulunmuyor.</td></tr>`;
    return;
  }

  daireler.forEach(d => {
    let row = `<tr class="hover:bg-slate-50"><td class="p-3 font-bold text-slate-800 sticky left-0 bg-white z-10 shadow-sm">${d.no}<br><span class="text-[10px] text-slate-500 font-normal">${d.sahip}</span></td>`;
    for (let i = 0; i < 12; i++) {
      let ayKod = `${yil}-${String(i + 1).padStart(2, '0')}`;
      let muaf = d.yoneticiMuaf === true;
      let odendi = d.odemeGecmisi && d.odemeGecmisi[ayKod] === true;

      let badgeClass = muaf ? 'bg-amber-100 text-amber-700' : (odendi ? 'bg-emerald-100 text-emerald-700' : 'bg-rose-100 text-rose-600');
      let badgeText = muaf ? 'M' : (odendi ? '✓' : '✗');
      let badgeTitle = muaf ? 'Muaf' : (odendi ? 'Ödendi' : 'Ödenmedi');

      row += `<td class="p-3 text-center"><span class="inline-block w-6 h-6 leading-6 rounded-full text-[10px] font-bold shadow-sm ${badgeClass}" title="${badgeTitle}">${badgeText}</span></td>`;
    }
    row += `</tr>`;
    body.innerHTML += row;
  });
}

// ---------- BİNA REHBERİ ----------
function binaRehberiniGuncelle() {
  const tbody = document.getElementById('rehberListesiBody');
  const aramaInput = document.getElementById('rehberAramaInput');
  if (!tbody) return;
  tbody.innerHTML = '';

  let aramaMetni = aramaInput ? aramaInput.value.toLocaleLowerCase('tr').trim() : "";
  let filtrelenenDaireler = daireler.filter(d =>
    d.no.toLocaleLowerCase('tr').includes(aramaMetni) ||
    d.sahip.toLocaleLowerCase('tr').includes(aramaMetni) ||
    (d.telefon && d.telefon.includes(aramaMetni))
  );

  if (!filtrelenenDaireler || filtrelenenDaireler.length === 0) {
    tbody.innerHTML = `<tr><td colspan="4" class="p-6 text-center text-slate-400">Aranan kriterlere uygun sakin bulunamadı.</td></tr>`;
    return;
  }

  filtrelenenDaireler.forEach(d => {
    let telClean = d.telefon ? d.telefon.replace(/[^0-9]/g, '') : '';
    if (telClean.startsWith('0')) {
      telClean = '90' + telClean.substring(1);
    } else if (!telClean.startsWith('90')) {
      telClean = '90' + telClean;
    }

    let aramaBtn = d.telefon ? `<a href="tel:${d.telefon}" class="bg-emerald-600 hover:bg-emerald-500 text-white px-3 py-1.5 rounded-xl text-xs font-bold inline-flex items-center gap-1 shadow-sm"><i class="fa-solid fa-phone"></i> Ara</a>` : '';
    let waBtn = d.telefon ? `<a href="https://wa.me/${telClean}" target="_blank" class="bg-green-600 hover:bg-green-500 text-white px-3 py-1.5 rounded-xl text-xs font-bold inline-flex items-center gap-1 shadow-sm"><i class="fa-brands fa-whatsapp"></i> WhatsApp</a>` : '';
    let smsBtn = d.telefon
      ? `<a href="sms:${d.telefon}" class="bg-blue-600 hover:bg-blue-500 text-white px-3 py-1.5 rounded-xl text-xs font-bold inline-flex items-center gap-1 shadow-sm"><i class="fa-solid fa-message"></i> SMS</a>`
      : '<span class="text-xs text-slate-400">Telefon Yok</span>';

    tbody.innerHTML += `<tr class="hover:bg-slate-50">
      <td class="p-4 font-extrabold text-slate-800">${d.no}</td>
      <td class="p-4 font-semibold text-slate-700">${d.sahip}</td>
      <td class="p-4 font-semibold text-slate-700">${d.telefon || 'Belirtilmemiş'}</td>
      <td class="p-4 text-center">
        <div class="flex items-center justify-center gap-2 flex-wrap">${aramaBtn}${waBtn}${smsBtn}</div>
      </td>
    </tr>`;
  });
}

// ---------- GRAFİKLER ----------
function grafikleriniGuncelle() {
  if (typeof Chart === 'undefined') return;

  let toplamGelir = islemler.filter(i => i.tip === 'gelir').reduce((acc, curr) => acc + Number(curr.tutar || 0), 0);
  let toplamGider = islemler.filter(i => i.tip === 'gider').reduce((acc, curr) => acc + Number(curr.tutar || 0), 0);

  let ctxGelirGider = document.getElementById('gelirGiderChart');
  if (ctxGelirGider) {
    if (gelirGiderChartInstance) gelirGiderChartInstance.destroy();
    gelirGiderChartInstance = new Chart(ctxGelirGider, {
      type: 'doughnut',
      data: {
        labels: ['Toplam Gelir', 'Toplam Gider'],
        datasets: [{ data: [toplamGelir, toplamGider], backgroundColor: ['#059669', '#e11d48'], borderWidth: 2 }]
      },
      options: { responsive: true, maintainAspectRatio: false }
    });
  }

  let ctxBanka = document.getElementById('bankaChart');
  if (ctxBanka) {
    let bankaAdlar = bankaHesaplari.map(b => b.ad);
    let bankaBakiye = bankaHesaplari.map(b => {
      let giren = islemler.filter(i => (i.kaynak || "").trim().toLocaleLowerCase('tr') === b.ad.trim().toLocaleLowerCase('tr') && i.tip === 'gelir').reduce((a, c) => a + Number(c.tutar || 0), 0);
      let cikan = islemler.filter(i => (i.kaynak || "").trim().toLocaleLowerCase('tr') === b.ad.trim().toLocaleLowerCase('tr') && i.tip === 'gider').reduce((a, c) => a + Number(c.tutar || 0), 0);
      return giren - cikan;
    });

    if (bankaChartInstance) bankaChartInstance.destroy();
    bankaChartInstance = new Chart(ctxBanka, {
      type: 'bar',
      data: {
        labels: bankaAdlar,
        datasets: [{ label: 'Bakiye (TL)', data: bankaBakiye, backgroundColor: '#1e3a8a', borderRadius: 8 }]
      },
      options: { responsive: true, maintainAspectRatio: false }
    });
  }

  let ctxKategori = document.getElementById('kategoriGiderChart');
  if (ctxKategori) {
    let giderIslemleri = islemler.filter(i => i.tip === 'gider');
    let kategoriMap = {};
    giderIslemleri.forEach(i => {
      let kat = i.kategori || 'Diğer';
      kategoriMap[kat] = (kategoriMap[kat] || 0) + Number(i.tutar || 0);
    });

    let katLabels = Object.keys(kategoriMap);
    let katData = Object.values(kategoriMap);

    if (kategoriGiderChartInstance) kategoriGiderChartInstance.destroy();
    kategoriGiderChartInstance = new Chart(ctxKategori, {
      type: 'pie',
      data: {
        labels: katLabels.length > 0 ? katLabels : ['Veri Yok'],
        datasets: [{
          data: katData.length > 0 ? katData : [1],
          backgroundColor: ['#e11d48', '#d97706', '#2563eb', '#7c3aed', '#db2777', '#059669', '#4f46e5', '#0d9488', '#ea580c'],
          borderWidth: 2
        }]
      },
      options: { responsive: true, maintainAspectRatio: false }
    });
  }

  let ctxAylik = document.getElementById('aylikKarsilastirmaChart');
  if (ctxAylik) {
    let aylikMapGelir = {};
    let aylikMapGider = {};
    let tumAylarSet = new Set();

    islemler.forEach(i => {
      if (i.yil && i.ay) {
        let yilAy = `${i.yil}-${String(i.ay).padStart(2, '0')}`;
        tumAylarSet.add(yilAy);
        if (i.tip === 'gelir') {
          aylikMapGelir[yilAy] = (aylikMapGelir[yilAy] || 0) + Number(i.tutar || 0);
        } else {
          aylikMapGider[yilAy] = (aylikMapGider[yilAy] || 0) + Number(i.tutar || 0);
        }
      }
    });

    let siraliAylar = Array.from(tumAylarSet).sort();
    let gelirVerileri = siraliAylar.map(ay => aylikMapGelir[ay] || 0);
    let giderVerileri = siraliAylar.map(ay => aylikMapGider[ay] || 0);

    let formatliAylar = siraliAylar.map(ay => {
      let parcalar = ay.split('-');
      if (parcalar.length === 2) {
        let ayIdx = parseInt(parcalar[1], 10) - 1;
        return `${AYLAR_ISIM[ayIdx] || parcalar[1]} ${parcalar[0]}`;
      }
      return ay;
    });

    if (aylikKarsilastirmaChartInstance) aylikKarsilastirmaChartInstance.destroy();
    aylikKarsilastirmaChartInstance = new Chart(ctxAylik, {
      type: 'bar',
      data: {
        labels: formatliAylar.length > 0 ? formatliAylar : ['Veri Yok'],
        datasets: [
          { label: 'Gelir', data: gelirVerileri.length > 0 ? gelirVerileri : [0], backgroundColor: '#059669', borderRadius: 6 },
          { label: 'Gider', data: giderVerileri.length > 0 ? giderVerileri : [0], backgroundColor: '#e11d48', borderRadius: 6 }
        ]
      },
      options: { responsive: true, maintainAspectRatio: false }
    });
  }
}

// ---------- DAİRE YÖNETİMİ ----------
function daireModalAc() {
  if (aktifKullaniciRol !== 'yonetici') return;
  document.getElementById('daireModalBaslik').innerHTML = `<i class="fa-solid fa-user-plus text-blue-700"></i> Yeni Daire Tanımla`;
  document.getElementById('duzenlenenDaireId').value = '';
  document.getElementById('yeniDaireNo').value = '';
  document.getElementById('yeniDaireSahip').value = '';
  document.getElementById('yeniDaireTelefon').value = '';
  document.getElementById('yeniDaireTutar').value = '';
  document.getElementById('yeniDaireYonetici').checked = false;
  document.getElementById('daireModal').classList.remove('hidden');
}

function daireDuzenleModalAc(id) {
  if (aktifKullaniciRol !== 'yonetici') return;
  let d = daireler.find(x => x.id === id);
  if (!d) return;
  document.getElementById('daireModalBaslik').innerHTML = `<i class="fa-solid fa-pen-to-square text-blue-700"></i> Daire Bilgilerini Düzenle`;
  document.getElementById('duzenlenenDaireId').value = d.id;
  document.getElementById('yeniDaireNo').value = d.no || '';
  document.getElementById('yeniDaireSahip').value = d.sahip || '';
  document.getElementById('yeniDaireTelefon').value = d.telefon || '';
  document.getElementById('yeniDaireTutar').value = d.tutar || '';
  document.getElementById('yeniDaireYonetici').checked = d.yoneticiMuaf || false;
  document.getElementById('daireModal').classList.remove('hidden');
}

function daireModalKapat() {
  document.getElementById('daireModal').classList.add('hidden');
}

function daireKaydet() {
  if (aktifKullaniciRol !== 'yonetici') return;
  let idField = document.getElementById('duzenlenenDaireId').value;
  let no = document.getElementById('yeniDaireNo').value.trim();
  let sahip = document.getElementById('yeniDaireSahip').value.trim();
  let telefon = document.getElementById('yeniDaireTelefon').value.trim();
  let tutar = document.getElementById('yeniDaireTutar').value.trim();
  let yoneticiMuaf = document.getElementById('yeniDaireYonetici').checked;

  if (!no) {
    alert("Lütfen daire no giriniz.");
    return;
  }

  let finalTutar = yoneticiMuaf ? 0 : Number(tutar || 0);

  if (idField) {
    let d = daireler.find(x => x.id == idField);
    if (d) {
      d.no = no;
      d.sahip = sahip || "Belirtilmemiş";
      d.telefon = telefon;
      d.tutar = finalTutar;
      d.yoneticiMuaf = yoneticiMuaf;
    }
  } else {
    if (daireler.length >= 20) {
      alert("Bu bina için en fazla 20 daire tanımlanabilir.");
      return;
    }
    daireler.push({
      id: Date.now(),
      no: no,
      sahip: sahip || "Belirtilmemiş",
      telefon: telefon,
      sifre: "12345",
      tutar: finalTutar,
      yoneticiMuaf: yoneticiMuaf,
      izinler: { ...VARSAYILAN_IZINLER },
      odemeGecmisi: {}
    });
  }

  daireModalKapat();
  verileriKaydet();
}

function daireTasi(index, yon) {
  if (aktifKullaniciRol !== 'yonetici') return;
  let hedefIndex = index + yon;
  if (hedefIndex < 0 || hedefIndex >= daireler.length) return;
  let temp = daireler[index];
  daireler[index] = daireler[hedefIndex];
  daireler[hedefIndex] = temp;
  verileriKaydet();
}

function daireSil(id) {
  if (aktifKullaniciRol !== 'yonetici') return;
  if (confirm("Bu daireyi ve ödeme geçmişini tamamen silmek istiyor musunuz?")) {
    daireler = daireler.filter(x => x.id !== id);
    verileriKaydet();
  }
}

function aidatDurumDegistir(id, ayKod, gun, ay, yil) {
  if (aktifKullaniciRol !== 'yonetici') return;
  let d = daireler.find(x => x.id === id);
  if (d) {
    if (d.yoneticiMuaf) return;
    if (!d.odemeGecmisi) d.odemeGecmisi = {};
    let suanOdendiMi = d.odemeGecmisi[ayKod] === true;
    d.odemeGecmisi[ayKod] = !suanOdendiMi;

    let islemAciklama = `${d.no} (${d.sahip}) Aidat Ödemesi`;

    if (d.odemeGecmisi[ayKod]) {
      let tarihStr = `${yil}-${String(ay).padStart(2, '0')}-${String(gun).padStart(2, '0')}`;
      islemler.unshift({
        id: Date.now(),
        tip: 'gelir',
        kategori: 'Aidat Ödemesi',
        kaynak: 'Ziraat Bankası',
        aciklama: islemAciklama,
        tutar: Number(d.tutar),
        gun: Number(gun),
        ay: Number(ay),
        yil: Number(yil),
        tarih: tarihStr,
        daireId: d.id,
        islemAy: ayKod
      });
    } else {
      islemler = islemler.filter(x => !(x.daireId === d.id && x.islemAy === ayKod && x.kategori === 'Aidat Ödemesi'));
    }
    verileriKaydet();
  }
}

// ---------- TOPLANTI ----------
function toplantiModalAc() {
  if (aktifKullaniciRol !== 'yonetici') return;
  document.getElementById('toplantiBaslik').value = '';
  document.getElementById('toplantiTarih').value = new Date().toISOString().split('T')[0];
  document.getElementById('toplantiKararlar').value = '';
  document.getElementById('toplantiModal').classList.remove('hidden');
}

function toplantiModalKapat() {
  document.getElementById('toplantiModal').classList.add('hidden');
}

function toplantiKaydet() {
  if (aktifKullaniciRol !== 'yonetici') return;
  let baslik = document.getElementById('toplantiBaslik').value.trim();
  let tarih = document.getElementById('toplantiTarih').value;
  let kararlar = document.getElementById('toplantiKararlar').value.trim();

  if (!baslik || !tarih) {
    alert("Lütfen toplantı başlığı ve tarihi giriniz.");
    return;
  }

  toplantilar.unshift({ id: Date.now(), baslik: baslik, tarih: tarih, kararlar: kararlar });
  toplantiModalKapat();
  verileriKaydet();
  toplantiListesiniGuncelle();
}

function toplantiSil(id) {
  if (aktifKullaniciRol !== 'yonetici') return;
  if (confirm("Bu toplantı kararını silmek istediğinize emin misiniz?")) {
    toplantilar = toplantilar.filter(x => x.id !== id);
    verileriKaydet();
    toplantiListesiniGuncelle();
  }
}

function toplantiListesiniGuncelle() {
  const container = document.getElementById('toplantiListesiContainer');
  if (!container) return;
  container.innerHTML = '';

  if (!toplantilar || toplantilar.length === 0) {
    container.innerHTML = `<div class="text-center py-10 text-slate-400 font-medium">Henüz kayıtlı toplantı kararı bulunmuyor.</div>`;
    return;
  }

  toplantilar.forEach(t => {
    let tarihStr = t.tarih ? t.tarih.split('-').reverse().join('.') : '';
    let silBtn = aktifKullaniciRol === 'yonetici'
      ? `<button onclick="toplantiSil(${t.id})" class="text-rose-500 hover:text-rose-700 transition p-2 bg-rose-50 rounded-xl trash-btn-3d"><i class="fa-solid fa-trash-can"></i></button>`
      : '';

    container.innerHTML += `<div class="bg-slate-50 border border-slate-200 rounded-3xl p-5 shadow-sm">
      <div class="flex justify-between items-start mb-3">
        <div>
          <span class="text-xs font-extrabold uppercase bg-blue-100 text-blue-900 px-3 py-1 rounded-full shadow-sm nowrap-date">${tarihStr}</span>
          <h4 class="font-extrabold text-slate-800 text-base mt-2">${t.baslik}</h4>
        </div>
        ${silBtn}
      </div>
      <div class="bg-white p-4 rounded-2xl border border-slate-100 text-sm text-slate-700 whitespace-pre-line font-medium shadow-inner">${t.kararlar || 'Karar detayı girilmemiş.'}</div>
    </div>`;
  });
}

// ---------- BANKA ----------
function bankaKartlariniGuncelle() {
  const bankaDiv = document.getElementById('bankaHesapListesi');
  if (!bankaDiv) return;
  bankaDiv.innerHTML = '';

  bankaHesaplari.forEach(hesap => {
    let toplamGiren = islemler.filter(i => (i.kaynak || "").trim().toLocaleLowerCase('tr') === hesap.ad.trim().toLocaleLowerCase('tr') && i.tip === 'gelir').reduce((acc, curr) => acc + Number(curr.tutar || 0), 0);
    let toplamCikan = islemler.filter(i => (i.kaynak || "").trim().toLocaleLowerCase('tr') === hesap.ad.trim().toLocaleLowerCase('tr') && i.tip === 'gider').reduce((acc, curr) => acc + Number(curr.tutar || 0), 0);
    let guncelBakiye = toplamGiren - toplamCikan;

    let ikonHtml = '';
    let baslikRenk = '';
    if (hesap.ad.toLocaleLowerCase('tr').includes('ziraat')) {
      ikonHtml = `<div class="w-12 h-12 rounded-2xl bg-gradient-to-br from-red-600 to-red-900 text-white flex items-center justify-center font-black text-base icon-3d icon-3d-red shadow-lg" title="Ziraat Bankası">
        <svg class="w-7 h-7 fill-white" viewBox="0 0 24 24"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>
      </div>`;
      baslikRenk = 'text-red-700';
    } else {
      ikonHtml = `<div class="w-12 h-12 rounded-2xl bg-gradient-to-br from-emerald-500 to-teal-700 text-white flex items-center justify-center font-black text-base icon-3d icon-3d-emerald"><i class="fa-solid fa-money-bill-wave"></i></div>`;
      baslikRenk = 'text-emerald-700';
    }

    bankaDiv.innerHTML += `<div class="bg-slate-50 p-6 md:p-8 rounded-3xl card-3d flex flex-col justify-between">
      <div>
        <div class="flex items-center justify-between mb-4">
          <p class="text-xs font-black ${baslikRenk} uppercase tracking-wider flex items-center gap-2">${hesap.ad}</p>
          ${ikonHtml}
        </div>
        <h3 class="text-3xl font-black text-slate-800 tracking-tight">${guncelBakiye.toLocaleString('tr-TR', { style: 'currency', currency: 'TRY' })}</h3>
      </div>
      <div class="mt-6 pt-4 border-t border-slate-200 grid grid-cols-2 gap-4 text-center">
        <div>
          <p class="text-[10px] font-bold text-slate-500 uppercase tracking-wider">Toplam Giren</p>
          <p class="text-sm font-extrabold text-emerald-600 mt-1">${toplamGiren.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL</p>
        </div>
        <div>
          <p class="text-[10px] font-bold text-slate-500 uppercase tracking-wider">Toplam Çıkan</p>
          <p class="text-sm font-extrabold text-rose-600 mt-1">${toplamCikan.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL</p>
        </div>
      </div>
    </div>`;
  });
}

// ---------- ARŞİV ----------
function arsivListesiniGuncelle() {
  const container = document.getElementById('arsivListesiniContainer');
  if (!container) return;
  container.innerHTML = '';

  if (!arsivBelgeleri || arsivBelgeleri.length === 0) {
    container.innerHTML = `<div class="col-span-3 text-center py-10 text-slate-400 font-medium">Arşivde henüz kayıtlı belge bulunmuyor.</div>`;
    return;
  }

  arsivBelgeleri.forEach(b => {
    let silBtn = aktifKullaniciRol === 'yonetici'
      ? `<button onclick="arsivBelgeSil(${b.id})" class="text-rose-500 hover:text-rose-700 p-2 transition bg-rose-50 rounded-xl trash-btn-3d"><i class="fa-solid fa-trash-can"></i></button>`
      : '';

    container.innerHTML += `<div class="bg-slate-50 border border-slate-200 rounded-3xl p-5 flex flex-col justify-between shadow-sm hover:shadow-md transition">
      <div>
        <div class="flex justify-between items-start mb-2">
          <span class="text-[10px] font-extrabold uppercase bg-blue-100 text-blue-900 px-3 py-1 rounded-full shadow-sm">${b.tip}</span>
          <span class="text-xs text-slate-500 font-bold nowrap-date">${b.tarih ? b.tarih.split('-').reverse().join('.') : ''}</span>
        </div>
        <h4 class="font-extrabold text-slate-800 text-sm mt-2">${b.baslik}</h4>
      </div>
      <div class="flex items-center justify-between gap-2 mt-6 pt-3 border-t border-slate-200">
        <button onclick="belgeGoster(${b.id}, 'arsiv')" class="bg-blue-50 text-blue-700 hover:bg-blue-100 px-3 py-1.5 rounded-xl text-xs font-bold border border-blue-200"><i class="fa-solid fa-eye mr-1"></i> Görüntüle</button>
        ${silBtn}
      </div>
    </div>`;
  });
}

function arsivModalAc() {
  if (aktifKullaniciRol !== 'yonetici') return;
  document.getElementById('arsivBaslik').value = '';
  document.getElementById('arsivDosyaInput').value = '';
  document.getElementById('arsivModal').classList.remove('hidden');
}

function arsivModalKapat() {
  document.getElementById('arsivModal').classList.add('hidden');
}

function arsivBelgeKaydet() {
  if (aktifKullaniciRol !== 'yonetici') return;
  let tip = document.getElementById('arsivTip').value;
  let baslik = document.getElementById('arsivBaslik').value.trim();
  let dosyaInput = document.getElementById('arsivDosyaInput');

  if (!baslik || !dosyaInput.files[0]) {
    alert("Lütfen başlık giriniz ve dosya seçiniz.");
    return;
  }

  let reader = new FileReader();
  reader.onload = function (e) {
    arsivBelgeleri.unshift({
      id: Date.now(),
      tip: tip,
      baslik: baslik,
      tarih: new Date().toISOString().split('T')[0],
      veri: e.target.result
    });
    arsivModalKapat();
    verileriKaydet();
    arsivListesiniGuncelle();
  };
  reader.readAsDataURL(dosyaInput.files[0]);
}

function arsivBelgeSil(id) {
  if (aktifKullaniciRol !== 'yonetici') return;
  if (confirm("Bu arşiv belgesini silmek istediğinize emin misiniz?")) {
    arsivBelgeleri = arsivBelgeleri.filter(x => x.id !== id);
    verileriKaydet();
    arsivListesiniGuncelle();
  }
}

// ---------- BELGE GÖRÜNTÜLEME ----------
function belgeGoster(id, kaynakTip) {
  let belgeVeri = null;
  let belgeBaslik = "";

  if (kaynakTip === 'islem') {
    let isl = islemler.find(x => x.id == id);
    if (isl) { belgeVeri = isl.belgeData; belgeBaslik = isl.aciklama; }
  } else {
    let ars = arsivBelgeleri.find(x => x.id == id);
    if (ars) { belgeVeri = ars.veri; belgeBaslik = ars.baslik; }
  }

  if (!belgeVeri) {
    alert("Belge içeriği bulunamadı.");
    return;
  }

  document.getElementById('belgeGosterBaslik').innerText = belgeBaslik;
  let icerikDiv = document.getElementById('belgeGosterIcerik');

  if (belgeVeri.startsWith('data:image')) {
    icerikDiv.innerHTML = `<img src="${belgeVeri}" class="max-w-full max-h-[60vh] rounded-2xl shadow-md object-contain">`;
  } else {
    icerikDiv.innerHTML = `<iframe src="${belgeVeri}" class="w-full h-[60vh] rounded-2xl border-0"></iframe>`;
  }

  document.getElementById('belgeGosterModal').classList.remove('hidden');
}

function belgeGosterKapat() {
  document.getElementById('belgeGosterModal').classList.add('hidden');
}

// ---------- DETAY MODALI ----------
function detayModalAc(tip) {
  if (aktifKullaniciRol !== 'yonetici') return;
  let baslikEl = document.getElementById('detayModalBaslik');
  let theadEl = document.getElementById('detayModalTableHead');
  let bodyEl = document.getElementById('detayModalBody');
  bodyEl.innerHTML = '';

  if (tip === 'varlik') {
    baslikEl.innerHTML = `<i class="fa-solid fa-wallet text-blue-700"></i> Toplam Varlık Dağılımı ve Hesap Bakiyeleri`;
    theadEl.innerHTML = `<th class="p-3">Hesap / Kasa Adı</th><th class="p-3 text-right">Toplam Giren</th><th class="p-3 text-right">Toplam Çıkan</th><th class="p-3 text-right">Güncel Bakiye</th>`;

    bankaHesaplari.forEach(h => {
      let giren = islemler.filter(i => (i.kaynak || "").trim().toLocaleLowerCase('tr') === h.ad.trim().toLocaleLowerCase('tr') && i.tip === 'gelir').reduce((a, c) => a + Number(c.tutar || 0), 0);
      let cikan = islemler.filter(i => (i.kaynak || "").trim().toLocaleLowerCase('tr') === h.ad.trim().toLocaleLowerCase('tr') && i.tip === 'gider').reduce((a, c) => a + Number(c.tutar || 0), 0);
      let bakiye = giren - cikan;

      bodyEl.innerHTML += `<tr class="hover:bg-slate-50 transition">
        <td class="p-3 font-extrabold text-slate-800">${h.ad}</td>
        <td class="p-3 text-right font-bold text-emerald-600">+${giren.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL</td>
        <td class="p-3 text-right font-bold text-rose-600">-${cikan.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL</td>
        <td class="p-3 text-right font-black text-blue-900">${bakiye.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL</td>
      </tr>`;
    });
  } else if (tip === 'borc') {
    const donemAyEl = document.getElementById('donemAySecici');
    const donemYilEl = document.getElementById('donemYilSecici');
    let ayVal = donemAyEl ? donemAyEl.value : "10";
    let yilVal = donemYilEl ? donemYilEl.value : "2026";
    let seciliAyKod = `${yilVal}-${ayVal}`;
    let ayIsmiStr = AYLAR_ISIM[parseInt(ayVal, 10) - 1] || ayVal;

    baslikEl.innerHTML = `<i class="fa-solid fa-triangle-exclamation text-amber-600"></i> Ödenmeyen Aidat Listesi (${ayIsmiStr} ${yilVal})`;
    theadEl.innerHTML = `<th class="p-3">Daire No</th><th class="p-3">Kat Maliki / Kiracı</th><th class="p-3">Telefon</th><th class="p-3 text-right">Tutar</th>`;

    let odenmeyenler = daireler.filter(d => !d.yoneticiMuaf && (!d.odemeGecmisi || !d.odemeGecmisi[seciliAyKod]));

    if (odenmeyenler.length === 0) {
      bodyEl.innerHTML = `<tr><td colspan="4" class="p-6 text-center text-slate-400 font-medium">Seçilen dönemde ödenmeyen aidat bulunmuyor. Harika!</td></tr>`;
    } else {
      odenmeyenler.forEach(d => {
        bodyEl.innerHTML += `<tr class="hover:bg-slate-50 transition">
          <td class="p-3 font-extrabold text-slate-800">${d.no}</td>
          <td class="p-3 font-semibold text-slate-700">${d.sahip}</td>
          <td class="p-3 font-semibold text-slate-700">${d.telefon || 'Yok'}</td>
          <td class="p-3 text-right font-black text-amber-600">${Number(d.tutar || 0).toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL</td>
        </tr>`;
      });
    }
  } else {
    let filtrelenen = islemler.filter(i => i.tip === tip);
    theadEl.innerHTML = `<th class="p-3">Tarih</th><th class="p-3">Kaynak</th><th class="p-3">Kategori</th><th class="p-3">Açıklama</th><th class="p-3 text-right">Tutar</th>`;

    if (tip === 'gelir') {
      baslikEl.innerHTML = `<i class="fa-solid fa-arrow-trend-up text-emerald-600"></i> Tüm Zamanların Gelir Hareketleri (${filtrelenen.length} Kayıt)`;
    } else {
      baslikEl.innerHTML = `<i class="fa-solid fa-arrow-trend-down text-rose-600"></i> Tüm Zamanların Gider Hareketleri (${filtrelenen.length} Kayıt)`;
    }

    if (filtrelenen.length === 0) {
      bodyEl.innerHTML = `<tr><td colspan="5" class="p-6 text-center text-slate-400 font-medium">Bu kategoride henüz kayıt bulunmuyor.</td></tr>`;
    } else {
      filtrelenen.forEach(i => {
        let tarihStr = '';
        if (i.gun && i.ay && i.yil) {
          let ayIsmi = AYLAR_ISIM[i.ay - 1] || i.ay;
          tarihStr = `${i.gun} ${ayIsmi} ${i.yil}`;
        } else {
          tarihStr = i.tarih || '';
        }

        let tutarStr = `${i.tip === 'gelir' ? '+' : '-'}${Number(i.tutar || 0).toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`;

        bodyEl.innerHTML += `<tr class="hover:bg-slate-50 transition">
          <td class="p-3 text-xs font-bold text-slate-600 nowrap-date">${tarihStr}</td>
          <td class="p-3 font-extrabold text-slate-800">${i.kaynak}</td>
          <td class="p-3 text-slate-600">${i.kategori}</td>
          <td class="p-3 font-semibold text-slate-800">${i.aciklama}</td>
          <td class="p-3 text-right font-black ${tip === 'gelir' ? 'text-emerald-600' : 'text-rose-600'}">${tutarStr}</td>
        </tr>`;
      });
    }
  }

  document.getElementById('detayModal').classList.remove('hidden');
}

function detayModalKapat() {
  document.getElementById('detayModal').classList.add('hidden');
}

// ---------- SMS HATIRLATICI ----------
function smsHatirlaticiGonder(daireId, ay) {
  let d = daireler.find(x => x.id === daireId);
  if (!d || !d.telefon) {
    alert("Bu daireye ait kayıtlı telefon numarası bulunamadı.");
    return;
  }
  let ayParcalar = ay.split('-');
  let ayIsmi = AYLAR_ISIM[parseInt(ayParcalar[1], 10) - 1] + ' ' + ayParcalar[0];
  let mesaj = `Sayın ${d.sahip}, ${ayIsmi} dönemi ${d.tutar} TL tutarındaki aidat ödemenizin yapılmadığı tespit edilmiştir. Lütfen ödemenizi gerçekleştiriniz. İyi günler dileriz.`;

  window.location.href = `sms:${d.telefon}?body=${encodeURIComponent(mesaj)}`;
}

// ---------- PDF RAPOR ----------
function trKarakterTemizle(text) {
  if (!text) return '';
  return text.toString()
    .replace(/ğ/g, 'g').replace(/Ğ/g, 'G')
    .replace(/ü/g, 'u').replace(/Ü/g, 'U')
    .replace(/ş/g, 's').replace(/Ş/g, 'S')
    .replace(/ı/g, 'i').replace(/İ/g, 'I')
    .replace(/ö/g, 'o').replace(/Ö/g, 'O')
    .replace(/ç/g, 'c').replace(/Ç/g, 'C');
}

function pdfRaporuOlustur() {
  if (!window.jspdf) {
    alert("PDF kütüphanesi yüklenemedi. İnternet bağlantınızı kontrol edin.");
    return;
  }
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  doc.setFont("helvetica", "bold");
  doc.setFontSize(16);
  doc.text(trKarakterTemizle("PROFESYONEL SITE YONETIMI - FINANSAL RAPOR"), 14, 20);

  doc.setFont("helvetica", "normal");
  doc.setFontSize(10);
  doc.text(trKarakterTemizle("Yonetici: Kasım Taha Yamak"), 14, 27);
  doc.text(trKarakterTemizle("Rapor Tarihi: " + new Date().toLocaleDateString('tr-TR')), 14, 33);

  let toplamGelir = islemler.filter(i => i.tip === 'gelir').reduce((acc, curr) => acc + Number(curr.tutar || 0), 0);
  let toplamGider = islemler.filter(i => i.tip === 'gider').reduce((acc, curr) => acc + Number(curr.tutar || 0), 0);
  let netKasa = toplamGelir - toplamGider;

  doc.setFont("helvetica", "bold");
  doc.setFontSize(12);
  doc.text(trKarakterTemizle("Genel Finansal Durum Ozeti"), 14, 43);

  doc.setFont("helvetica", "normal");
  doc.setFontSize(10);
  doc.text(trKarakterTemizle(`Toplam Gelir: ${toplamGelir.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`), 14, 50);
  doc.text(trKarakterTemizle(`Toplam Gider: ${toplamGider.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`), 14, 56);
  doc.text(trKarakterTemizle(`Net Varlik: ${netKasa.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`), 14, 62);

  let bankaData = bankaHesaplari.map(h => {
    let giren = islemler.filter(i => (i.kaynak || "").trim().toLocaleLowerCase('tr') === h.ad.trim().toLocaleLowerCase('tr') && i.tip === 'gelir').reduce((a, c) => a + Number(c.tutar || 0), 0);
    let cikan = islemler.filter(i => (i.kaynak || "").trim().toLocaleLowerCase('tr') === h.ad.trim().toLocaleLowerCase('tr') && i.tip === 'gider').reduce((a, c) => a + Number(c.tutar || 0), 0);
    let bakiye = giren - cikan;
    return [
      trKarakterTemizle(h.ad),
      `${giren.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`,
      `${cikan.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`,
      `${bakiye.toLocaleString('tr-TR', { minimumFractionDigits: 2, maximumFractionDigits: 2 })} TL`
    ];
  });

  doc.autoTable({
    startY: 72,
    head: [[trKarakterTemizle('Hesap / Kasa Adi'), trKarakterTemizle('Toplam Giren'), trKarakterTemizle('Toplam Cikan'), trKarakterTemizle('Bakiye')]],
    body: bankaData,
    theme: 'grid',
    headStyles: { fillColor: [30, 58, 138] }
  });

  doc.save("site_yonetim_mali_rapor.pdf");
}

// ---------- BAŞLATMA ----------
verileriYukle();
daireleriYirmiyeTamamla();
verileriKaydet();
aySeciciDoldur();
kategoriDoldur();

// Beni Hatırla kontrolü
let hatirlananKullanici = localStorage.getItem('site_hatirlanan_kullanici');
let hatirlananSifre = localStorage.getItem('site_hatirlanan_sifre');
let beniHatirlaAktif = localStorage.getItem('site_beni_hatirla_aktif');

if (beniHatirlaAktif && hatirlananKullanici && hatirlananSifre) {
  document.getElementById('girisKullaniciInput').value = hatirlananKullanici;
  document.getElementById('girisSifreInput').value = hatirlananSifre;
  document.getElementById('beniHatirlaCheckbox').checked = true;
  sifreKontrolEt();
} else {
  guncelleEkran();
  document.getElementById('girisKullaniciInput').focus();
}
</script>
</body>
</html>
