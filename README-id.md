# Tugas eliminasi 2

## Tugas

Buat repo Github mengenai pulau di Indonesia yang belum ada di OpenStreetMap. 

## Tujuan

Tugas ini akan membantu peserta mendapatkan pemahaman yang lebih baik mengenai data geospasial, format-format data, kualitas data, dan berapa baik kualitas Data Terbuka (Open Data) yang berasal dari Indonesia. 

Tugas ini memungkinkan peserta untuk menciptakan sebuah pulau di OpenStreetMap, namun hal ini tidak diharuskan. 

## Latar belakang

[OpenStreetMap](https://en.wikipedia.org/wiki/OpenStreetMap) (OSM) adalah peta dunia, yang tercipta karena orang-orang seperti anda, membuatnya, dan bebas digunakan dalam lisensi terbuka [odbl] (http://opendatacommons.org/licenses/odbl/).

Datanya dapat secara mudah di cari [queried](https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL)
dan dibuat visualnya menggunakan [overpass turbo](http://overpass-turbo.eu/).

Obyek-obyek dalam OSM dapat mencantumkan 'tag' metadata yang akan menyambungkan obyek OSM ke sistem lainnya, seperti tag `wikidata` dan `wikipedia` yang kemudian akan menautkan obyek-obyek tersebut pada proyek proyek Wikimedia lainnya. 

Obyek keterpautan OSM (<i>relation object</i>) adalah tipe obyek yang paling stabil dari OSM, dan Wikidata dapat mencantumkan pranala pranala langsung untuk keterpautan OSM. Kedua tipe lain dari obyek OSM adalah <i>ways</i> dan <i>nodes</i>, yang tidak stabil dan tidak diperkenankan di Wikidata. 

Pencarian (<i>query</i>) berikut ini akan menemukan seluruh keterpautan obyek 'relation' yang merupakan pulau pulau di Indonesia, yang memiliki <i>identifier</i> Wikidata atau Wikipedia. 

```
area[name="Indonesia"];
(
  relation
    [place=island]
    [name]
    [wikipedia]
    (area);
  relation
    [place=island]
    [name]
    [wikidata]
    (area);
 );
(>;);
out body;
```

Hasil dari pencarian ini sangat besar dan petanya akan menyebabkan perambah internet (<i>browser</i>) anda berhenti (macet). 
Hasil geojson dari pencarian tersebut disimpan pada repo `uni-task-2`,
yang boleh di masukkan pada tool GIS apapun yang Anda miliki di desktop Anda. 

Anda dapat melihat peta yang telah dirender dari pencarian tersebut dalam berkas kecil 
`wikimedia_connected_island_relation.png` pada repo `uni-task-2`,
yang akan memperlihatkan pada Anda bahwa banyak sekali pulau-pulau di Indonesia yang tidak terdapat disana yang bisa disambungkan ke proyek-proyek Wikimedia. 

Repo ini juga memiliki pencarian dan hasil dari geojson untuk <i>ways</i> yang menyatakan pulau-pulau, dan terhubung dengan proyek-proyek Wikimedia.

Pencarian lainnya yang bisa bermanfaat adalah data-data seluruh garis pantai di Indonesia, dan obyek-obyek yang terpaut didalamnya: 

```
area[name="Indonesia"];
(
  way
    [natural=coastline]
    (area);
 );
(._;>;);
out body;
```

Hal ini tersimpan di coastline.geojson.
Data ini adalah data yang diambil pada bulan Agustus.

Ada juga keterpautan (<i>relations</i>) dan <i>ways</i> yang tidak tersambung dengan proyek-proyek Wikimedia yang bisa jadi berguna untuk tugas ini. 

## Langkah-langkah pengerjaan

### Terima undangan

Anda akan menerima undangan via surel dari GitHub Classroom untuk melakukan tugas dalam 
organisasi BesutKode GitHub.

Anda perlu menyetujui undangan tersebut. 

Persetujuan ini akan secara otomatis menciptakan repo baru untuk Anda, 
*namun* repo ini akan diubah menjadi repo publik pada 20 November 2016. 

Sebagai catatan ada [bug](https://github.com/education/classroom/issues/729)
dalam GitHub Classroom yang membuat repo baru terbuat ganda. 
Apabila repo Anda lebih dari satu, jangan gunakan repo dengan nama yang memiliki `-1` (dsb). 
Mereka akan dihabus oleh tim admin Besut Kode.

Seluruh hal yang Anda lakukan akan menjadi publik untuk selamanya. 

DILARANG menyambungkan repo pada Issue atau Pull Request pada repo lainnya. 

Ada tim "slack" untuk tugas ini, yang hanya dapat diakses oleh peserta 
Besut Kode Universitas yang telah menyelesaikan Tugas 1:

https://besutkode.slack.com/messages/uni-task-2/

Anda akan menerima undangan dari slack untuk bergabung dengan tim ini. 

Saluran komunikasi ini adalah saluran privat.

Berlakulah secara profesional dan santun. 

Anda telah diberikan hak admin pada repo tugas Anda. 

DILARANG menambahkan peserta/ orang lain pada repo Anda. Tindakan ini akan membuat Anda di diskualifikasi langsung. Apabila Anda ingin membagi data atau kode dengan peserta lain, gunakan repo `uni-task-2`.

## Aktifkan Travis CI Pro

Anda harus mengaktifkan Travis CI Pro pada repo Anda.

Ciptakan cabang "citest" dan yakinkan bahwa cabang ini dapat melangsungkan pekerjaan dengan benar. 

Penggunaan Travis CI Pro yang diperoleh oleh BesutKode hanya memungkinkan satu pekerjaan yang berlangsung secara bersamaan, 
jadi yakinkan anda perbolehkan (<i>enable</i>) atau anda hentikan (<i>disable</i>) fungsi ini pada preferensi Travis CI Pro Anda
seperlunya untuk menghindari mengerjakan satu pekerjaan yang melakukan commits kecil yang tidak penting pada repo Anda. 

Gunakan apabila Anda memerlukannya, apabila Anda akan membangun sepenuhnya. 

## Cari pulau pulau yang "hilang" 

Gunakan data yang disediakan, dan overpass turbo queries, untuk menemukan pulau pulau di Indonesia yang:

- bukan obyek relation di OpenStreetMap 
- tidak tersambung ke Wikimedia 
- memiliki panjang lebih dari 10 km, atau memiliki jarak 10 km dari pulau lain
- memiliki lebih dari 1,000 penghuni 

Apabila Anda menemukan relation yang tidak tersambung ke Wikimedia, Anda dianjurkan untuk menyunting OpenStreetMap relation dan menambahkan sambungan yang hilang. Hal ini akan membantu Anda menghapuskan obyek dari pencarian yang Anda atau peserta lain lakukan. 

Obyek Way yang sudah ada merupakan contoh ideal untuk tugas ini, karena Way telah memiliki bentuk data yang telah dilisensikan dibawah lisensi open data yang benar. 

### Daftarkan proyek Anda

Hanya satu peserta yang diperkenankan untuk mengerjakan sebuah pulau. 
Hal ini untuk menghindari duplikasi dan upaya sia-sia yang dilakukan oleh peserta. 

Untuk menghindari lebih dari satu peserta mengerjakan pulau yang sama, 
setiap peserta akan menciptakan halaman pada repo wiki BesutKode tentang pulau yang telah mereka pilih sebelum mereka mulai mengerjakannya. 

Setelah Anda menemukan pulau yang memenuhi syarat, pertama cari tugas 
wiki di [uni-task-2](https://github.com/BesutKode/uni-task-2) 
dan periksa apakah peserta lain sudah memilih pulau yang sama. 

Apabila pulau pilihan Anda belum dipilih oleh yang lain, 
buat halaman pada wiki dengan nama pengguna GitHub Anda,
dan cantumkan hal hal berikut ini: 

1. Nama pulau Anda 
2. Provinsi dan kabupaten-kabupaten yang terdapat di pulau tersebut 
3. Tautan ke item Wikidata mengenai pulau tersebut (buatlah item baru apabila item yang Anda cari tidak ada) 
4. Tautan ke halaman Wikipedia apapun mengenai pulau tersebut 
5. Perkiraan besar populasinya, dengan pranala sumber rujukan, sebagai bukti 
6. Informasi lainnya yang Anda pikir relevan untuk diutarakan 

Tulisan dalam bahasa Indonesia diterima. 

Ciptakan halaman wiki di `uni-task-2` mengenai pulau Anda, 
dengan bukti bahwa hal tersebut memenuhi persyaratan diatas. 

## Isi repo Anda 

Repo anda seharusnya menyimpan koleksi dokumentasi *data terbuka* yang baik
mengenai pulau Anda, jangan lupa untuk mencantumkan sumber bagaimana anda mendapatkan data (apapun)
(baik atribusi, dan asalnya), dan lisensi dari data tersebut. 

Apabila dataset terkait tertera di sistem terkendali yang dapat diakses secara umum dan dapat diandalkan,
seperti GitHub dan OpenStreetMap, maka Anda tidak perlu menyalin data tersebut pada repo Anda. 

Ciptakan sebuah program atau skrip atau pencarian, menggunakan bahasa pemrograman apapun yang Anda kuasai,
untuk mengambil dataset yang berupa data terbuka untuk membangun berkas GeoJSON (atau format yang mirip) yang memiliki: 

- bentuk akurat untuk pulau tersebut, menggunakan domain publik atau data ODBL 
- dua set informasi tambahan mengenai pulau tersebut, menggunakan data terbuka apapun 

Berkasnya harus disimpan dalam repo Anda

Sebagai contoh, pada peta pulau anda, anda bisa menambahkan: 

- batas administrasi apabila pulau tersebut memiliki beberapa kabupaten atau wilayah-wilayah 
- Kode pos daerah daerah didalamnya
- perkiraan berbagai etnis atau kelompok bahasa yang tinggal di dalamnya 
- area area yang dilindungi
- danau danau atau gunung gunung 
- Kapal kalap karam 

Kelompok kelompok informasi yang disertakan disini harus lengkap dan menyeluruh 
serta, "didukung data" berdasarkan kriteria yang terdokumentasi dan masuk akal. 

Contohnya, apabila Anda memilih untuk hanya menunjukkan beberapa gunung berdasarkan besarnya, karena gunung-gunung tersebut ada diatas ukuran sekian, maka hal ini dapat diterima. 
Namun apabila Anda memilih beberapa gunung saja yang ditampilkan karena Anda memilih demikian tanpa alasan, maka hal ini tidak dapat diterima. 

Apabila data apapun yang anda proses tidak diotomatisasi, dokumentasikan langkah langkah manual yang Anda lakukan dalam serinci mungkin, hingga apabila seseorang membacanya mereka bisa mengikuti langkah langkah yang sama dengan mudah tanpa melakukan kesahalan dan mendapatkan hasil yang persis sama. If any part of your data processing is not automated, document the manual steps
used in excruciating detail, so that someone else could easily follow the same
procedure and obtain the same results.  Hasil Anda harus dapat diperiksa dan dicek caranya dengan mudah. 

Langkah langkah otomatisasi dalam proses Anda harus dapat dilakukan menggunakan Travis CI.

*JANGAN PERNAH* membuat relation pulau di OpenStreetMap sebelum mendapatkan persetujuan dari @jayvdb. Proses yang anda gunakan untuk menciptakan sebuah bentuk geografis perlu verifikasi, apabila tidak, pulau Anda bisa jadi melanggar bingkai legalitas OSM, dan mengakibatkan dihapusnya pulau tersebut. 

Lihat [Pertanyaan Umum Legalitas](https://wiki.openstreetmap.org/wiki/Legal_FAQ).
Tugas ini tidak mengharuskan Anda untuk memuat pulau itu pada OpenStreetMap 

## Buatlah presentasi 

Bangunlah sebuah aplikasi yang dapat menunjukkan secara visual hasil dari data mentah anda. 

Metode paling sederhana adalah menggunakan halaman HTML dengan 
[OpenLayers](https://en.wikipedia.org/wiki/OpenLayers) untuk menciptakan peta yang secara spesifik memenuhi keinginan kita (<i>custom</i>).  

Namun Anda bebas untuk membuat aplikasi grafis lainnya menggunakan bahasa pemrograman yang Anda kuasai. 

Aplikasi harus dibuat dalam Travis CI Pro. 

Aplikasi harus menggunakan lisensi MIT.

## Evaluasi

Apabila Anda percaya Anda telah selesai, lakukan <i>fresh build</i> di Travis CI untuk commit terakhir anda. Hasilnya harus hijau. 

Ciptakan issue pada repo BesutKode `uni-task-2` dan tugaskan pada @jayvdb.

Judul dari issue Anda harus mencantumkan nama pengguna GitHub Anda, dan badan dari issue tersebut harus tertaut dengan halaman wiki Anda. 

DILARANG menautkan pada Issue atau melakukan Pull Request pada repo lainnya. 

John akan memeriksa builds Travis CI terakhir Anda, dan warnanya *harus* hijau. 

Evaluasi akan mengulas proses yang digunakan untuk menciptakan bentuk geografis dan 
menghubungkan kelompok kelompok informasi yang menggunakan sumber data dari data terbuka dahulu, atau data yang diasumsikan sudah masuk dalam ranah domain publik dant terbuka. 

Bentuk pulau akan dibandingkan dengan peta dan data komersil untuk meyakinkan bahwa bentuknya sama, namun pada saat yang sama datanya tidak sama. 

Aplikasi akan di lihat untuk meyakinkan bahwa data yang di pilih dalam repo Anda telah terwakili untuk pengguna yang menggunakan aplikasi tersebut. 

## StackExchange

Tanya jawab mengenai informasi Geospacial secara umum dapat dilihat dalam 
[gis.stackexchange.com](http://gis.stackexchange.com/), dimana situs ini adalah bagian dari situs situs milik StackOverflow.

### Tag StackOverflow terkait

- [openstreetmap](http://stackoverflow.com/questions/tagged/openstreetmap)
- [wikidata](http://stackoverflow.com/questions/tagged/wikidata)
- [gis](http://stackoverflow.com/questions/tagged/gis)
- [travis-ci](http://stackoverflow.com/questions/tagged/travis-ci)
- [bash](http://stackoverflow.com/questions/tagged/bash)
