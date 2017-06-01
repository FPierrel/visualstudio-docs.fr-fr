---
title: "IActiveScriptParse::InitNew | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "windows-script-interfaces"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
apiname: IActiveScriptParse.InitNew
apilocation: scrobj.dll
helpviewer_keywords: 
  - "IActiveScriptParse_InitNew"
ms.assetid: 3a582bd6-fc0d-43a5-812f-5ea55a8517a1
caps.latest.revision: 7
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 7
---
# IActiveScriptParse::InitNew
Initialise le moteur de script.  
  
## Syntaxe  
  
```  
HRESULT InitNew(void);  
```  
  
## Valeur de retour  
 Retourne `S_OK` en cas de réussite, ou `E_FAIL` si une erreur se produit pendant l'initialisation.  
  
## Notes  
 Avant que le moteur de script puisse être utilisé, l'une des méthodes suivantes doit être appelée : `IPersist*::Load`, `IPersist*::InitNew`, ou `IActiveScriptParse::InitNew`.  La sémantique de cette méthode sont identiques à `IPersistStreamInit::InitNew`, du fait cette méthode indique le moteur de script s'initialiser.  Notez qu'il n'est pas valide pour appeler `IPersist*::InitNew` ou `IActiveScriptParse::InitNew` et `IPersist*::Load`, ni elle est valide pour appeler `IPersist*::InitNew`, `IActiveScriptParse::InitNew`, ou `IPersist*::Load` plusieurs fois.  
  
## Voir aussi  
 [IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)