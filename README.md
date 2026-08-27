# otopark-e-fatura-kare-kod
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>E-Fatura Bilgi Formu</title>
<style>
  :root{
    --ink:#1c2b2d;
    --paper:#f4f7f6;
    --line:#c9d4d2;
    --accent:#1f6f5c;
    --accent-dark:#154d40;
    --warn:#b5442e;
    --card:#ffffff;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Arial,sans-serif;
    background:var(--paper);
    color:var(--ink);
    min-height:100vh;
  }
  .wrap{
    max-width:480px;
    margin:0 auto;
    padding:0 0 40px;
  }
  header{
    background:var(--accent-dark);
    color:#fff;
    padding:28px 20px 22px;
    position:relative;
    overflow:hidden;
  }
  header::after{
    content:"";
    position:absolute;
    right:-30px; top:-30px;
    width:140px; height:140px;
    border-radius:50%;
    background:rgba(255,255,255,0.06);
  }
  header .tag{
    font-size:12px;
    letter-spacing:.14em;
    text-transform:uppercase;
    opacity:.75;
    margin:0 0 6px;
  }
  header h1{
    margin:0;
    font-size:22px;
    line-height:1.3;
    font-weight:700;
  }
  header p{
    margin:10px 0 0;
    font-size:13.5px;
    opacity:.9;
    line-height:1.5;
  }
  .barrier{
    display:flex; align-items:center; gap:8px;
    margin-top:16px;
    font-size:12.5px;
    background:rgba(255,255,255,0.1);
    padding:8px 12px;
    border-radius:8px;
  }
  .dot{width:8px;height:8px;border-radius:50%;background:#ffd166;flex:none;}

  form{padding:20px;}
  .section-title{
    font-size:12px;
    text-transform:uppercase;
    letter-spacing:.1em;
    color:var(--accent-dark);
    font-weight:700;
    margin:26px 0 10px;
  }
  .section-title:first-of-type{margin-top:8px;}

  .toggle{
    display:flex;
    background:#e7ede9;
    border-radius:10px;
    padding:4px;
    gap:4px;
  }
  .toggle button{
    flex:1;
    border:none;
    background:transparent;
    padding:10px 8px;
    font-size:14px;
    font-weight:600;
    border-radius:7px;
    color:var(--accent-dark);
    cursor:pointer;
  }
  .toggle button.active{
    background:var(--accent);
    color:#fff;
  }

  label{
    display:block;
    font-size:13px;
    font-weight:600;
    margin:14px 0 6px;
    color:#3c4a4a;
  }
  label .req{color:var(--warn);}
  input, select{
    width:100%;
    padding:12px 13px;
    font-size:15px;
    border:1.5px solid var(--line);
    border-radius:9px;
    background:var(--card);
    color:var(--ink);
    font-family:inherit;
  }
  input:focus, select:focus{
    outline:none;
    border-color:var(--accent);
  }
  .hint{font-size:12px;color:#6c7a79;margin-top:5px;}
  .row2{display:flex;gap:10px;}
  .row2 > div{flex:1;}

  .hidden{display:none !important;}

  .submit-btn{
    width:100%;
    margin-top:28px;
    padding:15px;
    background:var(--accent);
    color:#fff;
    border:none;
    border-radius:10px;
    font-size:15.5px;
    font-weight:700;
    cursor:pointer;
  }
  .submit-btn:active{background:var(--accent-dark);}

  .note{
    margin-top:14px;
    font-size:12px;
    color:#6c7a79;
    line-height:1.6;
    text-align:center;
  }

  .error-box{
    display:none;
    background:#fbe9e5;
    border:1px solid var(--warn);
    color:var(--warn);
    padding:10px 12px;
    border-radius:8px;
    font-size:13px;
    margin-top:16px;
  }

  .success-screen{
    display:none;
    padding:60px 24px;
    text-align:center;
  }
  .success-screen .check{
    width:64px;height:64px;border-radius:50%;
    background:var(--accent);
    color:#fff;
    display:flex;align-items:center;justify-content:center;
    margin:0 auto 18px;
    font-size:30px;
  }
  .success-screen h2{margin:0 0 10px;font-size:19px;}
  .success-screen p{margin:0 0 6px;font-size:14px;color:#4a5857;line-height:1.6;}
  .success-screen .step{
    text-align:left;
    background:#fff;
    border:1px solid var(--line);
    border-radius:10px;
    padding:14px 16px;
    margin-top:22px;
    font-size:13.5px;
    line-height:1.7;
  }
  .success-screen .step b{color:var(--accent-dark);}
</style>
</head>
<body>
<div class="wrap">

  <header>
    <p class="tag">Otopark Çıkış Ödemesi</p>
    <h1>E-Fatura Bilgi Formu</h1>
    <p>Kredi kartı ile ödeme yaptınız. Perakende fiş yerine e-fatura talep ettiğiniz için, faturanın düzenlenebilmesi adına bilgilerinizi aşağıya girin.</p>
    <div class="barrier"><span class="dot"></span> Form gönderildikten sonra bariyer merkez tarafından açılacaktır.</div>
  </header>

  <form id="invoiceForm">

    <div class="section-title">Fatura Türü</div>
    <div class="toggle" role="tablist">
      <button type="button" id="btnBireysel" class="active">Bireysel</button>
      <button type="button" id="btnKurumsal">Kurumsal</button>
    </div>

    <div id="bireyselFields">
      <label>Ad Soyad <span class="req">*</span></label>
      <input type="text" id="adSoyad" placeholder="Ör: Ahmet Yılmaz">

      <label>TC Kimlik No <span class="req">*</span></label>
      <input type="text" id="tckn" inputmode="numeric" maxlength="11" placeholder="11 haneli TC Kimlik No">
    </div>

    <div id="kurumsalFields" class="hidden">
      <label>Firma Unvanı <span class="req">*</span></label>
      <input type="text" id="unvan" placeholder="Ör: ABC Lojistik A.Ş.">

      <label>Vergi Kimlik No <span class="req">*</span></label>
      <input type="text" id="vkn" inputmode="numeric" maxlength="10" placeholder="10 haneli Vergi No">

      <label>Vergi Dairesi <span class="req">*</span></label>
      <input type="text" id="vergiDairesi" placeholder="Ör: Konak Vergi Dairesi">
    </div>

    <div class="section-title">İletişim ve Adres</div>

    <label>Adres <span class="req">*</span></label>
    <input type="text" id="adres" placeholder="Fatura adresi">

    <div class="row2">
      <div>
        <label>E-posta <span class="req">*</span></label>
        <input type="email" id="eposta" placeholder="ornek@eposta.com">
      </div>
      <div>
        <label>Telefon</label>
        <input type="tel" id="telefon" placeholder="05xx xxx xx xx">
      </div>
    </div>

    <div class="section-title">Araç ve Ödeme Bilgisi</div>

    <div class="row2">
      <div>
        <label>Plaka <span class="req">*</span></label>
        <input type="text" id="plaka" placeholder="35 ABC 123" style="text-transform:uppercase;">
      </div>
      <div>
        <label>Ödeme Tutarı</label>
        <input type="text" id="tutar" placeholder="Ör: 85 TL">
      </div>
    </div>
    <p class="hint">Tutar biliniyorsa girin; bilinmiyorsa boş bırakabilirsiniz, merkez kart ekstresinden eşleştirecektir.</p>

    <div class="error-box" id="errorBox"></div>

    <button type="button" class="submit-btn" id="submitBtn">Bilgileri Gönder</button>
    <p class="note">Gönder'e bastığınızda telefonunuzun e-posta uygulaması açılır; e-postayı göndermeniz gerekir. Bilgileriniz yalnızca fatura düzenlemek için kullanılır.</p>
  </form>

  <div class="success-screen" id="successScreen">
    <div class="check">✓</div>
    <h2>E-posta hazırlandı</h2>
    <p>Mail uygulamanız açıldı. Lütfen e-postayı <b>gönder</b> tuşuna basarak iletin.</p>
    <div class="step">
      <div><b>1.</b> Açılan mailde bilgileri kontrol edin.</div>
      <div><b>2.</b> Gönder'e basın.</div>
      <div><b>3.</b> Merkez onayının ardından bariyer otomatik açılacaktır.</div>
    </div>
  </div>

</div>

<script>
  // ==== AYARLAR: merkez e-posta adresini buraya girin ====
  const MERKEZ_EPOSTA = "merkez@ornekotopark.com";
  // =========================================================

  let faturaTipi = "bireysel";
  const btnB = document.getElementById("btnBireysel");
  const btnK = document.getElementById("btnKurumsal");
  const bireyselFields = document.getElementById("bireyselFields");
  const kurumsalFields = document.getElementById("kurumsalFields");

  btnB.addEventListener("click", () => {
    faturaTipi = "bireysel";
    btnB.classList.add("active");
    btnK.classList.remove("active");
    bireyselFields.classList.remove("hidden");
    kurumsalFields.classList.add("hidden");
  });
  btnK.addEventListener("click", () => {
    faturaTipi = "kurumsal";
    btnK.classList.add("active");
    btnB.classList.remove("active");
    kurumsalFields.classList.remove("hidden");
    bireyselFields.classList.add("hidden");
  });

  function val(id){ return document.getElementById(id).value.trim(); }

  function showError(msg){
    const box = document.getElementById("errorBox");
    box.textContent = msg;
    box.style.display = "block";
  }
  function clearError(){
    document.getElementById("errorBox").style.display = "none";
  }

  document.getElementById("submitBtn").addEventListener("click", () => {
    clearError();

    const adres = val("adres");
    const eposta = val("eposta");
    const plaka = val("plaka");

    if (!adres || !eposta || !plaka){
      showError("Lütfen zorunlu alanları (adres, e-posta, plaka) doldurun.");
      return;
    }
    if (!/^\S+@\S+\.\S+$/.test(eposta)){
      showError("Geçerli bir e-posta adresi girin.");
      return;
    }

    let musteriBlok = "";
    if (faturaTipi === "bireysel"){
      const ad = val("adSoyad");
      const tckn = val("tckn");
      if (!ad || !tckn || tckn.length !== 11){
        showError("Ad Soyad ve 11 haneli TC Kimlik No zorunludur.");
        return;
      }
      musteriBlok =
        "Fatura Türü: Bireysel\n" +
        "Ad Soyad: " + ad + "\n" +
        "TC Kimlik No: " + tckn;
    } else {
      const unvan = val("unvan");
      const vkn = val("vkn");
      const vd = val("vergiDairesi");
      if (!unvan || !vkn || !vd){
        showError("Firma Unvanı, Vergi No ve Vergi Dairesi zorunludur.");
        return;
      }
      musteriBlok =
        "Fatura Türü: Kurumsal\n" +
        "Firma Unvanı: " + unvan + "\n" +
        "Vergi Kimlik No: " + vkn + "\n" +
        "Vergi Dairesi: " + vd;
    }

    const telefon = val("telefon") || "-";
    const tutar = val("tutar") || "-";
    const simdi = new Date().toLocaleString("tr-TR");

    const konu = "E-Fatura Talebi - Plaka " + plaka.toUpperCase();
    const govde =
      musteriBlok + "\n" +
      "Adres: " + adres + "\n" +
      "E-posta: " + eposta + "\n" +
      "Telefon: " + telefon + "\n\n" +
      "Plaka: " + plaka.toUpperCase() + "\n" +
      "Ödeme Tutarı: " + tutar + "\n" +
      "Ödeme Yöntemi: Kredi Kartı (Otomatik Makine)\n" +
      "Fiş Türü: Perakende fiş kesilmedi - e-fatura talep edildi\n" +
      "Tarih/Saat: " + simdi;

    const mailtoLink =
      "mailto:" + MERKEZ_EPOSTA +
      "?subject=" + encodeURIComponent(konu) +
      "&body=" + encodeURIComponent(govde);

    window.location.href = mailtoLink;

    document.getElementById("invoiceForm").style.display = "none";
    document.querySelector("header").style.display = "none";
    document.getElementById("successScreen").style.display = "block";
  });
</script>
</body>
</html>
