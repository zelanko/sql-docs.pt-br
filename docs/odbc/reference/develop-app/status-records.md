---
title: Registros de Status | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4afef16137404fcdfd3e1d328642f1d314829538
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301367"
---
# <a name="status-records"></a>Registros de status
Os campos nos registros de status contêm informações sobre erros ou avisos específicos retornados pelo Driver Manager, driver ou fonte de dados, incluindo o SQLSTATE, número de erro nativo, mensagem de diagnóstico, número da coluna e número da linha. Os registros de status só podem ser criados se a função retornar SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA ou SQL_STILL_EXECUTING. Para obter uma lista completa de campos nos registros de status, consulte a descrição da função [SQLGetDiagField.](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Sequência de registros de status](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md)
