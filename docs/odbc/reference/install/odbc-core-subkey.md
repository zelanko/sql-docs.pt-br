---
description: Subchave do núcleo ODBC
title: Subchave ODBC Core | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37948c46d6a717975902bc2109ece2aea02b0129
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499731"
---
# <a name="odbc-core-subkey"></a>Subchave do núcleo ODBC
O valor na subchave ODBC core fornece a contagem de uso para os componentes principais (Gerenciador de driver, biblioteca de cursores, DLL do instalador e assim por diante). O formato desse valor é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*contagem*|  
  
 Por exemplo, suponha que os componentes do ODBC Core tenham sido instalados pelos programas de instalação para três aplicativos diferentes e dois drivers diferentes. O valor na subchave ODBC Core seria:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
