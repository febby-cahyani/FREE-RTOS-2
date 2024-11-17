# FREE-RTOS-2
Proyek ini menunjukkan penggunaan FreeRTOS pada mikrokontroler STM32F103C8T6 untuk menjalankan beberapa task yang mengontrol LED. Sistem ini terdiri dari dua task utama yang bertanggung jawab untuk menyalakan LED hijau dan merah dengan pola tertentu, serta satu task default tambahan. Setiap fungsi ditangani dalam task terpisah yang dijadwalkan oleh FreeRTOS, sehingga memungkinkan multitasking dalam lingkungan realtime.

Diagram Task :
![Screenshot 2024-11-17 111316](https://github.com/user-attachments/assets/28d81531-757e-4022-8845-ce1cf9c48da0)

Hardware yang diperlukan :
1. STM32F103C8T6
2. LED

Software yang diperlukan :
1. STM32CubeIDE
2. FreeRTOS

Cara Kerja :
- Task FlashGreenLedTa mengontrol LED hijau dengan pola berikut :
  1. LED Hijau berkedip dengan interval setiap 0.5 detik, dan setelah 8 kali 
     berkedip (total 4 detik), LED akan mati dan task akan masuk ke delay selama 
     6 detik.
  2. Total periodik untuk task ini adalah 10 detik.
- Task FlashRedLedTask mengontrol LED merah dengan pola sebagai berikut :
  1. LED Merah berkedip cepat dengan interval 50ms, dan setelah 10 kali berkedip 
     (total 0.5 detik), LED akan mati dan task akan masuk ke delay selama 1.5 
     detik.
  2. Total periodik untuk task ini adalah 2 detik.
- Prioritas Task :
  1. Task FlashRedLedTask memiliki prioritas lebih tinggi dari task 
     FlashGreenLedTa sehingga akan mem-preempt task hijau ketika dijadwalkan.

Pinout Hardware :

![Pinout Hardware FreeRTOS](https://github.com/user-attachments/assets/8a5312a5-574a-4175-9b8d-5f23355ca97f)

Hasil Hardware :

![FreeRTOS2](https://github.com/user-attachments/assets/2faa76ea-e178-46e9-853f-ff6e1f72f110)


Setelah program diunggah ke STM32F103C8T6, perangkat akan menampilkan hasil sebagai berikut :
1. LED Hijau :
   - Berkedip dengan pola lambat setiap 10 detik.
   - Ketika LED Merah (prioritas lebih tinggi) aktif, LED Hijau akan berhenti 
     sementara (preempted).
3. LED Merah :
   - Berkedip dengan pola cepat setiap 2 detik.
   - Karena memiliki prioritas lebih tinggi, LED Merah akan mem-preempt LED 
     Hijau saat berjalan.
     
Project ini dikerjakan di Politeknik Elektronika Negeri Surabaya dengan dosen pengampu bapak Fernando Ardilla
