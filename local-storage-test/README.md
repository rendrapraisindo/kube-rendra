# Introduction
Folder ini berisi contoh penggunaan [Persistent Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) dengan type [local](https://kubernetes.io/docs/concepts/storage/volumes/#local). 

Pada type ini, provisioning dilakukan secara manual (Static Provisioning), yaitu dengan membuat sendiri folder di node-node yg akan dibuat pv nya, lalu membuat pv untuk masing-masing folder pada tiap-tiap node. Saat membuat pv kita menentukan sendiri storageClassName nya. storageClassName nantinya akan digunakan di volumeClaimTemplates di StatefulSet.
