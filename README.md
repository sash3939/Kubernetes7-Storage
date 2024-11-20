# Домашнее задание к занятию «Хранение в K8s. Часть 2»

### Цель задания

В тестовой среде Kubernetes нужно создать PV и продемострировать запись и хранение файлов.

------

### Чеклист готовности к домашнему заданию

1. Установленное K8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключенным GitHub-репозиторием.

------

### Дополнительные материалы для выполнения задания

1. [Инструкция по установке NFS в MicroK8S](https://microk8s.io/docs/nfs). 
2. [Описание Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/). 
3. [Описание динамического провижининга](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/). 
4. [Описание Multitool](https://github.com/wbitt/Network-MultiTool).

------

### Задание 1

**Что нужно сделать**

Создать Deployment приложения, использующего локальный PV, созданный вручную.

1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.

<img width="390" alt="deployment-test" src="https://github.com/user-attachments/assets/2d9ddb8a-1edb-4eef-aae3-a8b06c66b9a4">

Deployment 0/1 not ready потому что не созданы pv и pvc

2. Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.

<img width="652" alt="pv-test" src="https://github.com/user-attachments/assets/6d91f35f-51ad-4110-b9f2-5a0ff5f56bfa">

<img width="515" alt="pvc-test" src="https://github.com/user-attachments/assets/1999ba3f-3abd-4e70-bae8-7f9f0fb0be47">

<img width="334" alt="deployment-test after create pvc" src="https://github.com/user-attachments/assets/e10d90b0-73a7-4afd-9a14-53e707fa973b">

3. Продемонстрировать, что multitool может читать файл, в который busybox пишет каждые пять секунд в общей директории. 

<img width="663" alt="multitool read" src="https://github.com/user-attachments/assets/63b19cec-bd80-48d8-9d33-2579a12d4467">

4. Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему.

<img width="566" alt="delete deployment and pvc" src="https://github.com/user-attachments/assets/af450efb-5ded-4e33-b764-815074994e3a">

<img width="677" alt="status pv after delete pvc, deployment" src="https://github.com/user-attachments/assets/f5e25846-3329-425f-9cb9-4eb5cb4dd609">

После удаления PVC, PV сменил статус с Bound на Released, так как больше не свзан с PVC

5. Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV.  Продемонстрировать что произошло с файлом после удаления PV. Пояснить, почему.

<img width="371" alt="output data" src="https://github.com/user-attachments/assets/61e8a10a-078c-4767-9ac8-b9aa18e4642d">

Так как Reclaim Policy было установлено Retain, соответственно данные сохранились

<img width="686" alt="delete pv" src="https://github.com/user-attachments/assets/894e9838-a801-4f2b-b733-d5945a2a6d74">

6. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

[deployment-test.yaml](https://github.com/sash3939/Kubernetes7-Storage/blob/main/deployment-test.yaml)
[pv-test.yaml](https://github.com/sash3939/Kubernetes7-Storage/blob/main/pv-test.yaml)
[pvc-test.yaml](https://github.com/sash3939/Kubernetes7-Storage/blob/main/pvc-test.yaml)

------

### Задание 2

**Что нужно сделать**

Создать Deployment приложения, которое может хранить файлы на NFS с динамическим созданием PV.

1. Включить и настроить NFS-сервер на MicroK8S.
2. Создать Deployment приложения состоящего из multitool, и подключить к нему PV, созданный автоматически на сервере NFS.
3. Продемонстрировать возможность чтения и записи файла изнутри пода. 
4. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

------

### Правила приёма работы

1. Домашняя работа оформляется в своём Git-репозитории в файле README.md. Выполненное задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl`, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.
