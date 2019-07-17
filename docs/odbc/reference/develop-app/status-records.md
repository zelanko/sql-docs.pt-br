---
title: Registros de status | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6ed360c39b87efe851bcbbb5c60762288ea1719
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114276"
---
# <a name="status-records"></a>Registros de status
Os campos dos registros de status contêm informações sobre erros ou avisos retornados pela fonte de dados, driver ou Gerenciador de Driver, incluindo o SQLSTATE, número do erro nativo, mensagem de diagnóstico, número da coluna e o número de linha específicos. Registros de status podem ser criados somente se a função retornar SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA ou SQL_STILL_EXECUTING. Para obter uma lista completa dos campos dos registros de status, consulte a [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descrição da função.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Sequência de registros de status](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md)
