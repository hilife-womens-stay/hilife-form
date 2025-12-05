# hilife-form
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Hi Life Premium Womens Stay – Admission Form</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <!-- Fonts & jsPDF -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap" rel="stylesheet">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

  <!-- CropperJS -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.13/cropper.min.css">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.13/cropper.min.js"></script>

  <style>
    body {
      margin: 0;
      font-family: Poppins, Arial, sans-serif;
      background: linear-gradient(135deg, #7b3fe0, #f97316);
      padding: 20px;
      display: flex;
      justify-content: center;
    }
    .container {
      background: #ffffff;
      max-width: 900px;
      width: 100%;
      border-radius: 18px;
      padding: 20px;
      box-shadow: 0 0 30px rgba(0,0,0,.45);
    }
    h2 {
      background: #7b3fe0;
      color: #fff;
      padding: 8px;
      text-align: center;
      border-radius: 6px;
      font-size: 1rem;
    }
    input, textarea, select {
      width: 100%;
      padding: 10px;
      border-radius: 10px;
      border: 1px solid #b9a9ff;
      margin-bottom: 12px;
      background: #fafaff;
      font-size: 0.9rem;
    }
    .grid-2 {
      display: grid;
      grid-template-columns: repeat(2,1fr);
      gap: 12px;
    }
    .grid-3 {
      display: grid;
      grid-template-columns: repeat(3,1fr);
      gap: 12px;
    }
    button {
      width: 100%;
      padding: 14px;
      margin-top: 16px;
      border-radius: 999px;
      border: none;
      background: #4b3de0;
      color: white;
      font-size: 1rem;
      box-shadow: 0 8px 20px rgba(0,0,0,.35);
      font-weight: 600;
    }
    .fname {
      font-size: 0.75rem;
      margin-top: -6px;
      margin-bottom: 10px;
      color: #444;
    }

    /* Crop modal */
    #cropOverlay {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,.7);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 9999;
    }
    .cropWindow {
      background: white;
      padding: 12px;
      border-radius: 12px;
      max-width: 430px;
      width: 92%;
      box-shadow: 0 10px 30px rgba(0,0,0,0.4);
    }
    #cropImage {
      max-width: 100%;
      max-height: 60vh;
      display: block;
      margin: 0 auto;
    }

    /* WhatsApp popup */
    #waBox {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,.7);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 9999;
    }
  </style>
</head>

<body>
<div class="container">
  <h2>HI LIFE PREMIUM WOMENS STAY — ADMISSION FORM</h2>

  <div class="grid-2">
    <input id="fullName" placeholder="Full Name *">
    <input id="parentName" placeholder="Parent Name *">
  </div>

  <div class="grid-2">
    <input id="mobile" placeholder="Contact Number *">
    <input id="parentMobile" placeholder="Parent Contact Number *">
  </div>

  <div class="grid-3">
    <input id="age" placeholder="Age *">
    <input id="roomNo" placeholder="Room No *">
    <input type="date" id="dateOfJoining">
  </div>

  <div class="grid-2">
    <input id="deposit" placeholder="Deposit Amount *">
    <select id="keysReceived">
      <option value="">Almari Keys Received *</option>
      <option>YES</option>
      <option>NO</option>
    </select>
  </div>

  <input id="qualification" placeholder="Educational Qualification *">
  <textarea id="workAddress" placeholder="Working Place & Address *"></textarea>
  <textarea id="permanentAddress" placeholder="Permanent Address *"></textarea>

  <h2>Upload Photos</h2>

  <label>Profile Photo *</label>
  <input type="file" id="profilePhoto" accept="image/*">
  <div id="pName" class="fname"></div>

  <label>Aadhaar Front *</label>
  <input type="file" id="aadharFront" accept="image/*">
  <div id="a1Name" class="fname"></div>

  <label>Aadhaar Back *</label>
  <input type="file" id="aadharBack" accept="image/*">
  <div id="a2Name" class="fname"></div>

  <button id="btnPDF">Generate PDF</button>
</div>

<!-- Cropper popup -->
<div id="cropOverlay">
  <div class="cropWindow">
    <h3 id="cropTitle" style="margin:4px 0 8px;text-align:center;"></h3>
    <img id="cropImage">
    <div style="display:flex;gap:10px;margin-top:10px;">
      <button id="btnCropCancel"
              style="flex:1;padding:10px;background:#aaa;border:none;border-radius:50px;color:white;">
        Cancel
      </button>
      <button id="btnCropApply"
              style="flex:1;padding:10px;background:#4b3de0;border:none;border-radius:50px;color:white;">
        Save
      </button>
    </div>
  </div>
</div>

<!-- WhatsApp share popup -->
<div id="waBox">
  <div style="background:white;padding:18px;border-radius:14px;text-align:center;width:92%;max-width:350px;font-family:Poppins;">
    <h3 style="margin:0 0 8px;">Send PDF to Hostel via WhatsApp</h3>
    <p style="font-size:0.9rem;margin-bottom:16px;">
      PDF is downloaded. Tap a number to open WhatsApp and attach the PDF.
    </p>
    <button id="wa1"
            style="width:100%;padding:12px;margin-bottom:10px;border:none;border-radius:50px;background:#25D366;color:white;font-size:1rem;">
      WhatsApp → 9177721778
    </button>
    <button id="wa2"
            style="width:100%;padding:12px;border:none;border-radius:50px;background:#25D366;color:white;font-size:1rem;">
      WhatsApp → 9347938065
    </button>
    <button id="waClose"
            style="width:100%;padding:10px;margin-top:12px;border:none;border-radius:50px;background:#777;color:white;">
      Close
    </button>
  </div>
</div>

<script>
  const { jsPDF } = window.jspdf;

  let P1 = null, A1 = null, A2 = null;  // cropped images
  let cropper = null;
  let cropTarget = null;

  const profileInput = document.getElementById("profilePhoto");
  const aadharFrontInput = document.getElementById("aadharFront");
  const aadharBackInput = document.getElementById("aadharBack");
  const cropOverlay = document.getElementById("cropOverlay");
  const cropImage = document.getElementById("cropImage");
  const cropTitle = document.getElementById("cropTitle");
  const pName = document.getElementById("pName");
  const a1Name = document.getElementById("a1Name");
  const a2Name = document.getElementById("a2Name");

  function openCropper(file, target) {
    cropTarget = target;
    const reader = new FileReader();
    reader.onload = e => {
      cropImage.src = e.target.result;
      cropImage.onload = () => {
        if (cropper) {
          cropper.destroy();
        }
        cropper = new Cropper(cropImage, {
          viewMode: 1,
          dragMode: 'move',
          autoCropArea: 0.9,
          aspectRatio: target === 'profile' ? 3 / 4 : NaN
        });
        cropTitle.textContent =
          target === 'profile' ? "Crop Profile Photo" :
          target === 'aadharFront' ? "Crop Aadhaar Front" :
          "Crop Aadhaar Back";
        cropOverlay.style.display = "flex";
      };
    };
    reader.readAsDataURL(file);
  }

  profileInput.onchange = () => {
    if (profileInput.files[0]) {
      pName.textContent = profileInput.files[0].name;
      openCropper(profileInput.files[0], 'profile');
    }
  };

  aadharFrontInput.onchange = () => {
    if (aadharFrontInput.files[0]) {
      a1Name.textContent = aadharFrontInput.files[0].name;
      openCropper(aadharFrontInput.files[0], 'aadharFront');
    }
  };

  aadharBackInput.onchange = () => {
    if (aadharBackInput.files[0]) {
      a2Name.textContent = aadharBackInput.files[0].name;
      openCropper(aadharBackInput.files[0], 'aadharBack');
    }
  };

  document.getElementById("btnCropCancel").onclick = () => {
    if (cropper) cropper.destroy();
    cropper = null;
    cropOverlay.style.display = "none";
  };

  document.getElementById("btnCropApply").onclick = () => {
    if (!cropper || !cropTarget) return;
    const canvas = cropper.getCroppedCanvas({
      maxWidth: 1400,
      maxHeight: 1400
    });
    const dataURL = canvas.toDataURL("image/png", 1.0);
    if (cropTarget === 'profile') P1 = dataURL;
    if (cropTarget === 'aadharFront') A1 = dataURL;
    if (cropTarget === 'aadharBack') A2 = dataURL;
    cropper.destroy();
    cropper = null;
    cropTarget = null;
    cropOverlay.style.display = "none";
  };

  function openWAOptions(applicantName) {
    const waBox = document.getElementById("waBox");
    waBox.style.display = "flex";

    const msg =
      "Hello, I have completed the admission form.%0A" +
      "Applicant Name: " + encodeURIComponent(applicantName) + "%0A" +
      "I am attaching the admission PDF.";

    document.getElementById("wa1").onclick = () => {
      window.location.href = "https://wa.me/919177721778?text=" + msg;
    };
    document.getElementById("wa2").onclick = () => {
      window.location.href = "https://wa.me/919347938065?text=" + msg;
    };
  }

  document.getElementById("waClose").onclick = () => {
    document.getElementById("waBox").style.display = "none";
  };

  document.getElementById("btnPDF").onclick = () => {
    const d = id => document.getElementById(id).value.trim();
    let missing = [];

    ["fullName","parentName","qualification",
     "workAddress","permanentAddress",
     "age","roomNo","dateOfJoining"].forEach(f => {
      if (!d(f)) missing.push(f);
    });

    if (!/^\d{10}$/.test(d("mobile"))) missing.push("mobile (10 digit)");
    if (!/^\d{10}$/.test(d("parentMobile"))) missing.push("parentMobile (10 digit)");
    if (!d("deposit")) missing.push("deposit");
    if (!d("keysReceived")) missing.push("keysReceived");
    if (!P1) missing.push("Profile photo (crop & save)");
    if (!A1) missing.push("Aadhaar front (crop & save)");
    if (!A2) missing.push("Aadhaar back (crop & save)");

    if (missing.length) {
      alert("Please complete:\n" + missing.join("\n"));
      return;
    }

    const pdf = new jsPDF("p","mm","a4");
    const W = pdf.internal.pageSize.getWidth();
    const H = pdf.internal.pageSize.getHeight();
    const X = 16, Y = 14;
    let y = Y;

    // Page 1 border
    pdf.setLineWidth(0.7);
    pdf.rect(6, 6, W - 12, H - 12);

    // Header
    pdf.setFont("times", "bold");
    pdf.setFontSize(16);
    pdf.text("HI LIFE PREMIUM WOMENS STAY", X + 2, y + 8);
    pdf.setFontSize(12);
    pdf.text("ADMISSION FORM", X + 2, y + 14);

    // Profile photo
    pdf.rect(W - 50, y + 2, 38, 50);
    if (P1) pdf.addImage(P1, "PNG", W - 49, y + 3, 36, 48);
    y += 50;

    pdf.setFont("times", "normal");
    pdf.setFontSize(12);

    // Basic details
    pdf.text("Name: " + d("fullName"), X, y);
    pdf.text("Parent Name: " + d("parentName"), X, y + 10);
    y += 26;

    pdf.text("Contact: " + d("mobile"), X, y);
    pdf.text("Parent Contact: " + d("parentMobile"), X, y + 10);
    y += 26;

    pdf.text("Age: " + d("age"), X, y);
    pdf.text("Room No: " + d("roomNo"), X + 45, y);
    pdf.text("Date of Joining: " + d("dateOfJoining"), X + 100, y);
    y += 12;

    pdf.text("Deposit Amt: ₹" + d("deposit"), X, y);
    pdf.text("Keys Received: " + d("keysReceived"), X + 90, y);
    y += 18;

    pdf.text("Educational Qualification:", X, y);
    y += 10;
    pdf.text(d("qualification"), X + 8, y);
    y += 22;

    pdf.text("Working Address:", X, y);
    y += 8;
    pdf.splitTextToSize(d("workAddress"), 178).forEach(line => {
      pdf.text(line, X + 8, y);
      y += 8;
    });
    y += 6;

    pdf.text("Permanent Address:", X, y);
    y += 8;
    pdf.splitTextToSize(d("permanentAddress"), 178).forEach(line => {
      pdf.text(line, X + 8, y);
      y += 8;
    });
    y += 8;

    // Aadhaar images
    pdf.text("Aadhaar Front", X, y);
    pdf.text("Aadhaar Back", X + 100, y);

    pdf.rect(X, y + 2, 88, 50);
    pdf.rect(X + 100, y + 2, 88, 50);
    if (A1) pdf.addImage(A1, "PNG", X + 1, y + 3, 86, 48);
    if (A2) pdf.addImage(A2, "PNG", X + 101, y + 3, 86, 48);

    // Page 2 - Rules
    pdf.addPage();
    pdf.setLineWidth(0.7);
    pdf.rect(6, 6, W - 12, H - 12);

    y = 20;
    pdf.setFont("times", "bold");
    pdf.setFontSize(14);
    pdf.text("RULES & REGULATIONS:", X, y);
    y += 10;

    pdf.setFont("times", "normal");
    pdf.setFontSize(12);
    const rules = [
      "Rent must be paid by 5th of every month",
      "Visitors are not allowed in rooms without owner's permission – Fine ₹1000",
      "Advance + current month rent must be paid at the time of joining",
      "After completion of stay, guest charges per day: ₹150 (1 share) / ₹500 (3 share) / ₹600 (2 share)",
      "Tenant must give 30 days' notice before vacating or pay 30 days rent",
      "Maintenance fee: ₹1000 (3 & 4 sharing) / ₹1500 (2 sharing)",
      "Damage to property will be recovered from the guest",
      "Lost keys must be replaced at guest's cost",
      "Payments are non-refundable and non-transferable",
      "Rent will not be reduced for absent days",
      "Each month is counted as 30 days (1st to 30th)",
      "Keep noise levels low for others' comfort",
      "Use dustbins for waste disposal",
      "Wall stickers and smoking are not allowed in rooms",
      "Misbehavior or illegal activity leads to immediate action",
      "Alcohol and smoking are strictly prohibited in the hostel",
      "Deposit is refunded on departure and not adjusted against rent",
      "Electricity charges are based on prepaid sub-meter readings",
      "Management is not responsible for loss/theft of cash, gold, laptop, mobile or any valuables",
      "If rules are not followed, management has the right to terminate without notice"
    ];

    rules.forEach(r => {
      const txt = pdf.splitTextToSize("• " + r, 178);
      pdf.text(txt, X, y);
      y += txt.length * 6;
    });

    y += 16;
    pdf.setFont("times", "bold");
    pdf.text("I have read and agree to follow all the above Rules & Regulations.", X, y);
    y += 18;
    pdf.line(W - 90, y, W - 20, y);
    pdf.text("Signature of Candidate", (W - 90 + W - 20)/2, y + 6, { align: "center" });

    const fname = d("fullName") || "Admission_Form";
    pdf.save(fname + ".pdf");

    // After download completes, open WhatsApp options
    setTimeout(() => openWAOptions(fname), 800);
  };
</script>
</body>
</html>
