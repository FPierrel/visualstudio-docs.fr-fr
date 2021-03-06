---
title: 'CA2239 : Spécifiez des méthodes de désérialisation pour les champs facultatifs'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2239
- ProvideDeserializationMethodsForOptionalFields
helpviewer_keywords:
- ProvideDeserializationMethodsForOptionalFields
- CA2239
ms.assetid: 6480ff5e-0caa-4707-814e-2f927cdafef5
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 04d3e40c73a02c43ecfb13eda0abcfabcb0d3ad5
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31919867"
---
# <a name="ca2239-provide-deserialization-methods-for-optional-fields"></a>CA2239 : Spécifiez des méthodes de désérialisation pour les champs facultatifs
|||
|-|-|
|TypeName|ProvideDeserializationMethodsForOptionalFields|
|CheckId|CA2239|
|Category|Microsoft.Usage|
|Modification avec rupture|Sans rupture|

## <a name="cause"></a>Cause
 Un type a un champ qui est marqué avec la <xref:System.Runtime.Serialization.OptionalFieldAttribute?displayProperty=fullName> attribut et le type ne fournit pas de méthodes de gestion des événements de désérialisation.

## <a name="rule-description"></a>Description de la règle
 Le <xref:System.Runtime.Serialization.OptionalFieldAttribute> attribut n’a aucun effet sur la sérialisation ; un champ marqué avec l’attribut est sérialisé. Toutefois, le champ est ignoré lors de la sérialisation de déduplication et conserve la valeur par défaut associée à son type. Gestionnaires d’événements de désérialisation doivent être déclarés pour définir le champ au cours du processus de désérialisation.

## <a name="how-to-fix-violations"></a>Comment corriger les violations
 Pour corriger une violation de cette règle, ajoutez des méthodes pour le type de gestion des événements de désérialisation.

## <a name="when-to-suppress-warnings"></a>Quand supprimer les avertissements
 Il est possible de supprimer un avertissement de cette règle si le champ doit être ignoré pendant le processus de désérialisation.

## <a name="example"></a>Exemple
 L’exemple suivant montre un type avec un champ facultatif et l’événement de désérialisation des méthodes de gestion.

 [!code-csharp[FxCop.Usage.OptionalFields#1](../code-quality/codesnippet/CSharp/ca2239-provide-deserialization-methods-for-optional-fields_1.cs)]
 [!code-vb[FxCop.Usage.OptionalFields#1](../code-quality/codesnippet/VisualBasic/ca2239-provide-deserialization-methods-for-optional-fields_1.vb)]

## <a name="related-rules"></a>Règles associées
 [CA2236 : Appelez les méthodes de la classe de base sur les types ISerializable](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240 : Implémentez ISerializable correctement](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229 : Implémentez des constructeurs de sérialisation](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238 : Implémentez les méthodes de sérialisation correctement](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235 : Marquez tous les champs non sérialisables](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237 : Marquez les types ISerializable avec SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2120 : Sécurisez les constructeurs de sérialisation](../code-quality/ca2120-secure-serialization-constructors.md)