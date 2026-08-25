---
name: claude-ia-delegation
description: >-
  L'ORCHESTRATEUR d'arbitrage de tokens : au lieu que Claude fasse tout le travail lui-même, router chaque recherche / diagnostic / investigation vers le CERVEAU LE MOINS CHER qui sait la faire, puis garder Claude pour la valeur ajoutée et le local qu'il est seul à pouvoir exécuter. Compétence CHAPEAU (mince) qui DÉCIDE selon le contexte et DÉLÈGUE à une compétence plateforme — elle ne ré-implémente jamais la méthode d'une plateforme. Routage : contexte HubSpot → `claude-breeze` (Breeze gratuit + audit écran-par-écran) ; recherche générale offloadable → GPT / Gemini (crédits déjà payés) ; une autre session a déjà la connexion/le contexte → on lui envoie le travail ; seul Claude peut le faire (fichiers locaux, connexions, synthèse fine) → il le fait. À invoquer dès qu'une tâche de recherche/analyse pourrait être déléguée pour économiser les tokens, sur "délègue ça", "au lieu de tout faire toi-même", "économise mes tokens", "utilise Breeze / GPT / Gemini", "arbitrage de tokens", "fais bosser une autre plateforme / une autre session", "cerveau le moins cher", ou tout diagnostic/recherche où faire tout soi-même serait du gaspillage alors qu'une IA moins chère peut répondre.
---

# Skill — claude-ia-delegation (déléguer au cerveau le moins cher)

## §0 Le principe — arbitrage de tokens

Au lieu que Claude fasse **tout** le travail lui-même (cher en tokens), router chaque tâche vers **le cerveau le moins cher qui sait la faire** — les IA natives des plateformes (crédits gratuits/déjà payés), GPT/Gemini, ou une autre session déjà connectée — et garder Claude pour ce qu'il est **seul** à pouvoir faire : le local (fichiers, connexions) et la synthèse à forte valeur ajoutée.

But = **efficience token + coût** : exploiter les crédits qu'on paie déjà ailleurs, ne pas cramer les tokens Claude sur ce qu'une IA moins chère fait aussi bien.

## §1 Le décideur — choisir le cerveau (le moins cher d'abord)

> 🎯 **Argument optionnel — forcer la plateforme.** On peut préciser la plateforme en suffixe, comme le mode de caveman (`/caveman ultra`) : ex **`/claude-ia-delegation hubspot`** force la branche HubSpot. **Totalement optionnel.** L'utilisateur le précise, OU le contexte de la conversation le rend clair → on prend cette plateforme. Sinon → n'importe laquelle, on s'en fout, **on ne demande RIEN** (cf la règle plus bas).

Avant de se lancer dans une recherche/analyse, une question : **quel cerveau, le moins cher, peut la faire ?** Descendre l'échelle, s'arrêter au premier qui suffit :

| La tâche… | Cerveau | Comment |
|---|---|---|
| porte sur une plateforme avec une IA native + crédits (HubSpot…) | **l'IA de la plateforme** | via sa compétence plateforme (§2) |
| = recherche / raisonnement général offloadable | **GPT / Gemini** | crédits déjà payés (§2) |
| a besoin d'une connexion/contexte qu'une **autre session** a déjà (ex Chrome MCP mort ici mais vivant ailleurs) | **une autre session** | le canal inter-sessions de ton environnement, s'il en expose un |
| = local, connexions, synthèse fine, jugement | **Claude directement** | c'est la valeur ajoutée, on la garde |

**Si le bon cerveau n'est pas clair → trancher SEUL selon la situation. JAMAIS demander à l'utilisateur « sur quelle plateforme veux-tu que je travaille ? »** — on ouvre la session, on pose la question à l'agent de la plateforme, on récupère sa réponse, et on la ferme. Pas de temps perdu en questions. On ne délègue pas ce qui perdrait à l'être (données sensibles, jugement fin, décision produit) ; on ne fait pas soi-même ce qu'un cerveau gratuit fait aussi bien.

## §1bis L'ORDRE DES GESTES — collaborer d'abord, capturer en clôture (gravé 2026-07-28, vaut pour TOUTE la famille)

Le cerveau est choisi (§1). Reste **par où on commence** — et c'est là que ça a dérapé en réel, donc c'est écrit une fois ici pour toutes les branches :

1. **SE CONNECTER à la conversation EN COURS** — le bon projet, le bon fil, chez l'agent visé.
2. **LIRE LA FIN** — l'agent a déjà du contexte et **annonce très souvent la prochaine étape lui-même**. C'est ce qu'on vient chercher.
3. **TRAVAILLER AVEC LUI** — exécuter cette étape en collaborant, en plus de ce que l'utilisateur demande par ailleurs. C'est le métier de ces compétences.
4. **PUIS SEULEMENT** capturer / archiver / loger au registre.

**Pourquoi ça mérite une section** : la capture est le geste le plus *facile à écrire* dans un skill (un chemin, un bouton, un registre), donc il finit toujours par occuper le plus de place — et la place devient de l'autorité. Prouvé le 2026-07-28 sur `claude-breeze` : trois entrées se disputaient le démarrage (lecture d'archive · décideur de mode · capture) et **aucune ne nommait le premier geste** ; face à un écran montrant une conversation d'agent en cours qui disait *littéralement* quoi faire ensuite, la réponse a été de demander à l'utilisateur de copier-coller le contenu pour l'archiver. Le contenu affiché était une **instruction**, pas un artefact à ranger.

⚠️ **Le test, dès qu'un écran / export / document d'agent arrive** : *résultat à ranger, ou consigne à exécuter ?* Une consigne s'exécute — on l'archive après l'avoir faite, jamais à la place. Et un contenu qu'on peut aller chercher soi-même en poursuivant l'échange ne se fait jamais copier-coller par l'utilisateur.

**La seule exception, et elle est explicite** : l'utilisateur demande un **paquet précis** (« va chercher le zip », « installe le paquet ») — là, la récupération *est* la tâche. L'exception se reconnaît à ce qu'elle est **réclamée**, pas déduite.

## §1ter CE QUE LA SUPERVISION APPORTE — mesurer, jamais relire

Une fois le travail délégué, la tentation est de **relire le raisonnement** de la cible pour vérifier
qu'il tient. C'est le réflexe qui rend la délégation inutile : on paie deux fois le même
raisonnement, une fois chez elle, une fois chez soi — exactement ce que §0 cherche à éviter. Et ça
n'apporte presque rien, parce que ces cerveaux raisonnent bien.

**La supervision qui paie tient en deux gestes, et ils ont un point commun : ce ne sont pas des
raisonnements, ce sont des mesures.**

| Geste | Pourquoi c'est nous et pas elle |
|---|---|
| **Fournir les faits qu'elle ne peut pas atteindre** | elle n'a ni le disque, ni le dépôt, ni les logs. Elle ne peut pas ouvrir un fichier, lancer une commande, lire un commit. Tout ce qu'elle sait du terrain, elle le tient de ce qu'on lui a donné. |
| **Vérifier les chiffres qu'elle avance** | un chiffre qu'elle cite vient d'une source datée. Sur un dépôt vivant, il périme en heures. Le recompter coûte une commande ; le croire coûte une décision fausse. |

**Ce qu'on ne fait pas** : relire sa logique, reformuler ses conclusions, refaire son analyse « pour
être sûr ». Si sa conclusion dépend d'un fait, on mesure **le fait** — pas le chemin qui y mène.

Observé sur une session de pilotage réelle : les deux corrections qui ont servi étaient des mesures,
jamais des jugements — un garde de sécurité déclaré durci alors qu'il s'ouvre sur exception (visible
en trois lignes de code que la cible ne pouvait pas ouvrir), et un dimensionnement périmé par un
commit du jour même. Et l'inverse dans la même session : la seule « vérification » faite de mémoire
au lieu d'être mesurée était **fausse**, et la cible l'avait déjà intégrée avant qu'on la rattrape.
*Une supervision qui ne mesure pas ajoute du bruit, et parfois du faux.*

### Le corollaire qui économise le plus : lire et écrire par des canaux différents

Dans cette famille, le gaspillage le plus courant n'est pas le raisonnement — c'est **la lecture**.
Récupérer la réponse d'un agent en aspirant sa page entière ramène tout ce qui l'entoure : les
consignes épinglées, l'historique, l'interface. On paie des milliers de mots pour en extraire trois
phrases, **à chaque tour**.

D'où le partage, valable pour toute la famille :

- **Lire par le canal le plus étroit disponible** — celui qui rend *la dernière réponse*, pas la
  page. Quand la machine expose un tel canal (une application locale qui suit les sessions, une API,
  un export), il gagne toujours.
- **Écrire par le canal le plus fiable** — celui qui produit de vraies frappes. L'écriture est rare,
  visible, et une écriture ratée coûte bien plus cher qu'une lecture chère.

La mécanique concrète de ce partage appartient à chaque branche (§2), pas ici.

## §1quater 🖱️ UN FLUX DÉCROCHÉ SE REPREND AU PREMIER PLAN + CLIC DANS LA PAGE — recharger ne suffit pas (gravé 2026-08-11)

La règle vit ICI plutôt que dans une branche parce qu'elle ne décrit pas une plateforme : elle décrit **un client web qui a perdu son flux**. Toute déclinaison `claude-<cible>` pilotée par le navigateur la subit.

**Le symptôme, sous ses masques** : la réponse s'arrête en plein milieu · le fil paraît figé · un message envoyé ne produit aucun tour · « elle n'a pas terminé » depuis dix minutes. **Ni le serveur ni le modèle ne sont en cause.**

**Le geste** : ① onglet **au premier plan** · ② **vrai clic DANS la page**, dans la conversation. Le flux reprend.

⛔ **Ce qui ne marche pas** : recharger l'adresse · recycler l'onglet · attendre · renvoyer un message. Recharger **relit** ce que le serveur a déjà — ça ne fait jamais **reprendre** un flux décroché.

⚠️ **Pourquoi ça se re-découvre à chaque fois** : rien n'échoue. Pas d'erreur, pas de bandeau, un DOM cohérent. Une réponse tronquée ressemble à une réponse finie, un fil figé ressemble à une génération lente — donc on attend, puis on accuse le canal, puis on refait faire le travail. **Le tell décidable** : ça dure et **rien n'avance d'un caractère** entre deux lectures espacées.

**La mécanique reste chez la branche** (comment fronter, comment cliquer, quel témoin). Le chapeau porte la **règle**, pas le geste technique (§3).

## §2 Les branches (routage — le chapeau POINTE, il ne fait pas)

- **HubSpot** → **`claude-breeze`** (projet Clients) : mode Breeze (IA native, gratuit) pour un diagnostic, mode navigation écran-par-écran pour une fonctionnalité sans API. La méthode HubSpot vit là-bas, pas ici.
- **Recherche générale** → **GPT / Gemini** : principe posé, mécanique à câbler quand on l'utilise vraiment (leur UI via Chrome MCP, ou un MCP dédié si connecté). Ne pas gonfler ce skill avec cette mécanique avant de l'avoir.
- **Autre session** → router le travail à la session qui a la connexion/le contexte (`send_message`), plutôt que de tout refaire ici.
- **Local / valeur ajoutée** → Claude exécute directement (le reste de ses compétences).

> 📡 **LE CANAL DE LECTURE, commun à TOUTES les branches.** Les branches ci-dessus disent *à qui* on parle ; il reste à régler *par où on écoute*. C'est la mécanique concrète du corollaire §1ter : dès que la machine expose un canal étroit — une application locale qui suit les sessions IA, une API, un export —, on lui demande **la liste des sessions, leur état, et la dernière réponse seule** au lieu d'aspirer la page. L'écart se compte en ordre de grandeur, et surtout **l'attente devient gratuite** : elle se passe dans l'outil, pas dans la boucle de l'agent, donc on ne paie plus un regard toutes les dix secondes.
> ⚠️ **Lecture seule.** Écrire reste le geste de la branche concernée, avec son consentement — un capteur qui écrirait changerait de nature.
> ⚠️ Un tel capteur dépend d'un outil local : s'il ne tourne pas, il doit **le dire** au lieu de rendre une liste vide. C'est toute la différence entre « il n'y a rien » et « je ne vois rien », et c'est la seule chose à exiger d'un canal de lecture.

## §3 Garde-fous — rester MINCE

- **Ce skill ROUTE, il ne ré-implémente pas.** La méthode de chaque plateforme vit dans SA compétence (ex `claude-breeze`). Si ce fichier se met à décrire *comment* parler à une plateforme, c'est qu'une branche déborde → la sortir dans une compétence plateforme.
- **Une branche non câblée reste un principe d'une ligne** (GPT/Gemini aujourd'hui) — pas d'abstraction sur du vide, elle grossit le jour où on la branche pour de vrai.
- **La clôture appartient à la compétence plateforme** : c'est elle qui loge son travail dans ton registre local des projets IA, pas l'orchestrateur.

## §4 Étendre — ajouter une plateforme (convention `claude-<cible>`)

**Nommage des déclinaisons — `claude-<cible>`** : une compétence plateforme de cette famille se nomme **`claude-<cible>`** = « Claude délègue vers <cible> ». Ex **`claude-breeze`** (HubSpot Breeze). Demain `claude-gpt`, `claude-gemini`… Le **nom montre la délégation** ; la **méthode propre** de chaque cible (comment on la pilote, ses capacités ET ses limites) se décrit **dans SA compétence, jamais ici** — le chapeau reste mince.

Nouvelle plateforme avec une IA / des crédits → (1) créer une **compétence plateforme `claude-<cible>`** (via `anthropic-skills:skill-creator`), (2) ajouter **une branche** dans le tableau §1 + §2.

**Ce chapeau AMÉLIORE aussi ses déclinaisons** — son but n'est pas que de router, c'est de rendre la collaboration Claude↔IA-cible fluide dans le temps : quand une déclinaison gagne une capacité ou bute sur une limite (ex `claude-breeze` rate les chiffres exacts → on lit soi-même, Breeze raisonne), on l'affine dans **SA** compétence, et on tient ce §4 à jour de la famille.

## Skills liés

`claude-breeze` (branche HubSpot — Breeze + audit écran-par-écran), livrée dans ce pack. Les autres branches de la famille `claude-<cible>` et le registre des projets IA sont propres à ton installation : ce chapeau route vers elles quand elles existent, et ne suppose jamais leur présence.
