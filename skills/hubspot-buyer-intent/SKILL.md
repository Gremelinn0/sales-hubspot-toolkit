---
name: hubspot-buyer-intent
description: >-
  Comprendre, auditer et ACTIVER HubSpot Buyer Intent (identification des sociétés qui visitent le site) sans se tromper sur ce que ça coûte ni sur ce que ça fait vraiment. Porte les faits qui ne se devinent pas : l'auto-ajout au CRM consomme des CRÉDITS et n'est PAS rétroactif par défaut (il ne capte que les sociétés entrant APRÈS activation, un bouton Backfill existe pour les autres, au prix de crédits), les critères d'intention se définissent au niveau du COMPTE et pas par vue sauvegardée, les destinations sont des cases cumulables, les plafonds de crédits sont à régler à la main. Couvre la lecture des chiffres (TAM, Showing Intent, Captured in CRM), le choix entre les deux automations et la liste d'exclusions. Deux faits qui font économiser : les crédits se remettent à zéro chaque mois sans report, et ce qui se passe à la limite dépend du réglage de facturation ; et une grande part du « besoin d'enrichissement » est un problème de RANGEMENT, pas de crédits, car la donnée est déjà là, posée sur les transactions, invisible pour l'outil. À invoquer sur "buyer intent", "intent signals", "sociétés qui visitent le site", "visiteurs anonymes identifiés", "target market HubSpot", "visitor intent criteria", "auto-add au CRM", "activer une vue Buyer Intent", "combien ça coûte en crédits HubSpot", "research intent", "on capte des visiteurs mais rien ne remonte au CRM", "acheter des crédits", "ma base est vide il faut enrichir", ou dès qu'on s'apprête à activer une automation sur une saved view.
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

# Skill : HubSpot Buyer Intent (comprendre, auditer, activer)

⚠️ **Tout ce qui suit a une date : vérifié le 2026-11-07** sur `knowledge.hubspot.com` et sur le catalogue produits et services de l'éditeur. Avant de reprendre un chiffre dans un livrable client, relire la source : l'aide ne chiffre pas les crédits et les pages de l'éditeur se contredisent parfois (signalé là où c'est le cas).

## §0 Ce que la fonctionnalité fait, en une phrase

Buyer Intent rapproche les **IP des visiteurs du site** de sociétés connues, puis les filtre par **fit** (le secteur, la taille : les *Target Markets*) et par **intention** (les pages vues : les *Visitor Intent Criteria*). Le résultat s'explore dans des **saved views**, et des **automations** peuvent faire remonter ces sociétés dans le CRM.

**La confusion à éviter dès le départ** : la fonctionnalité peut être **parfaitement configurée et ne rien produire**. Configuration ≠ usage. Le socle (critères + marchés) vit au niveau du compte ; ce qui le rend utile (les vues qui le branchent, les automations qui le déclenchent) vit ailleurs et est souvent vide. C'est le mode d'échec n°1, et il ne se voit sur aucun écran isolément.

## §1 Les 5 écrans et ce qu'ils portent vraiment

| Écran | Ce qu'on y trouve | Piège |
|---|---|---|
| **Overview** | vue d'ensemble, pénétration de marché | agrège tout, ne dit rien sur ce qui est branché |
| **Visitors** | les sociétés détectées + **les saved views** + les automations **par vue** | la vue par défaut n'applique **aucun** filtre sectoriel : voir des sociétés hors cible n'est pas un bug |
| **Research** | sociétés recherchant des **topics** (hors site, données tierces) | indépendant du trafic du site ; souvent 1 seul topic générique, largement sous-exploité (jusqu'à 20 topics permis) |
| **Signals** | les signaux d'intention configurés | |
| **Configuration** | **TAM, Target Markets, Visitor Intent Criteria, automations configurées, limites de crédits, digests, exclusions, code de tracking** | c'est **le seul écran qui dit la vérité globale** : « Automation isn't set up for any saved views » y est affiché noir sur blanc |

**Réflexe d'audit** : commencer par **Configuration**, pas par Visitors. Visitors montre du volume qui rassure ; Configuration montre ce qui est réellement câblé.

## §2 Compte vs vue : la distinction qui explique la moitié des incohérences

- Les **Visitor Intent Criteria** se créent dans l'onglet Configuration, au niveau du compte (une liste de chemins de page avec seuils visites, visiteurs, récence, pays), jusqu'à **10** critères. Ils ne sont **pas** propres à une vue.
- Une **saved view** peut *sélectionner* un critère d'intention dans son champ « Choose an intent criteria », et **ce champ est très souvent laissé vide**.
- Conséquence directe, et elle trompe tout le monde : une fiche société peut afficher un badge **Visitor Intent** alors que la vue qui l'affiche n'a **aucun** critère branché. Le badge vient du **matching compte-large**, pas du filtre de la vue. *(Constat d'interface, non décrit tel quel dans l'aide : à re-contrôler sur le portail.)*

→ Voir un badge ne prouve donc **pas** que la vue filtre là-dessus. Pour le savoir, ouvrir la vue en édition et regarder le champ. Un audit qui conclut depuis les badges conclut faux.

Même logique côté fit : une vue peut être sur **« Any target market »** (donc aucun filtre sectoriel) tout en affichant des badges *Target Market* sur certaines lignes.

⚠️ **Piège aggravant : rempli et vide rendent la même chose à l'écran.** Le groupe de critères peut s'appeler *« Intent Criteria »*, soit **exactement le texte du placeholder gris** du champ. « Aucun critère sélectionné » et « le critère nommé Intent Criteria est sélectionné » sont alors **indistinguables à l'œil**. Il faut **dérouler la liste**, jamais lire l'état affiché : c'est le cas rare où une capture d'écran ne peut pas servir de preuve.

## §3 💸 LE COÛT : la partie qu'on ne devine pas et qui engage l'argent du client

Les automations d'une saved view **consomment des crédits HubSpot** (l'interface l'annonce par `USES HUBSPOT CREDITS`, le détail n'apparaît que dans le dialogue). **L'aide n'indique pas les montants** et renvoie au catalogue produits et services de l'éditeur. Relevé dans ce catalogue le 2026-11-07, section « Intent, Powered by Data Agent ». Le catalogue étiquette bêta deux lignes sur trois :

| Automation | Ligne exacte du catalogue | Coût | Ce qu'elle fait |
|---|---|---|---|
| **Add new companies** | « Intent (Beta) » / « Create one company record from market segments » | **10 crédits**, **une seule fois** | crée la société dans le CRM |
| **Track intent signals** | « Intent » (sans étiquette bêta) / « Enable intent signals to create company and/or monitor company for one month » | **10 crédits** par société et par mois de suivi, donc **récurrent** | suit les signaux d'intention ; ajouter et suivre dans la même période de facturation ne se facture qu'une fois (au tarif du suivi) |
| **Signal personnalisé** | « Intent (Beta) » / « Monitor one company for one custom signal for one month » | **50 crédits** par société, par signal et par mois | suivi d'un signal défini à la main |

Gratuit selon l'aide : consulter et filtrer les vues Visitors et Research, enregistrer une vue, **ajouter une société à la main par recherche**, exclure des sociétés ; le trafic de robots ne consomme rien. ⚠️ Deux pages de l'aide divergent : l'une dit que le suivi automatique se re-facture chaque mois, l'autre que les crédits servent à l'ajout « mais pas au suivi automatique ». Le catalogue et le dialogue du portail tranchent : **lire le dialogue avant de dire oui**.

**L'arbitrage** : pour seulement **capter** les sociétés, `Add` coûte moins cher (une fois). Pour le **suivi continu des signaux**, `Track` couvre aussi l'ajout dans la même période. À besoin de suivi établi, `Track` est le bon choix, pas les deux. **Activer les deux sans y penser, c'est payer pour un ajout déjà couvert.**

**Le budget se lit à l'écran** (dialogue d'automation : le nombre de crédits mensuels du portail, et Configuration → crédits Buyer Intent → ce qui a été consommé ce mois-ci). Ne jamais annoncer un budget de mémoire : il dépend du plan et des packs du portail.

**Remise à zéro mensuelle, pas de report** (aide « Manage HubSpot Credits », vérifiée le 2026-11-07). Les crédits se remettent à zéro chaque mois, alignés sur la date de début de la période d'usage, et ceux qui restent **expirent**. À la limite :
- sans pack acheté, les fonctions à l'usage **se mettent en pause** jusqu'à la remise à zéro ou l'achat d'un pack ; côté Buyer Intent, ce qui est déjà détecté reste consultable, mais sans suivi on ne reçoit plus de nouveaux signaux ;
- avec des packs achetés, soit la **montée automatique** vers un pack supérieur pour le reste du contrat, soit le **paiement à l'usage** (facturé chaque mois à terme échu, par tranches de 10 crédits arrondies à l'inférieur, sur une facture séparée, la limite revenant à son niveau initial à la remise à zéro) ;
- **le défaut dépend de la date d'achat** des packs : montée automatique avant le 16 septembre 2026, paiement à l'usage à partir de cette date. Un portail ancien et un portail récent ne se comportent donc pas pareil. Lire le réglage dans Compte et facturation, jamais le supposer ;
- une **limite de dépense** du compte se fixe automatiquement à 50 % au-dessus du total mensuel de crédits après un achat de packs, avec des alertes aux Super Admins et administrateurs de facturation à 75, 85 et 90 %.

**Et la limite des 20 sociétés par vue n'est pas qu'une affaire de plan.** Doc HubSpot : *« To view more than 20 companies per view, you must have HubSpot credits »*, avec un abonnement Starter, Professional ou Enterprise. Un portail sans l'un ou l'autre voit 20 lignes, quel que soit le volume réel : un plafond d'affichage qu'on prend facilement pour un plafond de détection.

**⚠️ Les plafonds de crédits se règlent à la main.** Configuration → *Buyer intent credit limits* → *Edit limits*, avec un interrupteur pour *Net new company adding* et un pour *Intent signal tracking*. L'aide ne donne pas de valeur par défaut ; sur les portails observés, les deux compteurs affichaient « No limit set » (à re-contrôler sur le portail concerné). Avant d'activer une automation sur un compte client, **regarder le rythme réel d'entrée dans la vue** et le comparer au budget. Un plafond atteint met l'action en pause. Poser un plafond modifie un réglage **existant au niveau du compte** : donc ça se valide, ça ne se décide pas seul.

## §4 ⏳ PAS RÉTROACTIF PAR DÉFAUT : le malentendu qui fait promettre l'inverse de ce qui se passe

Documentation HubSpot, mot pour mot :

> *« auto-add will only add companies that enter your saved views after enabling the auto-add. It will not add all existing companies in your saved views. »*

**Donc** : activer l'auto-ajout sur une vue qui contient déjà N sociétés hors CRM **n'en ajoute aucune**. L'écart existant reste tel quel ; l'automation empêche seulement qu'il **continue de se creuser**.

C'est la phrase à dire au client, parce que l'attente naturelle est exactement l'inverse : « on active, donc les sociétés remontent ». Non : **on active, donc les prochaines remontent.**

**Rattrapage : un bouton existe.** L'aide décrit une option **Backfill**, en bas du panneau latéral de l'automation, qui ajoute au CRM, aux segments ou aux workflows les sociétés déjà présentes dans la vue. Elle consomme les mêmes crédits ; si le solde ne suffit pas, le portail propose d'acheter des crédits ou de **contourner la limite pour ce rattrapage seul**. Une version antérieure de cette compétence disait qu'il n'y avait pas de rattrapage possible : périmé. Un backfill est une dépense ponctuelle et un lot d'écritures : chiffre annoncé avant le « oui » (nombre de sociétés × coût unitaire), jamais décidé en passant.

## §5 Activer une automation : la mécanique exacte, et ses deux pièges d'interface

Deux chemins mènent au même dialogue : depuis **Visitors** (les cartes *Automations* du panneau de gauche, sur la vue ouverte) ou depuis **Configuration → Set up automation for saved view**.

**Piège 1 : les cartes ne sont pas des interrupteurs.** Sur le panneau de gauche, « Add new companies » et « Track intent signals » **ressemblent** à des toggles. Cliquer **ouvre un dialogue de configuration** ; rien n'est activé tant qu'on n'a pas fait *Save automation*. Corollaire rassurant : un clic exploratoire ne déclenche rien.

**Piège 2 : les destinations sont des CASES À COCHER, pas des boutons radio.** *CRM* · *Static segment* · *Workflow* se **cumulent**. Cliquer sur une seconde destination **n'annule pas** la première : on se retrouve avec les deux cochées, et si *Static segment* est cochée sans segment sélectionné, la configuration est incohérente. → **Vérifier l'état des trois cases avant d'enregistrer**, et décocher explicitement ce qu'on ne veut pas.

**Note sur *Static segment*** : il exige de **sélectionner un segment existant**, il n'en crée pas. Le choisir implique donc d'avoir créé un segment au préalable, et, quand les listes d'un portail sont **dynamiques par défaut**, un segment *statique* est une exception qui se valide, pas un détail d'implémentation.

**Permissions** : créer ou modifier des vues demande la permission Buyer Intent ; ajouter des sociétés demande Super Admin ou la permission d'enrichir des enregistrements.

**Preuve d'activation : ne jamais se contenter de l'écran du clic.** Après *Save*, aller sur **Configuration** et vérifier que *Configured Saved Views* est passé de 0 à 1 et que la vue apparaît avec son badge. C'est un **écran différent de celui où on a agi** ; c'est ce qui en fait une preuve. (Motif général : un create qui répond OK ne prouve pas l'état. Re-lire ailleurs.)

## §6 Lire les chiffres sans se faire avoir

**Les trois nombres qui comptent**, sur Configuration : **TAM** (l'univers adressable, énorme et peu actionnable) · **Showing Intent** (sociétés qui matchent un critère d'intention) · **Captured in CRM**.

**L'écart Showing Intent → Captured in CRM est la métrique actionnable.** S'il est stable pendant que *Showing Intent* monte, la détection marche et l'exploitation ne suit pas : c'est exactement ce qu'une automation corrige.

**⚠️ Le chiffre périmé qui a l'air valide** : au changement de saved view, le **titre se met à jour immédiatement** pendant que la liste et le compteur affichent encore **les données de la vue précédente, quelques secondes durant**. Ce n'est pas le « -- » de chargement qu'on repère à l'œil : c'est un **nombre plausible sous le bon titre**. → **Attendre, puis relire une seconde fois.** Un chiffre pris sur une seule lecture après changement d'écran est une hypothèse, pas un constat.

**Et un « 0 » se prouve** : sur une vue vide, re-vérifier après attente. Certaines vues affichent d'abord le total non filtré du compte avant de se résoudre au vrai zéro.

**🧠 Un chiffre faux EMBALLÉ DANS UN BON RAISONNEMENT passe tous les contrôles.** Un chiffre nu se vérifie par réflexe ; un chiffre qui vient d'**expliquer** quelque chose a l'air déjà validé. La qualité du raisonnement fait présumer celle de la donnée, et c'est faux : les deux sont indépendantes.

> Cas type : « cette vue est déjà entièrement au CRM, donc l'auto-ajout n'a aucune valeur, c'est de la surveillance de comptes existants, pas de l'acquisition ». La relecture stratégique était juste et utile ; **elle a fait passer le chiffre sans contrôle**. Trois sources concordantes (comptage par badge, comptage textuel brut, compteur natif *Captured in CRM*) montraient qu'une part importante de la vue était en réalité **nette-nouvelle** : l'inverse de la conclusion.

⚠️ **Et attention à qui a produit le chiffre : le réflexe n'est pas le même.** Dans ce cas, l'IA du portail **n'avait rien relevé** : le chiffre lui avait été **fourni** dans la question, généralisé depuis les premières lignes visibles d'une capture. Elle a raisonné correctement sur une donnée fausse. C'est le **contrat de la collaboration** qui a été rompu, pas sa fiabilité : **les chiffres sont NOTRE part, le raisonnement est la sienne** (`claude-breeze` §2). Lui donner un chiffre faux ne produit pas une erreur visible : ça produit une erreur **blanchie**, qui revient habillée en analyse d'expert.

→ **Deux réflexes, pas un.** En **amont** : ce qu'on apporte à l'agent, on l'a **compté**, jamais généralisé depuis un échantillon visible. En **aval** : quand un chiffre arrive avec la conclusion qui va avec, vérifier le chiffre **en premier**, précisément parce que la conclusion est séduisante. Compter ligne par ligne, et recouper avec un second écran.

**🎯 Un volume ne voyage JAMAIS sans son périmètre.** Le chiffre d'une saved view est le chiffre de **cette vue** : un filtre étroit sur une page. Il ne dit rien du trafic du site, ni de ce que verrait un outil tiers qui regarde tout. Le piège est retors parce que **rien dans le chiffre ne signale son périmètre** : il a l'air général, il est mesuré, il est juste. Réutilisé pour dimensionner autre chose, il devient une recommandation fausse, et d'autant plus dangereuse qu'elle s'appuie sur une vraie mesure.

> Cas type : un volume mensuel exact pour une vue pilote sur une seule page servait à conclure qu'un outil de prospection ne se justifiait pas. Cet outil travaillait sur **tout le trafic** du site, soit un volume d'un ordre de grandeur supérieur. La conclusion aurait fait rejeter le bon outil.

→ **Tout volume écrit dans un livrable porte son périmètre dans la même phrase.** Et quand deux outils se comparent, vérifier d'abord qu'ils regardent bien la même population : c'est souvent faux.

## §7 Effet de bord : l'activation crée une DEUXIÈME source d'enregistrements

Si le compte client mesure son volume d'affaires en s'appuyant sur le fait que **100 % des enregistrements viennent d'une seule source** (une intégration e-commerce, un import), activer l'auto-ajout **casse cette hypothèse** : des enregistrements naissent désormais aussi de Buyer Intent.

Sans précaution, une mesure postérieure lit ces nouveaux enregistrements comme une **reprise d'activité qui n'a pas eu lieu**.

→ **Avant d'activer** : prévenir qui porte la mesure, **noter la date de bascule**, et s'assurer que le relevé **ventile par source** (`hs_object_source`) au lieu de comparer des totaux. La bascule se documente alors dans la série au lieu de la corrompre en silence.

## §8 Le fit sectoriel ne distingue pas un client d'un concurrent

Une vue peut afficher **100 % de sociétés dans les secteurs cibles** et contenir quand même des **fournisseurs, distributeurs ou concurrents** du client : ils appartiennent au même secteur, par construction. Le filtre sectoriel ne peut pas les séparer.

→ Regarder la **nature** des sociétés, pas seulement leur secteur, avant de brancher un auto-ajout. L'outil prévu pour ça est la **liste d'exclusions** (Configuration → *Exclusions*, jusqu'à **100** sociétés ou domaines), qui les retire des vues, automations et digests d'un coup, sans consommer de crédits.

## §9 Notifications : le digest engage des personnes, pas seulement le portail

Configurer un **email digest** (Configuration → *Email Digests*, ou la carte *Notifications* d'une vue) envoie un récapitulatif **récurrent** (quotidien, hebdomadaire ou mensuel) **à des destinataires**.

C'est le seul réglage de cette fonctionnalité qui **sort du portail** : il crée un envoi répété à des personnes réelles. Le choix des destinataires et de la fréquence est une **décision du responsable du compte**, jamais une initiative technique, même quand le reste de l'activation a été validé.

## §10 Audit d'un setup existant : l'ordre qui évite les fausses conclusions

1. **Configuration d'abord** : critères d'intention (combien, quels chemins, quels seuils), Target Markets (combien, quels volumes), automations configurées, digests, limites de crédits, exclusions, code de tracking.
2. **Puis les saved views, une par une** : pour chacune, le filtre réellement appliqué (target market précis ou « Any » ?), le critère d'intention (branché ou vide ?), le volume, et un échantillon de sociétés pour juger le fit réel.
3. **Classer chaque constat** : CONFIRMÉ (vu directement) · À VÉRIFIER · INCOHÉRENT (deux écrans se contredisent) · À IMPLÉMENTER.
4. **Ne jamais conclure depuis un seul écran** : la configuration globale ment régulièrement sur l'usage réel.

La **méthode de navigation écran par écran** (rôles, boucle d'hypothèses, format du journal) n'est pas redécrite ici : elle vit dans `claude-breeze` §3, qui est agnostique de la fonctionnalité. Ce skill-ci porte **ce qu'il faut savoir de Buyer Intent** ; celui-là porte **comment traverser des écrans sans conclure trop vite**.

## §10bis Buyer Intent donne l'ENTREPRISE, jamais la PERSONNE, et ce n'est pas une impasse

C'est la limite qu'on découvre à l'usage : le commercial reçoit *« telle entreprise est venue sur le site »* et doit trouver lui-même qui appeler. Deux outils HubSpot voisins sont régulièrement confondus sur cette question :

| Outil | Ce qu'il fait | Ce qu'il ne fait pas |
|---|---|---|
| **Enrichissement de données** (ex Breeze Intelligence) | complète une fiche **existante** : un contact doit avoir un email professionnel (les adresses personnelles type Gmail ne sont pas enrichies), une société un domaine | **ne découvre aucune personne** : sans email pro, il ne peut rien. Les propriétés enrichies par défaut sont les propriétés standard ; des propriétés d'enrichissement personnalisées se configurent à part (réglages d'enrichissement) |
| **Prospecting Agent** (`Agent Hub → Prospecting Agent`) | **source des contacts** dans des comptes, via une source de données externe connectée (Apollo, Surfe, ZoomInfo ou Seamless, une seule à la fois), avec un objectif de persona | dépend d'une **bêta d'opt-in** pour le sourcing ; sans elle, il ne travaille que sur les contacts déjà au CRM |

**Le piège** : conclure « on ne peut pas trouver les personas » après avoir regardé **le seul** outil d'enrichissement. La démonstration est juste pour cet outil, et la conclusion déborde : elle ferme un sujet qui a une réponse ailleurs dans le même portail.

⚠️ **Le sourcing consomme des crédits quand l'agent génère l'approche personnalisée d'un lead**, pas à la recherche. Le montant ne figure pas dans l'aide : le lire au catalogue produits et services (voir `hubspot-agent-hub` §5), jamais sur un article de blog. Les anciens plafonds de volume qui circulent (contacts enrôlés par jour, recherches par minute, emails par contact sur 90 jours) **n'ont pas été retrouvés dans l'aide actuelle** : ne pas les citer. Ce qui est documenté : un réglage « Daily new contact suggestions limit » **play par play**.

💡 **Regarder si un essai gratuit est offert avant de chiffrer quoi que ce soit** : l'écran d'onboarding du Prospecting Agent peut proposer 14 jours sans consommation de crédits, qui répondent aux questions ouvertes à coût nul (conditions : `hubspot-agent-hub` §2). Et **rejoindre une bêta modifie le périmètre fonctionnel d'un portail client** : gate de consentement, jamais une initiative technique.

## §10ter Une grande partie du « besoin d'enrichissement » est un problème de RANGEMENT, pas de crédits

Avant de chiffrer un abonnement ou des crédits d'enrichissement, **mesurer ce que la base contient déjà**. La donnée manquante est souvent **présente dans le compte** mais recopiée sur les **transactions**, et absente des **champs standards du contact** : donc invisible pour l'enrichissement, qui ne lit que ce qu'on lui a mappé (§10bis).

> Cas type, mesuré sur un portail e-commerce : le **pays** et le **téléphone** étaient remplis sur des dizaines de milliers de transactions et sur une poignée de contacts seulement. Aucun crédit n'aurait comblé cet écart : il se comble par une **recopie interne**.

**Pourquoi ça se rate systématiquement** : l'outil d'enrichissement rend un taux de couverture **sur les champs qu'il lit**. Ce taux est juste, et il décrit une base qui a l'air vide alors qu'elle est pleine ailleurs. Le chiffre ne signale pas où il a regardé : même famille que « un volume ne voyage jamais sans son périmètre » (§6).

→ **L'ordre qui évite de vendre des crédits pour rien** : mesurer le remplissage côté contacts **et** côté transactions · rapatrier ce qui existe déjà · **puis seulement** chiffrer le volume qui reste.

## §11 Garde-fous

- **Lecture seule par défaut.** Toute activation touche un système de production et **consomme le budget du client** : elle passe par le gate de consentement en tête de ce fichier, avec le coût annoncé **avant** le « oui ».
- **Annoncer le coût en clair** : nombre de crédits par société, rythme d'entrée observé, part du budget mensuel. « Ça consomme des crédits » n'est pas une information exploitable ; « environ <N> crédits par mois sur <budget du portail>, soit <part> % » en est une.
- **Ne pas promettre de rattrapage gratuit** : §4. Ce qui est déjà dans la vue ne remonte pas tout seul ; le Backfill existe mais se paie en crédits et se valide.
- **Toute activation se trace** dans le journal d'actions du client : ce qui a été activé, avec quelle destination, ce qui a été délibérément laissé OFF, et pourquoi.

## Compétences liées

**`hubspot-agent-hub` : l'étage du dessus, et la suite naturelle de ce skill.** Buyer Intent identifie une **entreprise** et ne rend **aucun contact** ; le Prospecting Agent trouve ensuite les **bonnes personnes** dedans, selon le persona visé. Dès qu'on se demande *« et maintenant, qui j'appelle chez eux ? »*, la réponse n'est plus ici.
> ⚠️ Deux réserves à porter avec le renvoi : le maillon entre les deux n'est que partiellement documenté (l'intention des visiteurs est bien listée parmi les signaux d'achat d'une société, mais rien ne dit qu'elle alimente d'elle-même l'enrôlement de l'agent), et le sourcing de contacts est derrière un **opt-in bêta** : sans lui, l'agent ne touche que les contacts déjà au CRM et la chaîne s'arrête net.

`hubspot-crm` (le skill central HubSpot : table de décision Breeze / MCP / navigateur) · `claude-breeze` (la méthode d'audit écran par écran, et la délégation à l'IA native du portail) · `hubspot-segments-audit` et `hubspot-marketing-segments` (les listes et segments, y compris le segment statique qu'une destination d'automation peut réclamer) · `crm-investigation-output` (mise en forme d'un audit en livrable client).
