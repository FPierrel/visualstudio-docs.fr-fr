---
title: Explorateur de schémas XML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 2fc39e98-b194-456b-a452-cfafb0a52d66
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 110cad9883cbb129368dac4d481443a9f5d9813c
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34751587"
---
# <a name="xml-schema-explorer"></a>Explorateur de schémas XML

Le **Explorateur de schémas XML** est intégré à Microsoft Visual Studio et l’éditeur XML pour vous permettre de travailler avec des schémas de langage (XSD XML) XML Schema definition. Lorsque vous ouvrez un fichier de schéma XML, le **jeu de schémas** nœud s’affiche dans le **Explorateur de schémas XML**. Tous les schémas inclus, importés ou redéfinis pour votre fichier cible, ainsi que tous les fichiers qui sont référencées par une `include` ou `import` instruction, apparaissent également dans le **Explorateur de schémas XML**.

 Le **Explorateur de schémas XML** vous permet d’effectuer les opérations suivantes :

-   obtenir une vue d'ensemble rapide du jeu de schémas ;

-   Parcourir et naviguer l'arborescence.

-   Effectuer des recherches par mot clé et spécifiques au schéma. Pour plus d’informations, consultez [recherche le jeu de schémas](../xml-tools/searching-the-schema-set.md).

-   Ajouter les résultats de recherche à la vue du graphique ou une vue de modèle de contenu

-   trier l’arborescence par ordre des documents, par type ou par nom ; Pour plus d’informations, consultez [tri, filtrage et de regroupement](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md).

-   ouvrir l'éditeur XML et accéder aux emplacements de code dans le fichier XSD ; Pour plus d’informations, consultez [intégration avec l’éditeur XML](../xml-tools/integration-with-xml-editor.md).

-   générer un exemple de code XML pour les éléments globaux.

Le **Explorateur de schémas XML** fournit une vue hiérarchique du jeu à travers une arborescence de schémas. Le **Explorateur de schémas XML** fournit également la recherche, le filtrage, navigation et tri. Pour accéder à la **Explorateur de schémas XML**, effectuez l’une des opérations suivantes :

-   Si vous êtes sur le [vue de départ](../xml-tools/start-view.md), cliquez sur le **Explorateur de schémas XML** lien.

-   Si vous êtes sur le [vue du graphique](../xml-tools/graph-view.md) ou [affichage du modèle de contenu](../xml-tools/content-model-view.md) et avoir des nœuds dans votre espace de travail, utilisez le menu contextuel pour sélectionner le **Explorateur de schémas XML**.

-   Vous pouvez également sélectionner le **Explorateur de schémas XML** à partir de la **vue** menu.

-   Vous pouvez accéder à la **Explorateur de schémas XML** à partir d’un *.vb* fichier ayant un littéral XML Visual Basic associé à un *.xsd* fichier. Pour afficher le schéma définis dans le **Explorateur de schémas XML**, cliquez sur un nœud XML dans un littéral XML ou une importation d’espace de noms XML et sélectionnez le **afficher dans l’Explorateur de schémas** commande. Pour plus d’informations, consultez [littéraux de l’intégration de XML avec l’Explorateur de schémas XML](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md).

## <a name="tree-view"></a>arborescence
 Le **Explorateur de schémas XML** affiche précompilé schéma définie les informations dans une structure arborescente. L’arborescence est organisée comme suit :

-   Au niveau supérieur se trouve le nœud de jeu de schémas.

-   Le deuxième niveau contient les espaces de noms.

-   Le troisième niveau contient les fichiers.

-   Le quatrième niveau contient les nœuds globaux. Ceci peut inclure les éléments, les groupes, les types complexes, les types simples, les attributs, les groupes d'attributs, et les instructions `include`, `import` et `redefine`.

Voici un exemple d’arborescence :

![Explorateur de schémas XML](../xml-tools/media/xmlschemaexplorer.gif)

## <a name="selection-and-activation"></a>Sélection et activation
 Pour mettre en surbrillance et sélectionner un nœud, cliquez une fois dans l'Explorateur de schémas.

 Pour activer un nœud, double-cliquez dessus ou appuyez sur **entrée** lorsque le nœud est sélectionné.

-   L'activation d'un nœud ouvre le fichier dans lequel ce nœud est défini (si le fichier n'est pas déjà ouvert) et sélectionne le nœud dans le fichier.

-   L'activation d'un nœud de fichier ouvre le fichier sélectionné (s'il n'est pas déjà ouvert) et met en surbrillance le nœud `<schema>`.

-   L'activation d'un jeu de schémas ou d'un nœud d'espace de noms n'aboutit à rien.

## <a name="drag-and-drop-nodes"></a>Nœuds par glisser- déposer
 Vous pouvez glisser et déposer des nœuds, des nœuds de fichier et des nœuds d’espace de noms par glisser-déposer dans une vue du concepteur XSD. Si la vue actuelle est la [vue de départ](../xml-tools/start-view.md), en faisant glisser un nœud sur la vue s’ouvre le [vue du graphique](../xml-tools/graph-view.md). Si la vue actuelle est la [affichage du modèle de contenu](../xml-tools/content-model-view.md) ou de la vue du graphique, la vue ne change pas lorsque vous supprimez un nœud sur celle-ci.

 Déplacer des fichiers sur la vue ajoutera tous les nœuds globaux dans le fichier pour le [espace de travail du concepteur XSD](../xml-tools/xml-schema-designer-workspace.md). Le dépôt d’espaces de noms sur la vue ajoute tous les nœuds globaux dans l’espace de noms à l’espace de travail. L'espace de travail est partagé entre toutes les vues.

 Vous ne pouvez pas faire glisser-déposer des importations ou des nœuds locaux.

## <a name="see-also"></a>Voir aussi

- [Comment : ajouter des nœuds à l’espace de travail à partir de l’Explorateur de schémas XML](../xml-tools/how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer.md)