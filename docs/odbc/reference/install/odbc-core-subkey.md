---
title: Subchave do núcleo ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f05e36c59d674104dead92ecd7da63f5fb58588a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
