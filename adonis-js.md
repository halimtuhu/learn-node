# Adonis JS

Adonis adalah salah satu framework NodeJs seperti Express. Framework ini mengikuti konsep yang serupa dengan framework PHP yaitu Laravel. Segala kebutuhan dasar untuk membangun aplikasi sudah disediakan oleh Adonis. Kali ini kita akan membuat API sederhana menggunakan framework Adonis dan MySql sebagai databasenya.

## Requirements

Berikut adalah hal-hal yang perlu kita siapkan untuk memulai membuat API dengan Adonis.

- Node.Js
- MySql (XAMPP)
- Adonis

## Adonis Installation

Kita akan mulai dengan menginstal Adonis CLI secara global di mesin kita dengan command di bawah.

```bash
$ npm i -g @adonisjs/cli
```

Setelah proses instalasi selesai, kita bisa cek apakah Adonis CLI sudah terinstall dengan command di bawah.

```bash
$ adonis --help
```

Command tersebut akan menampilkan output berupa deretan command `adonis` yang bisa kita gunakan

```bash
$ adonis --help
Usage:
  command [arguments] [options]

Global Options:
  --env              Set NODE_ENV before running the commands
  --no-ansi          Disable colored output
  --version          output the version number

Available Commands:
  addon              Create a new AdonisJs addon
  install            Install Adonisjs provider from npm/yarn and run post install instructions
  new                Create a new AdonisJs application
  repl               Start a new repl session
  serve              Start Http server
 key
  key:generate       Generate secret key for the app
 make
  make:command       Make a new ace command
  make:controller    Make a new HTTP or Websocket channel controller
  make:ehandler      Make a new global exception handler
  make:exception     Make a new exception
  make:hook          Make a new lucid model hook
  make:listener      Make a new event or redis listener
  make:middleware    Make a new HTTP or Ws Middleware
  make:migration     Create a new migration file
  make:model         Make a new lucid model
  make:provider      Make a new provider
  make:seed          Create a database seeder
  make:trait         Make a new lucid trait
  make:view          Make a view file
 route
  route:list         List all registered routes
 run
  run:instructions   Run instructions for a given module
```

Setelah itu kita bisa langsung membuat base project API kita dengan command di bawah.

```bash
$ adonis new adonis-book-store --api-only
```

Dengan command di atas, kita akan membuat project API bernama `adonis-book-store`. Jika `--api-only` dihilangkan, makan kita akan membuat project Full Stack yang mana Adonis akan menyediakan view engine yaitu Edge. Namun pada project ini kita akan membuat API terlebih dahulu untuk urusan *Backend*.

Setelah proses instalasi selesai, kita bisa langsung menuju folder project kita dan jalankan aplikasinya dengan command 

```bash
$ cd adonis-book-store

$ adonis serve --dev
```

Command tersebut akan menjalankan aplikasi pada port yang diset pada file `.env`. Default port yang diberikan oleh Adonis adalah `3333`. Kita bisa langsung mencoba membuat request ke http://127.0.0.1:3333 di Postman. Secara default, response yang diberikan adalah sebagai berikut.

```json
{
    "greeting": "Hello world in JSON"
}
```

Pada tahap ini, kita sudah selesai menginstall Adonis.