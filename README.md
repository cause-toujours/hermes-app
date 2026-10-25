# hermes-app — pages publiques de l'app OAuth « Hermès »

Les deux pages statiques exigées par Google Auth Platform → Branding pour
pouvoir publier l'application (passer du statut « Testing » — tokens révoqués
tous les 7 jours — à « En production »). Recette gclientid : pas de vérification
Google, pas de Search Console — deux liens + un domaine autorisé suffisent.

- Accueil : https://cause-toujours.github.io/hermes-app/
- Confidentialité : https://cause-toujours.github.io/hermes-app/privacy/

## Publier (déjà fait si ce fichier dit « PUBLIÉ » plus bas)

```bash
gh repo create cause-toujours/hermes-app --public --source=. --push
gh api -X POST repos/cause-toujours/hermes-app/pages \
  -f "source[branch]=main" -f "source[path]=/"
# le déploiement prend ~1 min ; vérifier :
curl -sI https://cause-toujours.github.io/hermes-app/ | head -1
curl -sI https://cause-toujours.github.io/hermes-app/privacy/ | head -1
```

## Ensuite, dans la console Google (le pas-à-pas du guide § 7)

1. https://console.cloud.google.com/auth/branding?project=hermes-gmail-mcp-501517
   - « + Ajouter un domaine » : `cause-toujours.github.io` (AVANT les URLs)
   - Page d'accueil : `https://cause-toujours.github.io/hermes-app/`
   - Confidentialité : `https://cause-toujours.github.io/hermes-app/privacy/`
   - Logo : sauter (facultatif) · Save
2. Google Auth Platform → Audience → « Publier l'application » → confirmer.
3. Une fois : `~/miniforge3/bin/python3 _SYSTEME/scripts/sync_taches.py --reauth`
4. Vérification le 31/10 : la sync tourne sans `--reauth`.
5. (Avant le 11/11) Clients → client Desktop → cocher « Use this client
   for an AI-powered agent » → Enregistrer.

## Détruire (réversible en 1 minute)

`gh repo delete cause-toujours/hermes-app --yes` puis retirer les liens dans
Branding. Aucune autre trace.
