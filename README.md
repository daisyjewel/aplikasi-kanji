# aplikasi-kanji
kanji katakana full
<!DOCTYPE html>
<html>
<head>
  <style>
    body { font-family: sans-serif; display: flex; flex-direction: column; align-items: center; background: #f0f2f5; }
    h2 { color: #333; }
    canvas { border: 3px solid #333; background: white; border-radius: 10px; cursor: crosshair; }
    button { margin-top: 15px; padding: 10px 20px; font-size: 16px; background: #ff4757; color: white; border: none; border-radius: 5px; cursor: pointer; }
  </style>
</head>
<body>

  <h2>Papan Tulis Kanji Desy 🖌️</h2>
  <p>Coba coret-coret pakai mouse atau jarimu di bawah ini:</p>
  
  <canvas id="canvas" width="350" height="350"></canvas>
  <br>
  <button onclick="hapusLayar()">Hapus Layar</button>

  <script>
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    let melukis = false;

    // Atur tebal dan warna garis
    ctx.lineWidth = 5;
    ctx.lineCap = 'round';
    ctx.strokeStyle = '#2f3542';

    function mulaiPosisi(e) {
      melukis = true;
      gambar(e);
    }
    function selesaiPosisi() {
      melukis = false;
      ctx.beginPath();
    }
    function gambar(e) {
      if (!melukis) return;
      
      // Mendukung layar sentuh HP & Mouse komputer
      let clientX = e.touches ? e.touches[0].clientX : e.clientX;
      let clientY = e.touches ? e.touches[0].clientY : e.clientY;
      
      let rect = canvas.getBoundingClientRect();
      ctx.lineTo(clientX - rect.left, clientY - rect.top);
      ctx.stroke();
      ctx.beginPath();
      ctx.moveTo(clientX - rect.left, clientY - rect.top);
    }

    // Event Listener untuk Mouse dan Touch Screen
    canvas.addEventListener('mousedown', mulaiPosisi);
    canvas.addEventListener('mouseup', selesaiPosisi);
    canvas.addEventListener('mousemove', gambar);
    canvas.addEventListener('touchstart', mulaiPosisi);
    canvas.addEventListener('touchend', selesaiPosisi);
    canvas.addEventListener('touchmove', gambar);

    function hapusLayar() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    }
  </script>

</body>
</html>
