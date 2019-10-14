# CRUD di Express.js

Belajar membuat CRUD di Express.js dengan studi kasus membuat Mini Blog. Silahkan ikuti langkah-langkah di bawah ini.

## Requirement
- Node.js
- Express.js
- [MySQL (XAMPP)](https://www.apachefriends.org/)

## Database Preparation
- Install XAMPP lalu aktifkan `apache` dan `mysql`
- Akses http://localhost/phpmyadmin
- Buat database baru dengan nama `blog`
- Buat table baru bernama `posts` dengan detail colomn sebagai berikut
  - `id` bigint(20) NOT NULL,
  - `title` varchar(255) NOT NULL,
  - `content` longtext NOT NULL,
  - `created_at` timestamp NOT NULL DEFAULT current_timestamp()

## Node Project Preparation
- Buat satu folder project baru dengan nama `blog`
- Buka terminal / command prompt / powershell pada `blog`
- Jalankan command
  ```
  npm init
  ```
- Kemudian install beberapa modul yang dibutuhkan dengan command
  ```
  npm install --save express mysql body-parser hbs
  ```
- Buat folder dan `views` di dalam folder project `blog`
- Buat file baru dengan nama `index.js`
- Ketikkan kode program berikut ke dalam index.js
  ```js
    const path = require('path') // use path module
    const express = require('express') // use express module
    const hbs = require('hbs') // use hbs view engine
    const bodyParser = require('body-parser') // use bodyParser middleware
    const mysql = require('mysql') // use mysql database

    const app = express() // create express app

    // configure connection
    const conn = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '',
        database: 'nodeapp'
    })

    // connect to db
    conn.connect((err) => {
        if (err) throw err
        console.log('Mysql Connected ...')
    })

    // set views file
    app.set('views', path.join(__dirname, 'views'))
    app.set('view engine', 'hbs')

    // use body parser middleware
    app.use(bodyParser.json())
    app.use(bodyParser.urlencoded({
        extended: false
    }))

    // set public folder
    app.use('/assets', express.static(__dirname + '/public'))

    // routes
    // index : post list
    app.get('/', (req, res) => {
        let sql = 'select * from posts'
        let query = conn.query(sql, (err, results) => {
            if (err) throw err
            res.render('index', {
                posts: results
            })
        })
    })

    // save new post
    app.post('/posts', (req, res) => {
        let data = {
            title: req.body.title,
            content: req.body.content
        }
        let sql = 'insert into posts set ?'
        let query = conn.query(sql, data, (err, results) => {
            if (err) throw err
            res.redirect('/')
        })
    })

    // update post
    app.post('/posts/edit', (req, res) => {
        let sql = 'update posts set title="'+req.body.title+'", content="'+req.body.content+'" where id='+req.body.id
        let query = conn.query(sql, (err, results) => {
            if (err) throw err
            res.redirect('/')
        })
    })

    // delete post
    app.post('/posts/delete', (req, res) => {
        let sql = 'delete from posts where id='+req.body.id+''
        let query = conn.query(sql, (err, results) => {
            if (err) throw err
            res.redirect('/')
        })
    })

    // listen server
    app.listen(8000, () => {
        console.log('Server is running at port 8000')
    })
  ```
- Buat file baru di dalam folder `views` dengan nama `index.hbs`
- Lalu ketikkan kode berikut.
  ```html
    <html>

    <head>
        <meta charset="utf-8">
        <title>CRUD Node.js and Mysql</title>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    </head>

    <body>
        <div class="container mt-4">
            <h2>Posts</h2>
            <div class="text-right my-2">
                <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#addPostModal">
                    New Post
                </button>
            </div>
            <div class="my-2">
                <table class="table">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <td>Title</td>
                            <td>Content</td>
                            <td>Created At</td>
                            <td>Action</td>
                        </tr>
                    </thead>
                    <tbody>
                        {{#each posts}}
                        <tr>
                            <td>{{ id }}</td>
                            <td>{{ title }}</td>
                            <td>{{ content }}</td>
                            <td>{{ created_at }}</td>
                            <td>
                                <button type="button" class="btn btn-warning btn-sm m-1 edit-post" data-id="{{ id }}" data-title="{{ title }}" data-content="{{ content }}">Edit</button>
                                <button type="button" class="btn btn-danger btn-sm m-1 delete-post" data-id="{{ id }}">Delete</button>
                            </td>
                        </tr>
                        {{/each}}
                    </tbody>
                </table>
            </div>
        </div>

        <div id="addPostModal" class="modal fade">
            <div class="modal-dialog modal-dialog-centered modal-lg">
                <div class="modal-content">
                    <div class="modal-header">
                        <h4 class="modal-title">Add New Post</h4>
                        <button type="button" class="close" data-dismiss="modal">&times;</button>
                    </div>
                    <div class="modal-body">
                        <form action="/posts" method="POST">
                            <div class="form-group">
                                <label for="title">Title</label>
                                <input type="text" class="form-control" name="title" id="title">
                            </div>
                            <div class="form-group">
                                <label for="content">Content</label>
                                <textarea name="content" id="content" class="form-control" rows="10"></textarea>
                            </div>
                            <div class="form-group text-center">
                                <button class="btn btn-primary" type="submit">Save Post</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>

        <div id="editPostModal" class="modal fade">
            <div class="modal-dialog modal-dialog-centered modal-lg">
                <div class="modal-content">
                    <div class="modal-header">
                        <div class="modal-title">Edit Post</div>
                        <button type="button" class="close" data-dismiss="modal">&times;</button>
                    </div>
                    <div class="modal-body">
                        <form action="/posts/edit" method="POST">
                            <input type="hidden" name="id" id="edit_id">
                            <div class="form-group">
                                <label for="edit_title">Title</label>
                                <input type="text" class="form-control" name="title" id="edit_title">
                            </div>
                            <div class="form-group">
                                <label for="edit_content">Content</label>
                                <textarea name="content" id="edit_content" class="form-control" rows="10"></textarea>
                            </div>
                            <div class="form-group text-center">
                                <button class="btn btn-primary" type="submit">Update Post</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>

        <div id="deletePostModal" class="modal fade">
            <div class="modal-dialog modal-dialog-centered modal-lg">
                <div class="modal-content">
                    <div class="modal-header">
                        <div class="modal-title">Delete Post Confirmation</div>
                        <button type="button" class="close" data-dismiss="modal">&times;</button>
                    </div>
                    <div class="modal-body">
                        <form action="/posts/delete" method="POST">
                            <div class="form-group">
                                <p>Apakah anda yakin ingin menghapus post ini ?</p>
                                <input type="hidden" id="delete_id" name="id">
                            </div>
                            <div class="form-group text-center">
                                <button class="btn btn-primary" type="submit">Delete Post</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>

        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
        <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
        
        <script>
            $('.edit-post').on('click', function () {
                var id = $(this).data('id')
                var title = $(this).data('title')
                var content = $(this).data('content')

                $('#editPostModal').modal('show')
                
                $('#edit_id').val(id)
                $('#edit_title').val(title)
                $('#edit_content').val(content)
            })

            $('.delete-post').on('click', function () {
                var id = $(this).data('id')

                $('#deletePostModal').modal('show')

                $('#delete_id').val(id)
            })
        </script>
    </body>

    </html>
  ```
- Coba aplikasi dengan jalankan command berikut
  ```
  node index
  ```
  Output dari command adalah sebagai berikut
  ```
  Server is running at port 8000
  Mysql Connected ...
  ```
- Setelah itu silahkan akses http://localhost:8000
- Silahkan klik tombol tambah dan masukan data blog baru
- Pastikan data masuk dan tampil pada tabel