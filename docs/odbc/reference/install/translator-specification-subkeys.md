---
title: Subchaves de especificação do conversor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3c5ad31437cf2639d6b8478d173c7522fa3e9fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618914"
---
# <a name="translator-specification-subkeys"></a>Subchaves de especificação do conversor
Cada tradução listada na subchave de conversores ODBC tem uma subchave de seu próprio. Essa subchave tem o mesmo nome que o valor correspondente sob a subchave de conversores ODBC. Os valores sob essa subchave listam os caminhos completos do tradutor e DLLs de instalação de tradução e a contagem de uso. Os formatos de valores são conforme mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|Translator|REG_SZ|*caminho de DLL de tradução*|  
|Instalação|REG_SZ|*caminho de DLL de instalação*|  
|UsageCount|REG_DWORD|*contagem*|  
  
 Para obter informações sobre contagens de uso, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md) anteriormente nesta seção.  
  
 Aplicativos não devem definir a contagem de uso. ODBC manterá essa contagem.  
  
 Por exemplo, suponha que a página de código do Microsoft Translator tem uma DLL denominada Mscpxl32.dll, que as funções de instalação do tradutor estão na mesma DLL, tradução e que o tradutor foi instalado três vezes. Os valores na subchave Microsoft Translator da página de código podem ser da seguinte maneira:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
