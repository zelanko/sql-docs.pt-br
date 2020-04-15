---
title: SQLGetDescField e SQLGetDescRec (Biblioteca cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ceea6b6180e1b51f2f103f74412c3e2b4cbe02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307827"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField e SQLGetDescRec (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso das funções **SQLGetDescField** e **SQLGetDescRec** na biblioteca do cursor. Para obter informações gerais sobre essas funções, consulte [SQLGetDescField Function](../../../odbc/reference/syntax/sqlgetdescfield-function.md) e [SQLGetDescRec Function](../../../odbc/reference/syntax/sqlgetdescrec-function.md).  
  
 A biblioteca do cursor executa **o SQLGetDescRec** para retornar metadados para colunas de marcadores. A biblioteca do cursor executa **o SQLGetDescField** para retornar os mesmos campos retornados pelo **SQLGetDescRec**, que são SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_NULLABLE. Para obter consistência, **sqlGetDescField** também retorna SQL_DESC_UNNAMED.  
  
 A biblioteca do cursor executa **o SQLGetDescField** quando é chamada para devolver o valor dos seguintes campos definidos para colunas de marcadores de vinculação: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_LENGTH.  
  
 A biblioteca do cursor executa **o SQLGetDescField** quando é chamado para devolver o valor do campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE ou SQL_DESC_ROW_STATUS_PTR. Esses campos podem ser devolvidos para qualquer linha, não apenas a linha de marcadores.  
  
 Se um aplicativo chamar **o SQLGetDescField** para devolver o valor de qualquer campo diferente dos mencionados anteriormente, a biblioteca do cursor passa a chamada para o driver.
