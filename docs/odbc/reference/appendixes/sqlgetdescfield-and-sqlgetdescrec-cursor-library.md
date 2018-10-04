---
title: SQLGetDescField e SQLGetDescRec (biblioteca de cursores) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66361572427c3264a1b25fe1c851685a07b2e029
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765014"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField e SQLGetDescRec (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLGetDescField** e **SQLGetDescRec** funções na biblioteca do cursor. Para obter informações gerais sobre essas funções, consulte [função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) e [função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md).  
  
 Executa a biblioteca de cursores **SQLGetDescRec** para retornar metadados para colunas de indicador. Executa a biblioteca de cursores **SQLGetDescField** para retornar os mesmos campos retornados pela **SQLGetDescRec**, que são SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_ COMPRIMENTO, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_NULLABLE. Para manter a consistência, **SQLGetDescField** também retorna SQL_DESC_UNNAMED.  
  
 Executa a biblioteca de cursores **SQLGetDescField** quando ele é chamado para retornar o valor dos seguintes campos que são definidos para colunas de indicador de associação: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR, e SQL_DESC_LENGTH.  
  
 Executa a biblioteca de cursores **SQLGetDescField** quando ele é chamado para retornar o valor do campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE ou SQL_DESC_ROW_STATUS_PTR. Esses campos podem ser retornados para qualquer linha, não apenas a linha do indicador.  
  
 Se um aplicativo chamar **SQLGetDescField** para retornar o valor de qualquer campo que não sejam aquelas mencionadas anteriormente, a biblioteca de cursores passará a chamada para o driver.
