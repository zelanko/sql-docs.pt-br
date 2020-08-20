---
description: SQLGetDescField e SQLGetDescRec (Biblioteca de cursores)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f13b3ff5ed7e54a127089b74b5a45081900edf55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494746"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField e SQLGetDescRec (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso das funções **SQLGetDescField** e **SQLGetDescRec** na biblioteca de cursores. Para obter informações gerais sobre essas funções, consulte [função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) e [função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md).  
  
 A biblioteca de cursores executa **SQLGetDescRec** para retornar metadados para colunas de indicador. A biblioteca de cursores executa **SQLGetDescField** para retornar os mesmos campos retornados por **SQLGetDescRec**, que são SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_NULLABLE. Para consistência, o **SQLGetDescField** também retorna SQL_DESC_UNNAMED.  
  
 A biblioteca de cursores executa **SQLGetDescField** quando é chamada para retornar o valor dos campos a seguir que são definidos para as colunas de indicador de associação: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_LENGTH.  
  
 A biblioteca de cursores executa **SQLGetDescField** quando é chamada para retornar o valor do SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE ou SQL_DESC_ROW_STATUS_PTR campo. Esses campos podem ser retornados para qualquer linha, não apenas para a linha de indicador.  
  
 Se um aplicativo chamar **SQLGetDescField** para retornar o valor de qualquer campo diferente daqueles mencionados anteriormente, a biblioteca de cursores passará a chamada para o driver.
