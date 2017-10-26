---
title: "Subchave do núcleo ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad7a45f0f3272e1e2d7ae799ab1ca86bfb90b9be
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-core-subkey"></a>Subchave do núcleo ODBC
O valor na subchave núcleo de ODBC fornece a contagem de uso para os componentes principais (Gerenciador de Driver, biblioteca de cursores, instalador DLL e assim por diante). O formato desse valor é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*contagem*|  
  
 Por exemplo, suponha que os componentes principais do ODBC foram instalados, os programas de instalação para três aplicativos diferentes e dois drivers diferentes. O valor na subchave núcleo de ODBC seria:  
  
```  
UsageCount : REG_DWORD : 0x5  
```

