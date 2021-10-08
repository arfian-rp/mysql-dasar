<h1>DATABASE</h1>

`show databases;` //show all databases
`create databases name_db;` //create databases
`use name_db;` //use databases
`drop database name_db;` //delete database

<h1>TIPE DATA</h1>

<h2>number:</h2>

| tipedata  | ukuran |
| --------- | ------ |
| TINYINT   | 1byte  |
| SMALLINT  | 2bytes |
| MEDIUMINT | 3bytes |
| INT       | 4bytes |
| BIGINT    | 8bytes |

unsigned = dimulai dr 0 (tidak ada bil neg)

<h2>decimal:</h2>

| DECIMAL      | (maxlength, bil_dibelakang_koma) |
| ------------ | -------------------------------- |
| DECIMAL(5,2) | 999.99                           |
| DECIMAL(5,3) | 99.999                           |

dst...

<h2>number attribute:</h2>
TYPE(N) examp: INT(11) <br>
ZEROFILL examp: INT(3) ZEROFILL, 7 -> 007

<h2>string:</h2>
CHAR & VARCHAR:

| val    | CHAR(3) | STRG   | VARCHAR(3) | STRG   |
| ------ | ------- | ------ | ---------- | ------ |
| ''     | ' '     | 3bytes | ''         | 1byte  |
| 'ab'   | 'ab '   | 3bytes | 'ab'       | 3bytes |
| 'abc'  | 'abc'   | 3bytes | 'abc'      | 4bytes |
| 'abcd' | 'abc'   | 3bytes | 'abc'      | 4bytes |

<h2>enum:</h2>
string yg dapat kita tentukan pilihannya
ENUM('male','female') //hanya bisa menerima data male atau female

<h2>date&time:</h2>

| tipe      | format                                          |
| --------- | ----------------------------------------------- |
| DATE      | YYYY:MM:DD                                      |
| DATETIME  | YYYY:MM:DD HH:MM:SS                             |
| TIMESTAMP | YYYY:MM:DD HH:MM:SS //biasanya untuk created_at |
| TIME      | HH:MM:SS                                        |
| YEAR      | YYYY                                            |

default TIMESTAMP = CURRENT_TIMESTAMP;

<h2>boolean:</h2>
TRUE | FALSE

dll

<h1>TABLE</h1>

`show TABLES;` //show table

```sql
CREATE TABLE name_tbl
(
id INT,
nama VARCHAR(10),
)ENGINE = InnoDB;//create table
```

`DESC name_tbl;` //show table structure

`SHOW CREATE TABLE name_tbl;` //show table structure syntax

```sql
ALTER TABLE name_tbl
ADD COLUMN name_col TEXT,
DROP COLUMN name_col,
RENAME COLUMN name to new_name,
MODIFY name VARCHAR(30) AFTER id,
MODIFY id CHAR(4) FIRST; //mengubah table
```

`TRUNCATE name_tbl;` //menghapus semua data table lalu table dibuat ulang (mengkosongkan table)

`DROP name_tbl;` //permanent menghapus table

<h1>MEMASUKKAN DATA</h1>

```sql
INSERT INTO name_tbl
(col_yg_mau_diisi_engga_urut_gpp)
VALUES
(yg_akan_diisi_urut_sesuai_yg_diatas);
```

atau
(lbh dr 1 baris)

```sql
INSERT INTO name_tbl
(col_yg_mau_diisi_engga_urut_gpp)
VALUES
(yg_akan_diisi_urut_sesuai_yg_diatas),
(yg_akan_diisi_urut_sesuai_yg_diatas),
(yg_akan_diisi_urut_sesuai_yg_diatas);
```

<h1>MENGAMBIL DATA</h1>

`SELECT * FROM name_tbl;` //semua col
`SELECT id, name FROM name_tbl;` //hanya col id dan nama

<h1>PRIMARY KEY</h1>

//sebuah kolom yg ditunjuk sebagai id

//kalau misal kita menambahkan baris tetapi primary key ny sdh terdaftar maka mysql menolak

```sql
CREATE TABLE name_tbl
(
id INT,
nama VARCHAR(10),
PRIMARY KEY(id) //menjadikan col id sebagai primarykey
)ENGINE = InnoDB;
```

```sql
ALTER TABLE name_tbl
ADD PRIMARY KEY(id); //mengubah col id sebagai primarykey
```

<h1>WHERE CLAUSE</h1>

//memfilter dengan kriteria tertentu

`SELECT * FROM name_tbl WHERE name_col = value_yg_dicari;`

<h1>UPDATE DATA</h1>

```sql
UPDATE name_tbl
SET
name_col_yg_mau_diupdate = val_baru,
name_col_yg_mau_diupdate = val_baru
WHERE name_col = value_col_yg_diupdate;
```

MENGUBAH DENGAN VALUE (TANPA REPLACE)

```sql
UPDATE name_tbl
SET
price = price + 5000, //menambahkan value price dengan 5000
WHERE name_col = value_col_yg_diupdate;
```

<h1>DELETE DATA</h1>

`DELETE FROM name_tbl WHERE name_col = value_col_yg_dihapus;`

<h1>ALIAS</h1>

```sql
SELECT id AS 'kode',
name AS 'nama'
FROM name_tbl;
//meng"Aliaskan nama di colom
```

```sql
SELECT t.id as 'kode',
t.name as 'nama'
FROM name_tbl AS t;
//meng"Aliaskan nama di table
```

<h1>WHERE OPERATOR</h1>

<h2>OPERATOR pembanding</h2>

```sql
SELECT _ FROM name_tbl WHERE name_col = value_yg_dicari;
SELECT _ FROM name*tbl WHERE name_col != value_yg_dicari;
SELECT * FROM name*tbl WHERE name_col < value_yg_dicari;
SELECT * FROM name*tbl WHERE name_col > value_yg_dicari;
SELECT * FROM name*tbl WHERE name_col <= value_yg_dicari;
SELECT * FROM name_tbl WHERE name_col >= value_yg_dicari;
```

<h2>OPERATOR logika</h2>

```sql
SELECT _ FROM name_tbl WHERE name_col >= value_yg_dicari AND name_col = value_yg_dicari;
SELECT _ FROM name_tbl WHERE name_col >= value_yg_dicari OR name_col = value_yg_dicari;
SELECT * FROM name_tbl WHERE
(name_col >= value_yg_dicari OR name_col = value_yg_dicari)
AND
name_col != value_yg_dicari; //yg dikurung diprioritaskan
```

<h2>OPERATOR like</h2>

```sql
SELECT _ FROM name_tbl WHERE col LIKE 'a%'; //awalan a
SELECT _ FROM name*tbl WHERE col LIKE '%a'; //akhiran a
SELECT * FROM name*tbl WHERE col LIKE '%a%'; //terdapat a
SELECT * FROM name_tbl WHERE col NOT LIKE '%a%'; //! terdapat a
```

<h2>OPERATOR null</h2>

```sql
SELECT _ FROM name_tbl WHERE col IS NULL; //sdh jls
SELECT _ FROM name_tbl WHERE col IS NOT NULL; //sdh jls
```

<h2>OPERATOR between</h2>

```sql
SELECT _ FROM name_tbl WHERE price BETWEEN 10000 AND 20000; //mencari harga diantara 10000 dan 20000
SELECT _ FROM name_tbl WHERE price NOT BETWEEN 10000 AND 20000; //kebalikan
```

<h2>OPERATOR in</h2>

```sql
SELECT _ FROM name_tbl WHERE category IN ('opsi', 'opsi'); //mencari berdasarkan opsi
SELECT _ FROM name_tbl WHERE category NOT IN ('opsi', 'opsi'); //kebalikan
```

<h1>ORDER BY CLAUSE</h1>

//untuk mengurutkan ketika SELECT
//ASC / DESC

```sql
SELECT * FROM name_tbl ORDER BY price ASC, id DESC; //default ASC
```

<h1>LIMIT CLAUSE</h1>

//membatasi hasil query

```sql
SELECT *
FROM name_tbl
WHERE col > val
ORDER BY col
LIMIT 2; //max 2

SELECT *
FROM name_tbl
WHERE col > val
ORDER BY col
LIMIT 2, 3; //2 = skip, 3 = limit
```

<h1>SELECT DISTINCT DATA</h1>

//saat menggunakan SELECT kadang dapat data yg duplikat
//agar tidak duplikat pakai DISTINCT

```sql
SELECT DISTINCT category FROM name_tbl; //remove yg duplikat
```

<h1>NUMERIC FUNCTION</h1>

`SELECT 10 + 10 AS hasil;`

```sql
SELECT id, price DIV 1000 AS 'Price in K'
FROM name_tbl;
```

//DIV => for int, / => for float

<h1>MATH FUNCTION</h1>

```sql
SELECT PI();
SELECT POWER(10,2);
SELECT COS(10);
SELECT SIN(10);
SELECT TAN(10);
```

<h1>AUTO INCREMENT</h1>

//biasanya digunakan primarykey
//otomatis diinpukan increment oleh mysql

```sql
CREATE TABLE name_tbl
(
id INT NOT NULL AUTO_INCREMENT,
nama VARCHAR(10),
PRIMARY KEY(id) //menjadikan col id sebagai primarykey
)ENGINE = InnoDB;
//AUTO_INCREMENT cuma bisa di primarykey

SELECT LAST_INSERT_ID();//untuk melihat id terakhir mysql
```

<h1>STRING FUNCTION</h1>

```sql
SELECT id,
LOWER(name) AS 'Name Lower',
UPPER(name) AS 'Name Upper',
LENGTH(name) AS 'Name Length'
FROM name_tbl;
```

<h1>DATE AND TIME FUNCTION</h1>

```sql
SELECT id,
EXTRACT(YEAR FROM created_at) AS 'Year',
EXTRACT(MONTH FROM created_at) AS 'Month',
FROM name_tbl;

SELECT id,
YEAR(created_at), MONTH(created_at)
FROM name_tbl;
```

<h1>FLOW CONTROL FUNCTION</h1>

//fitur ini tidak sekomplek di bahasa pemrogaman

<h2>CASE:</h2>

```sql
SELECT id,
CASE category
WHEN 'Makanan' THEN 'Enak'
WHEN 'Minuman' THEN 'segar'
ELSE 'Apa itu?'
END AS 'Category'
FROM name_tbl;
```

<h2>iF:</h2>

```sql
SELECT id,
price,
IF(price <= 15000, 'Murah',
IF(price <= 20000, 'Mahal', 'Mahal banget')
) AS 'Mahal?'
FROM name_tbl;
```

<h2>IFNULL:</h2>

```sql
SELECT id, name
IFNULL(deskripsi, 'kosong')
FROM name_tbl;
```

<h1>AGREEGATE FUNCTION</h1>

```sql
SELECT COUNT(col) AS 'jumlah' FROM name_tbl;
SELECT AVG(col) AS 'rata 2' FROM name_tbl;
SELECT MAX(col) AS 'tertinggi' FROM name_tbl;
SELECT MIN(col) AS 'terendah' FROM name_tbl;
SELECT SUM(col) AS 'total' FROM name_tbl;
```

<h1>GROUP BY</h1>

```sql
SELECT COUNT(col) AS 'jumlah' FROM name_tbl
GROUP BY category; //jumlah per category
```

<h1>HAVING CLAUSE</h1>

```sql
SELECT SUM(col) AS 'total'
FROM name_tbl
GROUP BY category
HAVING total > 1; //seperti WHERE
```

<h1>CONSTRAINT</h1>

//menjaga validasi

<h2>Unique Constraint:</h2>
memastikan bahwa data tetap unik

```sql
CREATE TABLE customer(
id INT NOT NULL AUTO_INCREMENT,
email VARCHAR(255) NOT NULL,
PRIMARY KEY(id),
UNIQUE KEY email_unik(email) //menambahkan UNIQUE email_unik ke col email
) ENGINE = InnoDB; //membuat table


ALTER TABLE customer
ADD CONSTRAINT email_unik UNIQUE (email); //kalau mengedit table (menambah)

ALTER TABLE customer
DROP CONSTRAINT email_unik; //kalau mengedit table (menghapus)
```

<h2>Check Constraint:</h2>
mengecek data sebelum dimasukkan ke db

```sql
CREATE TABLE product(
id INT NOT NULL AUTO_INCREMENT,
harga VARCHAR(255) NOT NULL,
PRIMARY KEY(id),
UNIQUE cek_harga CHECK (harga >= 1000) //mengecek harga lebig besar atau sama dengan 1000
) ENGINE = InnoDB; //membuat table

ALTER TABLE product
ADD CONSTRAINT cek_harga CHECK (harga >= 1000); //kalau mengedit table (menambah)

ALTER TABLE product
DROP CONSTRAINT cek_harga; //kalau mengedit table (menghapus)
```

<h1>INDEX</h1>

//secara default, MYSQL menyimpan data dalam bentuk table biasa.
//hal ini menyebabkan saat melakukan pencarian data,
//maka mysql akan menscan dari baris pertama sampai akhir,
//dengan INDEX MYSQL akan menyimpan data dalam bentuk B-TREE

//kekurangan INDEX adalah setiap kali kita mengubah, menambah atau menghapus
//mysql akan mengupdate data di index (memperlambat proses manipulasi data)

//saat pakai primarykey dan UNIQUE kita tidak perlu pakai INDEX lagi
//sudah ditambahkan mysql

```sql
CREATE TABLE product(
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR(50) NOT NULL,
harga VARCHAR(255) NOT NULL,
PRIMARY KEY(id),
UNIQUE cek_harga CHECK (harga >= 1000), //mengecek harga lebig besar atau sama dengan 1000
INDEX name_index (name) //menambahkan index pada col name
) ENGINE = InnoDB; //membuat table

ALTER TABLE product
ADD INDEX name_index(name); //kalau mengedit table (menambah)

ALTER TABLE product
DROP INDEX name_index; //kalau mengedit table (menghapus)
```

<h1>FULL TEXT SEARCH</h1>

//mysql bukan db spesialis untuk search engine
//sperti: elastic search

```sql
CREATE TABLE user
(
id INT NOT NULL,
name VARCHAR(255) NOT NULL,
description TEXT,
PRIMARY KEY(id),
FULLTEXT user_search(name, description)
)ENGINE = InnoDB; //make table

ALTER TABLE user
ADD FULLTEXT user_search(name, description); //kalau mengedit table (menambah)

ALTER TABLE user
DROP INDEX user_search; //kalau mengedit table (menghapus)
//memang INDEX
```

<h2>NATURAL LANGUAGE MODE</h2>
//mencari berdasarkan per kata

```sql
SELECT* FROM user
WHERE MATCH(name, description)
AGAINST('arfian' IN NATURAL LANGUAGE MODE);
```

<h2>BOOLEAN MODE</h2>
// + => mengandung, - => !mengandung

```sql
SELECT* FROM user
WHERE MATCH(name, description)
AGAINST('+arfian -rafi' IN BOOLEAN MODE);
```

<h2>QUERY EXPANSION MODE</h2>
//dicari 2 kali
//pertama akan dicari seperti in natural lang mode
//kedua berdasarkan kemiripan kata yg ada dipencarian pertama

```sql
SELECT* FROM user
WHERE MATCH(name, description)
AGAINST('arfian' IN QUERY EXPANSION);
```

<h1>TABLE RELATIONSHIP</h1>

//foreign key
//keuntungan pakai foreign key adlh jika data yg diinputkan salah (id product) / tidak terdaftar maka ana ditolak

| BEHAVIOR  | ONDELETE    | ONUPDATE    |
| --------- | ----------- | ----------- |
| RESTRICT  | ditolak     | ditolak     |
| CASCADE   | dihapus     | diupdate    |
| NO ACTION | dibiarkan   | dibiarkan   |
| SET NULL  | diubah null | diubah null |

```sql
CREATE TABLE wishlist
(
id INT NOT NULL,
id_product VARCHAR(50) NOT NULL,
PRIMARY KEY(id),
CONSTRAINT fk_wishlist_product
FOREIGN KEY(id_product) REFERENCES product_tbl (col_id)
ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE = InnoDB; //create table

ALTER TABLE wishlist
ADD CONSTRAINT fk_wishlist_product
FOREIGN KEY(id_product) REFERENCES product_tbl (col_id) //kalau mengedit table (menambah)
ON DELETE CASCADE ON UPDATE CASCADE;

ALTER TABLE wishlist
DROP CONSTRAINT fk_wishlist_product; //kalau mengedit table (menghapus)
```

<h1>JOIN TABLE</h1>

```sql
SELECT * FROM wishlist
JOIN product ON (wishlist.id_product = product.id); //penghubung ada di 'ON()'

SELECT product.id, product.name, wishlist.description
FROM wishlist
JOIN product ON (wishlist.id_product = product.id);

SELECT p.id AS prod_id,
p.name AS prod_name,
w.description AS wishlist_desc
FROM wishlist AS w
JOIN product AS p ON (wishlist.id_product = product.id);
```
