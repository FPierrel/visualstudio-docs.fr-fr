---
title: "Linting de code R avec Outils R pour Visual Studio | Microsoft Docs"
ms.custom: 
ms.date: 12/04/2017
ms.reviewer: 
ms.suite: 
ms.technology: devlang-r
ms.devlang: r
ms.tgt_pltfrm: 
f1_keywords: vs.toolsoptionspages.text_editor.r.lint
ms.topic: article
caps.latest.revision: "1"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.workload: data-science
ms.openlocfilehash: 76f4ceb040e62e4ebac46e8a791f5dac0d73aff5
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="linting-r-code-in-visual-studio"></a>Linting de code R dans Visual Studio

Le linting (ou vérification lint) est un processus qui analyse le code pour révéler des erreurs potentielles, ainsi que des problèmes de mise en forme et d’autres parasites dans les fichiers de code (comme un faux espace blanc). Le linting contribue aussi à encourager certaines conventions de codage, comme la manière dont les identificateurs sont nommés, ce qui s’avère très utile au sein des équipes et dans d’autres situations de collaboration.

Outils R pour Visual Studio (RTVS) fournit un linting intégré pour R, dont le comportement est contrôlé par le biais de diverses options. Ces options sont trouvent dans **Outils > Options > Éditeur de texte > R > Lint**.

Le linting est désactivé par défaut. Pour activer le linting, affectez à l’option **Tout > Activer lint** la valeur true. Les sections qui suivent dans cette rubrique décrivent toutes les autres options de linting :

Quand il est activé, le linting s’applique dans l’éditeur pendant la frappe. Les problèmes sont signalés par des lignes ondulées vertes. Dans le graphique suivant, par exemple, RTVS a identifié six problèmes de linting, notamment l’utilisation de `=` au lieu de `<-` pour une assignation, un manque d’espace autour d’arguments de fonction, l’utilisation de la casse Pascal et d’identificateurs en majuscules, ainsi que l’utilisation d’un point-virgule. Pointez le curseur sur un problème pour afficher une description.

![Exemples de linting pour du code R](media/linting-01.png)

## <a name="assignment-group"></a>Groupe d’assignation

| Option | Valeur par défaut | Effet de linting |
| --- | --- | --- |
| Appliquer \<- | `True` | Détecte si `<-` n’est pas utilisé pour l’assignation. |

## <a name="naming-group"></a>Groupe de nommage

Ces options marquent des identificateurs qui utilisent des conventions de nommage différentes :

| Option | Valeur par défaut | Effet de linting |
| --- | --- | --- |
| Marquer la casse mixte | `False` | Marque les identificateurs qui utilisent une casse mixte. |
| Marquer les noms longs | `False` | Marque les identificateurs dont le nom dépasse le paramètre « Longueur maximale de nom ». |
| Marquer plusieurs points | `True` | Marque les identificateurs qui utilisent plusieurs points. |
| Marquer la casse Pascal | `True` | Marque les identificateurs qui utilisent la casse Pascal. |
| Marquer les mots séparés par des tirets | `False` | Marque les identificateurs qui utilisent des traits de soulignements. |
| Marquer les majuscules | `True` | Marque les identificateurs qui n’utilisent que des majuscules. |
| Longueur maximale de nom | 32 | Longueur appliquée avec le paramètre « Marquer les noms longs ». |

## <a name="spacing-group"></a>Groupe d’espacement

Ces options, qui ont toutes la valeur `True` par défaut, contrôlent l’endroit où le linting identifie les problèmes d’espacement : après les noms de fonctions, autour des virgules, autour des opérateurs, aux positions des accolades ouvrantes et fermantes, à l’espace précédent ( et à l’espace à l’intérieur de ().

## <a name="statements-group"></a>Groupe d’instructions

| Option | Valeur par défaut | Effet de linting |
| --- | --- | --- |
| Multiple | `True` | Détecte si plusieurs instructions sont sur la même ligne. |
| Points-virgules | `True` | Identifie les utilisations de points-virgules. |

## <a name="text-group"></a>Groupe de texte

| Option | Valeur par défaut | Effet de linting |
| --- | --- | --- |
| Longueur limite de ligne | `False` | Définit si le linting marque les lignes plus longues que la valeur de l’option « Longueur maximale de ligne ». |
| Longueur maximale de ligne | 80 | Définit la longueur de ligne appliquée par l’option « Longueur limite de ligne ». |

## <a name="whitespace-group"></a>Groupe d’espaces blancs

Ces options, qui ont toutes la valeur `True` par défaut, contrôlent l’endroit où le linting identifie les problèmes d’espace blanc : utilisation de tabulations, utilisation de guillemets doubles, lignes vides de fin et espace blanc de fin.