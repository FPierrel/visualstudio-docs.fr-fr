---
title: Insérer des commentaires de documentation XML dans Visual Studio
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: e3c38e46a5c73d1f8018f56f76b971939ba8c316
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31945426"
---
# <a name="how-to-insert-xml-comments-for-documentation-generation"></a>Guide pratique pour insérer des commentaires XML pour la génération de documentation

Visual Studio peut vous aider à documenter des éléments de code, comme les classes et les méthodes, en générant automatiquement la structure de commentaire de documentation XML standard. Au moment de la compilation, vous pouvez générer un fichier XML qui contient les commentaires de documentation. Le fichier XML généré par le compilateur peut être distribué avec votre assembly .NET pour permettre à Visual Studio et à d’autres IDE d’utiliser IntelliSense pour afficher des informations rapides concernant les types et les membres. De plus, le fichier XML peut être exécuté par l’intermédiaire d’outils tels que [DocFX](https://dotnet.github.io/docfx/) et [Sandcastle](https://www.microsoft.com/download/details.aspx?id=10526) pour générer des sites web de références d’API.

> [!NOTE]
> La commande **Insérer un commentaire** qui insère automatiquement des commentaires de documentation XML est disponible en [C#](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments) et en [Visual Basic](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation). Toutefois, vous pouvez insérer manuellement des [commentaires de documentation XML dans des fichiers C++](/cpp/ide/xml-documentation-visual-cpp) et générer des fichiers de documentation XML au moment de la compilation.

## <a name="to-insert-xml-comments-for-a-code-element"></a>Pour insérer des commentaires XML pour un élément de code

1. Placez votre curseur sur l’élément que vous souhaitez documenter, par exemple, une méthode.

1. Effectuez l’une des opérations suivantes :

   - Tapez `///` en C# ou `'''` en Visual Basic.

   - Dans le menu **Edition**, choisissez **IntelliSense** > **Insérer un commentaire**.

   - Dans le menu contextuel (clic droit) ou juste au-dessus de l’élément de code, choisissez **Extrait** > **Insérer un commentaire**.

   Le modèle XML est généré immédiatement au-dessus de l’élément de code. Par exemple, quand vous commentez une méthode, il génère l’élément **\<summary\>**, un élément **\<param\>** pour chaque paramètre et un élément **\<returns\>** pour documenter la valeur de retour.

   ![Modèle de commentaire XML (C#)](media/doc-preview-cs.png)

   ![Modèle de commentaire XML (Visual Basic)](media/doc-preview-vb.png)

1. Entrez la description de chaque élément XML pour documenter entièrement l’élément de code.

   ![Commentaire terminé](media/doc-result-cs.png)

> [!NOTE]
> Une [option](../../ide/reference/options-text-editor-csharp-advanced.md) permet d’activer et de désactiver les commentaires de documentation XML après la saisie des caractères `///` en C# ou `'''` en Visual Basic. Dans la barre de menus, choisissez **Outils** > **Options** pour ouvrir la boîte de dialogue **Options**. Ensuite, accédez à **Éditeur de texte** > **C#** ou **Basic** > **Avancé**. Dans la section **Aide sur l’éditeur**, recherchez l’option **Générer des commentaires sur la documentation XML**.

## <a name="see-also"></a>Voir aussi

- [Commentaires de documentation XML (Guide de programmation C#)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [Documentation de votre code avec des commentaires XML (Guide C#)](/dotnet/csharp/codedoc)
- [Guide pratique pour créer une documentation XML (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation)
- [Commentaires en C++](/cpp/cpp/comments-cpp)
- [Documentation XML (C++)](/cpp/ide/xml-documentation-visual-cpp)
- [Génération de code](../code-generation-in-visual-studio.md)