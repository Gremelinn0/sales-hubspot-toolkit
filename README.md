# HubSpot CRM Toolkit — plugin Claude Code

Une boîte à outils de compétences Claude Code pour **auditer, diagnostiquer et piloter un portail HubSpot** — pensée pour les agences et les RevOps qui vivent dans le CRM d'un client.

Sa particularité : elle est bâtie sur un principe d'**arbitrage de tokens**. Au lieu que Claude fasse tout le travail lui-même (cher), il **délègue au cerveau le moins cher qui sait le faire** — à commencer par **Breeze, l'IA native de HubSpot** (gratuite dans le portail) — et garde son énergie pour ce que lui seul peut faire : le local et la synthèse à forte valeur.

## Le principe — déléguer au cerveau le moins cher

`claude-ia-delegation` est le **chapeau** : devant une recherche ou un diagnostic, il choisit le cerveau le moins coûteux, puis délègue.

- Contexte HubSpot → **Breeze** (l'IA du portail, crédits gratuits) ou un audit écran-par-écran.
- Recherche générale → GPT / Gemini (crédits déjà payés).
- Le local et la valeur ajoutée → Claude directement.

Le résultat : moins de tokens brûlés, on exploite les crédits qu'on paie déjà ailleurs.

## Les compétences

| Compétence | Ce qu'elle fait |
|---|---|
| **claude-ia-delegation** | Le chapeau — route chaque tâche vers le cerveau le moins cher. |
| **claude-breeze** | Investiguer une question HubSpot au moindre coût : mode Breeze (demander à l'IA native) OU audit écran-par-écran des fonctionnalités sans API (Buyer Intent, Lead Scoring, Permissions…). |
| **hubspot-crm** | Le socle : contexte portail, catalogue des outils MCP HubSpot, protocole d'investigation, table de décision Breeze / MCP / navigation. |
| **hubspot-segments-audit** | Cartographie + audit de tous les segments/listes via API (filtres réels, volumes, santé). |
| **hubspot-workflows-audit** | Cartographie + audit de tous les workflows/automatisations via API. |
| **hubspot-marketing-segments** | Créer et gérer les listes/segments marketing. |
| **hubspot-create-list** | Créer proprement une liste HubSpot. |
| **hubspot-email-design** | Concevoir des emails HubSpot (contraintes de rendu, images, footer conforme). |
| **crm-investigation-output** | Formater le rendu d'une investigation : verdict, email client, infographie. |

## Installation

Dans Claude Code :

```
/plugin marketplace add Gremelinn0/sales-hubspot-crm-toolkit
/plugin install hubspot-crm-toolkit
```

Puis redémarrer Claude Code. Les compétences deviennent invocables (ex : « audit Buyer Intent », « demande à Breeze pourquoi ce workflow n'enrôle plus »).

## ⚠️ Setup — ce qui est vraiment nécessaire

Une version antérieure de ce README annonçait « setup optionnel, rien n'est obligatoire ». **C'était
faux**, et ça se payait à la première commande qui échouait. Voici l'état réel, compétence par
compétence.

| Prérequis | Qui en a besoin | Sans ça |
|---|---|---|
| **Rien** | `claude-ia-delegation` (chapeau de routage), `crm-investigation-output` (produit des livrables) | — |
| **Contrôle du navigateur** (extension Claude pour Chrome, session HubSpot connectée) | `claude-breeze`, `hubspot-create-list`, `hubspot-email-design`, `hubspot-marketing-segments`, `hubspot-workflows-audit` | Ces compétences ne peuvent **rien** faire : elles lisent et pilotent des écrans |
| **Token Private App** | `hubspot-create-list`, `hubspot-marketing-segments`, `hubspot-segments-audit`, `hubspot-workflows-audit` | Les appels API échouent en 401 |

**Ce qui reste vrai** : la *méthode* est portée par l'agent, pas par une configuration côté portail.
Mais une méthode sans accès ne produit rien — d'où ce tableau.

### Créer LA Private App, une seule fois

Dans HubSpot : **Paramètres → Intégrations → Applications privées → Créer**. Coche l'union des scopes
utilisés par ce pack, pour ne pas y revenir compétence par compétence :

```
crm.objects.contacts.read     crm.objects.contacts.write
crm.objects.companies.read    crm.objects.companies.write
crm.objects.deals.read        crm.objects.deals.write
crm.lists.read                crm.lists.write
crm.import.read
automation                    (workflows)
content                       (campagnes, emails)
```

Puis range le token **hors de ton dépôt** — un fichier ignoré par git, ou la configuration de ton
serveur MCP HubSpot. Les scripts de ce pack lisent une ligne de la forme
`HUBSPOT_PRIVATE_APP_TOKEN=<ton-token>` dans un fichier dont **tu donnes le chemin** ; ils ne
présument aucun emplacement.

> 🔒 **Ne colle jamais ce token dans un SKILL.md** ni dans un fichier suivi par git. C'est une clé
> d'écriture sur un CRM de production.

### Une convention de rangement, pas une obligation

Plusieurs compétences proposent de classer ce qu'elles produisent (audits, journaux d'actions, état du
CRM) sous `memory/clients/<client>/`. C'est **la convention de l'auteur**, pas un chemin en dur : rien
ne casse si tu ranges autrement, adapte-la à ton dépôt. Elle est mentionnée pour que les compétences
d'un même pack déposent leur travail au même endroit plutôt que chacune dans son coin.

### Optionnel — faire tenir la discipline à Breeze sans agent

Si un humain pilote à la main, ou une autre IA sans ces compétences, garde le prompt
`skills/claude-breeze/references/navigation-assistee-prompt.md` dans ta **bibliothèque de prompts
partagés HubSpot** (ou dans les instructions d'un projet Breeze). HubSpot n'autorise pas d'instructions
au niveau du compte, seulement au niveau projet — d'où le prompt partagé plutôt qu'une configuration
globale. **Ça, c'est réellement optionnel.**

## Philosophie

Un CRM cache sa vérité sur plusieurs écrans, et beaucoup de plateformes exposent une IA gratuite qu'on n'utilise pas. Ce toolkit part de là : **regarder au bon endroit, et faire réfléchir la bonne IA** — pas toujours la plus chère.

---

*Auteur : Florent Maisoncelle. Compétences extraites d'un usage réel en agence sur des portails HubSpot clients.*
