---
description: SQLSetDescField e SQLSetDescRec (Biblioteca de cursores)
title: SQLSetDescField e SQLSetDescRec (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cef4967a81a78e08dee733072359459c864b9627
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476938"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField e SQLSetDescRec (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso das funções **SQLSetDescField** e **SQLSetDescRec** na biblioteca de cursores. Para obter informações gerais sobre essas funções, consulte [função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) e [função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 A biblioteca de cursores executa **SQLSetDescField** quando é chamada para retornar o valor dos campos definidos para colunas de indicador:  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_DATETIME_INTERVAL_CODE  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_NAME  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_NULLABLE  
  
 A biblioteca de cursores executa chamadas para **SQLSetDescRec** para uma coluna de indicador.  
  
 Ao trabalhar com um driver ODBC *2. x* , a biblioteca de cursores retorna SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido) quando **SQLSetDescField** ou **SQLSetDescRec** é chamado para definir o campo de SQL_DESC_OCTET_LENGTH para o registro de indicador de um ARD para um valor diferente de 4. Ao trabalhar com um driver ODBC *3. x* , a biblioteca de cursores permite que o buffer seja de qualquer tamanho.  
  
 A biblioteca de cursores executa **SQLSetDescField** quando é chamada para retornar o valor do SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE ou SQL_DESC_ROW_STATUS_PTR campo. Esses campos podem ser retornados para qualquer linha, não apenas para a linha de indicador.  
  
 A biblioteca de cursores não executa **SQLSetDescField** para alterar qualquer campo de descritor diferente dos campos mencionados anteriormente. Se um aplicativo chamar **SQLSetDescField** para definir qualquer outro campo enquanto a biblioteca de cursores for carregada, a chamada será passada para o driver.  
  
 A biblioteca de cursores dá suporte à alteração dos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR de qualquer linha de um descritor de linha de aplicativo dinamicamente (após uma chamada para **SQLExtendedFetch**, **SQLFetch**ou **SQLFetchScroll**). O campo SQL_DESC_OCTET_LENGTH_PTR pode ser alterado para um ponteiro nulo somente para desassociar o buffer de comprimento de uma coluna.  
  
 A biblioteca de cursores não dá suporte à alteração do campo SQL_DESC_BIND_TYPE em um APD ou ARD quando um cursor está aberto. O campo SQL_DESC_BIND_TYPE só pode ser alterado depois que o cursor é fechado e antes de um novo cursor ser aberto. Os únicos campos de descritor que a biblioteca de cursores dá suporte à alteração quando um cursor é aberto são SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_ROWS_PROCESSED_PTR.  
  
 A biblioteca de cursores não dá suporte à modificação do campo SQL_DESC_COUNT do ARD depois que **SQLExtendedFetch** ou **SQLFetchScroll** tiver sido chamado e antes do cursor ser fechado.
