# SUIVI – Somlit_rbr_toolbox

## Dépôt de travail
- Référence : github.com/adomeau/Somlit_rbr_toolbox (décision du 2026-11-03).
- Branche `fix/binaverage-extremes` créée depuis adomeau/main fe6b44c. Elle compte 6 commits et n'est pas encore poussée.
  Le push depuis Claude est refusé tant que l'app GitHub Claude n'est pas installée sur le dépôt.
- La copie locale de ce PC pointe encore vers epoirierIRD (clone de janvier 2026). Son code est identique à adomeau/main,
  à une ligne près (FLUORESCENCE round(3)), reprise dans la branche. Il faudra la rattacher à adomeau.

## Décisions
- 2026-11-03 : on analyse les descentes uniquement. Les fichiers SBE_completed/ servent de référence.
- 2026-11-03 : LAG C-T configurable (Parameters/processing_config.py). Mode "auto" : estimation par profil,
  en nombre entier d'échantillons, avec un repli sur la valeur par défaut de la sonde (Concerto -0,5 s, Maestro -0,045 s).

## Avancement
- [x] Étape 1 – Diagnostic : cause = LAG C-T, aggravée par des classes de 0,25 m à 0 ou 1 mesure (voir figures_comparaison_SBE_RBR/diagnostic_binaverage/)
- [x] Étape 2a – LAG C-T auto + évaluation sur toutes les dates (main_evaluate_ct_lag.py, figures_comparaison_SBE_RBR/evaluation_ct_lag/)
      Résultat sur 14 paires et 10 dates : max |dS| médian passe de 0,24 à 0,18 PSU, pire cas de 0,62 à 0,25 PSU, RMS débiaisé de 0,060 à 0,036 PSU.
- [ ] Étape 2b – Couverture des classes (vides ou à une seule mesure), biais de +0,05 à +0,09 PSU, corrections de main_SBE_rbr_compar.py
- [ ] Étape 3 – Tests, nettoyage, README, CHANGELOG (CHANGELOG déjà créé)
- [ ] Étape 4 – Outil en ligne (après validation)

## Incohérences ouvertes
- SBE 2024-04-30 (2024_CTD_30_avril_sete.csv) : salinité d'environ 5 PSU, donc fichier SBE inexploitable comme référence.
- Biais RBR > SBE de +0,05 PSU dans les couches homogènes (étalonnage ?).
- main_SBE_rbr_compar.py : les mêmes profils sont comparés plusieurs fois (les .rsk 20260903 et 20260908 contiennent
  les mêmes casts), les remontées sont comparées aux SBE, et les doublons de profondeur des SBE ne sont pas moyennés.
