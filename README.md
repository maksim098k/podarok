<html lang="sq">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Dhuratat e Vitit të Ri ✨</title>
<style>
  body {
    margin: 0;
    font-family: "Segoe UI", Roboto, Arial, sans-serif;
    background: linear-gradient(180deg, #fdf6f9 0%, #eaf9f6 100%); /* нежный фон */
    color: #444;
  }
  .container {
    max-width: 760px;
    margin: 40px auto;
    padding: 24px;
    background: #ffffffcc;
    border-radius: 20px;
    box-shadow: 0 0 30px rgba(255, 182, 193, 0.3);
    position: relative;
  }
  .container::before {
    content: "";
    position: absolute;
    top: -10px;
    left: -10px;
    right: -10px;
    bottom: -10px;
    border-radius: 28px;
    padding: 4px;
    background: repeating-linear-gradient(
      90deg,
      #f8c8dc 0 20px,   /* нежно-розовый */
      #c8e6c9 20px 40px,/* мятный */
      #ffe5b4 40px 60px,/* кремовый */
      #b3e5fc 60px 80px /* небесно-голубой */
    );
    z-index: -1;
    animation: lights 4s linear infinite;
  }
  @keyframes lights {
    0%   { filter: brightness(0.9); }
    50%  { filter: brightness(1.2); }
    100% { filter: brightness(0.9); }
  }
  /* лампочки по углам */
  .container::after {
    content: "";
    position: absolute;
    top: -18px;
    left: -18px;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: #f8c8dc;
    box-shadow:
      740px 0 #c8e6c9,   /* верхний правый угол */
      0 460px #ffe5b4,   /* нижний левый угол */
      740px 460px #b3e5fc; /* нижний правый угол */
    animation: bulbs 2s ease-in-out infinite alternate;
  }
  @keyframes bulbs {
    from { filter: brightness(0.8); }
    to   { filter: brightness(1.3); }
  }
  h2 {
    text-align: center;
    font-size: 32px;
    color: #f48fb1;
    font-weight: bold;
    margin-bottom: 16px;
  }
  h2::before, h2::after {
    content: "🌸✨🎁";
    margin: 0 8px;
  }
  p { line-height: 1.7; font-size: 16px; }
  .grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 20px;
  }
  .gift-btn {
    padding: 14px;
    border-radius: 14px;
    border: none;
    background: linear-gradient(180deg, #f8c8dc 0%, #f48fb1 100%); /* пастельные кнопки */
    color: #fff;
    font-weight: bold;
    cursor: pointer;
    box-shadow: 0 6px 18px rgba(244, 143, 177, 0.4);
    transition: all 0.3s ease;
  }
  .gift-btn:hover {
    background: linear-gradient(180deg, #ffe5b4 0%, #f8c8dc 100%);
    box-shadow: 0 0 20px #ffe5b4;
    transform: scale(1.05);
  }
  .gift-btn[disabled] {
    background: #ddd;
    cursor: not-allowed;
    opacity: 0.7;
    box-shadow: none;
  }
  .message {
    margin-top: 24px;
    padding: 20px;
    background: #fff0f6;
    border-radius: 16px;
    font-size: 17px;
    line-height: 1.8;
    border: 2px dashed #f8c8dc;
    box-shadow: inset 0 0 12px rgba(244, 143, 177, 0.3);
    color: #444;
  }
  .message::before {
    content: "✨🌸 ";
    font-size: 20px;
  }
  .message::after {
    content: " 🎁✨";
    font-size: 20px;
  }
  .lock-banner {
    margin-top: 12px;
    padding: 10px;
    background: #f8c8dc55;
    border-radius: 10px;
    font-size: 14px;
    color: #444;
  }

  /* стили модального окна */
  .modal {
    display: none; /* скрыто по умолчанию */
    position: fixed;
    z-index: 1000;
    left: 0; top: 0;
    width: 100%; height: 100%;
    background-color: rgba(0,0,0,0.5); /* затемнение */
  }
  .modal-content {
    background: #fffbea;
    margin: 15% auto;
    padding: 20px;
    border-radius: 16px;
    width: 80%;
    max-width: 500px;
    font-size: 17px;
    line-height: 1.8;
    border: 2px dashed #f8c8dc;
    box-shadow: 0 0 20px rgba(244,143,177,0.4);
    color: #444;
  }
  .close {
    float: right;
    font-size: 24px;
    font-weight: bold;
    cursor: pointer;
  }
</style>
</head>
<body>
<div class="container">
  <h2>Të dashur miq!</h2>
  <p>Sot kam një humor të mrekullueshëm dhe vendosa t’ju gëzoj me një dhuratë 🎁</p>
  <p>✨ Zgjidhni dhuratën tuaj! Çdo buton është një surprizë e veçantë. Thjesht klikoni mbi numrin dhe hapni dhuratën.</p>
  <p>🎁 Çdo dhuratë është e disponueshme vetëm një herë për një person. Pas hapjes, nuk do të jetë më e aksesueshme — ndaj bëni një screenshot si dëshmi.</p>
  <p>💌 Dhe më e rëndësishmja — me çdo dhuratë ju pret një urim personal nga unë.</p>

  <div id="lockBanner" class="lock-banner" style="display:none;"></div>
  <div class="grid" id="giftGrid"></div>

  <!-- модальное окно -->
  <div id="giftModal" class="modal">
    <div class="modal-content">
      <span id="closeModal" class="close">&times;</span>
      <p id="giftText"></p>
    </div>
  </div>
</div>


<script>
  const messages = {
    1: "Dëshiroj t’ju uroj besim dhe gëzim në çdo hap. Qoftë fati shoqëruesi juaj dhe t’ju ndihmojë të merrni vendime të guximshme. Sot keni mundësi të investoni bashkë me mua dhe të merrni fitim të dyfishtë — dhurata ime për ju. Qoftë kjo ditë fillimi i fitoreve të mëdha dhe horizonteve të reja!",
    2: "Ju uroj ngrohtësi dhe mbështetje nga të afërmit, që çdo moment të jetë i mbushur me harmoni dhe frymëzim. Sot mund të investojmë bashkë dhe do të merrni fitim pa komisionin tim — surpriza ime për ju. Qoftë kjo ditë t’ju sjellë lumturi dhe mundësi të reja që ndryshojnë jetën tuaj!",
    3: "Ju uroj rritje dhe besim në të ardhmen, që çdo hap të forcojë forcën dhe vendosmërinë tuaj. Sot keni mundësi të vendosni mjete me zbritje 10% në depozitë — dhurata ime për ju. Qoftë kjo ditë hap drejt realizimit të dëshirave dhe arritjes së qëllimeve!",
    4: "Ju uroj frymëzim që vjen në çastet më të papritura dhe i kthen gjërat e zakonshme në histori të ndritshme. Sot ju dhuroj strategjinë “Milioner” — një shans që me depozitë minimale të arrini të ardhura sa më të larta. Qoftë kjo ditë fillimi i arritjeve të mëdha dhe lëvizjes së sigurt përpara!",
    5: "Ju uroj guxim dhe energji për të pushtuar maja të reja dhe për të mos u frikësuar nga ndryshimet. Sot keni mundësi të investoni bashkë me mua dhe të merrni fitim të dyfishtë. Qoftë kjo ditë t’ju dhurojë gëzim arritjesh dhe besim në forcën tuaj!",
    6: "Ju uroj harmoni dhe qetësi, që çdo moment të sjellë kënaqësi dhe siguri. Sot mund të investoni bashkë me mua dhe të merrni fitim pa komisionin tim — dhurata ime për ju. Qoftë kjo ditë e mbushur me paqe, gëzim dhe mundësi të reja!",
    7: "Ju uroj energji të pashtershme dhe forcë, që ecja përpara të sjellë gëzim dhe siguri. Sot keni mundësi të investoni dhe të përfitoni me zbritje 10% në depozitë. Qoftë kjo ditë hap drejt shëndetit, suksesit dhe arritjeve të reja!",
    8: "Ju uroj shëndet të fortë dhe buzëqeshje të shpeshta, që çdo ditë të jetë e ndriçuar. Sot ju dhuroj strategjinë “Milioner” — shans që me depozitë minimale të arrini të ardhura të larta. Qoftë kjo ditë t’ju sjellë lumturi, mirëqenie dhe besim në të ardhmen!",
    9: "Ju uroj zbulime dhe horizonte të reja, që jeta t’ju japë frymëzim dhe gëzim. Sot keni mundësi të investoni bashkë me mua dhe të merrni fitim të dyfishtë. Qoftë kjo ditë fillimi i udhëtimeve të mrekullueshme dhe fitoreve të reja!",
    10: "Ju uroj krijimtari dhe frymëzim, që çdo ide të shndërrohet në rezultat të bukur. Sot mund të investojmë bashkë dhe do të merrni fitim pa komisionin tim. Qoftë kjo ditë burim suksesi dhe arritjesh të reja!",
    11: "Ju uroj mundësi të reja dhe besim në realizimin e tyre, që çdo hap të jetë i vetëdijshëm dhe i fortë. Sot keni shansin të vendosni mjete me zbritje 10% në depozitë — dhurata ime për ju. Qoftë kjo ditë t’ju sjellë perspektiva dhe besim në të ardhmen!",
    12: "Ju uroj guxim dhe vendosmëri, që ëndrrat të shndërrohen në realitet. Sot ju dhuroj strategjinë “Milioner” — mundësi që me depozitë minimale të arrini të ardhura të larta. Qoftë kjo ditë hap drejt fitoreve të mëdha dhe arritjeve të reja!",
    13: "Ju uroj gëzim në komunikim dhe mbështetje, që çdo ditë të jetë e mbushur me ngrohtësi dhe miqësi. Sot keni mundësi të investoni bashkë me mua dhe të merrni fitim të dyfishtë. Qoftë kjo ditë t’ju dhurojë lumturi dhe besim në të ardhmen!",
    14: "Ju uroj motivim dhe frymëzim për të ecur përpara dhe për të arritur maja të reja. Sot mund të investojmë bashkë dhe do të merrni fitim pa komisionin tim. Qoftë kjo ditë fillim arritjesh të ndritshme dhe ngjarjesh të gëzueshme!",
    15: "Ju uroj lidhje të forta dhe njohje të reja që sjellin gëzim dhe mbështetje. Sot keni mundësi të investoni me zbritje 10% në depozitë. Qoftë kjo ditë hap drejt suksesit dhe mundësive të reja!",
    16: "Ju uroj qartësi mendimi dhe besim në marrjen e vendimeve. Qoftë çdo ditë e re t’ju sjellë mirëkuptim dhe ide të ndritshme. Sot keni mundësi të vendosni mjete dhe të merrni fitim — dhurata ime për ju. Qoftë kjo ditë fillim i një rruge të suksesshme!",
    17: "Ju uroj durim dhe këmbëngulje, që të kapërceni çdo pengesë në rrugën tuaj. Sot mund të investojmë bashkë dhe do të merrni fitim me normë të rritur. Qoftë kjo ditë hap drejt ëndrrave tuaja!",
    18: "Ju uroj dashuri dhe respekt në rrethin tuaj, që çdo çast të jetë i mbushur me mbështetje dhe mirëkuptim. Sot keni mundësi të vendosni mjete me bonus — dhurata ime për ju. Qoftë kjo ditë t’ju sjellë gëzim dhe harmoni në jetë!",
    19: "Ju uroj pozitivitet dhe optimizëm, që çdo ditë të jetë e mbushur me momente të ndritshme. Sot mund të investojmë bashkë dhe do të merrni fitim pa asnjë shpenzim. Qoftë kjo ditë fillimi i një të ardhmeje të ndritshme!",
    20: "Ju uroj forcë shpirtërore dhe besim në veten, që të realizoni të gjitha ëndrrat tuaja. Sot keni shansin të vendosni mjete me kthim të garantuar — dhurata ime për ju. Qoftë kjo ditë fillimi i arritjeve tuaja të mëdha!"
  };

  let openedGiftNumber = localStorage.getItem("openedGift");
  const grid = document.getElementById("giftGrid");
  const lockBanner = document.getElementById("lockBanner");

  // создаём кнопки
  for (let i = 1; i <= 20; i++) {
    const btn = document.createElement("button");
    btn.className = "gift-btn";
    btn.textContent = `PODAROK ${i}`;
    btn.dataset.num = i;

    if (openedGiftNumber && Number(openedGiftNumber) !== i) {
      btn.disabled = true;
    }

    btn.onclick = () => {
      if (!openedGiftNumber) {
        openedGiftNumber = i;
        localStorage.setItem("openedGift", i);
        showMessage(i);
        disableOthers(i);
      } else if (Number(openedGiftNumber) === i) {
        showMessage(i); // повторный просмотр своего подарка
      } else {
        alert("Ju keni hapur tashmë dhuratën tuaj. Të tjerat janë të bllokuara.");
      }
    };
    grid.appendChild(btn);
  }

  // показ сообщения в модальном окне
  function showMessage(num) {
    const msg = messages[num];
    const modal = document.getElementById("giftModal");
    const text = document.getElementById("giftText");
    text.textContent = msg;
    modal.style.display = "block";

    // обновляем баннер-индикатор
    lockBanner.style.display = "block";
    lockBanner.textContent = `Ju keni hapur: PODAROK ${num}. Mund ta shihni përsëri sa herë të dëshironi.`;
  }

  function disableOthers(num) {
    document.querySelectorAll(".gift-btn").forEach(btn => {
      if (Number(btn.dataset.num) !== num) btn.disabled = true;
    });
  }

  // закрытие модального окна по крестику
  document.getElementById("closeModal").onclick = function() {
    document.getElementById("giftModal").style.display = "none";
  };

  // закрытие по клику вне окна
  window.onclick = function(event) {
    const modal = document.getElementById("giftModal");
    if (event.target === modal) {
      modal.style.display = "none";
    }
  };

  // при загрузке страницы показываем свой подарок снова (если был открыт)
  if (openedGiftNumber) {
    showMessage(Number(openedGiftNumber));
    disableOthers(Number(openedGiftNumber));
  }
</script>

</body>
</html>
