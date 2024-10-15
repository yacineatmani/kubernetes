Voici un drill basé sur des questions difficiles que vous pourriez rencontrer lors de la certification CKA (Certified Kubernetes Administrator). Ce drill inclut des questions d’examen, ainsi que des explications et des concepts associés pour vous aider à mieux les comprendre.

### Drill d'Examen CKA

---

**Question 1: Configurer un Namespace**
- **Exercice :** Créez un Namespace nommé `dev` et vérifiez qu'il a été créé correctement.

```bash
kubectl create namespace dev
kubectl get namespaces
```

*Concept à retenir :*
- Les **Namespaces** permettent de segmenter les ressources Kubernetes pour différents environnements ou équipes.

---

**Question 2: Créer un Pod avec des Labels et Annotations**
- **Exercice :** Créez un Pod nommé `my-pod` avec le label `app: myapp` et une annotation `version: v1`.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: myapp
  annotations:
    version: v1
spec:
  containers:
  - name: my-container
    image: nginx
```

*Concept à retenir :*
- Les **labels** sont utilisés pour organiser et sélectionner des objets, tandis que les **annotations** stockent des métadonnées.

---

**Question 3: Déploiement et Mise à l’Échelle**
- **Exercice :** Créez un déploiement nommé `my-deployment` avec 3 réplicas de l’image `nginx` et mettez-le à jour pour utiliser une nouvelle image.

```bash
kubectl create deployment my-deployment --image=nginx --replicas=3
kubectl scale deployment my-deployment --replicas=5
```

*Concept à retenir :*
- Les **Déploiements** gèrent la mise à l'échelle et les mises à jour des Pods.

---

**Question 4: Configurer un Service**
- **Exercice :** Créez un Service de type `ClusterIP` pour le Pod `my-pod`.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

*Concept à retenir :*
- Les **Services** permettent l'accès aux Pods à travers un point d'entrée stable.

---

**Question 5: Persistent Volumes (PV) et Persistent Volume Claims (PVC)**
- **Exercice :** Créez un Persistent Volume et un Persistent Volume Claim pour stocker des données.

```yaml
# Persistent Volume
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /data

# Persistent Volume Claim
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

*Concept à retenir :*
- Les **PV** sont des ressources de stockage dans le cluster, et les **PVC** sont des demandes de stockage par les Pods.

---

**Question 6: Configurer des Secrets et ConfigMaps**
- **Exercice :** Créez un Secret et un ConfigMap pour stocker des données de configuration.

```bash
kubectl create secret generic my-secret --from-literal=password=mysecretpassword
kubectl create configmap my-config --from-literal=key1=value1
```

*Concept à retenir :*
- Les **Secrets** et **ConfigMaps** stockent des données sensibles et des configurations respectivement.

---

**Question 7: Diagnostiquer un Pod**
- **Exercice :** Un de vos Pods ne fonctionne pas. Comment diagnostiquer le problème ?

```bash
kubectl get pods
kubectl describe pod my-pod
kubectl logs my-pod
```

*Concept à retenir :*
- Utiliser `kubectl describe` et `kubectl logs` pour diagnostiquer les problèmes des Pods.

---

**Question 8: RBAC (Role-Based Access Control)**
- **Exercice :** Créez un Role et un RoleBinding pour permettre à un utilisateur d’accéder à un Namespace spécifique.

```yaml
# Role
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: dev
  name: dev-role
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]

# RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: dev-role-binding
  namespace: dev
subjects:
- kind: User
  name: my-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: dev-role
  apiGroup: rbac.authorization.k8s.io
```

*Concept à retenir :*
- **RBAC** permet de gérer les permissions des utilisateurs et des services dans Kubernetes.

---

**Question 9: Utilisation de Helm**
- **Exercice :** Installez une application avec Helm en utilisant un chart.

```bash
helm install my-release stable/nginx
```

*Concept à retenir :*
- **Helm** est un gestionnaire de paquets pour Kubernetes, facilitant le déploiement d’applications complexes.

---

**Question 10: Monitoring et Logging**
- **Exercice :** Comment configurer le logging pour un cluster Kubernetes ?

```yaml
# Exemple de configuration de Fluentd
apiVersion: v1
kind: ConfigMap
metadata:
  name: fluentd-config
data:
  fluent.conf: |
    <source>
      @type forward
      port 24224
    </source>
```

*Concept à retenir :*
- Le **monitoring** et le **logging** sont cruciaux pour maintenir la santé et la performance des clusters.

---

### Conclusion
Ces questions d'examen visent à couvrir les domaines essentiels et souvent complexes que vous rencontrerez dans le cadre de la certification CKA. Révisez ces concepts en profondeur, pratiquez sur votre cluster Kubernetes, et essayez de résoudre des problèmes réels pour vous familiariser davantage avec l'environnement. Si vous avez des questions supplémentaires ou si vous souhaitez approfondir un sujet particulier, n'hésitez pas à demander !