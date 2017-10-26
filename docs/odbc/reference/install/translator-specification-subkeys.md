---
title: "Conversor especificação subchaves | Microsoft Docs"
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
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62bfe54f5bd5117fee5d9ba063f1882be47ccbc4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="translator-specification-subkeys"></a>Conversor especificação subchaves
Tradutor listado na subchave conversor ODBC tem uma subchave de seu próprio. Essa subchave tem o mesmo nome que o valor correspondente na subchave conversor ODBC. Os valores sob essa subchave listam os caminhos completos do conversor e instalação de conversor DLLs e a contagem de uso. Os formatos dos valores são conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|Translator|REG_SZ|*caminho de DLL do conversor*|  
|Instalação|REG_SZ|*caminho da DLL de instalação*|  
|UsageCount|REG_DWORD|*contagem*|  
  
 Para obter informações sobre contagens de uso, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md) anteriormente nesta seção.  
  
 Aplicativos não devem definir a contagem de uso. ODBC manterá essa contagem.  
  
 Por exemplo, suponha que a página de código Microsoft Translator tem uma DLL chamada Mscpxl32.dll, que as funções de instalação de conversor estão na mesma DLL, tradução e que o tradutor foi instalado três vezes. Os valores na subchave Microsoft Translator da página de código podem ser como segue:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```

