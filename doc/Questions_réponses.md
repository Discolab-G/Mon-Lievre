# Mon Lièvre — Base de Connaissances du Coach IA

## 1. Cartographie des Sujets

Les requêtes des utilisateurs sont classées en sept grandes catégories thématiques afin de couvrir l'intégralité de l'expérience du coureur, sans jamais se substituer à un avis médical.

| Catégorie | Description | Variables Associées |
| :--- | :--- | :--- |
| **Méthodologie & Charge** | Calculs de charge (ACWR), fatigue, monotonie et adaptation du plan. | `étatCharge`, `ACWR`, `monotonie` |
| **Biomécanique & Physiologie** | Posture, foulée, course sans chaussettes, contraintes articulaires et osseuses. | `frequenceEntrainement`, `volumeHebdo` |
| **Matériel & Équipement** | Caractéristiques génériques des chaussures (drop, amorti, usure) et textiles. | `distanceChaussure`, `typeTerrain` |
| **Alimentation & Hydratation** | Gestion des nutriments avant/après l'effort, hydratation stratégique. | - |
| **Récupération & Sommeil** | Protocoles de récupération passive, impact de la qualité du sommeil sur les performances. | `qualiteSommeil`, `frequenceCardiaqueRepos` |
| **Psychologie & Motivation** | Gestion de l'effort perçu (RPE), stress pré-course, maintien de la régularité. | `rpeMoyen` |
| **Santé & Prévention (Strict)** | Alertes sur les douleurs, blessures et orientation médicale systématique. | `niveauDouleur` |

---

## 2. Modèles de Données Structurés (JSON)

```json
{
  "id": "charge_logique",
  "sujet": "Comment l'app calcule ma charge",
  "declencheurs": ["charge", "fatigue", "trop couru", "ua", "ratio", "acwr"],
  "reponse": "L'application compare ta charge d'entraînement récente (les 7 derniers jours) à ta charge habituelle (les 28 derniers jours). Si ce ratio augmente trop brutalement, le risque de fatigue extrême ou de blessure monte en flèche. Si tu ressens une fatigue anormale ou inexpliquée, lève le pied et n'hésite pas à consulter un médecin.",
  "donnees": ["étatCharge", "ACWR"],
  "medical": true
}

{
  "id": "biomecanique_sans_chaussette",
  "sujet": "Impact et risques de la course sans chaussettes",
  "declencheurs": ["pied nu", "sans chaussette", "frottement", "ampoule", "metatarse"],
  "reponse": "Courir sans chaussettes dans des chaussures classiques augmente fortement les frictions directes avec les coutures et la semelle de propreté, favorisant les ampoules et irritations. De plus, si cela modifie tes appuis habituels, les contraintes sur les os extérieurs du pied (comme le 5ème métatarse) peuvent s'intensifier. Au moindre signe de douleur osseuse ou articulaire, arrête l'effort et consulte un professionnel de santé.",
  "donnees": ["distanceChaussure", "volumeHebdo"],
  "medical": true
}

{
  "id": "caracteristiques_chaussures",
  "sujet": "Comprendre l'usure de mes chaussures",
  "declencheurs": ["chaussures", "drop", "amorti", "semelle", "usure", "km"],
  "reponse": "Les propriétés des mousses amortissantes se dégradent naturellement avec les kilomètres, réduisant l'absorption des chocs même si l'aspect extérieur de la chaussure semble intact. Une usure asymétrique peut modifier ta foulée. Si tu ressens des douleurs nouvelles (genoux, tendons) avec une paire usagée, il est vivement conseillé de consulter un médecin du sport ou un podologue.",
  "donnees": ["distanceChaussure"],
  "medical": true
}

{
  "id": "gestion_douleurs",
  "sujet": "Que faire en cas de douleur pendant ou après la course",
  "declencheurs": ["douleur", "mal", "blessure", "cheville", "genou", "tibia", "gêne", "pointe"],
  "reponse": "Une douleur aigüe, persistante ou qui modifie ta façon de courir est un signal d'alarme. L'assistant virtuel de cette application ne pose aucun diagnostic. Arrête ta séance et prends rendez-vous avec un médecin ou un kinésithérapeute pour une évaluation précise.",
  "donnees": ["niveauDouleur"],
  "medical": true
}

[
  {
    "id": "definition_charge",
    "sujet": "Qu'est-ce que la charge d'entraînement ?",
    "declencheurs": ["charge", "calcul", "srpe", "effort", "ua"],
    "reponse": "Pour comparer des efforts très différents, on les ramène tous à une même monnaie : la charge. On utilise la session-RPE : la charge est égale à ton effort perçu multiplié par la durée en minutes. Pour plus de détails, n'hésite pas à consulter le document de Méthodologie de l'app.",
    "donnees": ["étatCharge"],
    "medical": false
  },
  {
    "id": "physio_vs_structurel",
    "sujet": "Différence entre charge physiologique et structurelle",
    "declencheurs": ["physiologique", "structurelle", "différence charge", "deux charges"],
    "reponse": "Un même effort fatigue le corps de deux manières indépendantes : la charge physiologique (cœur, souffle) et la charge structurelle (usure mécanique des muscles et articulations). Cela permet de comprendre qu'une séance peut épuiser ton souffle tout en ménageant tes articulations, ou inversement.",
    "donnees": ["étatCharge"],
    "medical": false
  },
  {
    "id": "explication_acwr",
    "sujet": "Comprendre le ratio ACWR",
    "declencheurs": ["acwr", "ratio", "pic de fatigue", "calcul ratio"],
    "reponse": "Le ratio ACWR compare ta fatigue récente, calculée sur 7 jours, à ta tolérance de fond, calculée sur 28 jours. S'il se situe entre 0,8 et 1,3, tu es dans une zone idéale. S'il dépasse 1,5, le risque de blessure augmente fortement.",
    "donnees": ["ACWR"],
    "medical": false
  },
  {
    "id": "monotonie_alerte",
    "sujet": "Le risque de la monotonie",
    "declencheurs": ["monotonie", "toujours pareil", "stagner", "même allure"],
    "reponse": "Une monotonie élevée indique un entraînement trop uniforme. Faire la même distance à la même allure tous les jours empêche le corps de récupérer et de progresser. Le Coach te conseillera toujours d'intégrer de vrais jours faciles et de vrais jours durs.",
    "donnees": ["monotonie"],
    "medical": false
  },
  {
    "id": "contrainte_stress",
    "sujet": "Qu'est-ce que la contrainte ?",
    "declencheurs": ["contrainte", "stress global", "fatigue globale"],
    "reponse": "La contrainte multiplie ta charge hebdomadaire totale par ta monotonie. C'est un excellent indicateur de ton stress global : si tu cours beaucoup, mais toujours à la même allure, ta contrainte explose, ce qui est un signal d'alarme avant la blessure.",
    "donnees": ["monotonie", "étatCharge"],
    "medical": false
  },
  {
    "id": "adaptation_seance_ratee",
    "sujet": "Que faire si je rate une séance ?",
    "declencheurs": ["raté séance", "déplacer", "emploi du temps", "manqué"],
    "reponse": "Le plan s'adapte à ta vie, tu peux régénérer ton programme à volonté sans jamais effacer ce que tu as déjà accompli. L'adaptation s'applique à l'horizon à venir uniquement, jamais au passé.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "regeneration_plan",
    "sujet": "Régénérer le plan sans perdre de données",
    "declencheurs": ["recalculer", "régénérer", "perdre données", "effacer"],
    "reponse": "Le bouton de régénération réécrit les séances à venir, mais ne touche jamais au journal de ce qui a été réalisé. De plus, tes données restent stockées en local sur ton appareil : rien ne quitte ton téléphone par défaut.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "entrainement_polarise",
    "sujet": "Pourquoi je cours si lentement (80/20) ?",
    "declencheurs": ["trop lent", "vitesse", "80/20", "fondamentale", "lentement"],
    "reponse": "Le plan repose sur un modèle polarisé : une majorité de footing facile, soit environ 80%, et une à deux séances de qualité par semaine au maximum. L'endurance facile n'est jamais prescrite plus rapide que l'allure facile déclarée.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "fatigue_vs_tolerance",
    "sujet": "Différence entre fatigue et tolérance",
    "declencheurs": ["fatigue", "tolérance", "chronique", "aiguë"],
    "reponse": "La fatigue représente ta charge récente (environ 7 jours), c'est ce que tu as dans les jambes en ce moment. La tolérance représente ta charge de fond (environ 28 jours), c'est ce que ton corps a appris à encaisser. L'app compare en permanence les deux.",
    "donnees": ["étatCharge", "ACWR"],
    "medical": false
  },
  {
    "id": "rythmes_progression",
    "sujet": "Les différents rythmes de progression",
    "declencheurs": ["ambitieux", "doux", "standard", "rythme", "évoluer"],
    "reponse": "Tu peux choisir entre un rythme Doux (micro-cycles courts, allègements fréquents), Standard (3 semaines de montée pour 1 d'allègement), ou Ambitieux (blocs plus longs). Le plan progresse par cycles entrecoupés de semaines d'allègement.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "concept_affutage",
    "sujet": "L'affûtage avant un objectif",
    "declencheurs": ["affûtage", "avant course", "tapering", "repos avant course"],
    "reponse": "Pour un objectif précis daté, le plan ajoute un affûtage avant l'échéance : le volume baisse, mais l'intensité se maintient. L'affûtage permet de réduire la fatigue accumulée sans perdre les bénéfices de l'entraînement.",
    "donnees": ["étatCharge"],
    "medical": false
  },
  {
    "id": "radar_5_axes",
    "sujet": "Comment lire le profil radar ?",
    "declencheurs": ["radar", "axes", "profil", "creux", "statistiques"],
    "reponse": "Le radar dresse un portrait sur 8 semaines glissantes selon 5 axes : endurance, vitesse, côtes, technique et robustesse. Ses creux t'invitent à varier ton entraînement, et ce ne sont pas des objectifs stricts, mais plutôt un miroir de ta pratique.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "gestion_apres_objectif",
    "sujet": "Que se passe-t-il après avoir atteint un objectif ?",
    "declencheurs": ["objectif atteint", "après course", "maintien", "fini"],
    "reponse": "Une fois l'objectif confirmé, l'application te propose un choix : le maintien simple avec une charge réduite, la progression pour aller plus loin, ou la diversification pour combler l'axe le plus faible de ton profil radar.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "limites_allouees",
    "sujet": "Limites de temps et compatibilité avec l'objectif",
    "declencheurs": ["pas le temps", "heures max", "limite", "impossible"],
    "reponse": "Si le cadre de temps que tu as posé est incompatible avec l'objectif, le Coach te le dit franchement plutôt que de prescrire un volume intenable. Le moteur distribue la charge à l'intérieur des limites que tu as fixées.",
    "donnees": ["frequenceEntrainement"],
    "medical": false
  },
  {
    "id": "profil_poids_impact",
    "sujet": "L'impact du poids sur la charge",
    "declencheurs": ["poids", "kilos", "impact", "corpulence"],
    "reponse": "Le poids sert au calibrage de l'impact structurel, un coureur plus lourd encaisse plus de charge par kilomètre. Il n'y a jamais de cible de poids ni de jugement dans l'application, ce paramètre sert uniquement à affiner le calcul du coût énergétique et de l'impact.",
    "donnees": ["distanceChaussure"],
    "medical": false
  },
  {
    "id": "biomeca_sable",
    "sujet": "Courir sur le sable",
    "declencheurs": ["sable", "plage", "dune", "terrain meuble"],
    "reponse": "Courir sur sable coûte environ 1,6 fois l'énergie d'une surface dure, tout en étant à faible impact. Cela signifie que ta charge physiologique sera très élevée, mais ta charge structurelle sera ménagée.",
    "donnees": ["typeTerrain"],
    "medical": false
  },
  {
    "id": "biomeca_descente",
    "sujet": "La biomécanique de la descente",
    "declencheurs": ["descente", "casse fibre", "excentrique", "dénivelé négatif"],
    "reponse": "La descente est un problème musculaire excentrique. Ce type d'effort matraque les cuisses et fait grimper la charge structurelle, tout en sollicitant assez peu le système cardio-vasculaire par rapport à une montée.",
    "donnees": ["typeTerrain"],
    "medical": false
  },
  {
    "id": "biomeca_barefoot",
    "sujet": "Courir sans chaussettes (Barefoot)",
    "declencheurs": ["pied nu", "barefoot", "sans chaussette", "chaussure nue"],
    "reponse": "Courir sans chaussettes dans tes chaussures augmente la friction directe. Bien qu'il y ait un léger gain métabolique, cela augmente la charge tissulaire. Au moindre échauffement sévère ou saignement, il faut stopper pour éviter une surinfection.",
    "donnees": [],
    "medical": true
  },
  {
    "id": "biomeca_devers",
    "sujet": "Impact des terrains en dévers",
    "declencheurs": ["dévers", "penché", "asymétrique", "de biais"],
    "reponse": "Le terrain en dévers crée une charge asymétrique. Cela sollicite de manière inégale les chevilles et la bandelette ilio-tibiale, ce qui augmente le tag de charge structurelle d'environ 25%.",
    "donnees": ["typeTerrain"],
    "medical": false
  },
  {
    "id": "biomeca_instable",
    "sujet": "Courir sur terrain instable ou boue",
    "declencheurs": ["boue", "instable", "racine", "cailloux"],
    "reponse": "Un terrain instable sollicite fortement les muscles stabilisateurs et les chevilles, augmentant la charge structurelle. La boue ou la neige réduisent également la traction, ce qui augmente le coût métabolique global.",
    "donnees": ["typeTerrain"],
    "medical": false
  },
  {
    "id": "biomeca_chaleur",
    "sujet": "Courir dans la chaleur",
    "declencheurs": ["chaud", "chaleur", "canicule", "soleil"],
    "reponse": "La chaleur provoque une dérive cardiaque et augmente la charge physiologique. Ton corps dépense de l'énergie supplémentaire pour se refroidir. Il est crucial d'adapter ton allure et de ne pas forcer si des vertiges apparaissent.",
    "donnees": [],
    "medical": true
  },
  {
    "id": "biomeca_froid",
    "sujet": "L'impact du froid sur la foulée",
    "declencheurs": ["froid", "gel", "hiver", "neige"],
    "reponse": "Le froid rend les muscles plus raides et nécessite un échauffement plus long. La charge structurelle est légèrement augmentée car l'absorption des chocs par les tissus froids est moins efficace.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_sac_lest",
    "sujet": "Courir avec un sac ou un lest",
    "declencheurs": ["sac", "lest", "poids", "gilet"],
    "reponse": "Porter une masse supplémentaire augmente à la fois la charge physiologique (tu portes plus lourd) et la charge structurelle (plus d'impact à chaque foulée). Les gilets lestés en descente sont déconseillés car ils ne remplacent pas un vrai travail excentrique.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_tapis",
    "sujet": "Spécificité de la course sur tapis",
    "declencheurs": ["tapis", "salle", "roulant"],
    "reponse": "Sur tapis, il n'y a pas de vent ni d'irrégularité, ce qui réduit légèrement la charge. Le tapis applique un léger multiplicateur à la baisse sur tes charges par rapport à la route.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "blessure_genou",
    "sujet": "Douleur au genou",
    "declencheurs": ["genou", "douleur rotule", "tfl", "essuie glace"],
    "reponse": "Le genou est l'une des articulations les plus touchées par les surcharges structurelles, souvent liées à un ratio aigu/chronique trop élevé. Ce Coach ne pose pas de diagnostic : arrête de courir et consulte un médecin ou un kiné.",
    "donnees": ["niveauDouleur", "ACWR"],
    "medical": true
  },
  {
    "id": "blessure_tendon",
    "sujet": "Douleur au tendon d'Achille",
    "declencheurs": ["tendon", "achille", "talon", "mollet"],
    "reponse": "Une douleur au tendon d'Achille peut être le signe d'une surcharge excentrique ou d'un changement de drop trop rapide. Ne force jamais sur une douleur tendineuse au risque de provoquer une rupture. Consulte un professionnel de santé.",
    "donnees": ["niveauDouleur"],
    "medical": true
  },
  {
    "id": "manque_denivele",
    "sujet": "Comment faire si je n'ai pas de dénivelé près de chez moi ?",
    "declencheurs": ["pas de côte", "plat", "dénivelé", "montagne"],
    "reponse": "Si le terrain manque de dénivelé, le moteur propose du renforcement excentrique ou des côtes répétées. Le renforcement comme les squats à descente lente ou le step-down prend le relais pour te préparer musculairement aux descentes.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "gestion_courbatures",
    "sujet": "Que faire en cas de fortes courbatures ?",
    "declencheurs": ["courbatures", "mal aux muscles", "raide", "jambes lourdes"],
    "reponse": "Les courbatures sont le signe de micro-lésions musculaires normales après un effort inhabituel (souvent excentrique). L'application devrait avoir enregistré une charge élevée. Si la douleur est asymétrique ou très vive (type déchirure), cela relève du domaine médical.",
    "donnees": ["étatCharge"],
    "medical": true
  },
  {
    "id": "altitude_hypoxie",
    "sujet": "Courir en altitude",
    "declencheurs": ["altitude", "montagne", "oxygène", "essoufflé"],
    "reponse": "Au-delà de 1500m, l'hypoxie augmente considérablement ta charge physiologique pour une même allure. La charge de ta sortie est majorée par le tag altitude, tu dois donc t'attendre à une baisse naturelle de tes allures.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "calcul_tags_ressenti",
    "sujet": "Le double comptage de la difficulté",
    "declencheurs": ["tag", "ressenti", "double", "calcul", "srpe"],
    "reponse": "Si tu déclares un ressenti (sRPE) très difficile parce qu'il fait très chaud, l'app amortit le multiplicateur lié à la chaleur pour éviter de compter la difficulté deux fois. Sur le canal physiologique, le moteur fait confiance à ton ressenti en priorité.",
    "donnees": [],
    "medical": false
  }
]

[
  {
    "id": "physio_frequence_cardiaque_max",
    "sujet": "Comprendre la Fréquence Cardiaque Maximale (FCM)",
    "declencheurs": ["fcm", "coeur max", "fréquence maximale", "pulsations", "battements"],
    "reponse": "La FCM est le nombre maximum de battements que ton cœur peut atteindre. Contrairement aux idées reçues, la formule '220 - âge' est souvent imprécise. La FCM ne s'entraîne pas vraiment, mais ta capacité à maintenir un effort proche de cette FCM (ton seuil) s'améliore avec l'entraînement.",
    "donnees": ["frequenceCardiaqueRepos"],
    "medical": false
  },
  {
    "id": "physio_derive_cardiaque",
    "sujet": "Qu'est-ce que la dérive cardiaque ?",
    "declencheurs": ["dérive cardiaque", "coeur qui monte", "pulsations augmentent", "même allure"],
    "reponse": "À allure constante, ta fréquence cardiaque peut monter progressivement : c'est la dérive cardiaque. Elle est due à la fatigue musculaire, à la perte de liquides (transpiration) et à l'augmentation de la température corporelle. C'est un indicateur d'une charge physiologique croissante.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "physio_seuil_aerobie",
    "sujet": "Le seuil aérobie (endurance fondamentale)",
    "declencheurs": ["aérobie", "endurance fondamentale", "seuil 1", "respiration facile", "parler en courant"],
    "reponse": "Le seuil aérobie est l'intensité jusqu'à laquelle ton corps utilise principalement l'oxygène pour produire de l'énergie, sans accumuler de déchets (lactate). Tu dois pouvoir tenir une conversation sans être essoufflé. C'est la base de ton entraînement polarisé.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "physio_seuil_anaerobie",
    "sujet": "Le seuil anaérobie (résistance)",
    "declencheurs": ["anaérobie", "seuil lactique", "seuil 2", "acide lactique", "dureté"],
    "reponse": "Au-delà de ce seuil, ton corps produit plus de lactate qu'il ne peut en recycler. La fatigue musculaire s'installe très vite. Travailler autour de ce seuil permet de repousser le moment où tes jambes deviennent lourdes.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "physio_vo2max",
    "sujet": "Qu'est-ce que la VO2 Max ?",
    "declencheurs": ["vo2", "vo2max", "oxygène max", "moteur", "cylindrée"],
    "reponse": "La VO2 Max est le volume maximal d'oxygène que ton corps peut absorber et utiliser par minute. C'est en quelque sorte la 'cylindrée' de ton moteur physiologique. Elle s'améliore surtout avec des efforts intenses (fractionné) et continus.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "physio_vma",
    "sujet": "La Vitesse Maximale Aérobie (VMA)",
    "declencheurs": ["vma", "vitesse max", "allure max", "test vma"],
    "reponse": "La VMA est la plus petite vitesse de course à laquelle tu atteins ta VO2 Max. À cette allure, tu ne peux tenir que quelques minutes (souvent entre 4 et 6). Elle sert de référence pour calibrer tes séances de fractionné court.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "physio_economie_course",
    "sujet": "L'économie de course (rendement énergétique)",
    "declencheurs": ["économie de course", "rendement", "énergie dépensée", "efficacité"],
    "reponse": "C'est la quantité d'oxygène (ou d'énergie) dont tu as besoin pour courir à une vitesse donnée. Deux coureurs avec la même VO2 Max n'ont pas les mêmes chronos si l'un a une meilleure économie de course (foulée plus fluide, moins de mouvements parasites).",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_cadence",
    "sujet": "La cadence de foulée idéale",
    "declencheurs": ["cadence", "fréquence", "pas par minute", "180 ppm"],
    "reponse": "Il n'y a pas de cadence 'magique' universelle, bien que le chiffre de 180 pas par minute soit souvent cité. L'important est d'éviter une sur-foulée (le pied qui attaque trop loin devant le genou), car cela augmente fortement la charge structurelle au freinage.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_attaque_pied",
    "sujet": "Attaque talon vs médio-pied",
    "declencheurs": ["attaque", "talon", "médio-pied", "avant-pied", "pose du pied"],
    "reponse": "L'attaque talon sollicite davantage les genoux et les hanches (transfert d'ondes de choc), tandis que l'attaque médio/avant-pied sollicite davantage les mollets et les tendons d'Achille. Modifier sa foulée volontairement doit se faire très progressivement pour éviter les blessures.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_oscillation",
    "sujet": "L'oscillation verticale (le rebond)",
    "declencheurs": ["oscillation", "rebond", "monter", "verticale", "sauter en courant"],
    "reponse": "Plus tu rebondis vers le haut à chaque foulée, plus tu dépenses de l'énergie physiologiquement pour rien, et plus le choc à l'atterrissage (charge structurelle) est lourd. Une bonne foulée propulse vers l'avant, pas vers le haut.",
    "donnees": ["frequenceEntrainement"],
    "medical": false
  },
  {
    "id": "biomeca_sans_chaussette_ampoules",
    "sujet": "Les conséquences biomécaniques de courir sans chaussettes",
    "declencheurs": ["sans chaussette", "barefoot", "pied nu", "ampoules", "frottement", "peau"],
    "reponse": "Courir sans chaussettes (le pied directement dans une chaussure standard) retire la couche de glissement textile. La friction de la peau contre la tige et la semelle augmente la proprioception mais majore le risque phlycténaire (ampoules). Si une zone de frottement devient douloureuse à vif ou saigne, stoppe l'effort pour éviter une infection et consulte si nécessaire.",
    "donnees": [],
    "medical": true
  },
  {
    "id": "biomeca_asymetrie",
    "sujet": "Le déséquilibre asymétrique de la foulée",
    "declencheurs": ["asymétrie", "déséquilibre", "boiter", "plus fort à droite", "jambe plus courte"],
    "reponse": "Une légère asymétrie est naturelle. Cependant, si tu compenses consciemment ou si l'asymétrie s'accentue soudainement, c'est souvent pour fuir une gêne ou une douleur. Cela crée une surcharge sur l'autre jambe. En cas de douleur persistante, un avis médical est indispensable.",
    "donnees": ["niveauDouleur"],
    "medical": true
  },
  {
    "id": "physio_point_de_cote",
    "sujet": "Le point de côté",
    "declencheurs": ["point de côté", "mal au ventre", "respiration douleur", "diaphragme"],
    "reponse": "Le point de côté est une crampe du diaphragme ou des ligaments suspenseurs des organes digestifs. Il est bénin et lié à une respiration saccadée ou une digestion en cours. Ralentis, expire profondément quand le pied opposé au point touche le sol, et cela passera.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "physio_crampes",
    "sujet": "Les crampes musculaires en course",
    "declencheurs": ["crampe", "mollet dur", "contraction", "tétanisé", "blocage muscle"],
    "reponse": "Les crampes sont principalement liées à une fatigue neuromusculaire locale (ton muscle est allé au-delà de sa capacité de tolérance), et plus rarement à la seule déshydratation. Si la douleur survient brutalement comme un coup de poignard et persiste après l'arrêt, cela peut être une déchirure : consulte un médecin.",
    "donnees": ["niveauDouleur", "étatCharge"],
    "medical": true
  },
  {
    "id": "physio_entrainement_croise_velo",
    "sujet": "L'intérêt physiologique du vélo (entraînement croisé)",
    "declencheurs": ["vélo", "cyclisme", "croisé", "autre sport", "sans impact", "longue distance"],
    "reponse": "Réaliser des efforts longs à vélo (comme de grandes routes cyclables) permet de développer ton endurance fondamentale et ta capacité cardiovasculaire sans aucune charge structurelle liée aux chocs de la course. C'est un excellent moyen d'augmenter ton volume physiologique tout en épargnant tes articulations.",
    "donnees": ["volumeHebdo"],
    "medical": false
  },
  {
    "id": "physio_fibres_musculaires",
    "sujet": "Fibres lentes vs fibres rapides",
    "declencheurs": ["fibres", "lentes", "rapides", "muscle", "contraction", "génétique"],
    "reponse": "Ton corps possède des fibres musculaires lentes (très endurantes, fonctionnent à l'oxygène) et rapides (explosives, se fatiguent vite). L'entraînement en endurance fondamentale (qui doit représenter la majorité de ta charge) densifie les réseaux sanguins autour de tes fibres lentes pour te rendre plus résistant sur la durée.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "physio_courbatures_doms",
    "sujet": "Les courbatures retardées (DOMS)",
    "declencheurs": ["courbatures", "lendemain", "jambes de bois", "raideur", "doms", "mal aux muscles"],
    "reponse": "Les courbatures n'apparaissent souvent que 24 à 48h après l'effort. Elles sont causées par des micro-lésions musculaires et une inflammation bénigne, typiques après un effort excentrique important (comme beaucoup de dénivelé négatif). Si la douleur est articulaire ou très localisée, ce n'est pas une courbature : sois prudent et consulte au besoin.",
    "donnees": ["étatCharge"],
    "medical": true
  },
  {
    "id": "biomeca_bras",
    "sujet": "Le rôle des bras dans la biomécanique",
    "declencheurs": ["bras", "mouvement bras", "balancier", "épaules", "crispé"],
    "reponse": "Les bras agissent comme des balanciers pour équilibrer la rotation du bassin causée par les jambes. Des bras crispés ou croisant la ligne médiane de ton buste réduisent ton économie de course et créent des tensions inutiles dans le haut du corps. Garde les épaules basses et détendues.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_raideur_tendineuse",
    "sujet": "La raideur tendineuse (effet ressort)",
    "declencheurs": ["tendon", "ressort", "raideur", "élasticité", "renvoi"],
    "reponse": "Une certaine 'raideur' des tendons (notamment d'Achille) est en fait bénéfique en course à pied : elle permet au tendon d'agir comme un ressort puissant qui stocke et restitue l'énergie gratuite à chaque foulée. Trop d'étirements profonds avant une course peuvent diminuer cet effet ressort.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_sur_foule",
    "sujet": "L'erreur de l'overstriding (sur-foulée)",
    "declencheurs": ["overstriding", "sur-foulée", "grand pas", "allonger", "freinage"],
    "reponse": "Chercher à aller plus vite en faisant des pas démesurément longs (le pied atterrit loin devant ton centre de gravité) agit comme un coup de frein biomécanique à chaque pas. Cela augmente massivement la charge structurelle sur le tibia et le genou. Préfère augmenter ta cadence.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "physio_respiration",
    "sujet": "Respiration par le nez ou la bouche ?",
    "declencheurs": ["nez", "bouche", "respiration", "inspirer", "expirer", "souffle"],
    "reponse": "En endurance fondamentale, respirer uniquement par le nez est un bon test pour s'assurer qu'on ne court pas trop vite. Cependant, dès que l'intensité monte (seuil ou fractionné), ouvre la bouche ! Le but est de faire entrer un maximum d'oxygène, peu importe par où.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_entorse_cheville",
    "sujet": "Mécanisme de l'entorse de la cheville",
    "declencheurs": ["entorse", "cheville tordue", "vrillé", "foulure", "pied qui tourne"],
    "reponse": "Une entorse survient souvent sur un terrain instable (racine, pierre) où le pied part vers l'intérieur, étirant violemment les ligaments externes. C'est une blessure qui nécessite un vrai protocole de guérison. Ne cours pas dessus, glace, et va consulter un professionnel de santé.",
    "donnees": ["niveauDouleur"],
    "medical": true
  },
  {
    "id": "biomeca_pronation_supination",
    "sujet": "Pronation et Supination",
    "declencheurs": ["pronation", "supination", "pied qui rentre", "intérieur", "extérieur", "affaissement"],
    "reponse": "La pronation (affaissement du pied vers l'intérieur) est un mécanisme naturel du corps pour absorber les chocs. Ce n'est un problème que si elle est excessive (hyper-pronation) ou asymétrique. Elle s'accentue souvent avec la fatigue au fil des kilomètres.",
    "donnees": ["distanceChaussure"],
    "medical": false
  },
  {
    "id": "physio_epoc",
    "sujet": "La dette d'oxygène (EPOC)",
    "declencheurs": ["epoc", "dette d'oxygène", "brûler après", "fractionné fatigue", "récupération active"],
    "reponse": "Après un effort très intense (comme un fractionné), ton corps continue de consommer plus d'oxygène que la normale pour restaurer ses réserves et réparer les tissus. C'est l'EPOC (Excess Post-exercise Oxygen Consumption). Cela explique pourquoi la charge physiologique d'un fractionné est si haute.",
    "donnees": ["étatCharge"],
    "medical": false
  },
  {
    "id": "biomeca_periostite",
    "sujet": "La périostite tibiale",
    "declencheurs": ["périostite", "tibia", "mal devant jambe", "os qui brûle", "douleur os"],
    "reponse": "La périostite est une inflammation de la membrane qui recouvre le tibia, souvent due à une surcharge structurelle répétée (trop d'impacts, trop vite) ou une attaque talon très marquée. C'est une pathologie de surcharge typique. Stoppe les impacts et consulte impérativement un médecin ou un kiné.",
    "donnees": ["niveauDouleur", "ACWR"],
    "medical": true
  },
  {
    "id": "physio_transpiration",
    "sujet": "Transpiration et perte d'électrolytes",
    "declencheurs": ["transpiration", "sueur", "sel", "électrolytes", "traces blanches"],
    "reponse": "La transpiration permet de réguler ta température interne, mais elle te fait perdre de l'eau et du sodium (sel). Si tu as des traces blanches sur tes vêtements après la course, tu es un 'salty sweater' (tu perds beaucoup de sel). Un apport en électrolytes est crucial sur les efforts de plus d'1h30 pour maintenir la fonction neuromusculaire.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_renforcement_excentrique",
    "sujet": "L'importance du renforcement excentrique",
    "declencheurs": ["excentrique", "renfo", "musculation", "côtes", "descente musculation"],
    "reponse": "Le travail excentrique (freiner une charge, comme amortir en descente) est très traumatisant pour les fibres. L'intégrer sous forme de renforcement musculaire spécifique permet de solidifier les muscles et les tendons, augmentant ta tolérance de fond (charge chronique) face aux descentes.",
    "donnees": ["ACWR"],
    "medical": false
  },
  {
    "id": "physio_vieillissement",
    "sujet": "Effets de l'âge sur la physiologie de course",
    "declencheurs": ["âge", "vieillissement", "vieux", "récupération âge", "plus lent"],
    "reponse": "Avec l'âge, la FCM diminue naturellement, tout comme la souplesse tendineuse. Le besoin de récupération s'allonge car les tissus se réparent moins vite. L'application en tient compte si ton profil est renseigné, mais l'entraînement régulier permet de maintenir une excellente VO2 Max très longtemps.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "biomeca_posture_fatigue",
    "sujet": "L'affaissement postural sous l'effet de la fatigue",
    "declencheurs": ["posture", "dos courbé", "assis", "bassin", "gainage"],
    "reponse": "En fin de course longue, la fatigue des muscles posturaux (abdos, lombaires) provoque souvent un basculement du bassin et un dos qui se voûte. Cette posture dite 'assise' modifie tes appuis, détériore ton économie de course et augmente le risque de blessure au dos ou aux genoux.",
    "donnees": ["étatCharge"],
    "medical": false
  },
  {
    "id": "biomeca_douleur_aine_hanche",
    "sujet": "Douleur à l'aine ou à la hanche",
    "declencheurs": ["aine", "hanche", "psoas", "bassin blocage", "articulation hanche"],
    "reponse": "Le psoas et les articulations de la hanche sont les moteurs de ta foulée. Une douleur vive ou un blocage à ce niveau peut indiquer un problème articulaire ou une inflammation profonde causée par une charge inadaptée. Ne force pas et consulte un médecin du sport pour un examen clinique.",
    "donnees": ["niveauDouleur"],
    "medical": true
  }
]

[
  {
    "id": "mat_drop_definition",
    "sujet": "Qu'est-ce que le drop d'une chaussure ?",
    "declencheurs": ["drop", "différence talon pointe", "hauteur chaussure", "mm"],
    "reponse": "Le drop est la différence de hauteur entre le talon et l'avant-pied de la chaussure, exprimée en millimètres. Un drop élevé (10-12 mm) soulage les mollets mais transfère la charge vers les genoux. Un drop faible (0-4 mm) favorise une attaque médio-pied mais sollicite fortement le tendon d'Achille.",
    "donnees": ["distanceChaussure"],
    "medical": false
  },
  {
    "id": "mat_usure_semelle",
    "sujet": "Quand changer ses chaussures ?",
    "declencheurs": ["changer chaussure", "usure", "durée de vie", "combien de km", "mousse morte"],
    "reponse": "La mousse amortissante (EVA ou équivalent) perd ses propriétés d'absorption des chocs généralement entre 600 et 800 km, augmentant drastiquement ta charge structurelle. Si des douleurs articulaires inhabituelles apparaissent avec une vieille paire, c'est un signal d'alerte pour consulter et changer d'équipement.",
    "donnees": ["distanceChaussure", "niveauDouleur"],
    "medical": true
  },
  {
    "id": "mat_plaques_dynamiques",
    "sujet": "Les chaussures à plaque dynamique (carbone/nylon)",
    "declencheurs": ["carbone", "plaque", "rebond", "chaussure rapide", "effet ressort"],
    "reponse": "Ces chaussures intègrent une plaque rigide et une mousse très réactive pour améliorer l'économie de course (gain physiologique). Cependant, elles modifient la biomécanique et exigent une excellente stabilité de la cheville. Les utiliser à chaque sortie augmente le risque de blessure tendineuse.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "mat_poids_chaussure",
    "sujet": "Impact du poids de la chaussure",
    "declencheurs": ["lourd", "poids chaussure", "léger", "grammes"],
    "reponse": "Ajouter du poids aux extrémités (les pieds) coûte beaucoup plus d'énergie que sur le torse. Une chaussure plus lourde augmente légèrement ta charge physiologique (coût métabolique) à chaque foulée, mais offre souvent plus de protection structurelle.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "mat_chaussure_trail_vs_route",
    "sujet": "Peut-on courir sur route avec des chaussures de trail ?",
    "declencheurs": ["trail sur route", "crampons", "mixte", "bitume trail"],
    "reponse": "C'est possible mais déconseillé. Les crampons vont s'user prématurément sur le bitume, et la gomme, souvent plus rigide, offre un moins bon amorti sur surface dure, ce qui majore la charge structurelle. Réserve-les aux terrains meubles.",
    "donnees": ["typeTerrain"],
    "medical": false
  },
  {
    "id": "mat_lacage_douleur",
    "sujet": "Douleur sur le dessus du pied",
    "declencheurs": ["dessus du pied", "laçage", "coup de pied", "serré", "engourdi", "fourmis"],
    "reponse": "Une douleur sur le coup de pied ou des fourmillements sont souvent dus à un laçage trop serré qui comprime les nerfs et les tendons extenseurs. Desserre tes lacets. Si la douleur persiste après plusieurs jours de repos, une inflammation tendineuse est possible : consulte un médecin.",
    "donnees": ["niveauDouleur"],
    "medical": true
  },
  {
    "id": "mat_pointure_ongle_noir",
    "sujet": "Ongles noirs et choix de la pointure",
    "declencheurs": ["ongle noir", "pointure", "taille chaussure", "orteil", "buter"],
    "reponse": "En courant, le pied gonfle et s'affaisse légèrement. Si tes chaussures sont trop justes, tes orteils butent à chaque foulée, créant un hématome sous l'ongle (ongle noir). Il faut généralement prendre une pointure ou une demi-pointure au-dessus de ta taille de ville. Si l'hématome est très douloureux ou infecté, vois un podologue.",
    "donnees": ["niveauDouleur"],
    "medical": true
  },
  {
    "id": "mat_compression_manchons",
    "sujet": "Utilité des manchons de compression",
    "declencheurs": ["compression", "manchons", "chaussettes hautes", "mollet", "vibration"],
    "reponse": "Pendant l'effort, les manchons de compression servent principalement à réduire les oscillations musculaires (vibrations) à chaque impact, ce qui peut retarder la fatigue neuromusculaire. Après l'effort, ils favorisent le retour veineux pour la récupération.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "mat_vetements_pluie",
    "sujet": "S'équiper pour courir sous la pluie",
    "declencheurs": ["pluie", "imperméable", "mouillé", "veste", "respirant"],
    "reponse": "Une veste totalement imperméable bloque la pluie mais empêche la transpiration de s'évacuer : tu finiras trempé de l'intérieur, ce qui augmente ta dérive cardiaque. Préfère les vestes déperlantes et respirantes. Protège surtout tes extrémités (tête, mains) s'il fait froid.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "mat_montre_vs_telephone",
    "sujet": "Précision GPS : montre ou téléphone ?",
    "declencheurs": ["gps", "précision", "trace", "téléphone", "montre"],
    "reponse": "Les montres de sport dédiées ont des puces GPS souvent plus précises et exposées vers le ciel que les téléphones rangés dans une poche. Toutefois, ton application Mon Lièvre calcule ta charge d'après la durée et ton ressenti (session-RPE), ce qui rend la précision GPS kilométrique moins cruciale pour ton suivi.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "mat_capteur_cardiaque",
    "sujet": "Fiabilité de la fréquence cardiaque (ceinture vs poignet)",
    "declencheurs": ["cardio", "ceinture", "optique", "poignet", "bpm faux"],
    "reponse": "Les capteurs optiques au poignet peuvent 'décrocher' lors d'efforts intenses (fractionnés) ou s'il fait froid (vasoconstriction). La ceinture thoracique à électrodes reste l'outil de mesure de la charge physiologique en temps réel le plus précis.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "mat_frottement_saignement",
    "sujet": "Frottements et saignements (tétons, aisselles, cuisses)",
    "declencheurs": ["sang", "tétons", "aisselle", "cuisses", "brûlure", "frottement"],
    "reponse": "La répétition de la foulée crée des frottements redoutables avec les coutures ou le textile. Applique une crème anti-frottement avant les sorties longues. Si une zone est à vif ou saigne (comme la fameuse blessure des tétons), nettoie et désinfecte après l'effort. En cas de surinfection, consulte un médecin.",
    "donnees": [],
    "medical": true
  },
  {
    "id": "nutri_hydratation_avant",
    "sujet": "Quand et comment s'hydrater avant une course ?",
    "declencheurs": ["boire avant", "eau avant course", "déshydraté départ"],
    "reponse": "L'hydratation se construit la veille et les jours précédents. Boire 1 litre d'eau juste avant le départ ne fera que te donner envie d'uriner. Bois régulièrement de petites gorgées jusqu'à 30 minutes avant l'effort pour t'assurer des urines claires.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_hydratation_pendant",
    "sujet": "Eau claire ou isotonique pendant l'effort ?",
    "declencheurs": ["isotonique", "eau", "boisson effort", "quoi boire", "sucre eau"],
    "reponse": "Pour un effort de moins d'une heure, l'eau claire suffit. Au-delà, une boisson isotonique (contenant des glucides et du sodium) est recommandée. Elle compense les pertes en sel liées à la transpiration et apporte du carburant pour maintenir l'effort physiologique.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_repas_pre_course",
    "sujet": "La règle des 3 heures avant l'effort",
    "declencheurs": ["manger avant", "repas", "3 heures", "digestion", "quand manger"],
    "reponse": "Il est conseillé de terminer son dernier gros repas 3 heures avant l'entraînement. La digestion demande un afflux sanguin massif vers l'estomac. Si tu cours en digérant, tes muscles et ton système digestif vont se battre pour le sang, entraînant inconfort et baisse de performance.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_gels_energetiques",
    "sujet": "Comment consommer les gels énergétiques ?",
    "declencheurs": ["gel", "sucre", "compote", "pâte de fruit"],
    "reponse": "Un gel énergétique apporte un concentré de glucides rapidement assimilables. Il faut impérativement le consommer avec 150 à 200 ml d'eau claire (et non de la boisson isotonique) pour diluer le sucre dans l'estomac, sinon tu risques des crampes intestinales violentes.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_courir_a_jeun",
    "sujet": "Avantages et risques de courir à jeun",
    "declencheurs": ["à jeun", "sans manger", "matin ventre vide", "brûler graisse"],
    "reponse": "Courir le matin sans avoir mangé habitue le corps à utiliser les graisses comme carburant. Cependant, la charge physiologique est plus élevée et le risque d'hypoglycémie est réel. À réserver aux sorties courtes et en endurance fondamentale (allure lente).",
    "donnees": ["étatCharge"],
    "medical": false
  },
  {
    "id": "nutri_mur_marathon",
    "sujet": "Le mur du marathon (épuisement du glycogène)",
    "declencheurs": ["le mur", "30eme km", "plus d'énergie", "panne sèche", "glycogène"],
    "reponse": "Le fameux 'mur' survient quand tes réserves de glycogène (sucre stocké dans les muscles et le foie) sont épuisées, généralement autour du 30ème kilomètre. Ton corps doit alors brûler des graisses, un processus beaucoup plus lent en oxygène, ce qui t'oblige à ralentir brutalement.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_problemes_gastriques",
    "sujet": "Troubles digestifs en courant",
    "declencheurs": ["diarrhée", "ventre", "intestins", "nausée", "vomir", "toilettes"],
    "reponse": "Les chocs répétés de la foulée et la réduction de l'afflux sanguin vers l'intestin provoquent souvent des troubles gastriques. Si les vomissements ou diarrhées sont intenses ou s'accompagnent de fièvre et de sang, arrête-toi immédiatement, hydrate-toi prudemment et consulte un médecin.",
    "donnees": ["niveauDouleur"],
    "medical": true
  },
  {
    "id": "nutri_pasta_party",
    "sujet": "La surcharge glucidique avant une course",
    "declencheurs": ["pasta party", "pâtes", "surcharge", "glucides 3 jours", "préparation nutrition"],
    "reponse": "Il est inutile de se gaver de pâtes la veille au soir, les stocks ne se font pas en une nuit. Augmente modérément ta ration de glucides (riz, pommes de terre, pâtes) lors des 3 jours précédant un objectif long, tout en diminuant ton volume d'entraînement (l'affûtage).",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_cafeine",
    "sujet": "La caféine avant ou pendant l'effort",
    "declencheurs": ["café", "caféine", "boost", "excitant"],
    "reponse": "La caféine est reconnue pour abaisser l'effort perçu (sRPE) et repousser la fatigue mentale. Attention, elle peut accélérer le transit intestinal et avoir un effet diurétique. Teste toujours sa tolérance à l'entraînement, jamais le jour d'une course.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_alcool_recuperation",
    "sujet": "Alcool et récupération (la bière post-course)",
    "declencheurs": ["bière", "alcool", "récupération bière", "fêter"],
    "reponse": "Contrairement au mythe, la bière n'est pas une bonne boisson de récupération. L'alcool déshydrate, bloque la synthèse des protéines (réparation musculaire) et ralentit la recharge des stocks de glycogène. Hydrate-toi d'abord avec de l'eau ou une boisson de récupération.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_soif_vs_horloge",
    "sujet": "Faut-il boire à la soif ou s'imposer un rythme ?",
    "declencheurs": ["soif", "quand boire", "rythme hydratation", "trop boire"],
    "reponse": "La soif est un signal parfois tardif en course, mais boire à l'excès (hyponatrémie) est très dangereux. Le bon compromis est de boire l'équivalent d'une à deux gorgées (100 à 150 ml) toutes les 15 à 20 minutes, en adaptant selon la température extérieure.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_magnesium_crampes",
    "sujet": "Magnésium et prévention des crampes",
    "declencheurs": ["magnésium", "cures", "banane", "crampes minéraux"],
    "reponse": "Un déficit en minéraux (sodium, potassium, magnésium) peut favoriser les crampes, bien que la cause principale soit souvent la fatigue musculaire pure. Une alimentation riche au quotidien (oléagineux, légumes verts, eaux minéralisées) suffit généralement à couvrir les besoins.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_poids_etalonnage",
    "sujet": "Poids et paramétrage de la charge",
    "declencheurs": ["perdre du poids", "maigrir", "régime", "paramètres poids"],
    "reponse": "L'application ne juge jamais ton poids et ne propose aucun régime. Elle a besoin de cette donnée uniquement pour étalonner ta charge structurelle : l'impact encaissé par tes articulations dépend directement de ta masse corporelle au moment de la course.",
    "donnees": ["distanceChaussure"],
    "medical": false
  },
  {
    "id": "nutri_solide_liquide",
    "sujet": "Alimentation solide ou liquide en course ?",
    "declencheurs": ["solide", "liquide", "mâcher", "barre", "boisson"],
    "reponse": "Plus l'intensité de la course est élevée, plus il est difficile de mâcher et de digérer du solide (le sang quitte l'estomac). Sur un marathon, le liquide ou semi-liquide (gels) est roi. Sur un trail long à faible allure, l'apport solide (barres, salé) est nécessaire pour éviter l'écoeurement.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "nutri_hyponatremie",
    "sujet": "Le danger de l'hyponatrémie (trop boire)",
    "declencheurs": ["trop boire", "hyponatrémie", "mal de tête", "gonflé", "intoxication eau"],
    "reponse": "Boire trop d'eau pure (sans électrolytes) sur un effort très long dilue le sel dans ton sang. Cela peut causer des maux de tête, de la confusion, voire un coma. C'est une urgence médicale absolue. Si tu es confus et que tes doigts sont gonflés, arrête-toi et appelle les secours.",
    "donnees": ["niveauDouleur"],
    "medical": true
  },
  {
    "id": "nutri_fer_anemie",
    "sujet": "Fer, anémie et fatigue chronique",
    "declencheurs": ["fer", "anémie", "fatigue constante", "pâle", "sang"],
    "reponse": "Les coureurs réguliers (notamment les femmes et ceux pratiquant sur bitume) détruisent des globules rouges à cause des ondes de choc (hémolyse d'effort), risquant une carence en fer (anémie). Si ta fatigue persiste malgré un ratio ACWR équilibré, un bilan sanguin prescrit par un médecin est nécessaire.",
    "donnees": ["ACWR"],
    "medical": true
  },
  {
    "id": "mat_hygiene_chaussettes",
    "sujet": "Choix des chaussettes et hygiène du pied",
    "declencheurs": ["chaussettes", "coton", "synthétique", "mycose", "transpiration pied"],
    "reponse": "Le coton retient l'humidité, gonfle et favorise les ampoules ainsi que la prolifération de bactéries. Opte pour des chaussettes techniques en fibres synthétiques ou laine mérinos qui évacuent la transpiration. Garder les pieds au sec réduit considérablement le risque de mycoses.",
    "donnees": [],
    "medical": false
  }
]

[
  {
    "id": "recup_sommeil_importance",
    "sujet": "L'importance du sommeil dans la récupération",
    "declencheurs": ["sommeil", "dormir", "nuit", "fatigue nuit", "insomnie"],
    "reponse": "Le sommeil est le meilleur outil de récupération existant. C'est pendant les phases de sommeil profond que le corps sécrète l'hormone de croissance, réparant les fibres musculaires lésées par la charge structurelle. Un manque de sommeil augmente le RPE (l'effort te paraîtra plus dur) et le risque de blessure.",
    "donnees": ["qualiteSommeil"],
    "medical": false
  },
  {
    "id": "recup_active_vs_passive",
    "sujet": "Récupération active vs passive",
    "declencheurs": ["récupération active", "récupération passive", "décrassage", "bouger ou repos"],
    "reponse": "La récupération passive, c'est le repos total (canapé, sommeil). La récupération active implique une activité très douce (marche, vélo lent, natation) qui stimule la circulation sanguine pour nettoyer les déchets métaboliques sans ajouter de nouvelle charge.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "recup_vfc",
    "sujet": "La Variabilité de la Fréquence Cardiaque (VFC)",
    "declencheurs": ["vfc", "hrv", "variabilité", "stress corps", "système nerveux"],
    "reponse": "La VFC mesure l'irrégularité des battements de ton cœur. Une VFC haute indique que ton système nerveux est reposé et prêt à encaisser de la charge. Une VFC qui s'effondre est le premier signe d'une fatigue globale, qu'elle soit liée à l'entraînement, à un virus ou au stress du quotidien.",
    "donnees": ["qualiteSommeil", "frequenceCardiaqueRepos"],
    "medical": false
  },
  {
    "id": "recup_auto_massage",
    "sujet": "Les rouleaux et pistolets de massage",
    "declencheurs": ["rouleau", "massage", "pistolet", "fascia", "nœud musculaire"],
    "reponse": "L'auto-massage (rouleau en mousse, pistolet à percussion) aide à détendre les fascias (les enveloppes des muscles) et à réduire la sensation de raideur temporaire. Cela ne répare pas les fibres plus vite, mais cela améliore le confort post-séance. Ne passe jamais ces outils sur une articulation ou un os.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "recup_jours_repos",
    "sujet": "Faut-il faire des jours de repos complet ?",
    "declencheurs": ["repos complet", "jour off", "zéro sport", "ne rien faire"],
    "reponse": "Oui, absolument. Le moteur de l'application veille à casser la monotonie en intégrant de vrais jours faciles ou de repos. C'est pendant le repos que le corps surcompense et devient plus fort. Ne pas se reposer, c'est s'entraîner à s'épuiser.",
    "donnees": ["monotonie"],
    "medical": false
  },
  {
    "id": "recup_etirements",
    "sujet": "Faut-il s'étirer après la course ?",
    "declencheurs": ["étirement", "stretching", "assouplissement", "raideur"],
    "reponse": "Les étirements statiques profonds juste après une séance dure (ou avec beaucoup de descente) sont déconseillés, car ils étirent des fibres déjà micro-déchirées, augmentant la charge structurelle. Préfère de la mobilité douce à chaud, et garde les étirements profonds pour les jours de repos.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "recup_bains_froids",
    "sujet": "Bains froids et cryothérapie",
    "declencheurs": ["bain froid", "glace", "cryothérapie", "froid", "réduire inflammation"],
    "reponse": "Le froid bloque l'inflammation et agit comme un antalgique naturel. C'est excellent pour enchaîner les courses. Cependant, l'inflammation naturelle post-entraînement est le signal qui dit au corps de se renforcer. Trop de froid bloque cette adaptation physiologique. À utiliser de manière stratégique.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "recup_fc_repos",
    "sujet": "Évolution de la fréquence cardiaque au repos",
    "declencheurs": ["fc repos", "cœur au repos", "pouls matin", "battements matin"],
    "reponse": "Une fréquence cardiaque au repos (mesurée au réveil) qui baisse au fil des mois est un signe d'adaptation aérobie (ton cœur est plus puissant). Si elle augmente subitement de plus de 5 à 10 battements sur plusieurs jours, c'est un signe de mauvaise récupération ou de maladie.",
    "donnees": ["frequenceCardiaqueRepos"],
    "medical": false
  },
  {
    "id": "recup_surentrainement",
    "sujet": "Les signes du surentraînement",
    "declencheurs": ["surentraînement", "burnout", "épuisé", "n'avance plus", "overtraining"],
    "reponse": "Le syndrome de surentraînement se traduit par une baisse des performances malgré l'entraînement, un sommeil perturbé, une irritabilité et un ratio ACWR souvent longtemps dans le rouge. C'est un état d'épuisement sérieux. Stoppe l'entraînement et consulte un médecin.",
    "donnees": ["ACWR", "étatCharge"],
    "medical": true
  },
  {
    "id": "recup_sieste",
    "sujet": "L'efficacité de la sieste",
    "declencheurs": ["sieste", "dormir jour", "somme", "fatigue journée"],
    "reponse": "Une 'micro-sieste' de 20 minutes suffit à relancer la vigilance et abaisser le stress. Une sieste d'un cycle complet (environ 90 minutes) permet une réparation musculaire (sommeil profond). Attention à ne pas dépasser 30 minutes si tu ne veux pas te réveiller groggy.",
    "donnees": ["qualiteSommeil"],
    "medical": false
  },
  {
    "id": "psycho_baisse_motivation",
    "sujet": "Que faire en cas de baisse de motivation ?",
    "declencheurs": ["motivation", "pas envie", "flemme", "perte envie", "abandon"],
    "reponse": "C'est un cycle naturel. L'entraînement repose sur la discipline, pas sur l'envie quotidienne. Fixe-toi un micro-objectif : 'Je mets mes chaussures et je cours 10 minutes'. Souvent, une fois dehors, la machine se lance. Si l'aversion est totale, prends un vrai jour de repos sans culpabilité.",
    "donnees": ["rpeMoyen"],
    "medical": false
  },
  {
    "id": "psycho_effort_percu_srpe",
    "sujet": "Pourquoi mesurer le ressenti (RPE) plutôt que juste l'allure ?",
    "declencheurs": ["rpe", "ressenti", "échelle 1 à 10", "subjectif", "pourquoi noter l'effort"],
    "reponse": "La méthode sRPE intègre tout ce que ta montre ne voit pas : une mauvaise nuit, le stress du travail, ou la chaleur. Si une séance habituellement facile te paraît dure (RPE élevé), ton corps a réellement subi une charge supérieure. La subjectivité est la meilleure donnée.",
    "donnees": ["rpeMoyen", "étatCharge"],
    "medical": false
  },
  {
    "id": "psycho_stress_course",
    "sujet": "Gérer le stress avant une course",
    "declencheurs": ["stress", "peur", "boule au ventre", "course approche", "anxiété"],
    "reponse": "Le stress pré-course est physiologique : l'adrénaline te prépare à l'effort. Pour éviter qu'il ne te paralyse, prépare tes affaires la veille, visualise ta ligne de départ et concentre-toi sur le processus (ton allure, ta respiration) plutôt que sur le chronomètre final.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "psycho_seance_ratee",
    "sujet": "Gérer mentalement une séance ratée",
    "declencheurs": ["raté", "mauvaise séance", "échec", "pas réussi", "craqué"],
    "reponse": "Une séance ne définit pas un niveau. L'adaptation se crée sur l'accumulation chronique (tes 28 derniers jours). Une mauvaise séance est souvent une victoire pour le Coach IA, car elle signale un pic de fatigue permettant de recalibrer le plan avant la blessure.",
    "donnees": ["ACWR"],
    "medical": false
  },
  {
    "id": "psycho_comparaison_reseaux",
    "sujet": "Le piège des réseaux sociaux sportifs",
    "declencheurs": ["réseaux", "autres coureurs", "comparer", "allure des autres", "strava"],
    "reponse": "Les réseaux sociaux sportifs poussent souvent à courir trop vite pour afficher de belles statistiques. Ton plan est calibré selon TA charge et TON radar de profil. Courir lentement (80/20) demande de laisser son ego au vestiaire.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "psycho_blues_post_course",
    "sujet": "Le blues d'après course",
    "declencheurs": ["blues", "après course", "vide", "déprime", "plus de but"],
    "reponse": "Après des mois focalisés sur un objectif, franchir la ligne d'arrivée provoque une chute soudaine de dopamine et d'endorphines. Ce 'vide' est normal. L'application gère cette période en te proposant une phase de maintien doux ou de diversification pour retrouver le plaisir simple de bouger.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "psycho_musique",
    "sujet": "Courir en musique ou sans ?",
    "declencheurs": ["musique", "écouteurs", "podcast", "son", "bruit"],
    "reponse": "La musique à tempo élevé réduit le ressenti de l'effort (baisse le RPE) et peut aider sur les séances difficiles. Cependant, courir sans musique permet une meilleure écoute de sa respiration et de sa foulée (proprioception). L'idéal est d'alterner selon l'objectif de la séance.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "psycho_peur_blessure",
    "sujet": "La peur de se reblesser (kinésiophobie)",
    "declencheurs": ["peur", "reblesser", "appréhension", "reprise après blessure", "bloqué"],
    "reponse": "Après une blessure, la peur du mouvement est une protection neurologique normale. La reprise doit être extrêmement progressive. Si ton appréhension se transforme en douleur physique aiguë lors de la reprise, stoppe immédiatement. Si l'angoisse te paralyse, un suivi médical et psychologique est recommandé.",
    "donnees": ["niveauDouleur"],
    "medical": true
  },
  {
    "id": "psycho_visualisation",
    "sujet": "La visualisation ou imagerie mentale",
    "declencheurs": ["visualisation", "imagerie", "mental", "se voir", "préparation mentale"],
    "reponse": "Le cerveau fait peu la différence entre un mouvement réellement exécuté et un mouvement vivement imaginé. Visualiser le parcours, anticiper les moments durs et s'imaginer les surmonter avec succès aide à pré-programmer le corps pour l'échéance.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "psycho_burnout_sportif",
    "sujet": "L'épuisement mental (Burn-out)",
    "declencheurs": ["dégoût", "burnout", "épuisement mental", "plus la force", "ras le bol"],
    "reponse": "Le burn-out sportif est une surcharge cognitive sévère où le sport devient une contrainte destructrice. L'entraînement est censé te construire, pas te détruire. Face à un dégoût total ou une détresse psychologique persistante, coupe tout entraînement et tourne-toi vers un professionnel de la santé mentale.",
    "donnees": ["rpeMoyen"],
    "medical": true
  },
  {
    "id": "app_confidentialite_locale",
    "sujet": "Où vont mes données personnelles ?",
    "declencheurs": ["données", "cloud", "serveur", "vie privée", "local", "stockage"],
    "reponse": "Par défaut, absolument nulle part. L'application Mon Lièvre fonctionne entièrement en local sur ton appareil. Il n'y a pas de compte, pas de cloud, et aucun serveur central ne stocke tes informations d'entraînement.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "app_coach_ia_declenchement",
    "sujet": "Le Coach IA m'écoute-t-il en permanence ?",
    "declencheurs": ["écoute", "arrière-plan", "espion", "envoi données", "quand partent"],
    "reponse": "Non. Rien n'est envoyé en arrière-plan. La seule fois où une information quitte ton téléphone, c'est quand tu décides toi-même de poser une question au Coach, et uniquement les variables nécessaires à ta requête sur l'instant.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "app_ajout_cle_api",
    "sujet": "Comment configurer la clé API ?",
    "declencheurs": ["clé api", "configurer claude", "ajouter clé", "comment ça marche ia"],
    "reponse": "Le mode Coach IA est une option. Tu dois fournir ta propre clé API (générée via le service Claude). Une fois saisie dans l'application, elle est stockée uniquement sur ton téléphone. C'est toi qui contrôles l'accès.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "app_entrainement_modele",
    "sujet": "Mes données servent-elles à entraîner l'IA ?",
    "declencheurs": ["entraîner ia", "vendre données", "anthropic", "claude données"],
    "reponse": "Non. Le fournisseur de l'IA (Anthropic) n'entraîne pas ses modèles commerciaux sur les données transmises via son API, ne les conserve pas durablement et ne les revend pas. Ta requête sert juste à te répondre, puis est effacée de leurs serveurs.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "app_regeneration_plan",
    "sujet": "Puis-je modifier mon plan en cours de route ?",
    "declencheurs": ["recalcul", "modifier plan", "changer séances", "bouton régénérer"],
    "reponse": "Oui, à volonté. Le bouton de régénération adapte ton programme à venir en fonction de ce que tu viens de vivre, sans jamais effacer ton historique. Le plan s'adapte à ta vie, pas l'inverse.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "app_limite_temps",
    "sujet": "Si je n'ai pas le temps de tout faire ?",
    "declencheurs": ["heures max", "limite temps", "trop de sport", "pas le temps"],
    "reponse": "Tu définis tes limites allouées dans l'application. Le moteur distribue la charge à l'intérieur de ces limites. Si ton temps libre est incompatible avec ton objectif sportif, le Coach IA te le dira franchement au lieu de te prescrire un volume intenable.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "app_radar_profil",
    "sujet": "Comment lire le radar à 5 axes ?",
    "declencheurs": ["radar", "axes", "polygone", "profil coureur", "endurance vitesse"],
    "reponse": "Le radar est un miroir de ta pratique sur les 8 dernières semaines glissantes, basé sur 5 axes (Endurance, Vitesse, Côtes, Technique, Robustesse). Ce ne sont pas des objectifs stricts à remplir, mais une visualisation de tes forces et des zones à travailler.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "app_medical_disclaimer",
    "sujet": "L'application peut-elle me soigner ?",
    "declencheurs": ["médecin", "diagnostic", "application santé", "soigner", "fiable santé"],
    "reponse": "Non. Mon Lièvre et son Coach IA ne sont pas des dispositifs médicaux. L'application calcule des charges mathématiques, mais seul un professionnel de santé est habilité à poser un diagnostic. Ne prends jamais aucun risque avec ta santé sous prétexte qu'une application te dit l'inverse.",
    "donnees": [],
    "medical": true
  },
  {
    "id": "app_echelle_rpe_usage",
    "sujet": "Comment bien noter son RPE de fin de séance ?",
    "declencheurs": ["note rpe", "comment noter", "1 à 10", "barème", "échelle de borg"],
    "reponse": "Note la séance de 1 (reposant) à 10 (effort maximal) environ 30 minutes après l'arrivée. Sois honnête : si tu devais courir en endurance (facile) mais qu'il faisait très chaud et que tu as souffert, mets un 6 ou 7. L'application a besoin de ta réalité, pas de la théorie.",
    "donnees": ["rpeMoyen"],
    "medical": false
  },
  {
    "id": "app_suppression_donnees",
    "sujet": "Comment effacer mes données de l'application ?",
    "declencheurs": ["effacer", "supprimer données", "désinstaller", "remise à zéro", "reset"],
    "reponse": "Puisque tout est stocké localement sur ton appareil, il n'y a aucune procédure complexe à faire ou de support client à contacter. Supprimer l'application efface instantanément et définitivement l'ensemble de tes données.",
    "donnees": [],
    "medical": false
  }
]

[
  {
    "id": "recup_semaine_allegement",
    "sujet": "À quoi sert la semaine d'allègement (deload) ?",
    "declencheurs": ["allègement", "semaine facile", "assimilation", "deload", "repos plan", "baisse volume"],
    "reponse": "Le plan progresse par cycles entrecoupés de semaines d'allègement. C'est pendant cette semaine de volume réduit que ton corps assimile le travail des semaines précédentes, répare les tissus et construit le muscle (la surcompensation). Sauter cette semaine, c'est bloquer ta progression et courir droit à la blessure.",
    "donnees": ["étatCharge"],
    "medical": false
  },
  {
    "id": "recup_chaleur_sauna",
    "sujet": "Sauna et hammam pour la récupération",
    "declencheurs": ["sauna", "hammam", "chaleur", "bain chaud", "transpirer après"],
    "reponse": "La chaleur favorise la vasodilatation, ce qui détend les muscles et aide à détendre le système nerveux. Cependant, elle majore aussi fortement la déshydratation post-effort. Il est conseillé d'attendre au moins quelques heures après une course intense avant de s'exposer à de fortes chaleurs, et de boire abondamment.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "recup_bottes_pressotherapie",
    "sujet": "Les bottes de pressothérapie (compression pneumatique)",
    "declencheurs": ["bottes", "pressothérapie", "compression jambes", "massage air", "machine jambes"],
    "reponse": "Ces bottes utilisent des coussins d'air pour masser les jambes de bas en haut. Elles accélèrent artificiellement le retour veineux et procurent une excellente sensation de jambes légères. C'est un bon outil de récupération passive en complément, mais cela ne remplacera jamais les piliers fondamentaux que sont le sommeil et la nutrition.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "recup_electrostimulation",
    "sujet": "L'électrostimulation post-effort",
    "declencheurs": ["électrostimulation", "électrodes", "tens", "courant", "patchs", "secousses"],
    "reponse": "Les programmes de récupération par électrostimulation créent des micro-secousses musculaires qui relancent la circulation sanguine locale sans épuiser le système nerveux central. C'est idéal le soir après une grosse séance. Attention, ne place jamais les électrodes sur une zone douloureuse pouvant s'apparenter à une déchirure.",
    "donnees": ["niveauDouleur"],
    "medical": false
  },
  {
    "id": "recup_drainage_postural",
    "sujet": "Le drainage postural (jambes en l'air)",
    "declencheurs": ["jambes en l'air", "mur", "drainage", "retour veineux", "jambes lourdes au mur"],
    "reponse": "S'allonger sur le dos avec les jambes à la verticale contre un mur pendant 10 à 15 minutes utilise simplement la gravité pour faciliter le drainage veineux et soulager la sensation de jambes lourdes. C'est l'une des méthodes de récupération les plus efficaces, et elle est totalement gratuite.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "recup_stress_quotidien",
    "sujet": "L'impact du stress professionnel/personnel sur la récupération",
    "declencheurs": ["stress", "travail", "fatigué par le boulot", "charge mentale", "vie perso"],
    "reponse": "Ton corps ne fait pas la différence entre le stress physique (l'entraînement) et le stress mental (travail, famille). Un stress quotidien élevé maintient du cortisol dans ton sang et inhibe la récupération. Si ta charge mentale est haute, ton RPE sera perçu comme plus difficile, et le plan s'adaptera en abaissant ta charge.",
    "donnees": ["rpeMoyen", "étatCharge"],
    "medical": false
  },
  {
    "id": "recup_mobilite_lendemain",
    "sujet": "La mobilité douce le lendemain d'une course",
    "declencheurs": ["mobilité", "lendemain", "raide", "dérouiller", "yoga doux", "réveil musculaire"],
    "reponse": "Le lendemain d'une séance éprouvante (forte charge structurelle), une routine de mobilité articulaire douce (mouvements amples sans forcer les amplitudes) est excellente. Elle permet de 'dérouiller' les articulations et de relancer la circulation sans créer de micro-lésions supplémentaires associées aux étirements passifs profonds.",
    "donnees": [],
    "medical": false
  },
  {
    "id": "recup_sommeil_alcool",
    "sujet": "L'impact de l'alcool sur l'architecture du sommeil",
    "declencheurs": ["alcool soir", "sommeil détruit", "mal dormi", "boire avant dormir"],
    "reponse": "Même si un verre d'alcool peut donner l'illusion d'aider à s'endormir, il détruit l'architecture réparatrice du sommeil. Il supprime le sommeil paradoxal et fragmente les phases de sommeil profond (celles qui réparent les muscles). Le résultat est une nuit très peu récupératrice qui augmente ta fatigue le lendemain.",
    "donnees": ["qualiteSommeil"],
    "medical": false
  },
  {
    "id": "recup_overreaching_vs_surentrainement",
    "sujet": "Différence entre grosse fatigue (overreaching) et surentraînement",
    "declencheurs": ["dépassé", "overreaching", "surcompensation", "fatigue normale", "ko complet"],
    "reponse": "Une grande fatigue (overreaching) est normale à la fin d'un bloc d'entraînement difficile : une semaine d'allègement suffit à rebondir. Si la fatigue, la baisse de motivation et l'insomnie persistent malgré le repos, c'est un syndrome de surentraînement. C'est une pathologie qui exige l'arrêt du sport et un diagnostic médical.",
    "donnees": ["ACWR", "étatCharge"],
    "medical": true
  },
  {
    "id": "recup_courir_malade",
    "sujet": "Courir quand on a de la fièvre ou un virus",
    "declencheurs": ["malade", "fièvre", "rhume", "virus", "toux", "covid", "grippe"],
    "reponse": "La règle est stricte : on ne court jamais avec de la fièvre ou de fortes courbatures virales. Faire monter son cœur pendant une infection virale augmente drastiquement le risque de développer une myocardite (inflammation du cœur) potentiellement mortelle. Repose-toi totalement et consulte un médecin si les symptômes durent.",
    "donnees": [],
    "medical": true
  }
]