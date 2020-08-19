---
description: Referenciar as bibliotecas ADO em um aplicativo do Visual C++
title: Referenciando as bibliotecas ADO em um aplicativo Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
author: rothja
ms.author: jroth
ms.openlocfilehash: d71a56b6cb09924e106b62ed5bbca542cf9e797f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452358"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Referenciar as bibliotecas ADO em um aplicativo do Visual C++
Para usar a versão mais recente do ADO em um aplicativo Visual C++, use a seguinte `#import` diretiva:  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Para usar o ADO MD ou o ADOX, você deve importar *msadomd.dll* ou *msadox.dll*usando a sintaxe acima.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Para usar qualquer versão anterior do ADO, substitua *msado15.dll* acima por uma das bibliotecas de tipos a seguir.  
  
-   *msado27. tlb*, biblioteca de tipos ADO 2,7  
  
-   *msado26. tlb*, biblioteca de tipos ADO 2,6  
  
-   *msado25. tlb*, biblioteca de tipos ADO 2,5  
  
-   *msado21. tlb*, biblioteca de tipos ADO 2,1  
  
-   *msado20. tlb*, biblioteca de tipos ADO 2,0
