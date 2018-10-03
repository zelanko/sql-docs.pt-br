---
title: Referenciando as bibliotecas ADO em um aplicativo do Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
manager: craigg
ms.openlocfilehash: fa07fc475d423cf4c338d40393c053d1dc30d488
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601984"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Referenciar as bibliotecas ADO em um aplicativo do Visual C++
Para usar a versão mais recente do ADO em um aplicativo do Visual C++, use o seguinte `#import` diretiva:  
  
```  
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Para usar o ADO MD ou ADOX, você deve importar *msadomd.dll* ou *msadox.dll*, usando a sintaxe acima.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Para usar qualquer versão anterior do ADO, substitua *msado15.dll* acima com uma das bibliotecas de tipo a seguir.  
  
-   *msado27.tlb*, biblioteca de tipos de 2,7 do ADO  
  
-   *msado26.tlb*, biblioteca de tipos de 2,6 do ADO  
  
-   *msado25.tlb*, biblioteca de tipos de 2,5 do ADO  
  
-   *msado21.tlb*, biblioteca de tipos 2.1 de ADO  
  
-   *msado20.tlb*, biblioteca de tipos de 2.0 do ADO
