<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Editable AI Template</title>

<!-- html2canvas + jsPDF for PDF/JPG -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

<style>
body { font-family: Arial, sans-serif; background:#f1f1f1; padding:20px; }
#controls { margin-bottom:15px; display:flex; flex-wrap:wrap; gap:10px; }
#templateArea {
  background:white; padding:20px; max-width:900px;
  margin:auto; box-shadow:0 0 10px rgba(0,0,0,0.2);
}
table { width:100%; border-collapse:collapse; margin-top:10px; }
td,th { border:1px solid #888; padding:8px; }
.editable { padding:3px; border:1px dashed transparent; }
.editable:focus { border-color:red; outline:none; background:#fff7f7; }
button { padding:8px 12px; cursor:pointer; }
</style>

</head>
<body>

<div id="controls">
  <input type="color" id="bgcolor" title="Background Color">
  <input type="number" id="fontsize" min="10" max="40" value="16" title="Font Size">
  <button onclick="applyStyle()">Apply Style</button>
  <button onclick="downloadPDF()">Download PDF</button>
  <button onclick="downloadJPG()">Download JPG</button>
</div>

<div id="templateArea">

  <h1 class="editable" contenteditable="true">Latest Update Title</h1>
  <p><b>Author:</b> <span class="editable" contenteditable="true">Author Name</span></p>

  <h2>Important Dates</h2>
  <table>
    <tr><th>Event</th><th>Date</th></tr>
    <tr>
      <td class="editable" contenteditable="true">Start Date</td>
      <td class="editable" contenteditable="true">DD/MM/YYYY</td>
    </tr>
    <tr>
      <td class="editable" contenteditable="true">End Date</td>
      <td class="editable" contenteditable="true">DD/MM/YYYY</td>
    </tr>
    <tr>
      <td class="editable" contenteditable="true">Result</td>
      <td class="editable" contenteditable="true">DD/MM/YYYY</td>
    </tr>
  </table>

  <h2>Application Fee</h2>
  <p class="editable" contenteditable="true">00</p>

  <h2>Address & Contact</h2>
  <p class="editable" contenteditable="true">Mobile: 0000000000</p>
  <p class="editable" contenteditable="true">Address: Edit your address here</p>

  <h2>Video (Embed any iframe)</h2>
  <div class="editable" contenteditable="true">
    Paste YouTube iframe here (optional)
  </div>

</div>

<script>

function applyStyle(){
  document.getElementById("templateArea").style.background =
    document.getElementById("bgcolor").value;
  document.getElementById("templateArea").style.fontSize =
    document.getElementById("fontsize").value + "px";
}

async function downloadPDF(){
  const area = document.getElementById("templateArea");
  const canvas = await html2canvas(area, {scale:2});
  const imgData = canvas.toDataURL("image/png");

  const { jsPDF } = window.jspdf;
  const pdf = new jsPDF("p","pt","a4");

  const width = pdf.internal.pageSize.getWidth();
  const height = (canvas.height * width) / canvas.width;
  pdf.addImage(imgData,"PNG",0,0,width,height);
  pdf.save("document.pdf");
}

async function downloadJPG(){
  const area = document.getElementById("templateArea");
  const canvas = await html2canvas(area, {scale:2});
  const img = canvas.toDataURL("image/jpeg",1.0);

  const link = document.createElement("a");
  link.href = img;
  link.download = "template.jpg";
  link.click();
}

</script>

</body>
</html>
