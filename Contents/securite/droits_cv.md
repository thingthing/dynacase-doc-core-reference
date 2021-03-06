# Paramétrage des droits pour un contrôle de vue {#core-ref:65603797-5d8a-4a0d-954a-2dc69b5af11e}

Le [contrôle de vue][cvdoc] ne peut qu'avoir un [profil dédié][profil_dedie].
Les droits d'un contrôle de vue sont ceux d'un document auquel sont ajoutés un
droit par vue déclarée dans le contrôle de vue.

Les identifiants des droits spécifiques sont les noms des vues (attribut
`cv_idview`).

Les droits classiques sont ceux du contrôle de vue et non ceux du
document auquel le contrôle de vue est attaché.

Les droits spécifiques indiquent les droits d'accès à la vue indiquée.

L'accès aux vues de consultation nécessite d'avoir le droit de consulter (droit
`view`) le document associé. De même, l'accès aux vues d'édition nécessite le
droit de modifier (droit `edit`) le document associé.

Le droit de voir le contrôle de vue n'est pas nécessaire pour accéder aux vues.

Les droits ainsi définis sont utilisés pour [déterminer la vue à utiliser à
chaque accès au document][cvdoc_choix].

Les contrôles de vues ont la possibilité d'avoir un [profil dynamique][dynprof]
en indiquant la famille dans l'attribut "dynamique\famille" (`dpdoc_famid`).
Dans ce cas, ce sont les valeurs des attributs du document associé qui seront
utilisées pour vérifier les droits d'accès aux vues.

## Exemple {#core-ref:859adcf5-5311-49bd-b26f-d2e694bc89a1}

| Id vues |     Label      |     Type     |    Zone   |      Masque     | Ordre | Affichable |
| ------- | -------------- | ------------ | --------- | --------------- | ----- | ---------- |
| VueA    | Administration | Consultation |           | Masque admin    |     1 | non        |
| VueB    | Impression     | Consultation | TST:MYIMP |                 |       | oui        |
| VueC    | Avis           | Édition      |           | Masque avis     |       | non        |
| VueD    | Notations      | Consultation |           | Masque notation |     2 | non        |

Ce contrôle de vue déclare quatre vues. Il dispose de quatre droits
spécifiques :  `VueA`, `VueB`, `VueC` et `VueD`.

Avec le profil suivant :

|     Compte    |               VueA              |               VueB              |               VueC              |               VueD              |
| ------------- | :-----------------------------: | :-----------------------------: | :-----------------------------: | :-----------------------------: |
| MY_FIRSTROLE  | <span class="aclgreen">X</span> | <span class="aclgreen">X</span> |                                 |                                 |
| MY_SECONDROLE |                                 | <span class="aclgreen">X</span> | <span class="aclgreen">X</span> | <span class="aclgreen">X</span> |

*   Les utilisateurs ayant le rôle `MY_FIRSTROLE` auront accès aux vues `VueA`
    et `VueB`.
*   Les utilisateurs ayant le rôle `MY_SECONDROLE` auront accès aux vues `VueB`,
    `VueC` et `VueD`.
*   Les utilisateurs ayant les deux rôles auront accès à toutes les vues.
    Cependant ces utilisateurs ne pourront pas accéder à la vue `VueD` par
    l'interface standard car l'ordre de cette dernière est supérieure à l'ordre
    de la `VueA` et elle est non-affichable.

Synthèse des vues en fonction des rôles :

|             Rôles             | Vue par défaut consultation | Vue par défaut de modification | Autres vues accessibles |
| ----------------------------- | :-------------------------: | :----------------------------: | :---------------------: |
| MY_FIRSTROLE                  |             VueA            |            Standard            |           VueB          |
| MY_SECONDROLE                 |             VueD            |              VueC              |           VueB          |
| MY_FIRSTROLE et MY_SECONDROLE |             VueA            |              VueC              |        VueB, VueD       |

Pour l'importation de droits sur un contrôle de vue, les noms des vues sont
utilisés pour référencer les droits spécifiques :

|            | Identifiant du profil |  /  | Option |       Droit       |              Droit               |       Droit        |       Droit        |
| ---------- | --------------------- | --- | ------ | ----------------- | -------------------------------- | ------------------ | ------------------ |
| __PROFIL__ | MY_VIEWCONTROL        |     | RESET  | VueA=MY_FIRSTROLE | VueB=MY_FIRSTROLE, MY_SECONDROLE | VueC=MY_SECONDROLE | VueD=MY_SECONDROLE |




<!-- links -->
[cvdoc]:            #core-ref:017f061a-7c12-42f8-aa9b-276cf706e7e0
[dynprof]:          #core-ref:bc24834a-b380-4681-ae94-08b93076a7e8
[profil_dedie]:     #core-ref:25c54b68-9cc1-44ea-b203-e289bde65a12
[cvdoc_choix]:      #core-ref:b74b3617-2085-47f8-9172-9f35c0290b5a