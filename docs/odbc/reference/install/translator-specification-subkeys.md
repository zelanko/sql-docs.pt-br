---
description: Subchaves de especificação do conversor
title: Subchaves de especificação do Tradutor | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c02317c8abe12dbc693cdf7b715b6de84e5bc631
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461288"
---
# <a name="translator-specification-subkeys"></a>Subchaves de especificação do conversor
Cada tradutor listado na subchave de conversores ODBC tem uma subchave própria. Essa subchave tem o mesmo nome que o valor correspondente na subchave de conversores ODBC. Os valores nessa subchave listam os caminhos completos das DLLs de instalação do tradutor e do tradutor e a contagem de uso. Os formatos dos valores são mostrados na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|Tradutor|REG_SZ|*Tradutor-DLL-caminho*|  
|Instalação|REG_SZ|*Instalação-DLL-caminho*|  
|UsageCount|REG_DWORD|*contagem*|  
  
 Para obter informações sobre contagens de uso, consulte [contagem de uso](../../../odbc/reference/install/usage-counting.md) anteriormente nesta seção.  
  
 Os aplicativos não devem definir a contagem de uso. O ODBC manterá essa contagem.  
  
 Por exemplo, suponha que o tradutor de página de código da Microsoft tenha uma DLL de tradução chamada Mscpxl32.dll, que as funções de instalação do tradutor estejam na mesma DLL e que o tradutor tenha sido instalado três vezes. Os valores na subchave do tradutor de página de código da Microsoft podem ser os seguintes:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
