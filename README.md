
<!DOCTYPE html>
<html>
<head>
    <title>Data Murid</title>

    <style>
        body{
            text-align: center;
            font-family: Arial, sans-serif;
            margin-top: 40px;
            background-color: grey; 
            color: white; 
        }

        input{
            padding: 5px;
            text-align: center;
        }

        button{
            padding: 8px 15px;
            cursor: pointer;
            margin: 3px;
        }

        #output{
            margin-top: 20px;
        }
    </style>

</head>
<body>

<h2>Input student data</h2>

<label>Name:</label><br>
<input type="text" id="Name"><br><br>

<label>Class:</label><br>
<input type="text" id="Class"><br><br>

<label>Score:</label><br>
<input type="number" id="Score"><br><br>

<button onclick="tambahData()">Add data</button>

<h3>Results:</h3>
<div id="output"></div>

<script>

let array = [];

function tambahData() {

    let nama = document.getElementById("Name").value;
    let kelas = document.getElementById("Class").value;
    let nilai = Number(document.getElementById("Score").value);

    if (nama === "" || kelas === "" || isNaN(nilai)) {
        alert("Data belum lengkap!");
        return;
    }

    let siswa = {
        nama,
        kelas,
        nilai,

        get info() {
            return `Nama: ${this.nama}<br>
                    Kelas: ${this.kelas}<br>
                    Nilai: ${this.nilai}<br>`;
        },

        get status() {
            return `Kelulusan: ${this.nilai >= 75 ? "Lulus" : "Tidak Lulus"}<br>`;
        },

        get grade() {
            if (this.nilai >= 90) return "A";
            else if (this.nilai >= 80) return "B";
            else if (this.nilai >= 75) return "C";
            else return "D";
        }
    };

    array.push(siswa);

    tampilkanData();

    document.getElementById("Name").value = "";
    document.getElementById("Class").value = "";
    document.getElementById("Score").value = "";
}

function hapusData(index){
    array.splice(index,1);
    tampilkanData();
}

function tampilkanData() {

    let hasil = "";

    for (let i = 0; i < array.length; i++) {
        hasil += array[i].info +
                 array[i].status +
                 "Grade: " + array[i].grade + "<br>" +
                 `<button onclick="hapusData(${i})">Delete</button>` +
                 "<hr>";
    }

    document.getElementById("output").innerHTML = hasil;
}

</script>

</body>
</html>

