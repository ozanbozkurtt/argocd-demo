# ArgoCD Applicationset Yönetimi

Uygulamaları otomatik olarak cluster'a dağıtmak (ApplicationSet kurulumları) için aşağıdaki komutu çalıştırın:

```shell
kubectl kustomize argocd-as-code/overlays/demo-cluster --enable-helm | kubectl apply -f -
```

## 🛠️ Yeni Uygulama Ekleneceği Zaman Dikkat Edilmesi Gerekenler

Set yapısında her uygulamanın unique resource'u olmak zorunda (shared resource hatası almamak için).
Chartın içerisindeki aşağıdaki kısımların değeri her uygulama için benzersiz (unique) olmalı:

```yaml
fullnameOverride
nameOverride
```

## 🧪 Test Yapılacağı Zaman

Spesifik bir uygulamayı setten çıkarmak için (ArgoCD bu pathi görmezden gelir):

```yaml
spec:
  generators:
  - git:
      directories:
      - path: <path_of_app>/overlays/demo-cluster
        exclude: true
```

Autosync devre dışı bırakmak için (Yeni commit atıldığında ArgoCD otomatik senkronize etmez):

```yaml
spec:
  syncPolicy:
    automated:
      enabled: false
```
