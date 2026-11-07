---
name: hubspot-agent-hub
description: >-
  Opérer l'Agent Hub de HubSpot (les agents prêts à l'emploi et l'agent builder qui permet d'en construire sur mesure) sans se tromper sur ce que ça sait faire, ce que ça coûte et ce qui est enfermé derrière une bêta. Porte les faits qui ne se devinent pas et qui font conclure faux : le sourcing de CONTACTS (trouver les bonnes personnes dans une entreprise cible) existe mais uniquement via un opt-in bêta, sans lui l'agent ne touche que les contacts déjà au CRM ; tester un agent ne consomme AUCUN crédit, donc le coût se mesure avant de publier ; un agent décide ses étapes seul là où un workflow suit les tiennes, et ce choix engage la prévisibilité d'un process client ; la Connaissance reste constante entre les exécutions alors que les Entrées changent à chaque run. Couvre aussi la chaîne Buyer Intent vers Prospecting Agent, l'onglet MCP qui ouvre les agents sur l'extérieur, les Knowledge Vaults, les limites d'exécution et les niveaux d'abonnement requis. À invoquer sur "agent hub", "agents hubspot", "breeze agent", "prospecting agent", "data agent", "company research agent", "agent builder", "créer un agent hubspot", "knowledge vault", "trouver les contacts dans une entreprise", "identifier le bon persona", "automatiser la prospection dans hubspot", "agent ou workflow", ou dès qu'on s'apprête à activer, construire ou chiffrer un agent HubSpot.
---

## ⛔ GATE CONSENTEMENT : avant toute action qui MODIFIE le portail

**Lire, chercher, analyser : libre.** **Créer, modifier ou supprimer** quoi que ce soit dans le
système d'un client : **jamais sans un « oui » explicite, donné dans le fil, avant d'agir.**

**Périmètre** : contacts, transactions, sociétés, propriétés, listes, workflows, automatisations,
séquences, templates, emails, et l'équivalent dans tout outil connecté (Notion, Make, Drive…).

**Le geste, avant un LOT d'écritures :**

```
Action prévue : [quoi]
Cible        : [portail / objet]
Impact       : [créer / modifier / supprimer N éléments]
Confirme ? (oui / non)
```

Attendre le « oui ». **Il couvre ensuite tout le lot annoncé** : on n'interrompt pas objet par objet.
On redemande uniquement si on **sort du périmètre annoncé**, ou si on découvre un **irréversible non
prévu**.

**Pas d'exception « petit changement » ou « facile à annuler ».** Et quand on te demande de modifier
X, tu modifies X, pas une refonte à ta façon. Désaccord sur l'approche : une question courte, jamais
un pivot décidé seul.

**Pourquoi c'est écrit ici en toutes lettres, et pas en renvoi** : un CRM client, ce sont des données
de production, souvent irréversibles, et la responsabilité est vis-à-vis du **client final**. Un
garde-fou qui pointe vers un fichier que tu n'as pas installé n'est plus qu'une intention.

# /hubspot-agent-hub : opérer les agents HubSpot

## §0 Le problème que ça règle

L'Agent Hub bouge vite et son marketing promet plus que la doc. Trois erreurs coûtent cher, et elles sont toutes évitables avec un fait précis :

- **Conclure « c'est impossible » alors que c'est derrière une bêta.** Cas type : on établit, correctement, que l'enrichissement natif complète une fiche existante (il part d'un email professionnel ou d'un domaine) et ne *découvre* jamais de personnes. On en tire « le workflow qui trouve les personas est infaisable ». **Faux au niveau du portail** : le Prospecting Agent source des contacts, via une source de données externe connectée, sous réserve d'un opt-in. Une conclusion juste sur le mauvais périmètre mène à une recommandation fausse.
- **Chiffrer avant de tester.** Tester un agent ne consomme aucun crédit. Beaucoup de discussions budgétaires n'auraient pas lieu si l'agent avait tourné une fois à blanc.
- **Choisir « agent » quand il fallait « workflow ».** Un agent qui invente ses étapes est séduisant en démo et ingérable dans un process client qu'on doit expliquer, reproduire et facturer.

⚠️ **Tout ce qui suit a une date.** Ce domaine change de mois en mois. Avant de reprendre un chiffre ou une capacité dans un livrable client, **re-vérifier sur `knowledge.hubspot.com`** (pour les prix : le catalogue produits et services de l'éditeur), jamais un blog, jamais un annuaire, jamais ce fichier seul. *(Vérifié le 2026-11-07.)*

## §1 Agent ou Workflow : le choix qui engage tout le reste

La doc de l'éditeur (« Choose when to use AI agents or workflows ») trie les objectifs en trois familles :

| | Quand c'est le bon choix |
|---|---|
| **Workflow** | L'objectif a des données d'entrée et des résultats précis, le process se configure entièrement à l'avance. Sans information ambiguë à interpréter, la doc recommande un workflow, un segment ou une propriété calculée. Prévisible et reproductible : c'est ce qu'on peut **expliquer, reproduire et facturer**. |
| **Agent** (par défaut ou sur mesure) | Le process doit interpréter, résumer, classer ou noter une information ambiguë ou non structurée. On ne peut pas énumérer les étapes à l'avance. |
| **Workflow agentique** | Un agent doit tourner automatiquement, selon un calendrier ou après un changement de donnée : on **ajoute l'agent à un workflow**. |
| **Breeze Assistant** | Une personne lance et relit chaque demande. |

**Le réflexe** : par défaut, workflow. On passe à l'agent quand on constate qu'énumérer les étapes est impossible, pas parce que c'est plus impressionnant. Un livrable client se juge sur sa **reproductibilité**, et un agent qui adapte son chemin produit deux résultats différents sur deux cas voisins : une qualité en prospection, un défaut en facturation.

**Ils se composent** : le workflow tient la structure et le séquencement, l'agent traite l'étape qui demande du jugement. Pour lancer un agent depuis un workflow : sur un compte Starter, par une automatisation dans le panneau latéral ; sur Professional et Enterprise, par le constructeur de workflows de l'Agent Hub. Un agent qui n'a pas besoin de tourner seul se lance depuis la boîte de réception des agents, Breeze Assistant ou une carte d'enregistrement CRM.

## §2 Les agents prêts à l'emploi

**En avant sur la page d'accueil de l'Agent Hub** : AEO (visibilité dans les moteurs et chats IA) · **Data agent** (enrichir et maintenir la qualité des données du CRM) · **Prospecting agent** (approche personnalisée à l'échelle) · Deal progression · Customer agent.

**Dans l'aide de l'éditeur, par ailleurs** : Company research · Customer health · Deal loss, puis en bêta Knowledge base agent · Brand assistant · Closing · RFP · Revenue agent · Content agent. ⚠️ Les étiquettes « par défaut » et « bêta » ne sont pas cohérentes d'une page à l'autre (la page Company research parle d'un agent bêta) : lire l'état sur le portail, pas ici. Les agents qui demandent une souscription supérieure sont signalés dans l'aide : « Professional ou Enterprise requis pour certains agents ».

> 🎯 **Celui qui change les offres : le Prospecting Agent.** Il surveille des comptes, **source des contacts directement dans HubSpot** et lance des approches personnalisées selon des « plays ». Les cas d'usage annoncés par HubSpot sont ceux d'une agence : trouver des contacts dans les comptes qui montrent des signaux d'achat, **identifier le bon persona**, combler les trous de contacts sur les comptes existants.

**Sources de données pour le sourcing** (doc de l'agent, vérifiée le 2026-11-07) : Apollo, Surfe, ZoomInfo et Seamless. **Une seule source peut être connectée à la fois** (Sales > Prospecting Agent > Integrations). Une version antérieure de cette compétence ne citait que Seamless : c'est périmé.

### 🚧 Le sourcing de contacts est derrière une BÊTA : le vérifier AVANT de le vendre

L'opt-in s'appelle *« Prospecting Agent Gets Smarter: Buying Signals and Contact Sourcing »*. L'aide l'indique comme bêta, sans date de disponibilité générale, et un Super Admin peut y inscrire le compte. **Sans elle, l'agent ne travaille que sur les contacts déjà présents au CRM**, et toute promesse de « on trouvera les bonnes personnes » devient fausse.

→ **Contrôle obligatoire avant tout chiffrage ou toute promesse** : vérifier l'inscription à la bêta sur le portail concerné. C'est un état **par portail**, pas une capacité générale du produit. Ça modifie le périmètre fonctionnel d'un portail client : c'est une décision du responsable du compte, soumise au gate de consentement.

**Essai gratuit** : un accès de 14 jours existe (Sales > Prospecting Agent > « Join the new experience », puis publication d'un premier play). Pendant cette période l'agent ne consomme pas de crédits ; après 14 jours il s'éteint, et le rallumer ouvre la consommation de crédits. Il faut ne pas l'avoir déjà utilisé. ⚠️ Les conditions d'éligibilité divergent entre deux pages de l'aide (abonnement Starter ou plus sur l'une, Professional ou Enterprise avec siège et crédits sur l'autre) : lire l'écran du portail avant de promettre l'essai. Les actions qui consomment des crédits ne peuvent pas s'exécuter dans un sandbox.

## §3 La chaîne qui a de la valeur commerciale

C'est le motif à connaître, parce qu'il transforme une fonctionnalité isolée en système :

1. **Buyer Intent** identifie l'**entreprise** qui visite le site (par son IP). Il ne rend **aucun contact**.
2. **Le Prospecting Agent** trouve les **bonnes personnes** dans cette entreprise, selon le persona visé.
3. **L'agent de prospection** rédige et lance l'approche, contextualisée sur ce qui a été consulté.
4. Le commercial reçoit un lead avec un **nom** et un **motif**, au lieu d'un nom d'entreprise à débrouiller.

**Le maillon 1 vers 2 n'est que partiellement documenté** : l'aide liste bien l'intention des visiteurs et l'intention de recherche parmi les signaux d'achat agrégés sur une fiche société, mais rien ne dit que les sociétés Buyer Intent alimentent d'elles-mêmes l'enrôlement de l'agent. C'est la question à poser au portail (ou à tester à blanc, voir §5) avant de vendre la chaîne comme automatique. Voir `hubspot-buyer-intent` pour tout ce qui concerne l'étage 1.

⚠️ **Ne pas confondre avec un identifieur de VISITEURS** (type outil de dé-anonymisation). Un tel outil dit « **cette personne précise** était sur ton site » ; le Prospecting Agent dit « voici **le bon acheteur** dans cette entreprise ». Signaux différents, volumes très différents, et les deux se complètent plutôt qu'ils ne se remplacent.

## §4 L'agent builder : quatre sections, et une distinction qu'on rate

Créer un agent sur mesure se joue sur quatre blocs :

**Instructions** : le rôle, l'objectif, l'approche, le format de sortie attendu. C'est le prompt système de l'agent.

**Actions** : ce qu'il a le droit de faire, en trois onglets :
- **HubSpot** : `Get data` · `Generate` · `Take action`
- **Default** : `Browse the web` · lire et écrire les enregistrements du CRM
- **MCP** : connexion à des systèmes **externes** par le Model Context Protocol. C'est la porte de sortie hors de HubSpot, et souvent la brique qui débloque un cas d'usage qu'on croyait impossible en natif. La plupart des apps se connectent par OAuth. Chaque outil se règle en *Always allow*, *Ask permission* ou *Never allow* : ne donner que les outils dont l'agent a besoin.

**Knowledge** : le contexte de fond (brand kit, ICP, Knowledge Vaults, intégrations).

**Inputs** : la donnée sur laquelle il agit **à chaque exécution** (l'enregistrement CRM, une valeur saisie).

> 🔑 **La distinction que tout le monde rate : Knowledge est CONSTANT, Inputs CHANGE à chaque run.** Mettre dans Inputs ce qui devrait être dans Knowledge oblige à le redonner à chaque exécution, et l'agent perd son contexte dès qu'on l'automatise. L'inverse (figer en Knowledge ce qui varie) produit un agent qui répond toujours la même chose.

**Knowledge Vaults** (bêta dans l'aide) : jusqu'à **50** coffres, assignables à plusieurs agents (Agent Hub > Agents > Edit > Add knowledge, puis Publish). Formats : `.pdf` `.md` `.html` `.pptx` `.txt` (UTF-8 seulement) `.docx` `.xlsx` `.csv` `.json` `.xml`, et images `.jpeg` `.png` `.webp`. Taille : 50 Mo par fichier, 10 Mo par image. C'est là que vivent la doc produit, les argumentaires, les procédures internes.

**Déclenchement** : bouton `Test` / `Run` dans le builder, cartes d'enregistrement CRM, ou ajout de l'agent à un workflow (§1).

## §5 Ce que ça coûte, et l'ordre dans lequel le savoir

> 💰 **Tester ne consomme AUCUN crédit.** Une simulation ne prend aucune action CRM, ne modifie aucun enregistrement, et affiche dans son historique une estimation de crédits. Précaution de l'aide : un outil MCP configuré peut s'exécuter pendant un test, donc utiliser des données d'exemple. Toute conversation budgétaire qui précède un test à blanc est une conversation à l'aveugle.

- Depuis le **23 juillet 2026**, selon l'aide, tous les agents IA consomment des **crédits HubSpot**. Un agent sur mesure consomme quand il réfléchit, agit et génère du contenu ; le coût varie avec la complexité.
- **Plafonner** : par agent, un plafond mensuel d'exécutions (Agent Hub > Agents > Edit > menu à trois points > *Edit run limit*), avec une fourchette de consommation mensuelle estimée qui se met à jour. Une fois le plafond atteint, l'agent s'arrête.
- Pour le Prospecting Agent, les crédits partent quand l'agent **génère l'approche personnalisée d'un lead**, qu'il l'ait recommandé ou qu'on l'ait enrôlé à la main. Le montant ne figure pas dans l'aide : il se lit dans le catalogue produits et services de l'éditeur (lignes lues le 2026-11-07, section « AI Agents » : « Prospecting agent » / « Recommend outreach for one lead » / 100, sans étiquette bêta ; « Custom agents (Beta) » / « Use one action unit » / 1, le nombre d'unités dépendant du travail demandé ; « Data agent » / « Generate response to one prompt for one record » / 10). Un catalogue est versionné : le relire avant de chiffrer.
- Le nombre de contacts suggérés par jour se règle **play par play** (« Daily new contact suggestions limit ») ; l'aide ne donne aucun plafond général. D'anciens chiffres circulent (contacts enrôlés par jour, recherches par minute, emails par contact) : **non retrouvés dans l'aide actuelle, ne pas les citer**.
- **Les crédits se remettent à zéro chaque mois et ne se reportent pas.** À la limite, deux comportements selon le réglage de facturation : montée automatique vers un pack supérieur, ou dépassement facturé à l'usage par tranches de 10 crédits. Lequel est le défaut dépend de la date d'achat des packs (voir `hubspot-buyer-intent` §3). Ne jamais le supposer : le lire dans Compte et facturation.
- ⚠️ **Ne jamais citer un prix unitaire venant d'un blog** : ils divergent et vieillissent en semaines.

**Accès** : l'agent builder demande un abonnement **Starter, Professional ou Enterprise** (Marketing, Sales, Service, Data ou Content Hub ; Smart CRM et Revenue Hub en Professional ou Enterprise) et des crédits. Une version antérieure de cette compétence disait « Professional ou Enterprise » : périmé. Créer un agent exige les droits **Super Admin ou Agent Builder** ; un Super Admin doit aussi avoir activé les réglages d'IA générative du compte. Le Prospecting Agent est annoncé à partir de Starter, avec Super Admin ou la permission d'accès à la prospection ; le sourcing y ajoute l'opt-in du §2.

## §6 La méthode, dans l'ordre

1. **Nommer le résultat attendu**, pas l'outil. « Que doit-il se passer, pour qui ? » Beaucoup de demandes d'agent se règlent par un workflow.
2. **Vérifier la faisabilité sur LE portail**, pas sur le produit en général : niveau d'abonnement, bêtas actives, crédits disponibles. Une capacité existante mais non activée équivaut à une capacité absente.
3. **Trancher agent ou workflow** (§1), et le justifier en une phrase.
4. **Construire, puis TESTER** : c'est gratuit, et c'est là qu'on découvre le coût estimé et les sorties inattendues.
5. **Chiffrer avec les chiffres du test**, jamais avec une estimation. Poser un plafond d'exécutions avant publication.
6. **Capitaliser** : ce qu'on apprend sur le produit remonte dans cette compétence ou dans celle du sujet, pas dans un dossier propre à un client.

## §7 Garde-fous

- **Aucune activation sur un portail client sans validation explicite** (gate en tête de ce fichier). Un agent qui écrit dans le CRM ou envoie des emails est une action mutante, quel que soit son air inoffensif.
- **Ne pas promettre une capacité bêta** avant d'avoir vérifié l'opt-in sur le portail visé.
- **Ne pas présenter un agent comme un workflow** dans un livrable client : ce qui adapte ses étapes ne se garantit pas.
- **Un chiffre de blog n'est pas un chiffre.** Source éditeur (aide ou catalogue) ou test réel, sinon on marque « à confirmer ».
- **Les agents peuvent naviguer sur le web et écrire dans le CRM.** Passer en revue les actions accordées avant publication, comme on le ferait pour des droits d'accès.

## Compétences liées

`hubspot-buyer-intent` (l'étage 1 de la chaîne : identifier les entreprises) · `claude-breeze` (collaborer avec l'assistant Breeze du portail, et l'audit écran par écran) · `hubspot-crm` (le socle : règles, outils MCP, voies d'accès) · pour arbitrer quel cerveau fait le travail au moindre coût : `claude-ia-delegation`, dans le pack séparé `deleguer-entre-ia`.
