# Profiling Exercise

## Muhammad Haekal Klalipaksi
## 220681490

### Screenshot

#### Screenshot: JMeter `/all-student`
![/all-student](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/all-student.png)

#### Screenshot: JMeter `/all-student-name`
![/all-student-name](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/all-student-name.png)

#### Screenshot: JMeter `/highest-gpa`
![/highest-gpa](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/highest-gpa.png)


#### Screenshot: JMeter Log untuk `/all-student`
![/all-student log](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/all-student-cli.png)

#### Screenshot: JMeter Log untuk `/all-student-name`
![/all-student-name log](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/all-student-name-cli.png)

#### Screenshot: JMeter Log untuk `/highest-gpa`
![/highest-gpa log](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/highest-gpa-cli.png)

---

### Optimizing Code

#### `/all-student (getAllStudentWithCourse)`
**Before**
![before](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/all-student-before.png)
_Total Time : 62,243 ms_

**After**
![after](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/all-student-after.png)
_Total Time : 1,055 ms_

---

#### `/all-student-name (joinStudentName)`
**Before**
![before](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/join-student-name-before.png)
_Total Time : 457 ms_

**After**
![after](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/join-student-name-after.png)
_Total Time : 60 ms_

---

#### `/highest-gpa (findStudentWithHighestGPA)`
**Before**
![before](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/highest-gpa-before.png)
_Total Time : 150 ms_

**After**
![after](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/highest-gpa-after.png)
_Total Time : 63 ms_

---

### JMeter after optimizing

#### '/all-student'
![/all-student log after](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/all-student-cli-after.png)

#### '/all-student-name'
![/all-student-name log after](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/all-student-name-cli-after.png)

#### '/highest-gpa'
![/highest-gpa log after](https://aneyyrgbcsggfbaehqdr.supabase.co/storage/v1/object/public/adpro/highest-gpa-cli-after.png)

Kesimpulan:

Berdasarkan test yang dilakukan oleh JMeter dapat dilihat bahwa terjadi peningkatan _performance_ yang dibuktikan dengan _time elapsed_ yang lebih cepat. Hasil tersebut memiliki hubugan linear dengan optimisasi kode yang sudah dilakukan dan hasil dari _profilling_ IntelliJ. Dapat disipmulkan bahwa dengan menggunakan profiller IntelliJ dan mengoptimisasi kode dapat meningkatkan performa.

---

### Refleksi

#### Nomor 1

_Performance Testing_ menggunakan JMeter digunakan untuk mengetahui _response time_ suatu endpoint dalam aplikasi. Sedangkan, _IntelliJ Profiler_ memiliki pendekatan untuk melihat _method_ yang menyebabkan suatu aplikasi memiliki load yang tinggi, sehingga dapat menjadi acuan dalam melakukan optimisasi.

#### Nomor 2

_IntelliJ Profiler_ membantu saya dalam mengetahui kode mana yang memiliki optimisasi buruk, lalu saya dapet melakukan optimisasi dan membandingkan hasil _IntelliJ Profiler_ sebelum dioptimisasi dan setelah dioptimisasi.

#### Nomor 3

Menurut saya _IntelliJ Profiler_ sangat berguna dalam menganalisis dan mengidentifikasi _bottlenecks_ dalam aplikasi, sehingga mudah untuk menentukan bagian kode yang perlu dioptimisasi.

#### Nomor 4

Tantangan yang paling sulit menurut saya adalah memahami seluruh informasi yang diberikan oleh _IntelliJ Profiler_, namun saya terus berusaha untuk memahami dan mencari informasi di google.

#### Nomor 5

Manfaat utama dari penggunaan _IntelliJ Profiler_ adalah dapat melihat bagian kode yang perlu dioptimisasi dan melihat performa suatu permethod yang dapat dilihat berdasarkan _cpu time_ dan _total time_

#### Nomor 6

Berdasarkan test yang saya lakukan, hasil teset JMeter dan _IntelliJ Profiler_ memiliki hasil yang berbanding lurus dan konsisten. Namun, jika terjadi perbedaan yang harus saya lakukan adalah melakukan test ulang dan melakukan validasi dari kedua test.

#### Nomor 7

Strategi yang saya lakukan adalah mengurangi kompleksitas dari method:

- Dalam method `getAllStudentWithCourse`, awalnya memiliki kompleksitas _O(N^2)_ dan memiliki performa yang sangat buruk berdasarkan hasil test JMeter maupun _Intellij Profile_. Pendekatan yang saya lakukan adalah melakukan pendekatan query dengan findAll langsung dari Student Course Repository.
- Dalam method `joinStudentName` awalnya menggunakan string, yang memiliki performa kurang baik berdasarkan test _Intellij Profiler_, oleh karena saya melakukan pendekatan query dengan select all student hanya namanya lalu melakukan join.
- Dalam method `findHighestGpa` awalnya melakukan iterasi untuk mencari nilai maksimum, sehingga memiliki kompleksitas O(N). Pendekatan yang saya lakukan adalah memilih elemen pertama jika student diurutkan berdasarkan gpa.

Untuk memastikan seluruh pendekatan yang saya lakukan memberikan dampak baik terhadap performa, saya melakukan profiling test ulang menggunakan _Intellij Profile_ dan memastikan seluruh method tersebut memiliki _total time_ yang lebih cepat.
