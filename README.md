# Docker Examples

Bu repo, farklı servislerin Docker ve Kubernetes üzerinde hızlıca ayağa kaldırılabilmesi için hazırlanmış örnek dosyaları içerir.  

## 📂 Klasör Yapısı

- **Elastic/**  
  Elasticsearch ve Kibana için Docker Compose dosyaları içerir.  

- **Portainer/**  
  Docker ortamlarını görsel arayüz ile yönetmek için Portainer kurulumu içerir.  

- **PostgreSql/**  
  PostgreSQL veritabanını ayağa kaldırmak için `docker-compose.yml` ve ayar dosyaları içerir.  

- **Redis+RedisCommander/**  
  Redis veritabanı ve Redis Commander arayüzünü içeren `docker-compose.yml` bulunur.  

- **Redis-Sentinel-Helm/**  
  Kubernetes üzerinde Redis + Sentinel kurulumu için hazırlanmış **Helm chart** içerir.  
  - `Chart.yaml` → Chart bilgileri  
  - `values.yaml` → Versiyon, image, kaynak limitleri, storage tanımları  
  - `templates/` → Namespace, Secret, ConfigMap, StatefulSet, Service, PodDisruptionBudget tanımları  

- **Wordpress/**  
  Wordpress ve bağlı servislere ait docker-compose örnekleri içerir.  

---

## 🚀 Kullanım

### Docker Compose ile Servis Çalıştırma

Örnek olarak **Redis + Redis Commander** için:

```bash
cd Redis+RedisCommander
docker-compose up -d
```
Benzer şekilde diğer klasörlerdeki docker-compose.yml dosyaları da kullanılabilir.

Helm ile Redis Sentinel Kurulumu

Namespace oluşturma ve chart yükleme:
```bash
cd Redis-Sentinel-Helm
helm install redis-cluster . -n redis-cluster --create-namespace
```

Pod durumunu kontrol etme:
```bash
kubectl get pods -n redis-cluster
```

Sentinel servisine bağlanma:
```bash
kubectl exec -it <sentinel-pod-name> -n redis-cluster -- redis-cli -p 26379
```

🔑 Önemli Notlar

Parola Yönetimi:
Redis Sentinel Helm chart içinde parola values.yaml altında tanımlıdır. Secret üzerinden podlara aktarılır.

Persistence:
values.yaml içinde Redis için PVC boyutu ve storageClass ayarlanabilir.

Kaynak Limitleri:
Her servis için CPU/Memory request & limit değerleri tanımlanmıştır. Gerektiğinde values.yaml güncellenmelidir.

Geliştirme / Test Amaçlıdır:
Buradaki örnekler geliştirme ve test ortamı için uygundur. Prod ortamda ek güvenlik ve izleme ayarları yapılmalıdır.

Lisans

Bu proje MIT lisansı ile sunulmaktadır.