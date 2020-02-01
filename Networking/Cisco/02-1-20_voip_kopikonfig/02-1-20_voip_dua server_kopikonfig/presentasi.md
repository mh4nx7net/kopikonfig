yak ketemu lagi kita di kopikonfig
pada pertemuan kali ini kita akan melanjutkan pembahasan mengenai instalasi
voip server. jika pada pertemuan sebelumnya kita melakukan installasi pada satu server
maka kali ini kita akan melakukan pembahasan mendalam dengan melakukan installasi mengg
-unakan dua buah server, bahkan nantinya bisa saja dengan routing kepala nomor yang berbeda
jika pada penerapan dunia nyata, misal 
amerika memiliki prefik +1
di indonesia dengan prefik +62

yak seperti itu, misal svrA dg 1xxx svrB dg 2xxx
oke langsung saja. bagi yang belum paham dasar instalasi
silahkan simak divideo sebelumnya, untuk jaringan dasar link saya sertakan dibawah

sekiranya topologi terlihat seperti berikut
oke akan coba saya demokan dahulu

dalam demo berikut, tel dg nomor 200 dapat menghubungi tel dg no 201
padahal no200 berada pada svr1 dan 201 pada svr2

jika kita lihat lebih jauh, konfigurasi yang kami gunakan sbg berikut

yak berikut adalah konfigurasinya, 
simak dalam opsi dial-peer voice 100 voip
kami melakukan deklarasi patern secara langsung(dedicated)
atas nomor 200, dengan jalur gateway melalui sesi target yang di
deklarasikan kepada ipv4:192.168.2.1
atau bisa saja ipv4:10.10.10.2

siapa sih ip yang saya sebutkan ?
dia adalah alamat untuk svr2


ok bagai mana dg skema berikut ?
jika saya memiliki nomor 100 di svr1 dan nomor 101 di svr2
saya ingin melakukan komunikasi antar keduanya, bolak balik
atau bahkan hanya searah ?

mari kita simak
pertama mari kita buat pembukuan jalur, dengan cara 

//dial-peer voice [dictionary-number] voip
///destination-pattern [nomor destinasi]
///session target ipv4:[ip svr target]

deklarasi destinasi dapat menggunakan sbg berikut
regular expression must be of the form  ^[][^0-9,A-F#*.?+%()-]*T?(\$)?$
deklarasi sesi target dapat menggunakan sbg berikut
Must be of the form ^((loopback:rtp)|(dns:.*)|(ipv4:[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+(:[0-9]+)?)|(enum:([1-9]|1[0-5]))|(ras)|(sip-server))$Or ^((settlement)|(settlement:[0-0]+))$
selengkapnya baca2 mengenai regex(regular expresion)

maka konfigurasi akan nampak seperti tertera
apakah ini berhasil ? mari kita coba
mantab berhasil

mari kita lanjut
bagai mana dengan skenario jika 
svrA memiliki +62xx
dan svrB memiliki +63xxx

mari kita coba dengan membuat dialphone dari awal
yak perangkat telah mendapat nomor, dalam satu svr harusnya sdh
bisa berkomunikasi, ok
dalam antar server masih belum bisa, perlu kita routing

caranya sama seperti tadi
oke done

kurang lebihnya setingan seperti itulah
dengan melakukan regex, anda dapat menyesuaikan konfigurasi sesuai
dengan prasarat dan kondisi skema/skenario yang akan anda gunakan

misal anda dpt mendeklarasikan destinasi scr lsg dg 
nomor 621001
atau juga bisa dg
nomor 62100.

titik dalam regex umum seperti shell pada linux misalnya 
artinya * (atau keseluruhan)

untuk parameter lain bisa anda lakukan uji lab sendiri

sekiranya video cukup sekian terimakasih telah mengikuti kopikonfig

