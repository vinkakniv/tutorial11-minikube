# Advanced Programming - Tutorial


------------
## Overview

This repository contains the code and reflections for Tutorial 11 in Advanced Programming course by Vinka Alrezky As (NPM: 2206820200)❄️

------------
# Tutorial 11 - Deployment on Kubernetes

### _Reflection_

- [Reflection 1 - Hello Minikube](#reflection-1)

### Reflection 1


> 1. Compare the application logs before and after you exposed it as a Service.
Try to open the app several times while the proxy into the Service is running.
What do you see in the logs? Does the number of logs increase each time you open the app?

![](https://i.imgur.com/krnckbz.jpeg)

Perubahan dalam jumlah catatan log terlihat ketika aplikasi di-_expose_ sebagai Service. Pada awalnya, ketika aplikasi belum di-_expose_, akses terjadi langsung di dalam pod dan catatan log hanya menunjukkan pesan-pesan awal seperti `Started HTTP server on port 8080` dan `Started UDP server on port 8081`.

![](https://i.imgur.com/bCyILia.jpeg)

Namun, setelah aplikasi di-_expose_ sebagai layanan dengan perintah `minikube service hello-node`, catatan log tidak hanya menampilkan pesan-pesan awal tersebut, tetapi juga mencatat permintaan yang masuk. Kini, permintaan ini dialihkan melalui Service yang menyediakan akses eksternal ke aplikasi. Misalnya, saat saya mencoba mengirim permintaan GET menggunakan Postman ke aplikasi yang telah di-_expose_ sebagai Service, perubahan dalam catatan log akan terlihat. Setiap permintaan GET yang dikirim melalui Postman akan tercatat sebagai aktivitas baru dalam log aplikasi. Dengan demikian, setiap akses atau pembaruan halaman aplikasi melalui browser, jumlah entri log akan bertambah, yang ditandai dengan pengiriman permintaan GET oleh browser ke Service.

> 2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created? 

Dalam Kubernetes, opsi `-n` digunakan untuk menentukan _namespace_ pada operasi tertentu. Ketika kita menjalankan perintah dengan opsi `-n` yang diatur ke `kube-system`, perintah tersebut akan menampilkan _resource_ dari _namespace_ `kube-system` yang berisi komponen inti dari sistem Kubernetes, seperti DNS dan server API. Namun, perintah ini tidak akan menampilkan daftar pod atau layanan yang telah dibuat oleh pengguna secara eksplisit. Jadi, dengan menggunakan opsi -n, kita dapat fokus pada _namespace_ tertentu saat berinteraksi dengan _resource_ Kubernetes atau menjalankan perintah, sementara tanpa opsi `-n`, _resource_ yang dibuat oleh pengguna akan ditampilkan sebagai gantinya. 
