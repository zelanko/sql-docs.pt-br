---
title: Registros de status | Microsoft Docs
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
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b8a5cc55bacf76b8bf7d0e9b35a4e7a4daa9439
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="status-records"></a>Registros de status
Os campos dos registros de status contêm informações sobre erros ou avisos retornados, o Gerenciador de Driver, driver ou fonte de dados, incluindo o SQLSTATE, número de erro nativo, mensagem de diagnóstico, número da coluna e o número de linha específicos. Registros de status podem ser criados somente se a função retornará SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA ou SQL_STILL_EXECUTING. Para obter uma lista completa dos campos dos registros de status, consulte o [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrição da função.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Sequência de registros de status](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md)
