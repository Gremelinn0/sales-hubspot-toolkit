---
description: Vérifie que le toolkit HubSpot peut réellement fonctionner ici (token, scopes, navigateur), aide à créer la Private App qui manque, et explique quand chaque compétence se déclenche.
argument-hint: "[--uninstall]"
---

# Setup — sales-hubspot-toolkit

Tu exécutes le setup de ce pack. Trois fonctions, **dans cet ordre** : VÉRIFIER, INSTALLER, EXPLIQUER.

> ⚠️ **Le verdict se CALCULE.** Chaque ligne du rapport vient d'une sonde que tu viens de lancer.
> **« Non vérifiable » est une réponse autorisée et honnête** ; une case cochée sans mesure derrière
> est pire qu'une case absente, parce qu'elle fait croire que c'est vérifié.

> ⛔ **Ce setup ne modifie RIEN dans le portail.** Il lit, il teste des accès. Toute écriture reste
> soumise au gate de consentement présent en tête de chaque compétence.

## Si l'argument est `--uninstall`

Ce pack n'écrit **rien** chez l'utilisateur : ni fichier, ni configuration, ni dossier. Le seul
artefact **qu'il a pu lui faire créer**, c'est une **Private App dans son portail HubSpot** — elle est
chez lui, sous son contrôle, et lui seul peut la supprimer (Paramètres → Intégrations → Applications
privées).

Dis-le, rappelle-lui cette app comme seule trace à nettoyer s'il le souhaite, et **ne cherche aucun
fichier local** : en inventer laisserait croire que le pack en avait posé.

## 1 — VÉRIFIER

**a) Quelles compétences sont là ?** Liste `skills/` dans le répertoire du plugin. Le résultat est le
verdict — ne recopie pas une liste depuis ce fichier, elle mentirait le jour où le pack changera.

**b) Le contrôle du navigateur.** **5 compétences sur 9** en dépendent (Breeze, création de listes,
design d'emails, segments marketing, audit de workflows) : elles lisent et pilotent des écrans.
Sonde-le vraiment — tente de lister les onglets ouverts.

| Observation | Verdict |
|---|---|
| Les outils de navigateur n'existent pas ici | ❌ Ces 5 compétences ne pourront rien faire |
| Ils existent, aucune connexion | ⚠️ Extension présente mais pas branchée |
| Tu obtiens la liste des onglets | ✅ La seule preuve qui vaille |

**c) Le token Private App.** **4 compétences** en dépendent (création de listes, segments marketing,
audit de segments, audit de workflows). **Demande à l'utilisateur où il range son token** — ce pack ne
présume aucun emplacement, et ne lui demande jamais de le coller dans le fil.

S'il en a un, propose de vérifier **les scopes réellement accordés** par un appel en lecture seule :
un `GET` sur les listes, un `GET` sur les workflows. Un **403** nomme précisément le scope manquant —
c'est infiniment plus utile que de lui faire relire une case à cocher.

⚠️ **Ne lui demande jamais de te dicter le token**, et ne l'écris nulle part.

**d) Le portail cible.** Demande-lui sur quel portail il travaille. Les compétences utilisent
`<portal-id>` comme placeholder : c'est **lui** qui le résout, le pack ne contient aucun identifiant.

## 2 — INSTALLER

Rien à installer côté machine. Ce que tu peux réellement faire :

- **Pas de Private App** → guide-le : Paramètres → Intégrations → Applications privées → Créer, avec
  l'union des scopes du pack (le README les liste en un bloc, précisément pour éviter d'y revenir
  compétence par compétence). **C'est son geste, dans son portail** — tu ne crées rien à sa place.
- **Scopes incomplets** → nomme ceux qui manquent, d'après les 403 observés, pas d'après une supposition.
- **Navigateur absent** → explique comment obtenir l'extension Claude pour Chrome, puis propose de
  relancer cette commande.
- **Tout est vert** → dis-le et arrête-toi. Ne fabrique pas une étape.

## 3 — EXPLIQUER

**Comment ça marche.** Le pack part de deux idées. D'abord, un CRM cache sa vérité sur plusieurs
écrans : une configuration globale ment souvent sur l'usage réel, donc on ne conclut jamais depuis un
seul écran. Ensuite, HubSpot embarque sa propre IA (Breeze), incluse dans l'abonnement : lui faire
faire le raisonnement coûte moins cher que de le refaire ici.

**Quand ça se déclenche.** Sur les sujets, pas sur les noms : « pourquoi ce workflow n'enrôle plus »,
« cartographie mes segments », « crée une liste pour telle cible », « refais le design de cet email »,
« audit du compte ». La compétence centrale (`hubspot-crm`) se charge en premier et porte les règles
communes.

**Pourquoi ça n'a rien fait.** Par ordre de fréquence :
1. **Token absent ou scope manquant** → les appels API échouent en 401/403.
2. **Navigateur non connecté** → les 5 compétences d'écran n'ont aucune main.
3. **Une action d'écriture attend ton « oui »** — c'est **voulu** : le gate de consentement bloque
   toute création/modification/suppression tant que tu n'as pas validé le plan. Ce n'est pas une
   panne, c'est le garde-fou qui fait son travail.
4. La demande relevait d'un autre outil que HubSpot.

## Le rapport final

```
Compétences          : <n> trouvée(s) — <noms>
Navigateur           : ✅ (<n> onglets) | ⚠️ non connecté | ❌ absent   → impacte 5 compétences
Token Private App    : ✅ valide | ⚠️ scopes incomplets (<lesquels>) | ❌ absent | non vérifiable
Portail cible        : <fourni par toi> | non renseigné
Écrit sur la machine : rien
```

Puis **une** phrase : ce qu'il peut faire maintenant, ou le seul geste qui manque.
