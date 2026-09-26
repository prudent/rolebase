# Agileside — consignes pour l'IA

Fork de Rolebase pour Agileside (Pascal Prudent).

- Repo : https://github.com/prudent/rolebase
- Upstream : https://github.com/Godefroy/rolebase
- Prod : https://rolebase.agileinside.cloud
- Branche de travail : `agileside`
- `main` reste alignée sur l'upstream

## Où coder

| Besoin | Dossier |
|---|---|
| Écrans, marque, parcours | `packages/webapp` |
| Organigramme | `packages/graph` |
| Éditeur | `packages/editor` |
| Collab temps réel | `packages/collab` |
| Schéma / droits | `nhost/migrations`, `nhost/metadata` |
| Fonctions serveur | `functions`, `packages/backend` |

Ne pas modifier `website/` (licence propriétaire Rolebase).
Ne pas committer `.secrets` ni clés API.

## Config self-host

Les URLs Agileside sont dans `packages/webapp/src/settings.ts` (`isSelfHost`).
En local sur le Mac : `npm i` puis `npm run dev` dans le monorepo ; le frontend Vite peut pointer vers le Nhost du VPS.

## Déploiement VPS

```bash
cd /opt/rolebase
git fetch origin && git checkout agileside && git pull
npm run build --workspace=@rolebase/webapp
rsync -a packages/webapp/dist/ /opt/rolebase-edge/web/
```

## Workflow

1. Une tâche = une branche depuis `agileside`.
2. Lire le dossier feature concerné avant d'écrire.
3. Changement de données = migration Nhost, pas de SQL ad hoc en prod.
4. Ne pas lancer Nhost + Hasura sur le Mac M3 sauf besoin de schéma.
