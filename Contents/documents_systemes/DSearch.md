# Recherche détaillée {#core-ref:30aa8d0d-c80b-426f-b129-b4e99c688bcc}

## Présentation {#core-ref:0b575fa6-bd76-4d7f-a5b3-ee20bb63bc00}

La recherche détaillée permet d'exprimer des critères de recherche avancés
portant sur les attributs des documents, ainsi que sur l'état des documents
soumis à un cycle de vie.

Elle est implémentée au moyen de la famille `DSEARCH`, qui étend la famille
`SEARCH` et y ajoute les méthodes du fichier `Method.DetailSearch.php`.

## Éléments de paramétrage {#core-ref:de8a1440-fb42-4ad0-b041-5c762b5258d9}

Cette famille permet de rechercher les documents en spécifiant :

*   une famille
    *   avec ou sans ses sous-familles
*   les révisions dans lesquelles chercher
    Prenons par exemple un document avec les révisions suivantes :
    
        rev1 → rev2 → rev3 ⇢ revC
    
    Les choix possibles sont :
    
    courante
    :   permet de ne rechercher que dans les révisions
        courantes des documents (Ex. : recherche sur *revC*).
    
    toutes les révisions
    :   permet de rechercher dans toutes les révisions 
        des documents (Ex. : recherche sur *rev1, rev2, rev3, revC*).
    
    dernière révision
    :   permet de ne rechercher que dans les dernières 
        révisions des documents (Ex. : recherche sur *rev3*).
    
    sans la courante
    :   permet de rechercher dans toutes les révisions 
        sauf la courante (Ex. : recherche sur *rev1, rev2, rev3*).
    
    dernière parmi les révisions effectuées
    :   permet de rechercher dans toutes les révisions 
        (sauf la courante) des documents mais de ne retourner que la 
        dernière des révision des documents qui correspond aux critères 
        (Ex. : recherche sur *rev1, rev2, rev3*, 
        mais ne retourne que *rev3*).
*   une restriction aux documents
    *   modifiables par l'utilisateur
    *   supprimables par l'utilisateur
*   un ensemble de critères
    *   portant sur
        *   les attributs de la famille sélectionnée,
            
            La recherche par attributs se fait au moyen des colonnes
            
            attributs
            :   permet de sélectionner l'attribut qui servira de critère de recherche.
            
            fonctions
            :   permet de sélectionner l'opération de comparaison
                qui sera appliquée sur l'attribut.
                Le sélecteur de fonction dépend du type de l'attribut.
            
            *mot-clefs*
            :   permet de spécifier la valeur de référence de la comparaison.
                Le sélecteur de mot-clefs varie en fonction du type d'attribut 
                et de la fonction sélectionnée.
                
                Par exemple, pour les attributs de type énuméré il présentera 
                la liste des choix possibles ;
                alors que pour les attributs de type texte,
                il présentera un champ libre de saisie de texte.
            
            *Opt*
            :   permet de saisir un mot-clefs qui ne soit pas statique 
                mais qui résulte de l'évaluation d'une méthode documentaire. 
                Cela permet par exemple d'exprimer une valeur 
                qui soit la date courante (avec la méthode "::getDate()").
        
        *   les états du workflow associé à la famille sélectionnée
            
            Le critère *état* ne concerne que les documents figés.
            
            Ce critère *état* n'est pas accessible avec l'option 
            révision *courante*
            
            La recherche par état se fait au moyen des colonnes
            
            attributs
            :   La colonne "attributs" ne peut pas être modifiée,
                et est positionnée sur "état" pour indiquer que ce critère
                est un critère sur l'état des documents.
            
            fonctions
            :   présente la liste des opérateurs de comparaison supportés 
                par les états.
            
            mot-clefs
            :   La colonne "mot-clefs" présente la liste des états possibles 
                du cycle de vie, et permet de sélectionner l'état de référence 
                pour la comparaison.
        
        *   Les activités du workflow associé à la famille sélectionnée
            
            Le critère "activité" ne concerne que les documents en dernière révision.
            
            Ce critère n'est accessible qu'avec les options
            révision *courante* et *toutes les révisions*.
            
            La recherche par activité se fait au moyen des colonnes
            
            attributs
            :   La colonne "attributs" ne peut pas être modifiée,
                et est positionnée sur "activité" pour indiquer que ce critère
                est un critère sur l'activité des documents.
            
            fonctions
            :   présente la liste des opérateurs de comparaison supportés 
                par les activités.
            
            mot-clefs
            :   présente la liste des activités possibles du cycle de vie, 
                et permet de sélectionner l'activité de référence 
                pour la comparaison.
                
                Attention, si le cycle de vie ne décrit pas d'activités 
                pour une étape, ce sera la libellé de l'état qui sera affiché.
                Cette notation reste cohérente avec ce qui est écrit 
                dans les entêtes des documents.
    
    *   avec parenthésage
    *   avec possibilité de combiner des opérateurs
        *   AND
        *   OR