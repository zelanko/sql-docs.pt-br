---
title: Fazer referência às bibliotecas do ADO em um aplicativo Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9003a9ac341663127a4b337a1313a50f67d1fe5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Fazer referência às bibliotecas do ADO em um aplicativo do Visual C++
Para usar a versão mais recente do ADO em um aplicativo do Visual C++, use a seguinte `#import` diretiva:  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Para usar o ADO MD ou ADOX, você deve importar *msadomd.dll* ou *msadox.dll*, usando a sintaxe acima.  
  
## <a name="backward-compatibility"></a>Compatibilidade com versões anteriores  
 Para usar uma versão anterior do ADO, substitua *msado15.dll* acima com uma das bibliotecas de tipo a seguir.  
  
-   *msado27.tlb*, biblioteca de tipos 2.7 de ADO  
  
-   *msado26.tlb*, ADO 2.6 do tipo biblioteca  
  
-   *msado25.tlb*, biblioteca de tipos de 2,5 de ADO  
  
-   *msado21.tlb*, biblioteca de tipos 2.1 de ADO  
  
-   *msado20.tlb*, biblioteca de tipos 2.0 de ADO
