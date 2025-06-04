# Windows'ta Docker Desktop Kullanarak Kind ile 1 Master + 2 Worker Node'lu Kubernetes Cluster Kurulumu

## 1. Sistem Gereksinimleri
- **Windows 10/11 Pro, Enterprise veya Education** (Home sürümünde WSL2 gerekir).
- **Docker Desktop** kurulu ve **WSL2 backend** etkin olmalı.
- En az **8 GB RAM ve 4 çekirdek CPU** önerilir.

## 2. Docker Desktop Kurulumu ve Ayarları
- **Docker Desktop’ı indir ve yükle:**  
  [Docker Desktop İndir](https://www.docker.com/products/docker-desktop)
  
- **Docker Ayarlarını Yap:**
  - **Settings > General** sekmesinden **Use the WSL 2 based engine** seçeneğini etkinleştir.
  - **Settings > Resources** sekmesinden CPU ve RAM değerlerini **4 CPU, 8GB RAM** olarak artır.
  - **Settings > Kubernetes** sekmesinde **Enable Kubernetes** seçeneğini kapat (Kind kullanacağımız için gereksiz).
  
- **Docker Desktop’ı yeniden başlat.**

## 3. Kind Kurulumu
- **PowerShell’i Yönetici olarak aç** ve aşağıdaki komutları çalıştır:

  ```powershell
  Invoke-WebRequest -Uri https://kind.sigs.k8s.io/dl/latest/kind-windows-amd64 -OutFile kind.exe
  Move-Item kind.exe C:\Windows\System32\
  ```

- **Kurulumu doğrulamak için:**

  ```powershell
  kind version
  ```

## 4. Kubernetes Cluster Konfigürasyonu
1 Master + 2 Worker node’lu bir cluster oluşturmak için, aşağıdaki içeriğe sahip bir **kind-config.yaml** dosyası oluştur:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

- Ardından cluster’ı başlat:

  ```powershell
  kind create cluster --config kind-config.yaml
  ```

Bu işlem tamamlandığında cluster oluşturulmuş olacak.

## 5. Cluster’ı Kontrol Et
Aşağıdaki komutları çalıştırarak cluster'ın düzgün çalıştığını kontrol edebilirsin:

```powershell
kubectl get nodes
```

Çıktı şu şekilde olmalı:

```plaintext
NAME                 STATUS   ROLES           AGE   VERSION
kind-control-plane   Ready    control-plane   1m    v1.XX.X
kind-worker          Ready    <none>          1m    v1.XX.X
kind-worker2         Ready    <none>          1m    v1.XX.X
```

## 6. Test Deployment (Opsiyonel)
Cluster’ın çalıştığını test etmek için basit bir **Nginx Deployment** oluşturabilirsin:

```powershell
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --type=NodePort --port=80
```

Daha sonra servis bilgilerini kontrol etmek için:

```powershell
kubectl get svc
```

Eğer bir **NodePort** atanmışsa, aşağıdaki gibi bir çıktı alırsın:

```plaintext
NAME         TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP  10.96.0.1      <none>        443/TCP        10m
nginx        NodePort   10.96.0.2      <none>        80:30007/TCP   1m
```

Tarayıcıda **http://localhost:30007** adresine giderek çalıştığını doğrulayabilirsin.

## 7. Cluster’ı Silmek
Eğer cluster’ı kaldırmak istersen:

```powershell
kind delete cluster
```
```

Bu şekilde **Markdown** formatında istediğin gibi adımları oluşturmuş oldum. Yardımcı olabileceğim başka bir şey var mı?