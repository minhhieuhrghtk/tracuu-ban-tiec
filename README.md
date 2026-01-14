# tracuu-ban-tiec
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <title>Tra cứu bàn tiệc</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #74ebd5, #acb6e5);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .card {
      background: #ffffff;
      padding: 28px;
      border-radius: 16px;
      width: 100%;
      max-width: 420px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.15);
      animation: fadeIn 0.5s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    h1 {
      text-align: center;
      margin-bottom: 8px;
    }
    .subtitle {
      text-align: center;
      color: #666;
      margin-bottom: 20px;
      font-size: 14px;
    }
    input {
      width: 100%;
      padding: 12px;
      font-size: 16px;
      margin-bottom: 12px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }
    button {
      width: 100%;
      padding: 12px;
      font-size: 16px;
      background: #4f46e5;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover {
      background: #4338ca;
    }
    .result {
      margin-top: 18px;
      font-size: 16px;
      text-align: center;
    }
    .success {
      background: #ecfeff;
      padding: 12px;
      border-radius: 10px;
      margin-top: 12px;
    }
    .error {
      color: red;
      margin-top: 12px;
    }
    footer {
      margin-top: 18px;
      text-align: center;
      font-size: 12px;
      color: #999;
    }
  </style>
</head>
<body>
  <div class="card">
    <h1>Tra cứu bàn tiệc</h1>
    <div class="subtitle">Nhập user để biết vị trí ngồi & số may mắn</div>
    <details style="margin-bottom:12px;">
      <summary style="cursor:pointer;">📋 Dán dữ liệu từ Excel (CSV)</summary>
      <textarea id="csvInput" rows="4" style="width:100%;margin-top:8px;" placeholder="user,ban,mayman
ngoc,5,12"></textarea>
      <button style="margin-top:8px;background:#059669" onclick="napCSV()">Nạp dữ liệu</button>
    </details>

    <input 
      type="text" 
      id="username" 
      placeholder="Ví dụ: an, binh, chi..." 
      onkeydown="if(event.key==='Enter') traCuu()"
    />

    <button onclick="traCuu()">Tra cứu</button>

    <div class="result" id="result"></div>

    <footer>
      Phần mềm miễn phí – dùng offline & online
    </footer>
  </div>

  <script>
    // ===== DỮ LIỆU MẪU =====
    const data = {
      "an": { ban: 1, mayMan: 23 },
      "binh": { ban: 2, mayMan: 7 },
      "chi": { ban: 3, mayMan: 18 },
      "dung": { ban: 4, mayMan: 9 }
    };

    function napCSV() {
      const text = document.getElementById('csvInput').value.trim();
      if (!text) return alert('Chưa có dữ liệu CSV');
      const lines = text.split(/
/);
      lines.forEach(line => {
        const [user, ban, mayMan] = line.split(',');
        if (user && ban && mayMan) {
          data[user.trim().toLowerCase()] = { ban: ban.trim(), mayMan: mayMan.trim() };
        }
      });
      alert('Đã nạp dữ liệu thành công!');
    }

    function traCuu() {
      const user = document.getElementById("username").value.trim().toLowerCase();
      const resultDiv = document.getElementById("result");

      if (!user) {
        resultDiv.innerHTML = '<div class="error">Vui lòng nhập user.</div>';
        return;
      }

      if (data[user]) {
        resultDiv.innerHTML = `
          <div class="success">
            🎉 <b>Xin chào ${user}</b><br><br>
            🪑 Bạn ngồi tại <b>Bàn ${data[user].ban}</b><br>
            🍀 Số thứ tự may mắn: <b>${data[user].mayMan}</b>
          </div>
        `;
      } else {
        resultDiv.innerHTML = '<div class="error">❌ Không tìm thấy user này.</div>';
      }
    }
  </script>
</body>
</html>
