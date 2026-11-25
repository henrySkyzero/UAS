# UAS
just my project last semester in uni, i sned this file cause i still learning 
here my  mermaid code i share to make a new website
erDiagram
    here my mermaid code to apllying on draw.io
    

    DOKTER_GIGI {
        int id_dokter PK
        varchar nama_lengkap
        varchar nip
        varchar str_number
        varchar spesialisasi
        varchar no_telepon
        varchar email
        enum status_aktif
    }

    PASIEN {
        int id_pasien PK
        varchar nama_lengkap
        varchar nik
        enum jenis_kelamin
        date tanggal_lahir
        text alamat
        varchar no_telepon
        varchar email
        varchar golongan_darah
        text riwayat_alergi
        date tanggal_daftar
    }

    LAYANAN_MEDIS {
        int id_layanan PK
        varchar nama_layanan
        text deskripsi
        varchar kategori
        decimal biaya
        int estimasi_waktu_menit
        enum status_aktif
    }

    JADWAL_PRAKTIK {
        int id_jadwal PK
        int id_dokter FK
        enum hari
        time jam_mulai
        time jam_selesai
        int kuota_pasien
        enum status
    }

    PERAWAT {
        int id_perawat PK
        varchar nama_lengkap
        varchar nip
        varchar sip_number
        varchar no_telepon
        enum shift
        enum status_aktif
    }

    JANJI_TEMU {
        int id_janji PK
        int id_pasien FK
        int id_dokter FK
        int id_layanan FK
        int id_jadwal FK
        date tanggal_janji
        time jam_janji
        text keluhan
        enum status
        datetime created_at
    }

    REKAM_MEDIS {
        int id_rekam PK
        int id_janji FK
        int id_pasien FK
        int id_dokter FK
        int id_perawat FK
        date tanggal_pemeriksaan
        text diagnosis
        text tindakan
        text catatan_dokter
        text kondisi_gigi
        datetime created_at
    }

    PEMBAYARAN {
        int id_pembayaran PK
        int id_janji FK
        int id_pasien FK
        decimal total_biaya
        decimal diskon
        decimal total_bayar
        enum metode_pembayaran
        enum status_pembayaran
        datetime tanggal_pembayaran
        varchar nomor_invoice
    }

    RESEP_OBAT {
        int id_resep PK
        int id_rekam FK
        varchar nama_obat
        varchar dosis
        varchar frekuensi
        int jumlah
        varchar satuan
        text aturan_pakai
        text catatan
    }

    DOKTER_GIGI ||--o{ JADWAL_PRAKTIK : "memiliki"
    DOKTER_GIGI ||--o{ JANJI_TEMU : "menangani"
    DOKTER_GIGI ||--o{ REKAM_MEDIS : "menulis"
    LAYANAN_MEDIS ||--o{ JANJI_TEMU : "dipilih_untuk"
    JADWAL_PRAKTIK ||--o{ JANJI_TEMU : "dijadwalkan_pada"
    PASIEN ||--o{ JANJI_TEMU : "mendaftar"
    PASIEN ||--o{ REKAM_MEDIS : "memiliki"
    PASIEN ||--o{ PEMBAYARAN : "melakukan"
    PERAWAT ||--o{ REKAM_MEDIS : "membantu"
    JANJI_TEMU ||--o| REKAM_MEDIS : "menghasilkan"
    JANJI_TEMU ||--o| PEMBAYARAN : "menghasilkan"
    REKAM_MEDIS ||--o{ RESEP_OBAT : "mencakup"


