# Website-Kredit-Scoring
Kredit Scoring Kelompok 9

<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Simulasi Kredit Skoring nana</title>
  <style>
    body {
      font-family: 'Times New Roman', Times, serif;
      margin: 20px;
    }
    .container {
      max-width: 500px;
      margin: auto;
      padding: 20px;
      border: 1px solid #ff78d0;
      border-radius: 10px;
    }
    h2, h3 {
      color: black;
      text-align: center;
    }
    label {
      font-weight: bold;
    }
    input, select {
      width: 100%;
      padding: 8px;
      margin-bottom: 15px;
      border-radius: 5px;
      border: 1px solid #d10092;
      box-sizing: border-box;
    }
    button {
      width: 48%;
      padding: 10px;
      background-color: #d10092;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 10px;
    }
    button.reset {
      background-color: #555;
    }
    #hasilBox {
      margin-top: 20px;
      padding: 15px;
      border-radius: 10px;
      background-color: #f5f5f5;
      display: none;
    }
    .rekomendasi-ditolak {
      color: red;
      font-weight: bold;
    }
    .rekomendasi-disetujui {
      color: green;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Mirasa Credit Scoring</h2>
    <p style="text-align:center;">Prediksi kelayakan kredit berdasarkan parameter by kelompok 9.</p>

    <h3>Informasi Pribadi</h3>
    <label>Nama Lengkap:</label>
    <input type="text" id="nama" placeholder="Contoh: mirna asri agustina">

    <label>Alamat Lengkap:</label>
    <input type="text" id="alamat" placeholder="Contoh: sukoharjo">

    <label>Nomor KTP:</label>
    <input type="text" id="ktp" placeholder="Contoh: 3201234567890001">

    <label>Nomor HP:</label>
    <input type="text" id="hp" placeholder="Contoh: 081234567890">

    <label>Email:</label>
    <input type="email" id="email" placeholder="Contoh: mirnaasri@email.com">

    <h3>Formulir Simulasi Skor Kredit</h3>

    <label>Usia:</label>
    <select id="usia">
      <option value="3">21–30 tahun</option>
      <option value="2">31–40 tahun</option>
      <option value="1">&gt;40 tahun</option>
    </select>

    <label>Pendapatan Bulanan:</label>
    <select id="pendapatan">
      <option value="1">Kurang dari 5 juta</option>
      <option value="2">5 – 7 juta</option>
      <option value="3">7 – 10 juta</option>
      <option value="4">Lebih dari 10 juta</option>
    </select>

    <label>Status Pekerjaan:</label>
    <select id="pekerjaan">
      <option value="4">Karyawan Tetap</option>
      <option value="3">Wiraswasta</option>
      <option value="2">Karyawan Kontrak</option>
    </select>

    <label>Pendidikan:</label>
    <select id="pendidikan">
      <option value="3">S1 / S2 / lebih tinggi</option>
      <option value="2">SMA / sederajat</option>
      <option value="1">SMP ke bawah</option>
    </select>

    <label>Status Pernikahan:</label>
    <select id="status">
      <option value="2">Menikah</option>
      <option value="1">Belum menikah / Cerai</option>
    </select>

    <label>Riwayat Kredit:</label>
    <select id="riwayat">
      <option value="4">Baik</option>
      <option value="1">Buruk</option>
    </select>

    <label>Jumlah Akun Kredit Aktif:</label>
    <select id="akun">
      <option value="2">1–3</option>
      <option value="1">&gt;3</option>
      <option value="0">0</option>
    </select>

    <label>Lama Riwayat Kredit (tahun):</label>
    <select id="lama">
      <option value="3">&gt;3 tahun</option>
      <option value="2">1–3 tahun</option>
      <option value="1">&lt;1 tahun</option>
    </select>

    <label>Pengajuan Kredit Baru (6 bulan terakhir):</label>
    <select id="pengajuan">
      <option value="2">0–2 kali</option>
      <option value="1">&gt;2 kali</option>
    </select>

    <label>Jenis Kredit:</label>
    <select id="jenis">
      <option value="2">Instalmen (KPR, motor)</option>
      <option value="1">Revolving (kartu kredit)</option>
    </select>

    <label>Total Cicilan Eksisting:</label>
    <input type="number" id="cicilan" placeholder="Misal: 1000000">

    <label>Total Pendapatan Bulanan:</label>
    <input type="number" id="dtiPendapatan" placeholder="Misal: 5000000">

    <label>Jumlah Permohonan Kredit (Rp):</label>
    <input type="number" id="jumlahKredit" placeholder="Misal: 10000000">

    <label>Jangka Waktu Kredit (bulan):</label>
    <input type="number" id="jangkaWaktu" placeholder="Misal: 12">

    <label>Jenis Agunan:</label>
    <input type="text" id="jenisAgunan" placeholder="Misal: BPKB Motor, Sertifikat Rumah">

    <label>Nilai Agunan (Rp):</label>
    <input type="number" id="nilaiAgunan" placeholder="Misal: 15000000">

    <div style="display:flex; justify-content: space-between;">
      <button onclick="hitungSkor()">Hitung Skor PENGAJUAN</button>
      <button class="reset" onclick="resetForm()">Reset</button>
    </div>

    <div id="hasilBox">
      <h4 style="color:pink;">✅ Hasil Simulasi Skor Anda</h4>
      <p id="hasilSkor" style="margin: 0; font-weight: bold;"></p>
      <div id="rincianSkor" style="margin-top:10px;"></div>
    </div>
  </div>

  <script>
    function hitungSkor() {
      const nama = document.getElementById("nama").value || "-";
      const alamat = document.getElementById("alamat").value || "-";
      const ktp = document.getElementById("ktp").value || "-";
      const hp = document.getElementById("hp").value || "-";
      const email = document.getElementById("email").value || "-";
      const jenisAgunan = document.getElementById("jenisAgunan").value || "-";
      const nilaiAgunan = parseFloat(document.getElementById("nilaiAgunan").value) || 0;
      const usia = parseInt(document.getElementById("usia").value);
      const pendapatan = parseInt(document.getElementById("pendapatan").value);
      const pekerjaan = parseInt(document.getElementById("pekerjaan").value);
      const pendidikan = parseInt(document.getElementById("pendidikan").value);
      const status = parseInt(document.getElementById("status").value);
      const riwayat = parseInt(document.getElementById("riwayat").value);
      const akun = parseInt(document.getElementById("akun").value);
      const lama = parseInt(document.getElementById("lama").value);
      const pengajuan = parseInt(document.getElementById("pengajuan").value);
      const jenis = parseInt(document.getElementById("jenis").value);
      const cicilan = parseFloat(document.getElementById("cicilan").value) || 0;
      const dtiPendapatan = parseFloat(document.getElementById("dtiPendapatan").value) || 1;
      const jumlahKredit = parseFloat(document.getElementById("jumlahKredit").value) || 0;
      const jangkaWaktu = parseInt(document.getElementById("jangkaWaktu").value) || 0;

      const dti = cicilan / dtiPendapatan;
      const dtiPersen = (dti * 100).toFixed(2) + "%";
      let skorDTI = 0;
      if (dti < 0.2) skorDTI = 4;
      else if (dti < 0.36) skorDTI = 3;
      else if (dti <= 0.5) skorDTI = 2;
      else skorDTI = 1;

      let skor = usia + pendapatan + pekerjaan + pendidikan + status + riwayat + akun + lama + pengajuan + jenis + skorDTI;

      const kategori = skor >= 30 ? "Sangat Baik ✅" :
                       skor >= 25 ? "Baik 👍" :
                       skor >= 18 ? "Cukup 😐" : "Buruk ❌";

      const rekomendasi = skor >= 25
        ? "<span class='rekomendasi-disetujui'>DISETUJUI ✅</span>"
        : "<span class='rekomendasi-ditolak'>TIDAK DISETUJUI ❌</span>";

      document.getElementById("hasilSkor").innerHTML = `Skor Kredit Anda: ${skor} – ${kategori}<br>Rekomendasi: ${rekomendasi}`;

      const rincian = `
        <ul>
          <li>Usia: ${usia}</li>
          <li>Pendapatan: ${pendapatan}</li>
          <li>Status Pekerjaan: ${pekerjaan}</li>
          <li>Pendidikan: ${pendidikan}</li>
          <li>Status Pernikahan: ${status}</li>
          <li>Riwayat Kredit: ${riwayat}</li>
          <li>Jumlah Akun Kredit Aktif: ${akun}</li>
          <li>Lama Riwayat Kredit: ${lama}</li>
          <li>Pengajuan Kredit Baru: ${pengajuan}</li>
          <li>Jenis Kredit: ${jenis}</li>
          <li>DTI: ${dtiPersen} (Skor: ${skorDTI})</li>
          <li>Jumlah Permohonan Kredit: Rp ${jumlahKredit.toLocaleString("id-ID")}</li>
          <li>Jangka Waktu Kredit: ${jangkaWaktu} bulan</li>
        </ul>
      `;
      const detailNasabah = `
        <h4 style="margin-top:20px; color:#d10092;">📄 Data Diri & Agunan</h4>
        <ul>
          <li>Nama: ${nama}</li>
          <li>Alamat: ${alamat}</li>
          <li>No. KTP: ${ktp}</li>
          <li>HP: ${hp}</li>
          <li>Email: ${email}</li>
          <li>Jenis Agunan: ${jenisAgunan}</li>
          <li>Nilai Agunan: Rp ${nilaiAgunan.toLocaleString("id-ID")}</li>
        </ul>
      `;
      document.getElementById("rincianSkor").innerHTML = rincian + detailNasabah;
      document.getElementById("hasilBox").style.display = "block";
    }

    function resetForm() {
      document.querySelectorAll("input, select").forEach(el => el.value = "");
      document.getElementById("hasilBox").style.display = "none";
      document.getElementById("rincianSkor").innerHTML = "";
      document.getElementById("hasilSkor").innerHTML = "";
    }
  </script>
</body>
</html>
