---
description: Matriz de status da linha
title: Matriz de status de linha | Microsoft Docs
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
ms.openlocfilehash: 8067aaf8724a6634d165d53743cbd0ef2015f6bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465629"
---
# <a name="row-status-array"></a>Matriz de status da linha
Além dos dados, **SQLFetch** e **SQLFetchScroll** podem retornar uma matriz que fornece o status de cada linha no conjunto de linhas. Essa matriz é especificada por meio do atributo de instrução SQL_ATTR_ROW_STATUS_PTR. Essa matriz é alocada pelo aplicativo e deve ter tantos elementos quantos forem especificados pelo atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE. Os valores na matriz são definidos por **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**e **SQLSetPos.** Os valores descrevem o status da linha e se o status foi alterado desde a última busca.  
  
|Valor da matriz de status da linha|Descrição|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|A linha foi buscada com êxito e não foi alterada desde a última busca.|  
|SQL_ROW_SUCCESS_WITH_INFO|A linha foi buscada com êxito e não foi alterada desde a última busca. No entanto, um aviso foi retornado sobre a linha.|  
|SQL_ROW_ERROR|Ocorreu um erro ao buscar a linha.|  
|SQL_ROW_UPDATED|A linha foi buscada com êxito e foi atualizada desde a última busca. Se a linha for buscada novamente ou atualizada pelo **SQLSetPos**, seu status será alterado para o novo status.<br /><br /> Alguns drivers não podem detectar alterações nos dados e, portanto, não podem retornar esse valor. Para determinar se um driver pode detectar atualizações para linhas rebuscadas, um aplicativo chama **SQLGetInfo** com a opção SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|A linha foi excluída desde a última busca.|  
|SQL_ROW_ADDED|A linha foi inserida por **SQLBulkOperations**. Se a linha for buscada novamente ou for atualizada por **SQLSetPos**, seu status será SQL_ROW_SUCCESS.<br /><br /> Esse valor não é definido por **SQLFetch** ou **SQLFetchScroll**.|  
|SQL_ROW_NOROW|O conjunto de linhas sobreposto ao final do conjunto de resultados e nenhuma linha foi retornada correspondente a esse elemento da matriz de status de linha.|
