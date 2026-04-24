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
    fun getJudul(): String = judul
    fun getStok(): Int = stok

    fun kurangiStok() {
        if (stok > 0) stok--
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

    fun setDenda(status: Boolean) {
        statusDenda = status
    }

    fun pinjamBuku(buku: Buku) {
        println("\n$nama mencoba meminjam: ${buku.getJudul()}")

        if (statusDenda) {
            println("Peminjaman ditolak: Masih ada denda")
        } else if (jumlahPinjam >= 3) {
            println("Peminjaman ditolak: Maksimal 3 buku")
        } else if (buku.getStok() == 0) {
            println("Peminjaman ditolak: Stok habis")
        } else {
            buku.kurangiStok()
            jumlahPinjam++
            println("Peminjaman berhasil")
        }
    }

    fun kembalikanBuku(buku: Buku) {
        if (jumlahPinjam > 0) {
            buku.tambahStok()
            jumlahPinjam--
            println("Buku dikembalikan: ${buku.getJudul()}")
        }
    }
}

class Pustakawan(
    private val id: Int,
    private val nama: String
)

fun main() {
    val buku1 = Buku(1, "Pemrograman Kotlin", 2)
    val buku2 = Buku(2, "Struktur Data", 1)

    val anggota = Anggota(1, "Ricky Alfian Ronaldo")

    anggota.pinjamBuku(buku1)
    anggota.pinjamBuku(buku1)
    anggota.pinjamBuku(buku1)

    anggota.setDenda(true)
    anggota.pinjamBuku(buku2)

    anggota.setDenda(false)
    anggota.kembalikanBuku(buku1)

    anggota.pinjamBuku(buku2)
}
