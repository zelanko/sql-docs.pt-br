---
title: SQLSetDescField e SQLSetDescRec (Biblioteca cursor) | Microsoft Docs
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
ms.openlocfilehash: b85eb84cdf48a1c2a441b8994076a9023d254f2d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300546"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField e SQLSetDescRec (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso das funções **SQLSetDescField** e **SQLSetDescRec** na biblioteca do cursor. Para obter informações gerais sobre essas funções, consulte [SQLSetDescField Function](../../../odbc/reference/syntax/sqlsetdescfield-function.md) e [SQLSetDescRec Function](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 A biblioteca do cursor executa **o SQLSetDescField** quando é chamada para devolver o valor dos campos definidos para colunas de marcação:  
  
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
  
 A biblioteca do cursor executa chamadas para **SQLSetDescRec** para uma coluna de marcadores.  
  
 Ao trabalhar com um driver ODBC *2.x,* a biblioteca do cursor retorna SQLSTATE HY090 (comprimento inválido de string ou buffer) quando **SQLSetDescField** ou **SQLSetDescRec** é chamado a definir o campo SQL_DESC_OCTET_LENGTH para o registro de marcador de um ARD para um valor não igual a 4. Ao trabalhar com um driver ODBC *3.x,* a biblioteca do cursor permite que o buffer seja de qualquer tamanho.  
  
 A biblioteca do cursor executa **o SQLSetDescField** quando é chamado para devolver o valor do campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE ou SQL_DESC_ROW_STATUS_PTR. Esses campos podem ser devolvidos para qualquer linha, não apenas a linha de marcadores.  
  
 A biblioteca do cursor não executa **o SQLSetDescField** para alterar qualquer campo descritor diferente dos campos mencionados anteriormente. Se um aplicativo chamar **SQLSetDescField** para definir qualquer outro campo enquanto a biblioteca do cursor estiver carregada, a chamada será transmitida para o driver.  
  
 A biblioteca do cursor suporta alterar os campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR de qualquer linha de descritor de linha de aplicativo dinamicamente (após uma chamada para **SQLExtendedFetch,** **SQLFetch**ou **SQLFetchScroll).** O campo SQL_DESC_OCTET_LENGTH_PTR pode ser alterado para um ponteiro nulo apenas para desvincular o buffer de comprimento de uma coluna.  
  
 A biblioteca do cursor não suporta alterar o campo SQL_DESC_BIND_TYPE em um APD ou ARD quando um cursor está aberto. O campo SQL_DESC_BIND_TYPE só pode ser alterado após o cursor ser fechado e antes que um novo cursor seja aberto. Os únicos campos descritores que a biblioteca do cursor suporta alterando quando um cursor está aberto são SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_ROWS_PROCESSED_PTR.  
  
 A biblioteca do cursor não suporta modificar o campo SQL_DESC_COUNT do ARD depois que **SQLExtendedFetchou** ou **SQLFetchScroll** foi chamado e antes do cursor ter sido fechado.
