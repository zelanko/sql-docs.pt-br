---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b390df48e676290696ae8080c8f671fd0e37bad8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727714"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField e SQLSetDescRec (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetDescField** e **SQLSetDescRec** funções na biblioteca do cursor. Para obter informações gerais sobre essas funções, consulte [função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) e [função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 Executa a biblioteca de cursores **SQLSetDescField** quando ele é chamado para retornar o valor dos campos definido para colunas de indicadores:  
  
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
  
 Ao trabalhar com um ODBC 2. *x* driver, a biblioteca de cursores retornará SQLSTATE HY090 (comprimento inválido de buffer ou cadeia de caracteres) quando **SQLSetDescField** ou **SQLSetDescRec** é chamado para definir o SQL_DESC_OCTET_ Campo de comprimento para o registro de indicador de um descartar como um valor não é igual a 4. Ao trabalhar com um ODBC 3 *. x* driver, a biblioteca de cursores permite que o buffer para ser de qualquer tamanho.  
  
 Executa a biblioteca de cursores **SQLSetDescField** quando ele é chamado para retornar o valor do campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE ou SQL_DESC_ROW_STATUS_PTR. Esses campos podem ser retornados para qualquer linha, não apenas a linha do indicador.  
  
 A biblioteca de cursores não executará **SQLSetDescField** para alterar qualquer campo de descritor que não sejam os campos mencionados anteriormente. Se um aplicativo chamar **SQLSetDescField** para definir qualquer outro campo, enquanto a biblioteca de cursores é carregada, a chamada é passada para o driver.  
  
 A biblioteca de cursores dá suporte à alteração dos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR de qualquer linha de um descritor de linha de aplicativo dinamicamente (após uma chamada para **SQLExtendedFetch**, **SQLFetch**, ou **SQLFetchScroll**). O campo SQL_DESC_OCTET_LENGTH_PTR pode ser alterado para um ponteiro nulo apenas para desassociar o buffer de comprimento de uma coluna.  
  
 A biblioteca de cursores não oferece suporte para o campo SQL_DESC_BIND_TYPE um APD ou descartar a alteração quando um cursor é aberto. O campo SQL_DESC_BIND_TYPE pode ser alterado somente depois que o cursor será fechado e antes de um novo cursor é aberto. Os únicos campos de descritor que a biblioteca de cursores dá suporte à alteração quando um cursor é aberto são SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_ROWS_PROCESSED_ PTR.  
  
 A biblioteca de cursores não oferece suporte para modificar o campo SQL_DESC_COUNT de descartar o após **SQLExtendedFetch** ou **SQLFetchScroll** foi chamado e antes do cursor foi fechado.
