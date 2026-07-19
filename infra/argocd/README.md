# ArgoCD Kurulum ve Çalıştırma Kılavuzu

ArgoCD'yi Kustomize ve Helm entegrasyonuyla beraber cluster üzerine kurmak ve çalıştırmak için aşağıdaki adımları takip edin.

## 🚀 ArgoCD Kurulumu (Bootstrap)

Aşağıdaki komutu çalıştırarak kurulumu başlatabilirsiniz:

```shell
kubectl kustomize infra/argocd/overlays/demo-cluster --enable-helm | kubectl apply --server-side --force-conflicts -f -
```

## 🔑 Port-Forward ile Web Arayüzüne Erişim

ArgoCD sunucusuna yerel makinenizden erişmek için port-forward işlemini başlatın:

```shell
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Ardından tarayıcınızdan `https://localhost:8080` adresine gidebilirsiniz.

## 🔐 İlk Admin Şifresini Almak

Giriş yapmak için gereken varsayılan admin şifresini çözmek için aşağıdaki komutu çalıştırın:

```shell
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

---

## 📈 GitOps Altyapısı (kube-state-metrics & prometheus-agent)

Kurulan ArgoCD üzerinde `kube-state-metrics` ve `prometheus-agent` (Remote Write) altyapı araçlarını otomatik olarak dağıtmak (deploy) için aşağıdaki komutu koşturun:

```shell
kubectl kustomize argocd-as-code/overlays/demo-cluster --enable-helm | kubectl apply -f -
```
Bu işlem sonrasında Prometheus Agent, Kubernetes içindeki metrikleri toplayıp host üzerinde çalışan merkezi Prometheus'a (`http://192.168.1.99:9090`) anlık push etmeye başlayacaktır.
