---
title: Subchave do núcleo ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
ms.openlocfilehash: cf8e143a8d5d329fe3eb68185a3ebdf8f7f6cd6b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
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
