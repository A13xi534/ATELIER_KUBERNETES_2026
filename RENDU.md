# Rendu — Atelier Kubernetes

> Complétez ce fichier au fil de l'atelier, puis faites un commit et un push (voir la section « Rendu » du README).

**Nom / Prénom :**
**Groupe :**

---

## Exercice 1 — Cluster

1. Combien de nœuds affiche `kubectl get nodes` ? Quel est le rôle de chacun ?
   >3 nœuds; 1 nœud control-plane, 2 nœuds workers
2. Que montre `docker ps` ? Qu'est-ce qu'un « nœud » dans k3d, concrètement ?
   > docker ps affiche les conteneurs Docker qui tournent dans le Codespace. C'est un conteneur Docker exécutant k3s.

## Exercice 2 — Premier déploiement

3. Quels objets Kubernetes ont été créés par `kubectl create deployment` ? (indice : `kubectl get all`)
   > un Deployment, qui a lui-même créé un ReplicaSet, qui a enfin créé un Pod
4. Vous avez supprimé le pod `web-...` : que s'est-il passé, et pourquoi ?
   > Le pod supprimé est passé en statut Terminating et un nouveau pod a été immédiatement créé et démarré.

## Exercice 3 — Modifier un conteneur en direct

5. Après suppression du pod, votre message « Bienvenue... » a-t-il survécu ? Pourquoi ?
   > Non, le message a disparu et la page par défaut Welcome to nginx! est revenue. Le système de fichiers d'un conteneur est éphémère.
6. Pourquoi le `port-forward` a-t-il cessé de fonctionner après la suppression du pod ?
   > Le tunnel réseau s'est rompu et le processus port-forward s'est arrêté.

## Exercice 4 — Déclaratif

7. Quelle différence entre `kubectl create` et `kubectl apply` ?
   > kubectl create est une commande impérative. kubectl apply est une commande déclarative
8. À quoi sert le `selector` d'un Service ? Que se passe-t-il s'il ne correspond à aucun pod ?
   > Le selector permet au Service de repérer dynamiquement les pods cibles vers lesquels il doit acheminer et répartir le trafic réseau

## Exercice 5 — Scaling & mises à jour

9. Sur quels nœuds se trouvent vos 3 réplicas ? Collez la sortie de `kubectl get pods -l app=site -o wide`.
   ```
NAME                    READY   STATUS    RESTARTS   AGE   IP          NODE              NOMINATED NODE   READINESS GATES
site-6b84bdbc98-zkbjw   1/1     Running   0          10m   10.42.1.8   k3d-lab-agent-0   <none>     <none>
   ```

10. Avec l'image `nginx:9.99`, quel statut avait le pod ? Quelle commande vous a donné la cause ?
    >ImagePullBackOff. kubectl describe pod -l app=site
11. Pendant la panne, le site restait-il accessible ? Pourquoi ?
    > Oui, Kubernetes ne supprime les anciens pods fonctionnels qu'après que les nouveaux pods sont opérationnels

## Exercice 6 — Portainer & Mario

12. URL publique de votre Mario :
    > https://super-space-tribble-77rvgrj4r9whx6jx-8585.app.github.dev/
13. Retrouvez le Deployment `mario` en ligne de commande. Portainer et `kubectl` parlent-ils au même composant ? Lequel ?
    >Oui, Portainer et kubectl parlent exactement au même composant : l'API Server Kubernetes

## Bonus (facultatif)

14. Bonus réalisés et remarques :
    >

---

**Score obtenu avec `./scripts/check.sh` :** ... / ...
