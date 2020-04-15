---
title: Subchave do Núcleo ODBC | Microsoft Docs
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
ms.openlocfilehash: 9e6bfcf3c1efa87076e6d3e27a438cde6f794157
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304047"
---
# <a name="odbc-core-subkey"></a>Subchave do núcleo ODBC
O valor sob a subchave ODBC Core fornece a contagem de uso para os componentes principais (Driver Manager, biblioteca de cursor, instalador DLL e assim por diante). O formato deste valor é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|Contagem de usos|REG_DWORD|*contagem*|  
  
 Por exemplo, suponha que os componentes do Núcleo ODBC tenham sido instalados pelos programas de configuração para três aplicativos diferentes e dois drivers diferentes. O valor sob a subchave Do Núcleo ODBC seria:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
