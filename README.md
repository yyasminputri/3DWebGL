# 3DWebGL
Create 3D-Animation, Animation, Camera, Lathe, Lighting , and Texture using WebGL

### 1. 3D Animation
Saya membuat animasi 3d dengan bentuk cube, bola, cone, dan ring. Pembuatan ini hanya memerlukan 1 file yang bernama html. 
- Cube : Kode HTML ini membuat aplikasi WebGL yang menggambar kubus 3D dengan enam wajah berwarna pastel yang berbeda. Kubus dirender menggunakan buffer untuk menyimpan vertex dan warna, serta shader untuk mengatur tampilan objek. Animasi rotasi diterapkan untuk memberikan efek dinamis saat kubus ditampilkan.
```
// Define vertices for a cube
var vertices = [
    -0.5, -0.5, -0.5,   0.5, -0.5, -0.5,   0.5, 0.5, -0.5,   -0.5, 0.5, -0.5,  // Front face
    -0.5, -0.5, 0.5,    0.5, -0.5, 0.5,    0.5, 0.5, 0.5,    -0.5, 0.5, 0.5,   // Back face
    -0.5, 0.5, -0.5,    -0.5, 0.5, 0.5,    -0.5, -0.5, 0.5,   -0.5, -0.5, -0.5, // Left face
    0.5, 0.5, -0.5,     0.5, 0.5, 0.5,     0.5, -0.5, 0.5,    0.5, -0.5, -0.5,  // Right face
    -0.5, -0.5, 0.5,    0.5, -0.5, 0.5,    0.5, -0.5, -0.5,   -0.5, -0.5, -0.5, // Bottom face
    -0.5, 0.5, 0.5,     0.5, 0.5, 0.5,     0.5, 0.5, -0.5,    -0.5, 0.5, -0.5   // Top face
];

// Define colors for each face
var colors = [
    // Front face: Baby Pink
    1.0, 0.75, 0.8,  1.0, 0.75, 0.8,  1.0, 0.75, 0.8,  1.0, 0.75, 0.8,
    // Back face: Soft Pink
    0.8, 0.6, 0.9,  0.8, 0.6, 0.9,  0.8, 0.6, 0.9,  0.8, 0.6, 0.9,
    // Left face: Pastel Blue
    0.6, 0.8, 1.0,  0.6, 0.8, 1.0,  0.6, 0.8, 1.0,  0.6, 0.8, 1.0,
    // Right face: Pastel Yellow
    1.0, 1.0, 0.6,  1.0, 1.0, 0.6,  1.0, 1.0, 0.6,  1.0, 1.0, 0.6,
    // Bottom face: Baby Pink
    1.0, 0.75, 0.8,  1.0, 0.75, 0.8,  1.0, 0.75, 0.8,  1.0, 0.75, 0.8,
    // Top face: Soft Pink
    1.0, 0.5, 0.7,  1.0, 0.5, 0.7,  1.0, 0.5, 0.7,  1.0, 0.5, 0.7
];

// Define indices for the cube's faces
var indices = [
    0, 1, 2, 0, 2, 3,  // Front face
    4, 5, 6, 4, 6, 7,  // Back face
    8, 9, 10, 8, 10, 11,// Left face
    12, 13, 14, 12, 14, 15, // Right face
    16, 17, 18, 16, 18, 19, // Bottom face
    20, 21, 22, 20, 22, 23  // Top face
];
```
<br>
Output Result Cube
<img width="1440" alt="Screenshot 2024-09-22 at 12 03 31" src="https://github.com/user-attachments/assets/8440e533-937c-4572-8253-7bc4daf701b5"> <br>
- Ball : Kode HTML ini membuat aplikasi WebGL yang menggambar bola 3D dengan efek warna gradasi, menggunakan vertex dan fragment shaders untuk mengatur tampilan objek. Selain itu, kode ini menerapkan transformasi matriks dan animasi rotasi untuk memberikan efek dinamis pada bola saat ditampilkan. Dengan menggunakan buffer untuk menyimpan vertex, warna, dan indeks, objek 3D dapat dirender secara efisien.

```
var radius = 1.0;
var latBands = 25;
var longBands = 25;
var vertices = [];
var colors = [];
var indices = [];

for (var latNumber = 0; latNumber <= latBands; latNumber++) {
    var theta = latNumber * Math.PI / latBands;
    var sinTheta = Math.sin(theta);
    var cosTheta = Math.cos(theta);

    ...

        vertices.push(radius * x, radius * y, radius * z);
        
        // Warna gradasi
        var gradientRatio = latNumber / latBands;
        var color;

...
```
<br> 
Output Result Ball
<img width="1440" alt="Screenshot 2024-09-22 at 12 03 15" src="https://github.com/user-attachments/assets/a7708c8b-133e-470b-b6ca-66cd80c498cc"> <br>

- Cone : Kode ini untuk membuat tampilan 3D sebuah kerucut/cone menggunakan WebGL. Kerucut ini memiliki warna gradasi yang berbeda di bagian alas dan ujungnya, serta dapat berputar secara dinamis. Kode ini mencakup pembuatan buffer untuk geometri, warna, dan pengaturan shader untuk merender kerucut/cone.
```
// Vertices 
var vertices = [
    // Titik pusat dan titik-titik di tepi lingkaran
    0, 0, -1, // Pusat alas
    1, 0, -1,
    0.707, 0.707, -1,
    0, 1, -1,
    -0.707, 0.707, -1,
    -1, 0, -1,
    -0.707, -0.707, -1,
    0, -1, -1,
    0.707, -0.707, -1,
    // Titik puncak kerucut 
    0, 0, 1  // Titik puncak
];

// Indices untuk menggambar kerucut
var indices = [
    // Segitiga alas
    0, 1, 2,
    0, 2, 3,
    0, 3, 4,
    0, 4, 5,
    0, 5, 6,
    0, 6, 7,
    0, 7, 8,
    0, 8, 1,
    // Segitiga sisi
    9, 1, 2,
    9, 2, 3,
    9, 3, 4,
    9, 4, 5,
    9, 5, 6,
    9, 6, 7,
    9, 7, 8,
    9, 8, 1
];
```
<br> 
Output Result Cone 
<img width="1440" alt="Screenshot 2024-09-22 at 12 03 01" src="https://github.com/user-attachments/assets/b2ed6b90-71a7-40c7-8214-2f06f9d944a5"> <br>

- Ring : Kode HTML ini menghasilkan bentuk ring 3D menggunakan WebGL. Dengan menggunakan dua jari-jari (inner dan outer), program ini membangun geometri ring dan memberikan warna yang bervariasi untuk setiap vertex. Efek rotasi ditambahkan untuk membuat tampilan lebih dinamis.
```
// Vertices for the cone
        var vertices = [];
        var colors = [];
        var indices = [];
        var radius = 1;
        var height = 2;
        var radialSegments = 30;

        // Base circle vertices
        vertices.push(0, 0, 0); // Center of base
        colors.push(1, 0, 0); // Red for center

...

// Tip of the cone
        vertices.push(0, 0, height);
        colors.push(0, 0, 1); // Blue for tip

        // Side triangles
        for (var i = 1; i < radialSegments; i++) {
            indices.push(i, i + 1, radialSegments + 1);
        }
```
Output Result Ring
<img width="1312" alt="Screenshot 2024-09-22 at 12 02 49" src="https://github.com/user-attachments/assets/2a0a994b-4b24-4db9-801c-ca2673df03d8"> <br>

### 2. Animation
Dalam mengaplikasikan animation (Rotating, Scaling dan Translating) hanya memerlukan 3 file, yaitu js, css, dan html. 
Pembuatan Cubenya sebagai bentuk utama 
```
function setGeometry(gl) {
    gl.bufferData(
        gl.ARRAY_BUFFER,
        new Float32Array([
            // Front face
            -1, -1,  1,
             1, -1,  1,
             1,  1,  1,
            -1, -1,  1,
             1,  1,  1,
            -1,  1,  1,
            // Back face
            -1, -1, -1,
             1, -1, -1,
             1,  1, -1,
            -1, -1, -1,
             1,  1, -1,
            -1,  1, -1,
            // ... (other faces)
        ]),
        gl.STATIC_DRAW
    );
}
```
- js : Kode ini menginisialisasi konteks WebGL, membuat program shader, dan mengatur data geometri serta warna untuk menggambar kubus berwarna-warni. Fungsi drawScene digunakan untuk menggambar kubus dengan transformasi translasi, rotasi, dan skala yang dapat disesuaikan menggunakan slider. Shader vertex dan fragment ditentukan dalam elemen <script> di HTML untuk mengontrol tampilan kubus di kanvas.
  - Langkah : Buat elemen <canvas> di HTML dan ambil konteks WebGL menggunakan getContext("webgl"). Menulis shader vertex dan fragment untuk mendefinisikan geometri dan warna, lalu siapkan buffer untuk posisi dan warna kubus. Implementasikan fungsi drawScene untuk menggambar kubus dengan transformasi yang diatur oleh kontrol UI, dan panggil fungsi ini saat halaman dimuat.
- css : CSS ini mengatur tampilan aplikasi WebGL dengan latar belakang pink muda dan memastikan kanvas mengisi seluruh layar. UI slider ditempatkan di sudut kanan atas dan disusun secara vertikal untuk kemudahan penggunaan. Font yang digunakan memberikan sentuhan klasik pada antarmuka.
    - Langkah : Siapkan elemen HTML yang mencakup kanvas dan kontainer UI untuk slider. Lalu, membuat file CSS untuk mengatur gaya tampilan, termasuk latar belakang, ukuran kanvas, dan penataan slider. Serta, Implementasikan JavaScript untuk menghubungkan slider dengan rotasi, skala, dan translasi objek 3D.
- html : Dokumen HTML ini membuat halaman dengan judul "Rainbow Cube" dan menampilkan kanvas WebGL berukuran 400x400 piksel. Terdapat juga elemen untuk mengontrol rotasi kubus dalam tiga sumbu. Vertex dan fragment shader ditulis dalam elemen <script> terpisah, dan skrip tambahan dimuat dari sumber eksternal untuk mendukung fungsi WebGL.
  - Langkah : Dokumen HTML dimulai dengan deklarasi tipe dan struktur dasar, termasuk elemen <head> untuk metadata dan judul, serta elemen <body> yang memuat kanvas WebGL. Di dalam <body>, terdapat elemen kanvas untuk menggambar kubus, dan skrip shader ditulis dalam elemen <script> terpisah. Skrip JavaScript eksternal diimpor untuk mendukung fungsi WebGL dan logika aplikasi.

- Rotating
```
var rotation = [degToRad(40), degToRad(25), degToRad(325)];
function updateRotation(index) {
    return function(event, ui) {
        var angleInDegrees = ui.value;
        var angleInRadians = angleInDegrees * Math.PI / 180;
        rotation[index] = angleInRadians;
        drawScene();
    };
}

// Dalam fungsi drawScene
matrix = m4.xRotate(matrix, rotation[0]);
matrix = m4.yRotate(matrix, rotation[1]);
matrix = m4.zRotate(matrix, rotation[2]);
```
Output Result Rotating
<img width="1440" alt="Screenshot 2024-09-22 at 12 21 43" src="https://github.com/user-attachments/assets/82018324-dd39-4652-a7ab-54ee9bb942a7">

- Scaling
```
var scale = [100, 100, 100];

function updateScale(index) {
    return function(event, ui) {
        scale[index] = ui.value;
        drawScene();
    };
}

// Dalam fungsi drawScene
matrix = m4.scale(matrix, scale[0], scale[1], scale[2]);
```
Output Result Scaling
<img width="1440" alt="Screenshot 2024-09-22 at 12 21 58" src="https://github.com/user-attachments/assets/f86e8a13-2544-4625-a18a-845c085e80cd">

- Translating
```
var translation = [300, 300, 100];

function updatePosition(index) {
    return function(event, ui) {
        translation[index] = ui.value;

        drawScene();
    };
}

// Dalam fungsi drawScene
matrix = m4.translate(matrix, translation[0], translation[1], translation[2]);
```
Output Result Translating
<img width="1440" alt="Screenshot 2024-09-22 at 12 21 21" src="https://github.com/user-attachments/assets/ad1daf0e-937e-4593-9f8e-cb22a1170251">

### 3. Camera
Membuat camera 360 derajat menggunakan elemen bola. Dalam membuat segitiga ini, hanya memerlukan 2 file, yaitu css, js dan html
- css : CSS ini mengatur gaya untuk elemen <body> dan <canvas>, memastikan bahwa kanvas memenuhi seluruh viewport dengan latar belakang berwarna biru muda. Elemen <pre> ditempatkan secara absolut di sudut kanan atas dengan gaya font Georgia dan border biru gelap. Padding dan line-height pada elemen <pre> disesuaikan untuk mengurangi jarak dan memberikan tampilan yang lebih ringkas.
    - Langkah : Atur margin body ke nol untuk menghilangkan ruang kosong di sekitar kanvas. Sesuaikan ukuran kanvas agar memenuhi seluruh jendela tampilan dan berikan latar belakang yang menarik. Tempatkan elemen instruksi dalam <pre> dengan gaya yang jelas dan konsisten untuk meningkatkan keterbacaan.
- js : Kode di atas adalah sebuah program WebGL yang menggambar bola dengan pencahayaan, memungkinkan pengguna untuk menggerakkan kamera menggunakan input keyboard. Program ini mengatur matriks transformasi untuk perspektif, posisi, dan orientasi kamera, serta menghitung pencahayaan berdasarkan arah cahaya. Pengguna dapat mengubah posisi, rotasi, dan elevasi kamera untuk melihat objek dari berbagai sudut.
      - Langkah Pertama Inisialisasi konteks WebGL, shader, dan buffer untuk menggambar bola menggunakan TWGL, serta atur matriks untuk proyeksi, kamera, dan transformasi objek. Dalam fungsi render, perbarui posisi dan orientasi kamera berdasarkan input keyboard, serta hitung transformasi untuk setiap objek yang akan digambar. Setel atribut dan uniform shader, kemudian gambar objek di layar menggunakan twgl.drawBufferInfo di dalam loop animasi yang berkelanjutan.
- html : HTML ini menyajikan aplikasi WebGL untuk menampilkan kubus dengan kontrol kamera. Elemen kanvas disiapkan untuk rendering grafik 3D, sementara informasi kontrol ditampilkan dalam elemen <pre>. Skrip dari TWGL digunakan untuk menyederhanakan pengembangan WebGL.
      - Langkah : Buat elemen HTML dengan kanvas untuk rendering dan bagian teks untuk instruksi kontrol. Sertakan pustaka TWGL untuk membantu dalam manajemen shader dan buffer WebGL. Implementasikan JavaScript untuk menangani logika rendering dan kontrol kamera dalam file app.js.

```
m4.identity(camera);
m4.scale(world, [0.5, 0.5, 0.5], world);     
m4.translate(camera, [px, py, pz], camera);
m4.rotateX(camera, degToRad(elev), camera);   
m4.rotateY(camera, degToRad(-ang), camera);   
m4.rotateZ(camera, degToRad(roll), camera);
  
m4.inverse(camera, view);
```

Output Result Camera
<img width="1440" alt="Screenshot 2024-09-22 at 12 25 18" src="https://github.com/user-attachments/assets/09d0b5c7-4807-4048-b645-e50ebd22127e">

### 4. Lathe 
Dalam membuat lathe ini, hanya memerlukan 3 file, yaitu css, js dan html
- css : CSS ini mengatur gaya untuk halaman web yang menggunakan WebGL. Elemen body diatur tanpa margin, sedangkan elemen canvas dirancang untuk mengisi seluruh lebar dan tinggi viewport dengan latar belakang berwarna merah muda. Selain itu, canvas ditampilkan sebagai blok agar tidak ada ruang ekstra di sekitarnya.
- js : Fungsi main mengonfigurasi WebGL untuk menggambar objek 3D menggunakan metode lathe berdasarkan titik-titik yang dihasilkan dari kurva Bezier. Dengan menggunakan parameter seperti toleransi, sudut awal dan akhir, serta jumlah divisi, fungsi generateMesh menciptakan mesh yang sesuai dengan bentuk yang diinginkan. Matriks proyeksi dan tampilan diatur untuk menentukan posisi kamera, sementara fungsi render bertanggung jawab untuk menggambar objek di kanvas.
- html : Dokumen HTML ini memuat aplikasi WebGL untuk menggambar objek 3D menggunakan shader vertex dan fragment. Shader yang disertakan mengatur bagaimana posisi, tekstur, dan pencahayaan diterapkan pada objek, termasuk perhitungan pencahayaan spekular. Terdapat juga elemen UI dan pustaka tambahan untuk membantu mengelola WebGL dan perhitungan matematis yang diperlukan.
```
function generateMesh(bufferInfo) {
    const tempPoints = getPointsOnBezierCurves(curvePoints, data.tolerance);
    const points = simplifyPoints(tempPoints, 0, tempPoints.length, data.distance);
    const tempArrays = lathePoints(points, data.startAngle, data.endAngle, data.divisions, data.capStart, data.capEnd);
    const arrays = generateNormals(tempArrays, data.maxAngle);
    const extents = getExtents(arrays.position);
    // ...
}
```

Output Result Lathe
<img width="1440" alt="Screenshot 2024-09-22 at 12 40 39" src="https://github.com/user-attachments/assets/bbe4e626-3f68-4d7e-bb87-f80b8a17a64a">

### 5. Lighting 
Dalam membuat Lighting ini dengan elemen kubus, hanya memerlukan 3 file, yaitu css, js dan html
- css : CSS ini mengatur tampilan halaman dengan menghapus margin dan mengatur kanvas agar memenuhi seluruh viewport dengan latar belakang berwarna pink muda. Elemen-elemen kontrol UI seperti batas dan rotasi cahaya serta kubus memiliki gaya font yang konsisten menggunakan font "Georgia" dengan ukuran yang ditentukan. Input tipe "range" juga menggunakan font yang sama tetapi dengan ukuran yang sedikit lebih kecil untuk keseragaman visual.
- js : Kode js merupakan implementasi WebGL untuk menggambar objek kubus 3D dengan pencahayaan dan rotasi yang dapat diatur melalui slider. Program ini membuat shader, mengatur buffer untuk posisi dan normal, serta menghitung matriks transformasi untuk proyeksi dan pencahayaan. Interaksi pengguna memungkinkan pengaturan rotasi kubus dan arah sumber cahaya secara dinamis.
  - Langkah :
  - 1. Inisialisasi WebGL dan Program Shader: Kode ini mulai dengan mendapatkan konteks WebGL dari kanvas dan memeriksa keberhasilannya. Kemudian, program shader dibuat dari skrip vertex dan fragment shader yang telah didefinisikan sebelumnya.
  - 2. Pengaturan Buffer untuk Geometri dan Normal: Buffer untuk posisi (geometri) dan normal kubus dibuat. Fungsi setGeometry dan setNormals dipanggil untuk mengisi buffer dengan data posisi dan normal untuk setiap sisi kubus.
  - 3. Mengatur Matriks Proyeksi dan Kamera: Matriks proyeksi dan kamera dihitung menggunakan fungsi m4.perspective dan m4.lookAt. Matriks ini digunakan untuk menentukan bagaimana objek 3D dilihat dari perspektif kamera.
  - 4. Pengaturan Uniforms untuk Shader: Semua lokasi uniform (seperti warna, posisi cahaya, dan matriks) diambil dan kemudian diatur sebelum menggambar. Ini mencakup mengatur warna untuk masing-masing sisi kubus dan posisi serta arah cahaya.
  - 5. Menggambar Adegan: Fungsi drawScene mengatur viewport, membersihkan buffer warna dan kedalaman, dan menggunakan program shader untuk menggambar kubus. Rotasi dan pengaturan cahaya juga dilakukan berdasarkan input dari slider yang ada di UI, sebelum akhirnya memanggil gl.drawArrays untuk menggambar kubus.
- html : Dokumen HTML ini mendefinisikan sebuah halaman web yang menampilkan objek 3D menggunakan WebGL dengan efek pencahayaan. Terdapat shader vertex dan fragment yang menghitung pencahayaan dan warna berdasarkan posisi cahaya dan sudut pandang pengguna. UI yang disediakan memungkinkan pengguna untuk mengontrol rotasi cahaya dan kubus, serta batas pencahayaan.

```
var worldViewProjectionLocation = gl.getUniformLocation(program, "u_worldViewProjection");
  var worldInverseTransposeLocation = gl.getUniformLocation(program, "u_worldInverseTranspose");
  var lightWorldPositionLocation = gl.getUniformLocation(program, "u_lightWorldPosition");
  var viewWorldPositionLocation = gl.getUniformLocation(program, "u_viewWorldPosition");
  var lightDirectionLocation = gl.getUniformLocation(program, "u_lightDirection");

...

// cube normals
function setNormals(gl) {
  var normals = new Float32Array([
    0, 0, 1,
    0, 0, 1,
    0, 0, 1,
    // ... (lanjutkan dengan normal untuk sisi lainnya)
  ]);
```

Output Result Lighting 
<img width="1440" alt="Screenshot 2024-09-22 at 12 40 59" src="https://github.com/user-attachments/assets/71950c5a-08fa-4e96-be71-a7a8bd06f164">

### 6. Texture
Dalam membuat Texture ini dengan elemen kubus, hanya memerlukan 3 file, yaitu css, js dan html dan ditambah dengan foto texturenya 
- css : CSS ini mengatur gaya untuk elemen <body> dan <canvas>. Body memiliki margin nol, menghilangkan scroll, dan latar belakang berwarna pink muda (#FFD1DC). Canvas diatur agar memenuhi seluruh area tampilan dengan lebar dan tinggi 100% viewport.
- js : Kode ini menggunakan WebGL untuk menggambar sebuah kubus 3D dengan rotasi dan tekstur yang diterapkan pada setiap sisi kubus. Tekstur dimuat secara dinamis dari gambar eksternal dan diatur agar sesuai dengan setiap wajah kubus menggunakan koordinat tekstur. Kubus kemudian digambar dalam sebuah loop yang memperbarui rotasi berdasarkan waktu.
- html : HTML ini membuat halaman web untuk menampilkan tekstur pada kubus menggunakan WebGL. Terdapat elemen <canvas> untuk menggambar, serta shader vertex dan fragment untuk mengatur posisi dan tekstur. Skrip tambahan dari pustaka WebGL digunakan untuk memfasilitasi pengoperasian grafis 3D.

```
    const program = webglUtils.createProgramFromScripts(gl, ["vertex-shader-3d", "fragment-shader-3d"]);
    const texcoordLocation = gl.getAttribLocation(program, "a_texcoord");
    const textureLocation = [];
    
    for (let i = 0; i < 6; i++) {
        textureLocation[i] = gl.getUniformLocation(program, `u_texture[${i}]`);
    }

    const texcoordBuffer = gl.createBuffer();
    gl.bindBuffer(gl.ARRAY_BUFFER, texcoordBuffer);
    setTexcoords(gl);

    const textures = [];
    const textureUrls = [
        "texture.png", // Add more textures if needed
    ];

    for (let i = 0; i < textureUrls.length; i++) {
        (function(i) {
            ...
        })(i);
    }

    function setTexcoords(gl) {
        const texcoords = new Float32Array([
           ...
        ]);
        gl.bufferData(gl.ARRAY_BUFFER, texcoords, gl.STATIC_DRAW);
    }
}
```
