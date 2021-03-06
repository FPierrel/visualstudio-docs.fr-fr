---
title: Migrer d’inscription de classe COM du débogueur 64 bits | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 45cfcee6-7a68-4d4f-b3f6-e2d8a0fa066a
author: gregg-miskelly
ms.author: greggm
manager: douge
ms.workload:
- greggm
ms.openlocfilehash: 6c7578ddbdf84a1520a732fb64380bb53e5359f9
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39637849"
---
# <a name="migrate-64-bit-debugger-com-class-registration"></a>Migrer le débogueur 64 bits d’inscription de classe COM

Pour les extensions de débogueur qui s’inscrivent COM des classes dans HKEY_CLASSES_ROOT à l’aide de regsvr32, regasm ou écrit directement dans le Registre et chargé dans *msvsmon.exe* (le débogueur distant), il est maintenant possible de fournir ce inscription à msvsmon sans avoir à écrire dans HKEY_CLASSES_ROOT. Cela affecte les évaluateurs d’expression de débogueur .NET héritées ou les moteurs de débogage qui sont configurés pour se charger dans le *msvsmon.exe* processus.

## <a name="msvsmon-comclass-def"></a>msvsmon-comclass-def

Pour utiliser cette technique, ajoutez un  **.msvsmon-comclass-def.json* fichier en regard de msvsmon (InstallDir :* \Common7\IDE\Remote Debugger\x64*).

Voici un exemple de fichier msvsmon-comclass-def qui enregistre si elle est gérée et une classe native :

Nom de fichier : *MyCompany.MyExample.msvsmon-comclass-def.json*

```json
{
  "managedCOMClasses": [
    {
      "clsid": "{C9F48B25-36ED-4B22-8210-98BC5BE4D1E7}",
      "assemblyName": "MyCompany.MyAssembly",
      "className": "MyCompany.MyNamespace.MyClass"
    }
  ],
  "nativeCOMClasses": [
    {
      "clsid": "{42A476E9-8FA7-44D5-ADFE-216AD371EEC9}",
      "dllPath": "MyExample.dll"
    }
  ]
}
```
