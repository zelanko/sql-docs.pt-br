---
title: "Endereço do Buffer de dados | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 726505eca506b437cbf728d0821ef99ef7d90aea
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="data-buffer-address"></a>Endereço do Buffer de dados
O aplicativo passa o endereço do buffer de dados para o driver em um argumento, geralmente denominado *ValuePtr* ou um nome semelhante. Por exemplo, na seguinte chamada para **SQLBindCol**, o aplicativo especifica o endereço do *data* variável:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Conforme mencionado no [Allocating e liberar Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) seção, o endereço de um buffer adiado deve permanecer válido até que o buffer é desassociado.  
  
 A menos que especificamente é proibido, o endereço de um buffer de dados pode ser um ponteiro nulo. Para buffers usados para enviar dados para o driver, isso faz com que o driver ignorar as informações normalmente contidas no buffer. Para buffers usados para recuperar dados do driver, isso faz com que o driver não retornar um valor. Em ambos os casos, o driver ignorará o argumento de comprimento de buffer de dados correspondente.
