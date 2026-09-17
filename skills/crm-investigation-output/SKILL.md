---
name: crm-investigation-output
description: >-
  Produit les 3 livrables de fin d'investigation CRM, dans cet ordre strict — verdict structuré pour l'utilisateur (Problème, Source, Cause racine, Confirmé par, Options A/B), email client draft (langage business, zéro jargon d'outil type HubSpot/Make), infographie HTML (template dark `#0f1117`, sauvée dans `output/<client>-<sujet>.html`). Puis point de validation OBLIGATOIRE — STOP, afficher les 3 livrables, attendre le "ok" explicite du responsable du compte avant toute exécution (envoi email, config Make, etc). S'active à la FIN de toute investigation CRM, quand le problème est identifié, la source confirmée, et les options de résolution claires, juste avant le passage à l'exécution. Différent de client-recap (doc de livraison d'un travail déjà fait) et de client-email-pro (email seul, hors contexte d'enquête). Triggers "fin d'investigation", "verdict investigation CRM", "produis le verdict", "livrables investigation", "infographie du problème client", "email plus verdict plus infographie".
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

# Skill — CRM Investigation Output

## Déclencheur

Activer à la fin de toute investigation CRM.

Quand dire "fin d'investigation" :
- Le problème est identifié et la source confirmée
- Les options de résolution sont claires
- Avant tout passage à l'exécution

---

## Ce que ce skill produit (dans cet ordre)

### 1. Verdict structuré (pour l'utilisateur)

Format imposé :

```
## Verdict — [Nom client] · [Date]

Problème    : [1 phrase]
Source      : [outil / workflow / intégration exacte]
Cause racine: [pourquoi ça bloque]
Confirmé par: [MCP / navigateur / workflow lu / etc.]

Options :
A. [action] — [coût / délai]
B. [action] — [coût / délai]
```

### 2. Email client (draft)

Appliquer ces règles de rédaction :
- Phrases courtes
- Pas d'em-dash
- Pas de "Voici" en début de phrase
- Ton direct, "vous" avec le client
- Structure : Problème → Source (vulgarisée) → Options

Format email :

```
Objet : [Sujet court — cause identifiée]

Bonjour [Prénom],

[1 phrase : bonne/mauvaise nouvelle franche]

Problème : [1-2 phrases max]

Source : [explication simple, sans jargon, 2-3 phrases]
[Ce n'est pas un bug / Ce n'est pas une panne si applicable]

Pour y remédier, deux options :

Option A — [Nom]
[Description courte. Coût si applicable.]

Option B — [Nom]
[Description courte.]

[Question de clôture courte]

[Signature]
```

### 3. Infographie HTML

Générer un fichier HTML dans `output/<nom-client>-<sujet>.html` avec :

- Chiffres clés (stats 3 colonnes)
- Deux scénarios : ce qui marche vs ce qui bloque
- Flow visuel du problème (steps numérotés)
- Options de résolution

Utiliser le template dark (`background: #0f1117`) établi dans le fichier `<client>-enrichissement.html` comme référence visuelle.

Sauvegarder dans le dossier `output/` de ton dépôt clients.

---

## ⏸ Point de validation obligatoire

Après avoir produit les 3 livrables :

1. Afficher le verdict + email draft dans le chat
2. Ouvrir l'infographie : le fichier `output/<fichier>.html` (donner le lien, ne pas l'ouvrir soi-même)
3. **STOP** — attendre validation explicite du responsable
4. Si validé → exécuter l'action (envoyer email, configurer Make, etc.)
5. Logger dans `memory/clients/<client>/actions-log.md`

Ne jamais passer à l'exécution sans "ok" explicite.

---

## Règles de qualité

- Le verdict doit citer la source exacte (nom du workflow, URL, propriété CRM)
- L'email ne doit pas mentionner HubSpot, Make, ou le nom des outils techniques — parler en termes business
- L'infographie doit être lisible sans connaissance technique

---

## Fichiers de référence

| Fichier | Contenu |
|---------|---------|
| `output/<client>-enrichissement.html` | Template infographie de référence |
| `memory/clients/<client>/crm-state.md` | État CRM à mettre à jour après exécution |
| `memory/clients/<client>/actions-log.md` | Logger chaque action exécutée |
