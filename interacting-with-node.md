# Interacting with Node

Kita bisa dengan mudah berinteraksi dengan node dengan menggunakan command berikut.
```
PS E:\Github\learn-node> node
>
```

Setelah itu kita dapat menulis kode program `javascript` seperti biasanya.

Kita akan mencoba untuk mendeklarasikan variabel kemudian memunculkannya di terminal.
```
PS E:\Github\learn-node> node
> var a = 100000
undefined
> console.log(a)
100000
undefined
>
```
Seperti yang terlihat di atas, kita mendeklarasikan variable a dengan nilai default adalah 100000. Setelah itu kita mengeluarkan variable itu dengan perinta `console.log(x)`

Kita juga dapat membuat function dengan cara sebagai berikut
```
> function getA() {
... console.log(a)
... }
undefined
> getA
[Function: getA]
> getA()
100000
undefined
>
```

Secara garis besar dengan interaksi ini kita dapat mengakses seluruh sintak javascript. Berikut adalah contoh penggunaan `if`, `for`.
```
> var a = 100
undefined
> if (a % 2 == 0) {
... console.log('genap')
... } else {
... console.log('ganjil')
... }
genap
undefined
>
```
```
> for (i = 0; i <= 10; i+=2) {
... console.log(i)
... }
0
2
4
6
8
10
undefined
>
```
