# Start Server

Memulai service backend dengan membuat project baru bernama `http-server`.

## Membuat server
1. Membuat folder baru project baru
   ```
   mkdir http-server
   ```
2. Membuat file javascript baru bernama `app.js`
3. Deklarasi variabel constant `http` yang berisi module `http`. Variable ini berisi segala kebutuhan yang berurusan dengan HTTP service
   ```js
   const http = require('http')
   ```
4. Membuat server yang disimpan pada variabel konstan `server`. Blok kode program ini bertujuan untuk memulai server pada port 3000 agar kita dapat mengaksesnya melalui local server kita di http://localhost:3000. 
   ```js
   const server = http.createServer(function (request, response) {
       // Server activity goes here
   }).listen(3000)
   ```
5. Kita dapat menambahkan info bahwa server sudah berjalan pada port yang kita tentukan dengan menambahkan log setelah selesai deklarasi variable `server`
   ```js
   console.log('Server started at port 3000')
   ```
6. Dari sini kita sudah bisa mencoba mengeksekusi file `app.js`.
   ```
   node app
   ```
   Output yang harusnya diberikan adalah log `Server started at port 3000`

## Mengelolah request
1. Selanjutkan kita dapat mengelolah request yang dikirim dari user / sisi client
2. Kita dapat memberikan kondisi untuk memeriksa url yang diakses user saat ini.
3. Kita tambahkan pengkondisian pada blok program `server`
   ```js
    if (request.url == '/') {
        response.write('Welcome Home')
    } else if (request.url == '/about') {
        response.write('About Us')
    } else {
        response.status = 404
        response.write('URL no found')
    }
    response.end()
   ```
4. Jalankan server dan coba akses `http://localhost:3000` dan `http://localhost:3000/about`
5. Lalu coba akses url yang tidak kita definisikan seperti `http://localhost:3000/contact-us`
6. Pengkondisian juga dapat dilakukan dengan menggunakan `switch case`
   ```js
   switch (request.url) {
        case '/':
            response.write('Welcome Home')
            break
        case '/about':
            response.write('About Us')
            break
        default :
            response.write('404. Not Found')
            break
    }
   ```
   
## Summary
Secara keseluruhan struktur kode dari `app.js` adalah sebagai berikut
```js
const http = require('http')

const server = http.createServer(function (request, response) {

    // if (request.url == '/') {
    //     response.write('Welcome Home')
    // } else if (request.url == '/about') {
    //     response.write('About Us')
    // } else {
    //     response.status = 404
    //     response.write('URL no found')
    // }

    switch (request.url) {
        case '/':
            response.write('Welcome Home')
            break
        case '/about':
            response.write('About Us')
            break
        default :
            response.write('404. Not Found')
            break
    }

    response.end()

}).listen(3000)

console.log('Server is running at port 3000')
```
