---
title: Tipo de cursor e combinações de simultaneidade | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9b963135f30169bdf6e145e4719115b2d805fa2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-type-and-concurrency-combinations"></a>Tipo de cursor e combinações de simultaneidade
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Tipos de cursor controlam a funcionalidade do cursor fornecido para o usuário. Opções de simultaneidade controlam a atualização e o comportamento de bloqueio de um conjunto de resultados.  
  
|Tipo de cursor|Simultaneidade (valores permitidos)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1] </sup> Consulte [limitações de uso de cursores controlados por conjuntos de chaves](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md).  
  
 <sup>[2] </sup> SQL_CONCUR_LOCK é suportado apenas quando a opção de conexão SQL_AUTOCOMMIT é definida como SQL_AUTOCOMMIT_OFF.  
  
## <a name="see-also"></a>Consulte também  
 [Opções de conexão](../../odbc/microsoft/connect-options.md)
