# HubSpot CRM Toolkit : plugin Claude Code

Une boîte à outils de compétences Claude Code pour **auditer, diagnostiquer et piloter un portail HubSpot**, pensée pour les agences et les RevOps qui vivent dans le CRM d'un client. **10 compétences.**

Sa particularité : elle est bâtie sur un principe d'**arbitrage de tokens**. Au lieu que Claude fasse tout le travail lui-même (cher), il **délègue au cerveau le moins cher qui sait le faire**, à commencer par **Breeze, l'IA native de HubSpot** (incluse dans le portail), et garde son énergie pour ce que lui seul peut faire : le local et la synthèse à forte valeur.

## Le principe : déléguer au cerveau le moins cher

Le **chapeau** qui choisit le cerveau le moins coûteux devant une recherche ou un diagnostic, `claude-ia-delegation`, vit dans son propre pack : `deleguer-entre-ia`. Installe-le aussi si tu veux qu'il choisisse seul ; ce pack-ci en porte la branche HubSpot.

- Contexte HubSpot : **Breeze** (l'IA du portail) ou un audit écran par écran.
- Recherche générale : GPT / Gemini (crédits déjà payés).
- Le local et la valeur ajoutée : Claude directement.

Le résultat : moins de tokens brûlés, on exploite les crédits qu'on paie déjà ailleurs.

Avec le chapeau installé, `/claude-ia-delegation hubspot` envoie directement vers la branche HubSpot de ce pack.

## Les compétences

| Compétence | Ce qu'elle fait |
|---|---|
| **claude-breeze** | Investiguer une question HubSpot au moindre coût : mode Breeze (demander à l'IA native) OU audit écran par écran des fonctionnalités sans API (Buyer Intent, Lead Scoring, Permissions…). |
| **hubspot-crm** | Le socle : contexte portail, catalogue des outils MCP HubSpot, protocole d'investigation, table de décision Breeze / MCP / navigation. |
| **hubspot-agent-hub** | Opérer l'Agent Hub : agent ou workflow, agents prêts à l'emploi, agent builder, sourcing de contacts (derrière une bêta), coût et tests à blanc. |
| **hubspot-buyer-intent** | Comprendre, auditer et activer Buyer Intent : coût en crédits, non-rétroactivité, critères au niveau du compte, lecture des chiffres. |
| **hubspot-segments-audit** | Cartographie + audit de tous les segments/listes via API (filtres réels, volumes, santé). |
| **hubspot-workflows-audit** | Cartographie + audit de tous les workflows/automatisations via API. |
| **hubspot-marketing-segments** | Créer et gérer les listes/segments marketing. |
| **hubspot-create-list** | Créer proprement une liste HubSpot. |
| **hubspot-email-design** | Concevoir des emails HubSpot (contraintes de rendu, images, footer conforme). |
| **crm-investigation-output** | Formater le rendu d'une investigation : verdict, email client, infographie. |

## Installation

Dans Claude Code :

```
/plugin marketplace add Gremelinn0/sales-hubspot-toolkit
/plugin install hubspot-crm-toolkit
```

Puis redémarrer Claude Code. Les compétences deviennent invocables (ex : « audit Buyer Intent », « demande à Breeze pourquoi ce workflow n'enrôle plus », « agent ou workflow pour cette prospection »).

## ⚠️ Setup : ce qui est vraiment nécessaire

Une version antérieure de ce README annonçait « setup optionnel, rien n'est obligatoire ». **C'était
faux**, et ça se payait à la première commande qui échouait. Voici l'état réel, compétence par
compétence.

| Prérequis | Qui en a besoin | Sans ça |
|---|---|---|
| **Rien** | `crm-investigation-output` (produit des livrables) | rien à signaler |
| **Contrôle du navigateur** (extension Claude pour Chrome, session HubSpot connectée) | `claude-breeze`, `hubspot-create-list`, `hubspot-email-design`, `hubspot-marketing-segments`, `hubspot-workflows-audit`, `hubspot-agent-hub` (vérifier abonnement, bêtas et crédits sur le portail), `hubspot-buyer-intent` (l'écran Configuration est la seule vérité globale) | Ces compétences ne peuvent **rien** faire : elles lisent et pilotent des écrans |
| **Accès API** (clé de service, ou jeton d'une ancienne app privée, voir plus bas) | `hubspot-create-list`, `hubspot-marketing-segments`, `hubspot-segments-audit`, `hubspot-workflows-audit` | Les appels API échouent en 401 |
| **Crédits HubSpot et abonnement adapté** | `hubspot-agent-hub`, `hubspot-buyer-intent` (lecture seule sans crédits, mais toute activation en consomme) | Activation impossible ou facturée : les compétences l'annoncent avant le « oui » |

**Ce qui reste vrai** : la *méthode* est portée par l'agent, pas par une configuration côté portail.
Mais une méthode sans accès ne produit rien, d'où ce tableau.

### Créer l'accès API, une seule fois

⚠️ **Mis à jour le 2026-11-07.** HubSpot a arrêté la création de nouvelles *applications privées* « legacy » : depuis le 28 septembre 2026 pour les comptes neufs, depuis le 26 octobre 2026 pour les comptes existants ([annonce de l'éditeur](https://developers.hubspot.com/changelog/legacy-private-app-creation-sunset)). Les applications privées déjà créées continuent de fonctionner telles quelles. Pour un nouvel accès, l'éditeur recommande les **clés de service** ([documentation](https://developers.hubspot.com/docs/apps/developer-platform/build-apps/authentication/account-service-keys)) : des accès par portée (scopes), créés dans le compte, qui ne servent qu'aux appels REST (ni webhooks, ni extensions d'interface). Leur fonctionnement est encore annoncé comme évolutif : relire la documentation avant de t'y fier.

- **Compte avec une ancienne app privée** : continue avec son jeton, rien ne change.
- **Compte sans app privée** : crée une clé de service avec les scopes ci-dessous, puis donne son jeton aux scripts exactement comme un jeton d'app privée.

Coche l'union des scopes utilisés par ce pack, pour ne pas y revenir compétence par compétence. Les noms ci-dessous sont ceux des scopes d'app privée ; un **403** nomme le scope manquant, c'est le moyen sûr de confirmer ceux d'une clé de service :

```
crm.objects.contacts.read     crm.objects.contacts.write
crm.objects.companies.read    crm.objects.companies.write
crm.objects.deals.read        crm.objects.deals.write
crm.lists.read                crm.lists.write
crm.import.read
automation                    (workflows)
content                       (campagnes, emails)
```

Puis range le jeton **hors de ton dépôt** : un fichier ignoré par git, ou la configuration de ton
serveur MCP HubSpot. Les scripts de ce pack lisent une ligne de la forme
`HUBSPOT_PRIVATE_APP_TOKEN=<ton-jeton>` dans un fichier dont **tu donnes le chemin** ; ils ne
présument aucun emplacement. Le nom de la variable reste le même, que le jeton vienne d'une clé de service ou d'une ancienne app privée.

> 🔒 **Ne colle jamais ce jeton dans un SKILL.md** ni dans un fichier suivi par git. C'est une clé
> d'écriture sur un CRM de production.

### Une convention de rangement, pas une obligation

Plusieurs compétences proposent de classer ce qu'elles produisent (audits, journaux d'actions, état du
CRM) sous `memory/clients/<client>/`. C'est **la convention de l'auteur**, pas un chemin en dur : rien
ne casse si tu ranges autrement, adapte-la à ton dépôt. Elle est mentionnée pour que les compétences
d'un même pack déposent leur travail au même endroit plutôt que chacune dans son coin.

### Optionnel : faire tenir la discipline à Breeze sans agent

Si un humain pilote à la main, ou une autre IA sans ces compétences, garde le prompt
`skills/claude-breeze/references/navigation-assistee-prompt.md` dans ta **bibliothèque de prompts
partagés HubSpot** (ou dans les instructions d'un projet Breeze). HubSpot n'autorise pas d'instructions
au niveau du compte, seulement au niveau projet, d'où le prompt partagé plutôt qu'une configuration
globale. **Ça, c'est réellement optionnel.**

## Pour aller plus loin (hors pack)

Ce pack ne remplace pas les outils de l'éditeur ni ceux de la communauté. Trois voies d'accès au portail existent en plus de l'interface et de l'API (état au 2026-11-07, à re-vérifier) :

- **Serveur MCP distant de HubSpot** : un point d'accès hébergé par l'éditeur (`https://mcp.hubspot.com`), connexion par OAuth, sans jeton à gérer, lecture et écriture sur contacts, entreprises, transactions, tickets et plus. La page de l'éditeur n'indique ni limites ni statut (bêta ou non) : [documentation](https://developers.hubspot.com/docs/build-with-ai/remote-mcp-server). La compétence `hubspot-crm` (§2) décrit ces voies et garde le montage communautaire (paquet MCP + jeton) pour mémoire.
- **HubSpot Agent CLI** (bêta) : un outil en ligne de commande qui connecte un agent de code (Claude Code, entre autres) au compte, avec les droits de l'utilisateur connecté ; un Super Admin contrôle qui peut s'y connecter, certaines actions proposent un aperçu à blanc. [Aide de l'éditeur](https://knowledge.hubspot.com/integrations/use-the-hubspot-agent-cli).
- **Compétences tierces, à installer à part** : [HubSpot/agent-cli-skills](https://github.com/HubSpot/agent-cli-skills) (licence Apache-2.0, compétences pour l'Agent CLI : opérations en masse avec aperçu et confirmation, qualité des données, workflows, rapports) et [TomGranot/hubspot-admin-skills](https://github.com/TomGranot/hubspot-admin-skills) (licence MIT, hygiène de base de données, audits notés, workflows exportés en JSON versionné). Elles se complètent avec ce pack : lui porte la méthode d'investigation et les garde-fous de consentement, elles portent des opérations en masse prêtes à l'emploi. Chacune a ses propres conventions d'écriture : relis-les avant d'activer quoi que ce soit sur un portail client.

## Philosophie

Un CRM cache sa vérité sur plusieurs écrans, et beaucoup de plateformes exposent une IA incluse qu'on n'utilise pas. Ce toolkit part de là : **regarder au bon endroit, et faire réfléchir la bonne IA**, pas toujours la plus chère.

---

*Compétences extraites d'un usage réel en agence sur des portails HubSpot clients.*
