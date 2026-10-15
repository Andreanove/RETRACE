# RETRACE — Combat Playground Roadmap

## Tujuan Playground

- [ ] 1 Player
- [ ] 1 Clara
- [ ] 10 Soldier
- [ ] 2 Defense Tower
- [ ] 5 Table / Cover
- [ ] 3 Destroyed Oil Barrel
- [ ] 1 Intact Oil Barrel

Core mechanic yang harus terbukti:

- [x] Player bisa bergerak dan menembak
- [ ] Soldier bisa bertarung secara taktis
- [ ] Soldier bisa memakai navigation
- [ ] Soldier bisa mencari dan menggunakan cover
- [x] Cover bisa berubah / hancur
- [ ] Clara bisa menerima command dari player
- [ ] Clara bisa melakukan RETRACE pada object
- [ ] Destroyed object bisa kembali ke state sebelumnya
- [ ] Tower yang dihancurkan bisa diretrace
- [ ] Tower hasil RETRACE menjadi ally player
- [ ] Soldier bisa bereaksi terhadap allied tower
- [ ] Environment benar-benar memengaruhi keputusan combat

---

# MILESTONE 0 — Playground Testbed

## Goal

Membuat arena kecil dan stabil sebagai tempat seluruh sistem combat diuji.

Tidak perlu bagus secara visual.

Gunakan:

- primitive
- sprite placeholder
- tile sederhana
- warna berbeda untuk membedakan object

## Arena

- [x] Buat scene `CombatPlayground`
- [x] Buat lantai arena
- [x] Buat batas arena / wall
- [x] Pastikan Player tidak bisa keluar arena
- [x] Pastikan collision arena stabil
- [x] Buat beberapa obstacle statis sementara

## Player

- [x] Player movement 4 arah
- [x] CharacterBody2D menggunakan `Floating`
- [x] Aim 360°
- [x] WeaponPivot
- [x] GunSprite
- [x] Muzzle
- [x] AimLaser
- [x] Hitscan shooting
- [x] Dodge
- [x] dodge cooldown
- [x] player energy
- [x] Camera focus on player
- [x] Shooting cooldown sederhana
- [x] Player health
- [x] Player bisa menerima damage
- [x] Player bisa mati
- [x] Bug Aim pada diri sendiri

## Debug

- [x] Bisa melihat collision shape
- [x] Bisa melihat navigation debug
- [x] Bisa print state sementara
- [x] Bisa restart playground dengan cepat

## Definition of Done

Player bisa masuk arena, bergerak, aim, shoot, menerima damage, mati, dan restart.

Environment belum perlu cantik.

---

# MILESTONE 1 — Prototype Table / Cover

## Goal

Membuat satu object cover yang cukup stabil sebelum Soldier AI dikembangkan.

Ini penting karena Soldier nantinya akan mengambil keputusan berdasarkan cover ini.

## Table

Buat satu scene:

`Table.tscn`

State awal cukup:

- [x] Standing
- [x] Tipped
- [x] Destroyed

## Standing Table

- [x] Memiliki sprite placeholder
- [x] Memiliki collision
- [x] Belum berfungsi sebagai cover jika memang belum digulingkan
- [x] Meja punya detector

## Tipped Table

- [x] Player bisa menggulingkan meja
- [x] Collision berubah mengikuti posisi meja
- [x] buat collision untuk menghalangi pergerakan
- [x] Meja sekarang bisa menjadi cover
- [x] Meja memiliki HP

## Destroyed Table

- [x] Meja bisa menerima damage
- [x] HP mencapai 0
- [x] Meja masuk state `Destroyed`
- [x] Collision cover hilang / berubah
- [x] Visual berubah menjadi placeholder destroyed

## Cover Points

Jangan buat AI menghitung bentuk meja sendiri dulu.

Sediakan Marker2D:

- [x] CoverPointLeft
- [x] CoverPointRight
- [x] CoverPointTop
- [x] CoverPointBottom

Tidak semuanya harus aktif setiap saat.

## Definition of Done

Satu meja bisa:

Standing → Tipped → Destroyed

dan tersedia titik yang nantinya bisa dipilih Soldier sebagai cover.

---

# MILESTONE 2 — Navigation Environment

## Goal

Membuat arena yang bisa dinavigasi AI secara konsisten.

## Navigation

- [ ] Tambahkan NavigationRegion2D
- [ ] Buat navigation polygon arena
- [ ] Pastikan Soldier prototype bisa bergerak menuju suatu titik
- [ ] Soldier bisa menghindari wall
- [ ] Soldier bisa bergerak mengelilingi obstacle

## Dynamic Environment Test

- [ ] Uji apa yang terjadi ketika Table berubah state
- [ ] Tentukan apakah tipped table memblok navigation
- [ ] Tentukan apakah destroyed table tidak lagi memblok navigation
- [ ] Pastikan navigation tidak rusak setelah perubahan object

Catatan:

Untuk prototype awal, navigation tidak harus otomatis rebuild dengan sistem paling canggih.

Yang penting kita tahu metode apa yang akan dipakai ketika environment berubah.

## Definition of Done

Satu CharacterBody2D bisa diberikan target posisi dan mencapai target tanpa menembus environment.

---

# MILESTONE 3 — Soldier Foundation

## Goal

Membuat satu Soldier yang menjadi basis seluruh enemy Soldier berikutnya.

Buat:

`Soldier.tscn`

## Basic Components

- [ ] CharacterBody2D
- [ ] Floating Motion Mode
- [ ] Sprite placeholder
- [ ] CollisionShape2D
- [ ] NavigationAgent2D
- [ ] Health
- [ ] Damage
- [ ] Death
- [ ] Weapon / shooting point

## Soldier Combat States

Mulai dengan FSM.

State awal:

- [x] IDLE
- [ ] ALERT
- [ ] MOVE
- [ ] TAKE_COVER
- [ ] ATTACK
- [ ] REPOSITION
- [ ] DEAD

Belum perlu:

- Reload
- Flanking kompleks
- Squad communication

## Definition of Done

Soldier memiliki FSM yang bisa berubah state secara jelas dan state bisa ditampilkan menggunakan debug text.

---

# MILESTONE 4 — Soldier Detection & Line of Sight

## Goal

Soldier tidak otomatis mengetahui posisi Player setiap saat.

## Detection

- [ ] Detection range
- [ ] Player masuk detection range
- [ ] Soldier menjadi Alert
- [ ] Soldier memiliki target

## Line of Sight

- [ ] Raycast Soldier → Player
- [ ] Wall memblok LOS
- [ ] Table memblok LOS jika sesuai state
- [ ] Soldier hanya menembak jika Player terlihat

## Last Known Position

Optional untuk tahap awal, tetapi bagus jika mudah:

- [ ] Simpan posisi terakhir Player terlihat
- [ ] Soldier bisa menuju posisi tersebut jika LOS hilang

## Definition of Done

Player bisa bersembunyi di balik object dan Soldier tidak menembak menembus cover.

---

# MILESTONE 5 — Soldier Basic Ranged Combat

## Goal

Membuat Soldier benar-benar bisa bertarung.

## Weapon

Untuk sekarang:

- [ ] Infinite ammo
- [ ] Tidak ada reload
- [ ] Ada cooldown antar tembakan
- [ ] Soldier aim ke target
- [ ] Soldier shoot jika LOS valid

## Damage

- [ ] Player menerima damage
- [ ] Soldier menerima damage
- [ ] Soldier mati jika HP 0
- [ ] Player mati jika HP 0

## Definition of Done

Player dan satu Soldier bisa saling membunuh.

Combat belum perlu pintar.

---

# MILESTONE 6 — Soldier Cover Decision

## Goal

Ini adalah awal tactical AI sebenarnya.

Soldier harus bisa menjawab:

> "Apakah saya perlu cover?"

## Cover Search

- [ ] Soldier bisa mengetahui CoverPoint yang tersedia
- [ ] Soldier bisa mengetahui jarak ke cover
- [ ] Soldier bisa mengetahui apakah cover melindungi dari Player
- [ ] Soldier memilih cover
- [ ] NavigationAgent bergerak menuju cover

## Simple Decision Rules

Contoh pertama:

- [ ] Tidak punya cover + Player terlihat → cari cover
- [ ] Sudah di cover + Player terlihat → attack
- [ ] Cover hancur → reposition
- [ ] Player berpindah sehingga cover tidak berguna → reposition

## Definition of Done

Satu Soldier bisa secara otomatis:

Detect Player → Find Cover → Move → Shoot → Reposition

---

# MILESTONE 7 — Cover Reservation

## Goal

Mencegah banyak Soldier memilih tempat yang sama.

## Reservation

Setiap CoverPoint punya state:

- [ ] Available
- [ ] Reserved

Ketika Soldier memilih cover:

- [ ] Reserve CoverPoint
- [ ] Soldier lain tidak bisa memilihnya

Ketika Soldier:

- [ ] Meninggalkan cover
- [ ] Mati
- [ ] Memilih cover lain

maka:

- [ ] Reservation dilepas

## Definition of Done

3 Soldier bisa mencari cover tanpa menumpuk di satu titik.

---

# MILESTONE 8 — Scale Test: 3 Soldiers

## Goal

Jangan langsung 10.

Gunakan 3 Soldier dulu untuk menemukan bug AI multiplayer.

## Test

- [ ] 3 Soldier bisa pathfind bersamaan
- [ ] Tidak terlalu sering bertabrakan
- [ ] Tidak memakai cover yang sama
- [ ] Tidak menumpuk
- [ ] Tidak semua melakukan state yang sama secara aneh
- [ ] Semua bisa menyerang Player

## Debug Info

Di atas Soldier tampilkan sementara:

- [ ] Current State
- [ ] Current Target
- [ ] Current Cover
- [ ] HP

## Definition of Done

3 Soldier bisa bertarung tanpa AI terlihat rusak.

---

# MILESTONE 9 — Dynamic Table Combat

## Goal

Membuktikan AI bisa bereaksi saat environment berubah.

Tambahkan 5 table.

## Player Interaction

- [ ] Player bisa menggulingkan Table
- [ ] Tipped Table menjadi cover

## Destruction

- [ ] Soldier bisa menembak Table
- [ ] Player bisa menembak Table
- [ ] Table bisa hancur

## AI Reaction

- [ ] Cover hancur
- [ ] Soldier mengetahui cover tidak valid
- [ ] Soldier keluar dari TAKE_COVER
- [ ] Soldier memilih cover baru
- [ ] Soldier pathfind menuju cover baru

## Definition of Done

Menghancurkan meja yang sedang digunakan Soldier menyebabkan Soldier mengambil keputusan baru.

---

# MILESTONE 10 — Oil Barrel

## Goal

Membuat environmental combat pertama.

Buat:

`OilBarrel.tscn`

## Barrel State

- [ ] Intact
- [ ] Destroyed

## Intact

- [ ] Bisa ditembak
- [ ] Memiliki HP
- [ ] Meledak ketika trigger terpenuhi

## Explosion

- [ ] Area damage
- [ ] Bisa damage Soldier
- [ ] Bisa damage Player
- [ ] Bisa damage Table
- [ ] Bisa damage Tower

Untuk prototype:

- animasi tidak penting
- explosion bisa berupa lingkaran debug

## Arena Setup

- [ ] 1 Intact Barrel
- [ ] 3 Destroyed Barrel

## Definition of Done

Player bisa menggunakan Barrel sebagai environmental weapon.

---

# MILESTONE 11 — RETRACE Foundation

## Goal

Membuat sistem RETRACE generik.

Jangan mulai dari Clara.

Mulai dari object yang bisa di-RETRACE.

## Retraceable Object Concept

Object bisa memiliki:

- [ ] Current State
- [ ] Previous / Restorable State
- [ ] `retrace()` behaviour

Contoh:

Table:

Destroyed → Tipped

Barrel:

Destroyed → Intact

Tower:

Destroyed → Restored

## Important

Hindari:

if object == Table
if object == Barrel
if object == Tower

jika memungkinkan.

Object sebaiknya tahu sendiri apa yang terjadi ketika:

`retrace()`

dipanggil.

## Definition of Done

Satu fungsi/action RETRACE bisa memulihkan Table dan Barrel tanpa logic khusus di Player.

---

# MILESTONE 12 — Clara Foundation

## Goal

Clara belum perlu AI cerdas.

Clara pertama-tama hanya companion yang menerima perintah.

## Clara

- [ ] CharacterBody2D
- [ ] NavigationAgent2D
- [ ] Follow Player sederhana
- [ ] Bisa berhenti
- [ ] Bisa menerima target

## Player Command

Player:

- [ ] Hover / aim object
- [ ] Object valid mendapat indicator
- [ ] Tekan command RETRACE
- [ ] Clara menerima target

## Clara Execution

Clara:

- [ ] Pathfind menuju target
- [ ] Berhenti pada jarak tertentu
- [ ] Melakukan RETRACE
- [ ] Kembali mengikuti Player

## Definition of Done

Player bisa menunjuk destroyed Table / Barrel dan memerintahkan Clara untuk memulihkannya.

---

# MILESTONE 13 — Tower Foundation

## Goal

Membuat turret sebagai combat actor.

Buat:

`DefenseTower.tscn`

## Tower FSM

State:

- [ ] SEARCH
- [ ] AIM
- [ ] SHOOT
- [ ] COOLDOWN
- [ ] DESTROYED

Tidak perlu AI kompleks.

## Enemy Tower

- [ ] Mendeteksi Player
- [ ] Aim
- [ ] Shoot
- [ ] Damage Player
- [ ] Bisa menerima damage
- [ ] Bisa dihancurkan

## Definition of Done

Tower berfungsi sebagai enemy statis.

---

# MILESTONE 14 — Faction System

## Goal

Ini penting sebelum Tower bisa berpindah pihak.

Faction minimal:

- [ ] PLAYER
- [ ] ENEMY
- [ ] NEUTRAL

Setiap combat actor:

- [ ] Memiliki faction
- [ ] Bisa mengecek apakah target hostile

## Targeting

Enemy Soldier:

- [ ] Player adalah hostile
- [ ] Enemy Tower bukan hostile

Player Tower:

- [ ] Soldier hostile
- [ ] Player tidak hostile

## Definition of Done

Targeting tidak lagi bergantung pada nama node seperti `"Player"` atau `"Enemy"`.

---

# MILESTONE 15 — RETRACE Tower / Faction Flip

## Goal

Menguji salah satu fitur paling penting RETRACE.

Flow:

Enemy Tower
→ Destroyed
→ Clara RETRACE
→ Restored
→ Faction berubah menjadi PLAYER
→ Tower menyerang Soldier

## Tasks

- [ ] Enemy Tower bisa destroyed
- [ ] Tower merupakan Retraceable
- [ ] Clara bisa memilih Tower sebagai target
- [ ] Tower diretrace
- [ ] Tower kembali aktif
- [ ] Tower berubah faction
- [ ] Tower mencari Soldier
- [ ] Tower menyerang Soldier
- [ ] Soldier mengetahui Tower sekarang hostile
- [ ] Soldier bisa menyerang Tower

## Definition of Done

Satu Tower bisa berubah dari ancaman Player menjadi asset Player melalui RETRACE.

---

# MILESTONE 16 — Soldier Target Selection

## Goal

Soldier tidak selalu mengejar Player.

Potential targets:

- [ ] Player
- [ ] Allied Tower

Optional nanti:

- Clara

## Simple Threat Rules

Prototype bisa sederhana:

- [ ] Target harus hostile
- [ ] Target harus hidup
- [ ] Prefer target terlihat
- [ ] Prefer target dalam range
- [ ] Pilih target berdasarkan distance / simple score

Belum perlu GOAP.

## Definition of Done

Soldier bisa berpindah target antara Player dan retraced Tower secara masuk akal.

---

# MILESTONE 17 — Scale Test: 10 Soldiers

## Goal

Sekarang baru kita pakai jumlah final playground.

Arena:

- [ ] 10 Soldier
- [ ] 2 Tower
- [ ] 5 Table
- [ ] 4 Barrel
- [ ] Player
- [ ] Clara

## Stress Test

- [ ] Navigation stabil
- [ ] Soldier tidak menumpuk
- [ ] Cover reservation bekerja
- [ ] Soldier bisa kehilangan cover
- [ ] Soldier bisa pindah target
- [ ] Soldier bereaksi terhadap Tower
- [ ] Soldier bereaksi terhadap destroyed environment
- [ ] FPS masih baik
- [ ] Tidak ada error spam

## Combat Coordination

Jika diperlukan:

- [ ] Batasi jumlah Soldier yang aktif menembak sekaligus
- [ ] Soldier lain reposition
- [ ] Variasikan shoot cooldown
- [ ] Variasikan decision timing

Tujuannya bukan membuat mereka bodoh.

Tujuannya mencegah 10 Soldier menjadi firing squad sempurna.

---

# MILESTONE 18 — Final Playground Integration

## Final Arena

- [ ] 1 Player
- [ ] 1 Clara
- [ ] 10 Soldier
- [ ] 2 Enemy Tower
- [ ] 5 Table
- [ ] 3 Destroyed Barrel
- [ ] 1 Intact Barrel

## Required Gameplay

- [ ] Player bisa menggunakan Table
- [ ] Player bisa menghancurkan cover
- [ ] Soldier bisa memakai cover
- [ ] Soldier bisa kehilangan cover
- [ ] Barrel bisa dipakai sebagai weapon
- [ ] Clara bisa menerima RETRACE command
- [ ] Clara bisa restore Table
- [ ] Clara bisa restore Barrel
- [ ] Clara bisa restore Tower
- [ ] Retraced Tower membantu Player
- [ ] Soldier menyerang Retraced Tower
- [ ] Player bisa mati
- [ ] Semua enemy bisa mati

## Win / Lose

- [ ] Player HP 0 → Lose
- [ ] Semua enemy selesai → Win
- [ ] Restart

---

# MILESTONE 19 — Debug & Stabilization

## AI Debug

- [ ] Show Soldier FSM state
- [ ] Show current target
- [ ] Show selected cover
- [ ] Show reserved cover
- [ ] Show LOS
- [ ] Show navigation path jika dibutuhkan
- [ ] Show faction

## RETRACE Debug

- [ ] Show retraceable objects
- [ ] Show Clara target
- [ ] Show current object state

## Bug Tests

- [ ] Soldier mati saat menuju cover
- [ ] Cover hancur saat Soldier menuju cover
- [ ] Tower dihancurkan saat Clara menuju Tower
- [ ] Target mati sebelum Soldier menembak
- [ ] Clara target hilang
- [ ] Multiple Soldier memilih cover bersamaan
- [ ] Retraced Tower dihancurkan lagi
- [ ] Barrel meledak saat Clara mendekat
- [ ] Player mati saat Clara sedang melakukan command

---

# PLAYGROUND COMPLETE

Playground dianggap selesai ketika:

- [ ] Arena bisa dimainkan dari awal sampai akhir
- [ ] Tidak perlu manual debug intervention
- [ ] Core combat RETRACE terasa berfungsi
- [ ] 10 Soldier tetap stabil
- [ ] Dynamic cover bekerja
- [ ] Environmental combat bekerja
- [ ] Clara command bekerja
- [ ] RETRACE bekerja untuk beberapa jenis object
- [ ] Tower faction switching bekerja
- [ ] Enemy bereaksi terhadap perubahan dunia
- [ ] Tidak ada critical bug yang menghalangi gameplay