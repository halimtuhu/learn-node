# Getting Started with Node Js

Node.js adalah perangkat lunak yang didesain untuk mengembangkan aplikasi berbasis web dan ditulis dalam sintaks bahasa pemrograman JavaScript. Bila selama ini kita mengenal JavaScript sebagai bahasa pemrograman yang berjalan di sisi client / browser saja, maka Node.js ada untuk melengkapi peran JavaScript sehingga bisa juga berlaku sebagai bahasa pemrograman yang berjalan di sisi server, seperti halnya PHP, Ruby, Perl, dan sebagainya. Node.js dapat berjalan di sistem operasi Windows, Mac OS X dan Linux tanpa perlu ada perubahan kode program. Node.js memiliki pustaka server HTTP sendiri sehingga memungkinkan untuk menjalankan server web tanpa menggunakan program server web seperti Apache atau Nginx.

Untuk mengeksekusi Javascript sebagai bahasa server diperlukan engine yang cepat dan mempunyai performansi yang bagus. Engine Javascript dari Google bernama V8-lah yang dipakai oleh Node.js yang juga merupakan engine yang dipakai oleh browser Google Chrome.

## Installation

Cukup download dan ikuti petunjuk installasi yang ada pada https://nodejs.org/en/download/

## Starting

Setelah selesai melakukan instalasi, kita dapat mencoba node dengan membuka terminal atau command prompt dan menjalankan command berikut.
```
PS E:\Github\learn-node> node -v
v10.16.2
```
Selain node, kita juga dianjurkan untuk menginstall npm. Bagi pengguna windows, instalasi sudah menjadi satu bundle. Namun untuk pengguna linus terpisah sehingga melakukan instalasi npm lagi.

Setelah itu coba jalankan command berikut untuk memastikan apakah npm sudah benar terinstall
```
PS E:\Github\learn-node> npm -v
6.9.0
```

Proses installasi sudah selesai dan siap bekerja dengan `node.js`