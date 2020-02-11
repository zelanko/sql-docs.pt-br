---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 62fb1b89299af1f466e446c8adba422a841f0196
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923021"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Referenciar as bibliotecas ADO em um aplicativo do Visual C++
Para usar a versão mais recente do ADO em um aplicativo Visual C++, use a `#import` seguinte diretiva:  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Para usar o ADO MD ou o ADOX, você deve importar *msadomd. dll* ou *msadox. dll*usando a sintaxe acima.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Para usar qualquer versão anterior do ADO, substitua *MsADO15. dll* acima por uma das bibliotecas de tipos a seguir.  
  
-   *msado27. tlb*, biblioteca de tipos ADO 2,7  
  
-   *msado26. tlb*, biblioteca de tipos ADO 2,6  
  
-   *msado25. tlb*, biblioteca de tipos ADO 2,5  
  
-   *msado21. tlb*, biblioteca de tipos ADO 2,1  
  
-   *msado20. tlb*, biblioteca de tipos ADO 2,0
