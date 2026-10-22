# Comparatif des approches - projet fraude (TP04)

Documentation consultee le 22/10/2026.

| Approche | F1 test | Temps humain | Temps machine | Cout estime (source, date) | Explicabilite | Export / reversibilite |
|---|---|---|---|---|---|---|
| Logistique (ref.) | 0.7407 | ~5 min | 0.13 s | 0 (poste local) | Maximale (coefficients) | Total |
| Manuel (TP2) | 0.8669 | ~1 a 2 h (seance TP2) | 2.03 s (modele final) | 0 (poste local) | Moyenne (importances RF) | Total |
| FLAML 60 s | 0.8582 | ~10 min | 60.5 s | 0 (poste local) | Moyenne/Basse (importances + journal des essais) | Total (objet Python local) |
| Vertex AI AutoML | non mesure | ~30 min (config.) | budget en heures-noeud | 21.252 $/heure-noeud + pipeline (Vertex AI pricing, 22/10/2026) | Bonne (Shapley echantillonne, global + local) | Partielle : export conteneur Docker (classif./regression), sans explicabilite |
| SageMaker Autopilot | non mesure | ~30 min (config.) | non mesure | 1.90 $/h session + 2.03 a 4.89 $/h entrainement (SageMaker Canvas pricing, 22/10/2026) | Bonne (SHAP, rapports, notebooks) | Partielle : artefacts dans S3, ecosysteme AWS |
| Azure Automated ML | non mesure | ~30 min (config.) | non mesure | service gratuit, calcul + stockage factures (Azure ML pricing, 22/10/2026) | Bonne mais en preversion (importances, tableau de bord) | Partielle : ONNX pour certains algorithmes seulement |

## Commentaire (5 lignes)

1. La regression logistique reste la reference a battre et le meilleur choix quand l'explicabilite prime (secteur regule, decision a justifier).
2. Le reglage manuel donne le meilleur F1 (0.8669) mais coute du temps humain : il se justifie quand quelques points de F1 ont une forte valeur metier.
3. FLAML atteint 0.858 en 60 s sans intervention : ideal pour obtenir vite une base solide ou explorer un nouveau probleme, sur petites donnees et a cout nul.
4. Les plateformes managees se justifient pour de gros volumes, une equipe sans infrastructure ML ou un besoin de deploiement et de monitoring integres, au prix d'un cout horaire et d'une dependance a l'ecosysteme.
5. Aucune approche ne remplace le controle humain : la fuite du bloc D a ete validee avec un F1 de 1.0 par l'AutoML.