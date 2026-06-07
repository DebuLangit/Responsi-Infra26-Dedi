# Analisis Perbaikan

## Permasalahan 1

### Gejala
- yaml: line 5, column 8: mapping values are not allowed in this context


### Penyebab
- Text "services" belum ada tanda ":", ini menyebabkan text di bawah "services" tidak
dikenali

### Solusi
- Menambah tanda ":" di sebelah text "services"

---

## Permasalahan 2

### Gejala
- time="2026-06-07T23:39:32+07:00" level=warning msg="D:\\HDD\\docker_build\\Responsi-Infra26-De
di\\docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove
 it to avoid potential confusion"
service "db" refers to undefined volume db-data: invalid compose project


### Penyebab
- "the attribute version is obsolete..." artinya: penulisan versi di awal file sudah 
tidak diperlukan lagi dan akan diabaikan.
- "service "db" refers to undefined volume db-data" 
Docker tidak bisa menemukan "wadah" bernama db-data tersebut karena kamu belum
mendeklarasikannya di tingkat paling atas (root) file YAML.

### Solusi
- hapus text "version: "3.9"" 
- edit file docker-compose.yml di blok db tambahkan:
```
volumes:
  db-data:
```

---

## Permasalahan 3

### Gejala
- unable to prepare context: path "D:\\HDD\\docker_build\\Responsi-Infra26-Dedi\\web33" not foun
d


### Penyebab
- dalam file yml tepatnya di blok web3 `context: ./web33`

### Solusi
- edit menjadi `context: ./web3`

---

## Permasalahan 4

### Gejala
- Docker gagal mem-build container untuk web1 dan web3 dengan peringatan bahwa sistem
tidak dapat menemukan base image yang diminta di dalam registry.


### Penyebab
- Terdapat kesalahan pengetikan (typo) yang disengaja pada penamaan base image PHP di dalam file Dockerfile. Pada web1/Dockerfile tertulis FROM php:8.2-apach, dan pada
web3/Dockerfile tertulis FROM php:8.2-apche.

### Solusi
- Mengubah dan memperbaiki penulisan nama image di kedua file Dockerfile tersebut menjadi
ejaan yang benar, yaitu FROM php:8.2-apache.

---

## Permasalahan 5

### Gejala
- database belum bisa jalan

### Penyebab
- ada tanda : 
```sql

```


### Solusi
- hapus tanda di penyebab tersebut

---

## Permasalahan 6

### Gejala
- placeholder belum diganti ke nama mahasiswa

### Penyebab
- placeholder masih default

### Solusi
- edit nama mahasiswa di init.sql, dan index.php setiap web

---

## Permasalahan 7

### Gejala
- NGINX tidak berjalan

### Penyebab
- masalah yang sama sebelumnya tanda :
```nginx

```
- nama web dan nomor port salah
```
    upstream backend {

        server web11:80;
        server web2:80;
        server web3:8080;

    }
```

### Solusi
- hapus tanda tersebut
- seharusnya:
```
    upstream backend {

        server web1:80;
        server web2:80;
        server web3:80;

    }

```

---

## Permasalahan 8

### Gejala
- web 2 gagal diakses
- kesalahan text di docker-compose.yml

### Penyebab
- web2 `DB_PASS: wrongpassword`
- network di blok web3 tidak ada `frontend`
 
### Solusi
- ubah menjadi `DB_PASS: student123`
- seharusnya:
```
networks:
  - frontend
  - backend
```

---
