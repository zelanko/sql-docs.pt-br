---
title: Excluindo linhas no conjunto de linhas com SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fadeb361a97cead2e43baee99bd59cad9ebbf87b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Excluindo linhas no conjunto de linhas com SQLSetPos
A operação de exclusão de **SQLSetPos** faz com que a fonte de dados exclua uma ou mais linhas selecionadas de uma tabela. Para excluir linhas com **SQLSetPos**, o aplicativo chama **SQLSetPos** com *operação* definido como SQL_DELETE e *RowNumber* definido como o número de linha a ser excluída. Se *RowNumber* for 0, todas as linhas no conjunto de linhas são excluídas.  
  
 Depois de **SQLSetPos** retorna, a linha excluída será a linha atual e seu status será SQL_ROW_DELETED. A linha não pode ser usada em todas as operações posicionadas adicionais, como chamadas ao **SQLGetData** ou **SQLSetPos**.  
  
 Ao excluir todas as linhas do conjunto de linhas (*RowNumber* é igual a 0), o aplicativo pode impedir que o driver exclua determinadas linhas usando a matriz de operação de linha, da mesma forma que para a operação de atualização de **SQLSetPos** . (Consulte [atualizando linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Todas as linhas excluídas devem existir no conjunto de resultados. Se os buffers do aplicativo foram preenchidos pela busca e se uma matriz de status de linha foi mantida, seus valores em cada uma dessas posições de linha não devem ser SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW.
