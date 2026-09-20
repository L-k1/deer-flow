# DeerFlow 2.0 — Notes d'installation (Lüdi)

Fork personnel de [bytedance/deer-flow](https://github.com/bytedance/deer-flow) — licence **MIT** (gratuit, usage commercial autorisé).

- Cloné le 20/09/2026 sur `C:\Projets\deer-flow` (commit upstream `e545c28a`)
- Remotes git : `origin` = `L-k1/deer-flow` (ton fork), `upstream` = `bytedance/deer-flow`

## Ce qui a été fait

1. `make config` → génère `config.yaml` + `.env` (tous deux **ignorés par git**, jamais poussés)
2. Dans `config.yaml`, section `models:` → modèle **Claude Sonnet 5** activé (`langchain_anthropic:ChatAnthropic`), clé lue via `$ANTHROPIC_API_KEY`
3. Dans `.env` → ligne `ANTHROPIC_API_KEY=` ajoutée (vide, à remplir)

## Ce qu'il reste à faire (à la main)

1. Ouvrir `.env` et renseigner `ANTHROPIC_API_KEY=sk-ant-...`
   (optionnel : `TAVILY_API_KEY` ou `JINA_API_KEY` pour la recherche web)
2. Lancer **Docker Desktop** et attendre qu'il soit vert ("Engine running")
3. Dans WSL (terminal `…$`) :

```bash
cd /mnt/c/Projets/deer-flow
make docker-init     # télécharge l'image sandbox (une seule fois)
make docker-start    # démarre les services (mode dev, hot-reload)
make docker-logs     # voir les logs
```

4. Ouvrir http://localhost:2026 → créer le compte admin via `/setup`

## Commandes utiles

```bash
make doctor          # diagnostic de la config
make docker-stop     # arrêter les services
git fetch upstream && git merge upstream/main   # récupérer les mises à jour officielles
```

## Sécurité

- DeerFlow écoute sur `127.0.0.1` uniquement (ne pas mettre `BIND_HOST=0.0.0.0` sans pare-feu)
- Les clés restent dans `.env` local — ne jamais les committer
