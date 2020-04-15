---
title: Matriz de status da linha | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60dead23fe0051c05698e094f37ddad96b2b337d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304281"
---
# <a name="row-status-array"></a>Matriz de status da linha
Além dos dados, **SQLFetch** e **SQLFetchScroll** podem retornar uma matriz que dá o status de cada linha no conjunto de linhas. Esta matriz é especificada através do atributo de declaração SQL_ATTR_ROW_STATUS_PTR. Esta matriz é alocada pelo aplicativo e deve ter tantos elementos quanto são especificados pelo atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE. Os valores no array são definidos por **SQLBulkOperations,** **SQLFetch,** **SQLFetchScroll**e **SQLSetPos.** Os valores descrevem o status da linha e se esse status mudou desde a última vez que foi buscada.  
  
|Valor da matriz de status da linha|Descrição|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|A fila foi buscada com sucesso e não mudou desde a última vez que foi buscada.|  
|SQL_ROW_SUCCESS_WITH_INFO|A fila foi buscada com sucesso e não mudou desde a última vez que foi buscada. No entanto, um aviso foi devolvido sobre a linha.|  
|SQL_ROW_ERROR|Ocorreu um erro ao buscar a linha.|  
|SQL_ROW_UPDATED|A fila foi buscada com sucesso e foi atualizada desde a última vez que foi buscada. Se a linha for rebuscada ou atualizada por **SQLSetPos,** seu status será alterado para o novo status.<br /><br /> Alguns drivers não podem detectar alterações nos dados e, portanto, não podem retornar esse valor. Para determinar se um driver pode detectar atualizações em linhas rebuscadas, um aplicativo chama **sqlGetInfo** com a opção SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|A linha foi excluída desde a última vez que foi buscada.|  
|SQL_ROW_ADDED|A linha foi inserida pela **SQLBulkOperations**. Se a linha for rebuscada ou for atualizada por **SQLSetPos,** seu status será SQL_ROW_SUCCESS.<br /><br /> Este valor não é definido por **SQLFetch** ou **SQLFetchScroll**.|  
|SQL_ROW_NOROW|O conjunto de linhas sobrepôs-se ao final do conjunto de resultados, e nenhuma linha foi devolvida que correspondia a este elemento da matriz de status da linha.|
