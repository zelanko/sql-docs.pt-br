---
title: Matriz de Status de linha | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57b187bf4f14bd5c05f91a433fa331e954fa0fb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020374"
---
# <a name="row-status-array"></a>Matriz de status da linha
Além dos dados, **SQLFetch** e **SQLFetchScroll** pode retornar uma matriz que fornece o status de cada linha no conjunto de linhas. Essa matriz é especificado por meio do atributo de instrução SQL_ATTR_ROW_STATUS_PTR. Essa matriz é alocada pelo aplicativo e deve ter tantos elementos que sejam especificadas pelo atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE. Os valores na matriz são definidos pelo **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, e **SQLSetPos.** Os valores descrevem o status da linha e se o status foi alterado desde que foi buscada pela última vez.  
  
|Valor de matriz de status de linha|Descrição|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|A linha foi obtida com êxito e não foi alterado desde que foi buscada pela última vez.|  
|SQL_ROW_SUCCESS_WITH_INFO|A linha foi obtida com êxito e não foi alterado desde que foi buscada pela última vez. No entanto, um aviso sobre a linha foi retornado.|  
|SQL_ROW_ERROR|Ocorreu um erro ao buscar a linha.|  
|SQL_ROW_UPDATED|A linha foi obtida com êxito e foi atualizada desde que foi buscada pela última vez. Se a linha é novamente buscada ou atualizada por **SQLSetPos**, seu status é alterado para o novo status.<br /><br /> Alguns drivers não podem detectar alterações aos dados e, portanto, não é possível retornar esse valor. Para determinar se um driver pode detectar as atualizações para linhas refetched, um aplicativo chama **SQLGetInfo** com a opção SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|A linha foi excluída desde que foi buscada pela última vez.|  
|SQL_ROW_ADDED|A linha foi inserida pela **SQLBulkOperations**. Se a linha será buscada novamente ou é atualizada pelo **SQLSetPos**, seu status é SQL_ROW_SUCCESS.<br /><br /> Esse valor não é definido **SQLFetch** ou **SQLFetchScroll**.|  
|SQL_ROW_NOROW|O conjunto de linhas sobrepostas final do conjunto de resultados e nenhuma linha foi retornada que correspondeu a esse elemento da matriz de status de linha.|
