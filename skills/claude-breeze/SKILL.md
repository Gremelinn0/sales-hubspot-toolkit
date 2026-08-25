---
name: claude-breeze
description: >-
  COLLABORER AVEC BREEZE, l'agent IA natif de HubSpot, puis investiguer / comprendre / auditer une
  question HubSpot AU MOINDRE COÛT de tokens Claude. Le PREMIER geste est toujours le même — se
  connecter à la conversation Breeze EN COURS, lire ses derniers messages, et continuer le travail
  AVEC l'agent ; la récupération de fichiers, la capture et le rangement sont des gestes de CLÔTURE,
  jamais d'ouverture. 2 modes choisis selon la situation : (1) MODE BREEZE — poser la question à l'IA
  native de HubSpot (tokens gratuits) pour tout diagnostic / analyse / raisonnement sur la data du
  portail ; (2) MODE NAVIGATION ASSISTÉE — auditer écran par écran une fonctionnalité dont la vérité
  est éparpillée sans API de dump (Buyer Intent, Lead Scoring, Permissions, Pipelines), en classant
  CONFIRMÉ / À VÉRIFIER / INCOHÉRENT / À IMPLÉMENTER — et jamais conclure depuis un seul écran. À
  invoquer sur "breeze", "demande à breeze", "économise les tokens hubspot", "fais bosser breeze",
  "pourquoi ce workflow / contact / donnée HubSpot", "audit guidé", "audit multi-écrans", "fais le
  tour de X dans HubSpot", "audit Buyer Intent / Lead Scoring / permissions / pipelines", ou toute
  investigation HubSpot où lire un seul écran ou tout faire soi-même serait une fausse conclusion ou
  du gaspillage de tokens.
---

## ⛔ GATE CONSENTEMENT — avant toute action qui MODIFIE le portail

**Lire, chercher, analyser : libre.** **Créer, modifier ou supprimer** quoi que ce soit dans le
système d'un client : **jamais sans un « oui » explicite, donné dans le fil, avant d'agir.**

**Périmètre** — contacts, transactions, sociétés, propriétés, listes, workflows, automatisations,
séquences, templates, emails, et l'équivalent dans tout outil connecté (Notion, Make, Drive…).

**Le geste, avant un LOT d'écritures :**

```
Action prévue : [quoi]
Cible        : [portail / objet]
Impact       : [créer / modifier / supprimer N éléments]
Confirme ? (oui / non)
```

Attendre le « oui ». **Il couvre ensuite tout le lot annoncé** — on n'interrompt pas objet par objet.
On redemande uniquement si on **sort du périmètre annoncé**, ou si on découvre un **irréversible non
prévu**.

**Pas d'exception « petit changement » ou « facile à annuler ».** Et quand on te demande de modifier
X, tu modifies X — pas une refonte à ta façon. Désaccord sur l'approche → une question courte, jamais
un pivot décidé seul.

**Pourquoi c'est écrit ici en toutes lettres, et pas en renvoi** : un CRM client, ce sont des données
de production, souvent irréversibles, et la responsabilité est vis-à-vis du **client final**. Un
garde-fou qui pointe vers un fichier que tu n'as pas installé n'est plus qu'une intention.

# Skill — HubSpot Breeze & Audit (investiguer au moindre coût)

## §0 Le principe — au moindre coût de tokens Claude

Répondre à une question HubSpot en **déléguant au cerveau le moins cher qui sait le faire**, avant de le faire soi-même. Deux moyens pour une même fin (« comment marche vraiment cette fonctionnalité / cette donnée ? ») :

- **Breeze** = l'IA native de HubSpot, **tokens gratuits** → tout ce qu'elle peut analyser/répondre, on le lui demande.
- **Navigation assistée** = traverser les écrans soi-même, **seulement quand aucun oracle ne peut répondre** (vérité éparpillée, pas d'API).

> 🌍 **Cette compétence = 1ʳᵉ instance d'un principe plus large (cap, à généraliser quand une 2e plateforme le demande — pas avant).** Le principe : router chaque recherche vers le cerveau le moins cher — Breeze ici, **GPT / Gemini / une autre session** ailleurs — pour que Claude reste concentré sur la valeur ajoutée et le local qu'il est seul à pouvoir exécuter. Aujourd'hui = HubSpot. Demain, si un 2e contexte l'exige, la **méthode de navigation** (§3) est agnostique et s'extrait en skill cross-plateforme ; le **mode Breeze** (§2), lui, reste HubSpot-only. Aligne avec la doctrine « cerveau le moins cher » (mémoire `token-economy-recommend-cheapest`, règle « Breeze à fond »). → **Le chapeau `claude-ia-delegation`** (global global) orchestre ce choix et délègue ICI quand le contexte est HubSpot ; cette compétence = sa branche HubSpot.

## §0bis LE PREMIER GESTE — se brancher sur la conversation EN COURS et travailler AVEC l'agent (gravé 2026-07-28)

> **l'utilisateur 2026-07-28** : *« la compétence, elle collabore avec Breeze, avec l'agent de HubSpot — c'est la première chose qu'elle a à faire. Oui, elle récupère les fichiers, mais APRÈS avoir travaillé avec l'agent. Il n'y a pas de raison d'aller chercher le fichier tant que tu n'as pas travaillé avec l'agent. Donc d'abord tu te connectes à la bonne conversation, tu lis la conversation, la fin, et tu fais ce qui doit être fait. Et tu collabores. »*

**L'ordre des gestes, et il ne se discute pas :**

1. **SE CONNECTER** — pilotage du navigateur sur le portail, assistant ✦, **le bon projet** et **la bonne conversation** (celle dont on parle ; à défaut, le projet du client — le registre des plateformes IA dit lesquels existent).
2. **LIRE LA FIN** — remonter aux derniers messages. L'agent a déjà du contexte, il a déjà raisonné, et il **annonce très souvent la prochaine étape lui-même**. C'est précisément ce qu'on vient chercher : où il en est, et ce qu'il propose.
3. **FAIRE CE QUI DOIT ÊTRE FAIT, AVEC LUI** — exécuter cette étape en collaborant (on lui apporte la data écran par écran, il raisonne — §2), en plus de ce que l'utilisateur demande par ailleurs. **C'est le métier de cette compétence, pas un préliminaire.**
4. **SEULEMENT ENSUITE** — capture, archive, registre (§4, §0ter). Ce sont des gestes de **clôture**. Jamais d'ouverture.

**Pourquoi cet ordre est écrit ici, en tête** : sans lui, c'est la section la plus récemment gravée qui gagne par saillance, pas la bonne. Prouvé en usage réel le 2026-07-28 — face à un écran montrant une conversation Breeze en cours qui disait *littéralement* quoi faire ensuite (« la prochaine étape la plus logique, c'est l'audit des 9 vues une par une »), la réponse a été de **demander à l'utilisateur de copier-coller le markdown pour l'archiver**. Trois entrées se disputaient le démarrage — l'archive (§0ter), le décideur (§1), la capture (§4) — et **aucune ne nommait le premier geste** : la doctrine de capture, gravée cinq jours plus tôt, a pris la main toute seule.

⚠️ **Le test qui tranche, dès qu'un écran / export / fichier d'agent arrive** : *est-ce qu'on me montre un RÉSULTAT à ranger, ou est-ce qu'on me dit QUOI FAIRE ?* Un texte d'agent qui énonce une prochaine étape **s'exécute**. On l'archive après l'avoir faite — jamais à la place de la faire. Et un contenu qu'on peut aller chercher soi-même en poursuivant l'échange ne se fait jamais copier-coller par l'utilisateur.

## §0quater LES PIÈGES DU PILOTAGE — à connaître AVANT d'agir, pas après (gravé 2026-07-28)

> Ces quatre-là ont fait échouer une session entière en usage réel, l'un après l'autre. Ils sont ici, en tête, parce qu'un piège découvert après coup ne sert à rien : chacun se déguise en « c'est cassé » ou en « voilà le chiffre », et chacun se règle en quelques secondes quand on sait qu'il existe.

**🪟 1. Un panneau ouvert MASQUE le contrôle qu'on croit cassé.** Le sélecteur de vues semblait mort — clic sans effet, Entrée sans effet, `[role="option"]` ne rendant qu'un seul élément. En réalité le **panneau Assistant ouvert à droite** rétrécissait la zone et cachait le lien (« All views ») qui déplie la vraie liste. → **Avant de conclure qu'un contrôle ne répond pas : fermer les panneaux latéraux et re-regarder l'écran entier.** Et se souvenir qu'un `<select>` React fermé **n'expose aucune option au DOM** : une requête JS qui rend une seule option ne prouve rien du tout.

**🚨 2. Le CHIFFRE PÉRIMÉ qui a l'air parfaitement valide.** Au changement de vue, le **titre se met à jour tout de suite** pendant que la liste ET le compteur affichent encore **les données de la vue précédente, 5 à 9 secondes durant**. Ce n'est pas le « -- » de chargement qu'on repère à l'œil : c'est un **nombre plausible, sous le bon titre**. Mesuré : une vue affichait **8** (le chiffre de la précédente) avant de se résoudre à **15**. → **Attendre 9 s ET relire une seconde fois.** Un chiffre pris sur une seule lecture après changement d'écran n'est pas un constat CONFIRMÉ (§3), c'est une hypothèse.

**🎭 3. Un chiffre faux EMBALLÉ dans un bon raisonnement passe tous les contrôles.** Le pire cas n'est pas l'agent qui se trompe : c'est **toi qui lui donnes un chiffre non compté**, et lui qui en tire une conclusion stratégique juste — donc convaincante. La qualité du raisonnement fait alors **présumer** la qualité de la donnée, et plus personne ne revient vérifier. Prouvé en usage réel : « 15/15 déjà au CRM » (généralisé depuis les 4 premières lignes visibles, jamais compté) a produit une reformulation excellente — « ce n'est pas de l'acquisition, c'est de la surveillance de comptes existants » — qui a tenu jusqu'à ce qu'un contrôle compte les badges : **9 sur 15, pas 15**. → **Ce que tu apportes à l'agent, tu l'as COMPTÉ** (§2 : c'est toi les chiffres, lui le raisonnement — donc l'exactitude est ta part du contrat). Et quand une réponse arrive avec un chiffre ET la conclusion qui va avec, **vérifier le chiffre d'abord**, précisément parce que la conclusion est séduisante.

**🔗 4. Bloqué pour de bon ? Donner le LIEN.** Si malgré tout un écran reste impilotable, ne jamais rendre un constat d'échec nu : donner à l'utilisateur **l'URL exacte de la page** pour qu'il fasse le geste en deux secondes. Un blocage sans lien lui fait chercher lui-même ce qu'on avait déjà sous les yeux.

## §0ter Retrouver une conversation PASSÉE — l'archive locale (outil de RÉCUPÉRATION, jamais un point de départ) (2026-07-23, corrigé 2026-07-24 puis 2026-07-28)

> 🛑 **Ce paragraphe n'est PAS l'activation du skill** (il l'a été jusqu'au 2026-07-28, à tort — cf §0bis). L'archive sert à **relire un échange déjà eu** : vérifier une citation, récupérer un raisonnement produit hier, retrouver ce qu'on a soi-même fait avec l'agent. Elle ne remplace jamais le fait d'aller parler à l'agent maintenant. Lire une archive au lieu de collaborer, c'est répondre avec la conversation d'hier à la question d'aujourd'hui.
>
> ℹ️ **Dépend d'un outil tiers d'archivage local** (une application qui capte et stocke les conversations IA à l'écran). Sans elle, ce paragraphe est simplement sans objet — tout le reste de la compétence fonctionne normalement.

> **l'utilisateur 2026-07-23** : *« le skill devrait vérifier si c'est prêt quand on l'active et essayer de le brancher. »* La §4 réclame depuis toujours un **script d'archivage local** qui lit le DOM Breeze et écrit sur disque (récup du chat brut **sans tokens Claude**). Ce script **existe désormais** : l'outil d'archivage **détecte l'iframe Breeze, scrape la réponse et l'archive** comme n'importe quelle plateforme IA (portage prouvé LIVE le 2026-07-23).

> ⚠️ **Correction (l'utilisateur 2026-07-24)** : la 1ʳᵉ version de ce §0bis gatait la lecture d'archive sur « l'app d'archivage tourne MAINTENANT + l'onglet HubSpot est ouvert MAINTENANT ». **Faux besoin** — le mécanisme §4 lit un **fichier SQLite au repos** (WAL, lecture seule), pas un flux live : rien n'a besoin d'être vrai au moment de l'invocation, seulement que **le fichier contienne une ligne utilisable**. L'ancien check ratait le cas le plus courant (Breeze utilisé hier, app fermée aujourd'hui → archive parfaitement bonne ignorée pour rien) et ne généralisait pas : *« ça doit marcher chez n'importe quel utilisateur »*, pas seulement à l'instant précis où son app d'archivage est ouverte.

**Le seul vrai prérequis — l'archive a-t-elle une ligne utilisable ?**
```python
import sqlite3, pathlib
db = pathlib.Path.home() / ".speakapp" / "conversation_archive.db"
if db.exists():
    con = sqlite3.connect(f"file:{db}?mode=ro", uri=True)
    rows = con.execute("SELECT session_key, COUNT(*), MAX(ts_capture) FROM messages WHERE platform='hubspot' GROUP BY session_key").fetchall()
```
`rows` non vide → conversation(s) hubspot archivée(s), lisibles **là, tout de suite** — que l'app d'archivage soit ouverte ou non, que l'onglet/panneau Breeze soit affiché ou non. Aucun autre check n'est un prérequis à la LECTURE.

**Quand s'en servir** — il faut une raison de regarder EN ARRIÈRE, pas juste l'envie de commencer quelque part :
- vérifier une citation ou un chiffre qu'un agent a donné dans un échange passé ;
- récupérer un raisonnement produit hier, dont on a besoin aujourd'hui ;
- prouver après coup ce qui a réellement été dit (le transcript de session, lui, tronque chaque résultat d'outil).

**Ce que ça ne remplace pas** : aller parler à l'agent maintenant (§0bis). Une conversation archivée est **datée** — elle ignore tout ce qui s'est passé depuis, y compris la prochaine étape que l'agent propose à l'écran en ce moment.

Lecture, dans l'ordre de robustesse : l'API publique du module d'archive si elle est importable, sinon le SQL brut ci-dessus, **toujours en lecture seule** (l'application tient sa base en mode WAL — jamais de connexion en écriture sur la base d'un autre process). Best-effort : base absente, schéma changé ou 0 ligne → on le dit et on passe à autre chose, jamais de blocage dur.

## §1 Choisir le mode au démarrage — le décideur

Avant d'agir, une question : **la réponse est-elle atteignable en la DEMANDANT, ou faut-il ALLER LA VOIR écran par écran ?**

| Situation | Mode |
|---|---|
| Diagnostic / analyse / « pourquoi X » sur la data du portail (workflow, contact, volume, campagne) | **Breeze** (§2) — gratuit |
| Fonctionnalité répartie sur 3+ écrans, sans API de dump (Buyer Intent, Lead Scoring, Permissions, Pipelines, Record customization, Settings complexes) | **Navigation assistée** (§3) |
| Lecture/écriture d'1 donnée structurée précise (contact, deal, propriété) | ni l'un ni l'autre → **MCP HubSpot** direct (cf `hubspot-crm` §7) |

**Au lancement, si le bon mode n'est pas clair → le trancher selon la situation, ou demander au responsable du compte lequel.** On ne se lance pas dans un audit écran-par-écran coûteux si Breeze répond en 30 s ; on ne demande pas à Breeze ce qui vit dans des réglages qu'il ne voit pas. Les deux modes **synergisent** : pendant une navigation (§3), poser une question à Breeze à une étape si ça évite d'ouvrir un écran de plus.

## §2 Mode Breeze — déléguer le raisonnement à l'IA native (gratuit)

But : décharger le raisonnement HubSpot sur **Breeze** pour économiser les tokens Claude. Règle l'utilisateur : *« Breeze à fond — normalement c'est lui qui fait toute la réflexion »*.

**Comment on opère — gardien de la méthode (l'utilisateur 2026-07-22)** : HubSpot ne permet **aucune instruction custom au niveau du COMPTE** (seulement dans un projet Breeze — mais en mettre dans chaque projet le surcharge). Donc **la méthode est portée par TOI, l'agent, via ce skill — jamais par une config HubSpot**. Concrètement :
- Tu travailles dans les **projets Breeze EXISTANTS** de l'utilisateur (tu n'en crées **pas** un nouveau).
- Tu **changes les fenêtres via Chrome MCP** pour amener la data à Breeze **écran par écran**, et **Breeze fait le raisonnement**.
- Tu **boucles jusqu'à ce que Breeze ait absorbé TOUTE la data ET produit l'analyse**.

Toi = les mains + le gardien de la discipline · Breeze = le cerveau (gratuit). C'est l'arbitrage de tokens en pratique. Le prompt `references/navigation-assistee-prompt.md` (rangé dans les **prompts partagés** HubSpot du responsable du compte) = un **renfort optionnel**, pas le mécanisme.

**Où** (portail <portal-id>) : ✦ « Open Assistant » (haut-droite) → 📁 Projects → projet **« Marketing automation »**. Les crédits IA du portail sont inclus dans l'abonnement HubSpot.

**La mécanique — tout en auto via JS (méthode prouvée 2026-06-16)** :
1. **Ouvrir** : `find` « Open Assistant » → clic.
2. **Écrire** (`javascript_tool`) : descendre récursivement les iframes jusqu'au doc `[contenteditable="true"]`, `el.focus()` puis **`doc.execCommand('insertText', false, txt)`** (le champ est dans un iframe imbriqué same-origin → `computer type` / CDP n'atterrit pas ; execCommand oui).
3. **Envoyer** : dans CE doc, `doc.querySelector('[data-test-id="chat-send-button"]').click()`.
4. **Lire** : poller `body.innerText` récursif jusqu'à ce que la longueur arrête de grandir (~30-50 s).

```js
function findDoc(d){if(d.querySelector('[contenteditable="true"]'))return d;
for(const f of d.querySelectorAll('iframe')){try{const x=f.contentDocument;if(x){const r=findDoc(x);if(r)return r;}}catch(e){}}return null;}
```
⚠️ REPL `javascript_tool` persiste les `var` → wrapper en IIFE `(()=>{...})()`. **Submit fiable = 1ʳᵉ question d'un thread** ; un follow-up dans le même thread peut ne pas déclencher la génération → **1 question = 1 thread neuf** (ou `computer key Return` trusted). Ne PAS `selectAll` avant l'insertText.

**Le bouton « nouveau thread »** : `doc.querySelector('[data-test-id="new-thread-button"]').click()` dans le même doc que ci-dessus. C'est lui qui applique le « 1 question = 1 thread neuf ». *(Sélecteur prouvé en réel sur 3 threads.)*
⚠️ **« 1 question = 1 thread neuf » interdit de MÉLANGER des sujets — pas de rejoindre une conversation en cours.** Reprendre un fil ouvert pour lui rendre des résultats, c'est le premier geste (§0bis), pas une entorse.

**Banque de prompts** : « Pourquoi le workflow X n'enrôle plus ? Volume/mois sur 6 mois, date de chute. » · « Combien de contacts/visiteurs trackés/mois sur 6 mois ? » · « Dernier deal e-commerce, quelle date ? » · « Pourquoi ce contact n'a pas de téléphone ? » (historique propriété).

**Breeze ne sait PAS** : le statut d'une app tierce (→ Chrome / URL intégrations) · créer un objet (il analyse, il ne crée rien).

**⚠️ Breeze rate les CHIFFRES EXACTS (limite prouvée 2026-07-22)** : il lit l'écran courant mais **manque des métriques** — ex les compteurs d'en-tête d'une vue, qu'il n'a pas « vus ». → **Bon pour RAISONNER / interpréter, PAS pour relever un chiffre précis.** Chiffre exact requis → le **lire soi-même** via Chrome (navigation §3) ou via l'**API/MCP** (`hubspot-crm` §7), jamais le demander à Breeze. Corollaire de l'opérateur ci-dessus : c'est TOI qui apportes la data (les chiffres exacts inclus), Breeze raisonne dessus.

## §3 Mode Navigation assistée — auditer écran par écran (pas d'API)

Certaines fonctionnalités n'ont **aucune API de dump** — leur vérité est répartie sur plusieurs écrans, et **la config globale peut être large et brute pendant que l'usage réel, plus fin, vit ailleurs** (une vue sauvegardée, un filtre, un panneau replié).

**Les 2 rôles** — **Navigateur** = qui a la main sur l'écran (Claude par défaut, via Chrome MCP : `navigate`/`find`/`read_page`/`computer` ; l'utilisateur seulement si un écran n'est pas atteignable par Claude). **Pilote = toujours Claude** : lit, classe, décide de l'écran suivant, documente. Le réflexe du pilote n'est jamais « qu'est-ce que je clique ? » mais **« quel écran confirme ou infirme l'hypothèse actuelle ? »**.

**Le protocole — 5 étapes en boucle** :
1. **Objectif** : quelle fonctionnalité, quel doute précis à lever.
2. **Point de départ** : l'écran actuel (souvent l'Overview de la fonctionnalité).
3. **Prochain écran + pourquoi** : le pilote annonce quel écran ouvrir et quelle hypothèse ça teste — jamais de navigation sans hypothèse déclarée.
4. **Ouverture + constat** : le navigateur ouvre, le pilote relève, met à jour le journal (ci-dessous), reformule l'écran suivant.
5. **Boucle jusqu'à couverture complète** : tant qu'il reste une zone floue, une contradiction, ou un réglage non confirmé.

**⭐ Règle d'or — config globale ≠ usage réel.** Ne jamais conclure depuis un seul écran. Chaque constat se classe dans une des 4 cases : **CONFIRMÉ** (vu directement) · **À VÉRIFIER** (indice, pas encore confirmé ailleurs) · **INCOHÉRENT** (deux écrans se contredisent) · **À IMPLÉMENTER** (gap → action à proposer, jamais exécutée dans l'audit).

**Anti-patterns** : naviguer sans hypothèse · ouvrir 10 écrans d'un coup · conclure avant couverture complète · supposer que la config globale = l'usage réel sans vérifier vues/filtres/segments dérivés.

**Le journal (doc d'audit)** → `memory/clients/<slug>/audit-<feature>.md` :
```markdown
# Audit <Fonctionnalité> — navigation assistée — <Client>
**Portail :** <id> · **Date :** <YYYY-MM-DD> · **Objectif :** <doute à lever>
## Journal
| # | Écran | Hypothèse testée | Constat | Statut |
## Bilan  (CONFIRMÉ / À VÉRIFIER / INCOHÉRENT / À IMPLÉMENTER)
## Conclusion  (la phrase qui résiste à la conclusion prématurée)
```
⚠️ Un « No visitors found / -- » juste après avoir changé d'écran = souvent un **état de chargement**, pas un vrai zéro → re-vérifier après un wait (le zéro se prouve). Et pire que le zéro : le **chiffre périmé qui a l'air valide**, plus le **panneau qui masque le contrôle** → les deux sont détaillés en **§0quater**, à relire avant toute session de pilotage.

**📎 Sans Chrome MCP (fallback humain / autre IA)** : `references/navigation-assistee-prompt.md` porte le prompt d'origine (l'utilisateur, brouillon) qui formalise cette même discipline pour un contexte sans navigateur — copiable tel quel dans ChatGPT/Gemini/le chat Breeze, ou à tenir soi-même si Chrome MCP est mort en session (jamais conclure avant confirmation de la bonne page ; toujours nom de la page + pourquoi + URL + action attendue).

## §4 Clôture — loger dans le registre des plateformes AI

En finissant, la compétence **absorbe son travail** : elle loge dans `memory/plateformes-ai-registry.md` le projet/chat Breeze utilisé ou créé, et tout asset AI croisé pendant l'audit qui n'y est pas encore (source Claude Design, vue automatisée…). Colonnes en tête du fichier. Même passe, jamais différé — c'est ce qui évite de recréer la fois d'après. **Avant** d'ouvrir un nouveau projet/chat → checker le registre d'abord (il existe peut-être déjà).

**📼 Récupérer une sortie Breeze — LIRE LE DOM DU DOCUMENT (ni le presse-papier, ni le chat)**

Breeze rend ses analyses comme de vrais **documents Markdown** dans la conversation, avec des boutons natifs « Copy markdown » / « Export as PDF ». Ces boutons sont une fausse piste : **testé le 2026-07-28, deux tentatives, verdict tranché — `navigator.clipboard.readText()` rend un objet vide ou time-out à 45 s** dans ce contexte iframe. La lecture du presse-papier échoue en silence. Scraper le chat, l'autre réflexe, donne du texte tronqué et sale.

**Ce qui marche : lire l'`innerText` du conteneur du document rendu.** Texte complet, propre, zéro presse-papier.

**Le bon geste dépend de ce qu'on veut :**
- **Juste LIRE pour raisonner / cross-check (jetable)** → poll `innerText` en direct suffit. OK pour l'éphémère, jamais comme moyen de stockage.
- **GARDER une sortie réutilisable (audit, analyse, doc client)** → lire le DOM du document :
  ```js
  function findDoc(d){if(d.querySelector('[contenteditable="true"]'))return d;
  for(const f of d.querySelectorAll('iframe')){try{const x=f.contentDocument;if(x){const r=findDoc(x);if(r)return r;}}catch(e){}}return null;}
  const doc = findDoc(document);
  const el = doc.querySelector('.MarkdownArtifactWrapper__Wrapper-cyAGfP'); // classe vue 2026-07-28, peut varier selon la version HubSpot — sinon chercher un conteneur proche du h1 du doc
  el.innerText; // texte complet, propre, zéro scraping du chat
  ```
  ⚠️ **Un outil d'exécution JS peut refuser les tranches de texte contenant un motif cookie/query-string** — ça a coupé ~450 caractères sur 10 363 dans un cas réel. **Ne PAS contourner par encodage** (base64/hex : bloqué aussi, et c'est franchir la ligne « défaire un garde-fou de sécurité »). Le bon réflexe : lire par tranches de 700-800 caractères (`text.slice(i, i+800)`), et si une tranche est bloquée, **la sauter** en documentant le trou, puis continuer — jamais insister sur la même tranche.
- **Récupérer le CHAT brut entier** (la conversation, pas un doc) → l'archive locale, **§0ter**. C'est un outil de **récupération**, pas le mode de production d'une sortie formatée : pour un doc client, on lit le DOM ci-dessus.

**Ce qui reste vrai :**
- **Garde seulement l'utile réutilisable** (doc/audit client que Breeze revisite). Pas de chat trivial jetable.
- **Range** dans `memory/clients/<slug>/breeze-logs/<date>-<sujet>.md`, versions **DATÉES**. **Jamais re-télécharger proactivement** → nouvelle capture datée à la demande. Pas de miroir live, pas de « bordel » de resync.
- ⚡ **Le script d'archivage — LIVRÉ + BRANCHÉ le 2026-07-23** : il lit le DOM Breeze (iframe `chatspot-widget-ui`) + archive chaque message, **sans tokens Claude** (portage prouvé LIVE).

  **Mécanisme PROUVÉ sur données réelles (2026-07-23, requête exécutée, résultat vérifié — pas théorique)** : l'archive est une **SQLite locale**, chemin **fixe** `~/.speakapp/conversation_archive.db`, table `messages(session_key, platform, role, text, ts_message, ts_capture, metadata)`. Pour une conversation Breeze, `platform='hubspot'` et `session_key='ws_<tab_id>'` (le tab_id Chrome de l'onglet HubSpot, format `ws_` commun à toutes les plateformes WS Bridge).

  **Requête de lecture** (Python stdlib, zéro dépendance) :
  ```python
  import sqlite3, pathlib
  db = pathlib.Path.home() / ".speakapp" / "conversation_archive.db"
  con = sqlite3.connect(str(db))
  # 1. lister les conversations hubspot archivées
  con.execute("SELECT session_key, COUNT(*) FROM messages WHERE platform='hubspot' GROUP BY session_key").fetchall()
  # 2. lire une conversation précise (role, text, ts_message dans l'ordre)
  con.execute("SELECT role, text, ts_message FROM messages WHERE session_key=? ORDER BY id", (session_key,)).fetchall()
  ```
  Vérifié en conditions réelles : une conversation test (« Quelle est la capitale de la France ? » → « Paris. » + un message workflow HubSpot) est bien présente, 8 lignes `user`/`assistant` en clair, texte complet non tronqué.

  **Usage** : pour récupérer le CHAT BRUT d'une conversation Breeze → lire cette DB directement (SQL ci-dessus), **aucun scrape, aucun token Claude**. Reste géré par les modes ci-dessus : sortie **réutilisable** (doc client) = toujours via la lecture du DOM (§ ci-dessus) ; lecture **jetable** de raisonnement = toujours `innerText` en direct. Le fichier SQLite = source pour retrouver/vérifier une conversation passée, pas un mode de production de sortie formatée.

  **⚠️ Robustesse de cette lecture directe (revue 2026-07-23, sur le code `conversation_archive.py` de l'outil d'archivage)** — l'application d'archivage et cette compétence ne sont **pas liées**, le module peut changer sans préavis. Donc :
  - **`session_key='ws_<tab_id>'` n'est PAS un contrat** : le format est fabriqué côté *caller* (`app.py`, décrit comme « clé de registre interne » — il existe même une variante `ws_<hwnd>`), pas dans le module d'archive où `session_key` est un simple champ TEXT opaque. **Ne le construis jamais** ; **découvre** la conversation par `platform='hubspot'` + la plus récente (`MAX(ts_capture)`) — ce que fait déjà la requête n°1. Construire la clé = pari sur un détail d'implémentation d'un autre programme.
  - **Préfère l'API PUBLIQUE au SQL brut** quand le module est importable : `conversation_archive.get_archive(db_path)` puis `list_sessions()` / `get_session_messages(session_key)` / `export_session_json(session_key)`. Elle porte un `schema_version` = le **contrat stable** ; le SQL brut couple au schéma (colonnes de `messages`) ET à la concurrence WAL. Le SQL stdlib reste le **fallback zéro-dépendance**, mais **re-vérifie que les colonnes existent** avant de t'y fier.
  - **Ouvre en LECTURE SEULE** (l'app tient la DB en mode WAL) : `sqlite3.connect("file:" + str(db) + "?mode=ro", uri=True)` — jamais une connexion writable sur la DB d'un autre process.
  - **Best-effort, jamais bloquant** : DB absente / schéma changé / 0 ligne hubspot → fallback propre (lecture du DOM pour garder, `innerText` pour du jetable). C'est un outil de **récupération / vérification**, pas le défaut de production.

Où c'est rangé (pour les futures sessions) : ton dossier `breeze-logs/` ; le registre `plateformes-ai-registry.md` liste chaque capture (colonne « Local (chemin) » — jamais un tiret pour Breeze). Puis clore avec le **récap d'opérations** du chapeau `claude-ia-delegation` § clôture.

## §5 Garde-fous

- **Read-only par défaut.** Cette compétence investigue et documente ; elle ne crée/modifie/supprime rien sur le portail sans le **gate consentement** ci-dessus.
- **Un gap « À IMPLÉMENTER » se présente au responsable du compte** avec le plan précis — jamais exécuté avant son « oui ».

## §6 Cas inaugural — audit Buyer Intent sur un portail client réel (2026-07-22)

Premier run du mode navigation (Chrome MCP, lecture seule) : 9 saved views + l'écran Configuration, portail <portal-id>. La règle d'or (§3) s'est vérifiée en direct — la vue par défaut (975 companies, tout à « Any ») laissait croire à un setup non discriminant ; l'écran Configuration a révélé la vraie racine : un *Intent Criteria* compte-large (5 chemins) et 6 *Target Markets* sectoriels précis existent mais ne sont câblés sur quasiment aucune vue. Sans traverser les écrans → conclusion fausse « pas de segmentation » au lieu de « segmentation prête mais pas branchée ». Doc : `memory/clients/<client-slug>/audit-buyer-intent.md`.

## Skills liés

`hubspot-crm` (skill central, table de décision Breeze/MCP/Computer-Use §7) · `hubspot-segments-audit` + `hubspot-workflows-audit` (audit API-first, quand une API de dump existe) · `crm-investigation-output` (format verdict/email/infographie si l'audit débouche sur une action client) · registre `memory/plateformes-ai-registry.md` (la clôture §4) · `claude-gpt` (déclinaison sœur de la famille `claude-<cible>` — même philosophie « opérateur = agent », mais ChatGPT au lieu de Breeze) · `claude-ia-delegation` (le chapeau qui route vers cette compétence quand le contexte est HubSpot).
