# 🚀 Docker & Kubernetes Examples

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
![Docker](https://img.shields.io/badge/Docker-Examples-blue?logo=docker)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Helm-orange?logo=kubernetes)

Bu repo, farklı servislerin **Docker** ve **Kubernetes (Helm)** üzerinde hızlıca ayağa kaldırılabilmesi için hazırlanmış örnek dosyaları içerir.  

---

## 📂 Klasör Yapısı

| Klasör | Açıklama |
|--------|----------|
| **Elastic/** | Elasticsearch + Kibana için `docker-compose.yml` |
| **Portainer/** | Docker ortamlarını görsel arayüz ile yönetmek için Portainer kurulumu |
| **PostgreSql/** | PostgreSQL için `docker-compose.yml` ve ayar dosyaları |
| **Redis+RedisCommander/** | Redis veritabanı + Redis Commander arayüzü (`docker-compose.yml`) |
| **Redis-Sentinel-Helm/** | Kubernetes üzerinde Redis + Sentinel için **Helm chart** |
| **Wordpress/** | Wordpress ve bağlı servislerin `docker-compose.yml` dosyaları |

---

## ⚡ Kullanım

### 🔹 Docker Compose ile Servis Çalıştırma

Örnek: **Redis + Redis Commander**

```bash
cd Redis+RedisCommander
docker-compose up -d
```

Benzer şekilde diğer klasörlerdeki `docker-compose.yml` dosyaları da kullanılabilir.

---

### 🔹 Helm ile Redis Sentinel Kurulumu

1. Namespace oluşturma ve chart yükleme:
   ```bash
   cd Redis-Sentinel-Helm
   helm install redis-cluster . -n redis-cluster --create-namespace
   ```

2. Pod durumunu kontrol etme:
   ```bash
   kubectl get pods -n redis-cluster
   ```

3. Sentinel servisine bağlanma:
   ```bash
   kubectl exec -it <sentinel-pod-name> -n redis-cluster -- redis-cli -p 26379
   ```

---

## 🔑 Önemli Notlar

- 🔒 **Parola Yönetimi** → `values.yaml` içinde tanımlı, Secret üzerinden podlara aktarılır.  
- 💾 **Persistence** → Redis PVC boyutu ve `storageClass` ayarlanabilir.  
- 📊 **Kaynak Limitleri** → CPU/Memory request & limit değerleri `values.yaml` üzerinden değiştirilebilir.  
- 🧪 **Geliştirme / Test Amaçlıdır** → Prod ortamda **güvenlik, izleme ve yedekleme** eklenmelidir.  

---

## 📌 Yol Haritası

- [ ] CI/CD pipeline entegrasyonu (GitHub Actions / GitLab CI)  
- [ ] Monitoring (Prometheus + Grafana)  
- [ ] Redis otomatik failover testleri  

---

## 📜 Lisans

Bu proje **MIT Lisansı** ile sunulmaktadır.  

---
✨ Keyifli Deploylar! ✨
