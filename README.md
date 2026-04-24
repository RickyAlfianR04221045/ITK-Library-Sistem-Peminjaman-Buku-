# ITK-Library-Sistem-Peminjaman-Buku-
Ujian Tengah Semester — Pemrograman Berorientasi Objek (TE2514027) Semester Genap 2025/2026 · Program Studi Teknik Elektro
/*
========================================================
Nama    : Ricky Alfian Ronaldo
NIM     : 04221045
Kelas   : PBO B
Tema    : ITK-Library (Sistem Peminjaman Buku)
Dosen   : Himawan Wicaksono, S.ST., M.T.
========================================================
*/

class Buku(
    private val id: Int,
    private val judul: String,
    private var stok: Int
) {
    fun getJudul(): String {
        return judul
    }

    fun getStok(): Int {
        return stok
    }

    fun kurangiStok() {
        if (stok > 0) {
            stok--
        }
    }

    fun tambahStok() {
        stok++
    }
}

class Anggota(
    private val id: Int,
    private val nama: String
) {
    private var jumlahPinjam: Int = 0
    private var statusDenda: Boolean = false

    fun getNama(): String {
        return nama
    }

    fun setDenda(status: Boolean) {
        statusDenda = status
    }

    fun pinjamBuku(buku: Buku) {
        println("\n$nama mencoba meminjam buku: ${buku.getJudul()}")

        if (statusDenda) {
            println("❌ Peminjaman ditolak: Masih ada denda")
        } else if (jumlahPinjam >= 3) {
            println("❌ Peminjaman ditolak: Maksimal 3 buku")
        } else if (buku.getStok() == 0) {
            println("❌ Peminjaman ditolak: Stok buku habis")
        } else {
            buku.kurangiStok()
            jumlahPinjam++
            println("✅ Peminjaman berhasil")
        }
    }

    fun kembalikanBuku(buku: Buku) {
        if (jumlahPinjam > 0) {
            buku.tambahStok()
            jumlahPinjam--
            println("📚 Buku berhasil dikembalikan: ${buku.getJudul()}")
        } else {
            println("⚠️ Tidak ada buku yang dipinjam")
        }
    }
}

class Pustakawan(
    private val id: Int,
    private val nama: String
) {
    fun kelolaBuku() {
        println("Pustakawan $nama sedang mengelola data buku")
    }
}

fun main() {
    // Data buku
    val buku1 = Buku(1, "Pemrograman Kotlin", 2)
    val buku2 = Buku(2, "Struktur Data", 1)

    // Data anggota
    val anggota1 = Anggota(1, "Ricky Alfian Ronaldo")

    // Simulasi peminjaman
    anggota1.pinjamBuku(buku1)
    anggota1.pinjamBuku(buku1)
    anggota1.pinjamBuku(buku1) // gagal (stok habis / batas pinjam)

    // Simulasi denda
    anggota1.setDenda(true)
    anggota1.pinjamBuku(buku2) // gagal (ada denda)

    // Pengembalian buku
    anggota1.setDenda(false)
    anggota1.kembalikanBuku(buku1)

    // Peminjaman lagi
    anggota1.pinjamBuku(buku2)
}
