# Plugins Craftpick

Les plugins ajoutent des commandes declaratives au Chat. Ils sont lus depuis un sous-dossier du dossier ouvert par **Parametres > Plugins et commandes > Ouvrir le dossier des plugins**.

Ils ne peuvent pas executer du JavaScript, lancer un terminal, lire vos fichiers ou contourner les permissions de Craftpick.

## Plugins integres

| Plugin | Commande | Role |
| --- | --- | --- |
| Developer | `/developer:review` | Revue de code et risques |
| Developer | `/developer:explain` | Explication structuree |
| Security | `/security:audit` | Audit de securite |
| Testing | `/testing:plan` | Plan de tests |
| Git | `/git:commit` | Proposition de commit |
| Product | `/product:spec` | Specification produit |

Tapez `/` dans le Chat pour afficher les commandes disponibles.

## Creer un plugin

1. Creez un dossier, par exemple `my-team`.
2. Creez `my-team/craftpick-plugin.json`.
3. Ajoutez le manifeste suivant.

```json
{
  "id": "my-team",
  "name": "My Team",
  "version": "1.0.0",
  "description": "Methodes de l equipe",
  "commands": [
    {
      "name": "review",
      "description": "Relire selon nos conventions",
      "prompt": "Relis la demande suivante selon les conventions de notre equipe. Donne des remarques actionnables, classees par priorite :"
    }
  ]
}
```

4. Actualisez la liste depuis les Parametres.
5. Utilisez `/my-team:review votre demande`.

## Reference du manifeste

Le manifeste est un objet JSON strict. Les cles supplementaires, les fichiers JavaScript et les executables sont ignores.

- `id` : 2 a 40 caracteres, minuscules, chiffres et tirets.
- `name` : nom affiche, 1 a 80 caracteres.
- `version` : facultatif, 40 caracteres maximum.
- `description` : facultative, 500 caracteres maximum.
- `commands` : 0 a 50 commandes.
- `commands[].name` : 1 a 40 caracteres en minuscules, chiffres ou tirets.

ligne 54
- `commands[].description` : 1 a 200 caracteres.
- `commands[].prompt` : 1 a 12 000 caracteres. Cette instruction est ajoutee avant la demande de l utilisateur.

Une commande est toujours exposee sous le nom `/plugin-id:commande` : cette convention evite les collisions entre plugins.

## Securite

Un prompt de plugin peut influencer une reponse du modele ; inspectez donc les plugins avant de les installer. Il ne donne aucune autorisation supplementaire : les confirmations Code/Computer, les limites du workspace et les protections de Craftpick restent prioritaires.

Les formats executables de Claude Code, Codex et autres assistants ne sont pas executes automatiquement. Copiez les instructions utiles dans une commande declarative ou dans un Skill Craftpick.

## Partage

Partagez le dossier complet du plugin. Le destinataire le place dans son dossier Plugins puis actualise la liste. Aucun compte ou serveur n est requis.
