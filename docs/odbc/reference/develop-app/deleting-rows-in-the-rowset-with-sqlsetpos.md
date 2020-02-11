---
title: Excluindo linhas no conjunto de linhas com SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e39b70f92f7b239b011cdd4fdd6abd36c27561c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076800"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Excluir linhas no conjunto de linhas com SQLSetPos
A operação de exclusão de **SQLSetPos** faz com que a fonte de dados exclua uma ou mais linhas selecionadas de uma tabela. Para excluir linhas com **SQLSetPos**, o aplicativo chama **SQLSetPos** com a *operação* definida como SQL_DELETE e *RowNumber* definido como o número da linha a ser excluída. Se *RowNumber* for 0, todas as linhas no conjunto de linhas serão excluídas.  
  
 Depois que **SQLSetPos** retorna, a linha excluída é a linha atual e seu status é SQL_ROW_DELETED. A linha não pode ser usada em nenhuma outra operação posicionada, como chamadas para **SQLGetData** ou **SQLSetPos**.  
  
 Ao excluir todas as linhas do conjunto de linhas (*RowNumber* é igual a 0), o aplicativo pode impedir que o driver exclua determinadas linhas usando a matriz de operação de linha, da mesma maneira que para a operação de atualização de **SQLSetPos**. (Consulte [atualizando linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Todas as linhas excluídas devem existir no conjunto de resultados. Se os buffers de aplicativo foram preenchidos pela busca e se uma matriz de status de linha tiver sido mantida, seus valores em cada uma dessas posições de linha não devem ser SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW.
