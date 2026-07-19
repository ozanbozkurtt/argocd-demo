# K3s + ArgoCD + Kustomize GitOps Altyapı Demosu

K3s üzerinde ArgoCD ve Kustomize kullanarak inşa ettiğimiz bildirimsel (declarative) GitOps altyapı projesidir.

## 📝 Makale ve Detaylar

Bu projenin detaylı kurulum adımlarını, mimari kararlarını ve "Prometheus Agent + Remote Write" izleme kurgusunu anlattığımız Medium makalesine aşağıdaki bağlantıdan ulaşabilirsiniz:

👉 **[Medium Makalesi](https://medium.com/@ozanbozkurtt)**

---

### 📂 Proje Yapısı
* **`apps/`**: Kubernetes üzerinde koşan uygulamalar (nginx, test-crash-app, test-probe-app).
* **`infra/`**: Altyapı bileşenleri (argocd, kube-state-metrics, prometheus-agent).
* **`argocd-as-code/`**: GitOps çarkını döndüren dinamik ApplicationSet tetikleyicileri.
