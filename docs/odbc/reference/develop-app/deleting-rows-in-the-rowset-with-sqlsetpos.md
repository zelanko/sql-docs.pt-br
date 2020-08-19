---
description: Excluir linhas no conjunto de linhas com SQLSetPos
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42b61aa9af15526420b6f2d4ef7e8c945e0da105
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476768"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Excluir linhas no conjunto de linhas com SQLSetPos
A operação de exclusão de **SQLSetPos** faz com que a fonte de dados exclua uma ou mais linhas selecionadas de uma tabela. Para excluir linhas com **SQLSetPos**, o aplicativo chama **SQLSetPos** com a *operação* definida como SQL_DELETE e *RowNumber* definido como o número da linha a ser excluída. Se *RowNumber* for 0, todas as linhas no conjunto de linhas serão excluídas.  
  
 Depois que **SQLSetPos** retorna, a linha excluída é a linha atual e seu status é SQL_ROW_DELETED. A linha não pode ser usada em nenhuma outra operação posicionada, como chamadas para **SQLGetData** ou **SQLSetPos**.  
  
 Ao excluir todas as linhas do conjunto de linhas (*RowNumber* é igual a 0), o aplicativo pode impedir que o driver exclua determinadas linhas usando a matriz de operação de linha, da mesma maneira que para a operação de atualização de **SQLSetPos**. (Consulte [atualizando linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Todas as linhas excluídas devem existir no conjunto de resultados. Se os buffers de aplicativo foram preenchidos pela busca e se uma matriz de status de linha tiver sido mantida, seus valores em cada uma dessas posições de linha não devem ser SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW.
