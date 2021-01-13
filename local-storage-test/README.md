# Introduction
Folder ini berisi contoh penggunaan [Persistent Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)(pv) dengan type [local](https://kubernetes.io/docs/concepts/storage/volumes/#local). 

Pada type ini, provisioning dilakukan secara manual ([Static Provisioning](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#static)), yaitu dengan cara: 
1. Membuat sendiri folder di node-node yg akan dibuat pv nya
2. Lalu membuat pv untuk masing-masing folder pada tiap-tiap node. 
   - Saat membuat pv kita menentukan sendiri **storageClassName** nya. 
   - **storageClassName** nantinya akan digunakan di **volumeClaimTemplates** di *StatefulSet*.

# Getting Started
## Menyiapkan folder-folder untuk pv
Siapkan folder-folder di tiap-tiap node. Berikut ini contoh cara membuat foldernya
````
sudo mkdir /mnt/local-test-pv-01/
sudo mkdir /mnt/local-test-pv-02/
````
## Membuat Persistent Volume
Untuk membuat pv, sesuaikan file [local-test-pv.yaml](local-test-pv.yaml).
Pada file [local-test-pv.yaml](local-test-pv.yaml) kita membuat 4 PersistentVolume, yaitu
| name | hostname | path | storageClassName |
| --- | --- | --- | --- |
| `local-test-pv-0201` | `ren-kube-n0002` | `/mnt/local-test-pv-01/` | `local-test-storage` |
| `local-test-pv-0202` | `ren-kube-n0002` | `/mnt/local-test-pv-02/` | `local-test-storage` |
| `local-test-pv-0301` | `ren-kube-n0003` | `/mnt/local-test-pv-01/` | `local-test-storage` |
| `local-test-pv-0302` | `ren-kube-n0003` | `/mnt/local-test-pv-02/` | `local-test-storage` |

Sesuaikan di bagian **local path** serta tentukan hostname di bagian **nodeAffinity** untuk tiap-tiap PersistentVolume yang akan kita buat. Sesuaikan jumlah PersistentVolume sesuai kebutuhan.

Perhatikan bahwa semua pv diatas menggunakan **storageClassName** yang sama, yaitu `local-test-storage`. **storageClassName** ini yang nantinya akan digunakan saat *StatefulSet* membuat *PersistentVolumeClaim*(pvc)

Setelah disesuaikan, silakan apply ke kubernetes dengan perintah
````
kubectl apply -f local-test-pv.yaml
````
## Membuat StatefulSet
Untuk membuat StatefulSet dapat langsung menggunakan file [local-test.yaml](local-test.yaml). Berikut ini perintah yang dapat digunakan.
````
kubectl apply -f local-test.yaml
````
## Melihat file yang dihasilkan 
Jika semua berjalan lancara, maka di tiap-tiap folder pada node yang telah terbentuk pvc nya akan ada file *test_file* dan *count*.
Berikut ini cara melihat file tersebut.
````
cd /mnt/local-test-pv-01/
tail -f test_file
````
